---
title: 计算表达式
description: 了解如何创建方便的语法中编写计算F#，可以进行序列化和组合使用控制流构造和绑定。
ms.date: 03/15/2019
ms.openlocfilehash: 3c2abb5c6204309fc8d5215a53ce8af46c01d218
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2019
ms.locfileid: "58125507"
---
# <a name="computation-expressions"></a>计算表达式

中的计算表达式F#提供的方便语法用于编写计算，可以进行排列和组合使用控制流构造和绑定。 根据计算表达式的种类，它们可以认为的 monad、 monoids、 monad 转换器和 applicative 函子的表达方式。 但是，不同于其他语言 (如*是否表示法*Haskell 中)，它们不受限于单一的抽象概念，而不依赖宏或其他形式的元编程来完成方便且与上下文相关的语法。

## <a name="overview"></a>概述

计算可以采取多种形式。 计算的最常见形式是单线程执行，这是易于理解和修改。 但是，并非所有形式都是计算的单线程执行像简单。 一些示例包括：

* 非确定性计算
* 异步计算
* Effectful 计算
* 生成计算

一般来说，有*上下文相关*必须在应用程序的某些部分中执行的计算。 编写与上下文相关代码极具挑战性，因为可轻松之外不抽象来阻止你执行此操作的情况下的给定上下文将"泄漏"计算。 这些抽象通常具有挑战性，若要编写的自己，这就是为什么F#具有一个通用的方法来实现所谓**计算表达式**。

计算表达式提供统一的语法和抽象的编码与上下文相关的计算模型。

每个计算表达式受*生成器*类型。 生成器类型定义可用于计算表达式的操作。 请参阅[创建一个新类型的计算的表达式](computation-expressions.md#creating-a-new-type-of-computation-expression)，其中说明了如何创建自定义计算表达式。

### <a name="syntax-overview"></a>语法概述

所有计算表达式都具有以下形式：

```
builder-expr { cexper }
```

其中`builder-expr`的定义是计算表达式的生成器类型名称和`cexper`是计算表达式的表达式主体。 例如，`async`计算的表达式代码可以如下所示：

```fsharp
let fetchAndDownload url =
    async {
        let! data = downloadData url

        let processedData = processData data

        return processedData
    }
```

没有中计算表达式，提供的特殊的附加语法，如前面的示例中所示。 以下表达式窗体而言，可能有计算表达式：

```fsharp
expr { let! ... }
expr { do! ... }
expr { yield ... }
expr { yield! ... }
expr { return ... }
expr { return! ... }
expr { match! ... }
```

这些关键字和其他标准的每个F#关键字才在计算表达式中可用，如果它们已在后备生成器类型中定义。 唯一的例外是`match!`，它本身就是使用的语法糖`let!`跟模式匹配的结果。

生成器类型是一个对象，定义的管理的方式合并的片段的计算表达式; 的特殊方法也就是说，其方法控制计算表达式的行为方式。 另一种方法来描述的生成器类是说它允许你自定义的许多操作F#构造，如循环和绑定。

### `let!`

`let!`关键字将调用与另一个计算表达式的结果绑定到一个名称：

```fsharp
let doThingsAsync url =
    async {
        let! data = getDataAsync url
        ...
    }
```

如果将绑定到具有的计算表达式调用`let`，则不会计算表达式的结果。 相反，您将有绑定的值*未实现*调用到该计算表达式。 使用`let!`要绑定到结果。

`let!` 由定义`Bind(x, f)`生成器类型上的成员。

### `do!`

`do!`关键字是用于调用计算表达式将返回`unit`-等类型 (由定义`Zero`生成器上的成员):

```fsharp
let doThingsAsync data url =
    async {
        do! submitData data url
        ...
    }
```

有关[异步工作流](asynchronous-workflows.md)，此类型是`Async<unit>`。 对于其他计算表达式，该类型很可能是`CExpType<unit>`。

`do!` 定义由`Bind(x, f)`成员上的生成器类型，其中`f`生成`unit`。

### `yield`

`yield`关键字，以便它可以用作从计算表达式返回一个值是<xref:System.Collections.Generic.IEnumerable%601>:

```fsharp
let squares =
    seq {
        for i in 1..10 do
            yield i * i
    }

for sq in squares do
    printfn "%d" sq
```

如同[yield 关键字在 C# 中的](../../csharp/language-reference/keywords/yield.md)，因为它循环访问生成计算表达式中的每个元素。

`yield` 定义由`Yield(x)`成员上的生成器类型，其中`x`是要重新生成的项。

### `yield!`

`yield!`关键字是用于平铺中计算表达式的值的集合：

```fsharp
let squares =
    seq {
        for i in 1..3 -> i * i
    }

let cubes =
    seq {
        for i in 1..3 -> i * i * i
    }

let squaresAndCubes =
    seq {
        yield! squares
        yield! cubes
    }

printfn "%A" squaresAndCubes // Prints - 1; 4; 9; 1; 8; 27
```

计算表达式求值时，由调用`yield!`将具有其项生成后一通过一，平展结果。

`yield!` 定义由`YieldFrom(x)`成员上的生成器类型，其中`x`是值的集合。

### `return`

`return`关键字将值包装在对应于计算表达式的类型。 除了使用的计算表达式`yield`，使用它来"完成"计算表达式：

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        let! data = fetch url
        return data
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return` 定义由`Return(x)`成员上的生成器类型，其中`x`是要包装的项。

### `return!`

`return!`关键字意识到计算表达式的值并将该结果包装中对应于计算表达式的类型：

```fsharp
let req = // 'req' is of type is 'Async<data>'
    async {
        return! fetch url
    }

// 'result' is of type 'data'
let result = Async.RunSynchronously req
```

`return!` 定义由`ReturnFrom(x)`成员上的生成器类型，其中`x`是另一个计算表达式。

### `match!`

从F#4.5 中，`match!`关键字可以内联调用根据其结果的另一个计算表达式和模式匹配：

```fsharp
let doThingsAsync url =
    async {
        match! callService url with
        | Some data -> ...
        | None -> ...
    }
```

调用具有的计算表达式时`match!`，它将会获得如下调用的结果`let!`。 这常用于调用计算表达式结果时[可选](options.md)。

## <a name="built-in-computation-expressions"></a>内置的计算表达式

F#核心库定义了三个内置的计算表达式：[序列表达式](sequences.md)，[异步工作流](asynchronous-workflows.md)，和[查询表达式](query-expressions.md)。

## <a name="creating-a-new-type-of-computation-expression"></a>创建新的计算表达式的类型

可以通过创建一个生成器类和类上定义某些特殊的方法来定义您自己的计算表达式的特征。 下表中列出，生成器类可以选择定义方法。

下表介绍可在工作流生成器类的方法。

|**方法**|**典型的签名**|**说明**|
|----|----|----|
|`Bind`|`M<'T> * ('T -> M<'U>) -> M<'U>`|为调用`let!`和`do!`中计算表达式。|
|`Delay`|`(unit -> M<'T>) -> M<'T>`|包装一个函数作为计算表达式。|
|`Return`|`'T -> M<'T>`|为调用`return`中计算表达式。|
|`ReturnFrom`|`M<'T> -> M<'T>`|为调用`return!`中计算表达式。|
|`Run`|`M<'T> -> M<'T>` 或<br /><br />`M<'T> -> 'T`|执行计算表达式。|
|`Combine`|`M<'T> * M<'T> -> M<'T>` 或<br /><br />`M<unit> * M<'T> -> M<'T>`|调用用于在计算表达式中的排序。|
|`For`|`seq<'T> * ('T -> M<'U>) -> M<'U>` 或<br /><br />`seq<'T> * ('T -> M<'U>) -> seq<M<'U>>`|为调用`for...do`中计算表达式的表达式。|
|`TryFinally`|`M<'T> * (unit -> unit) -> M<'T>`|为调用`try...finally`中计算表达式的表达式。|
|`TryWith`|`M<'T> * (exn -> M<'T>) -> M<'T>`|为调用`try...with`中计算表达式的表达式。|
|`Using`|`'T * ('T -> M<'U>) -> M<'U> when 'U :> IDisposable`|为调用`use`中计算表达式的绑定。|
|`While`|`(unit -> bool) * M<'T> -> M<'T>`|为调用`while...do`中计算表达式的表达式。|
|`Yield`|`'T -> M<'T>`|为调用`yield`中计算表达式的表达式。|
|`YieldFrom`|`M<'T> -> M<'T>`|为调用`yield!`中计算表达式的表达式。|
|`Zero`|`unit -> M<'T>`|调用空`else`的分支`if...then`中计算表达式的表达式。|
|`Quote`|`Quotations.Expr<'T> -> Quotations.Expr<'T>`|指示计算表达式传递给`Run`作为报价的成员。 它将转换到报价计算的所有实例。|

许多生成器类中的方法使用并返回`M<'T>`构造，这通常是已单独定义的类型特征的计算种类的组合，例如，`Async<'T>`对异步工作流和`Seq<'T>`表示序列工作流。 这些方法的签名启用它们要合并且相互嵌套，以便从一个构造返回的工作流对象可以传递到下一步。 编译器分析计算表达式时使用上表中的方法和计算表达式中的代码，为一系列嵌套的函数调用的转换表达式。

嵌套的表达式采用以下形式：

```fsharp
builder.Run(builder.Delay(fun () -> {| cexpr |}))
```

在上面的代码中，对调用`Run`和`Delay`省略了如果中计算表达式生成器类未定义。 计算表达式，此处表示为正文`{| cexpr |}`下, 表中所描述的翻译转换为涉及生成器类的方法的调用。 计算表达式`{| cexpr |}`定义以递归方式根据这些翻译其中`expr`是F#表达式并`cexpr`是计算表达式。

|表达式|转换|
|----------|-----------|
|<code>{&#124; let binding in cexpr &#124;}</code>|<code>let binding in {&#124; cexpr &#124;}</code>|
|<code>{&#124; let! pattern = expr in cexpr &#124;}</code>|<code>builder.Bind(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; do! expr in cexpr &#124;}</code>|<code>builder.Bind(expr, (fun () -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; yield expr &#124;}</code>|`builder.Yield(expr)`|
|<code>{&#124; yield! expr &#124;}</code>|`builder.YieldFrom(expr)`|
|<code>{&#124; return expr &#124;}</code>|`builder.Return(expr)`|
|<code>{&#124; return! expr &#124;}</code>|`builder.ReturnFrom(expr)`|
|<code>{&#124; use pattern = expr in cexpr &#124;}</code>|<code>builder.Using(expr, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; use! value = expr in cexpr &#124;}</code>|<code>builder.Bind(expr, (fun value -> builder.Using(value, (fun value -> {&#124; cexpr &#124;}))))</code>|
|<code>{&#124; if expr then cexpr0 &#124;}</code>|<code>if expr then {&#124; cexpr0 &#124;} else binder.Zero()</code>|
|<code>{&#124; if expr then cexpr0 else cexpr1 &#124;}</code>|<code>if expr then {&#124; cexpr0 &#124;} else {&#124; cexpr1 &#124;}</code>|
|<code>{&#124; match expr with &#124; pattern_i -> cexpr_i &#124;}</code>|<code>match expr with &#124; pattern_i -> {&#124; cexpr_i &#124;}</code>|
|<code>{&#124; for pattern in expr do cexpr &#124;}</code>|<code>builder.For(enumeration, (fun pattern -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; for identifier = expr1 to expr2 do cexpr &#124;}</code>|<code>builder.For(enumeration, (fun identifier -> {&#124; cexpr &#124;}))</code>|
|<code>{&#124; while expr do cexpr &#124;}</code>|<code>builder.While(fun () -> expr, builder.Delay({&#124;cexpr &#124;}))</code>|
|<code>{&#124; try cexpr with &#124; pattern_i -> expr_i &#124;}</code>|<code>builder.TryWith(builder.Delay({&#124; cexpr &#124;}), (fun value -> match value with &#124; pattern_i -> expr_i &#124; exn -> reraise exn)))</code>|
|<code>{&#124; try cexpr finally expr &#124;}</code>|<code>builder.TryFinally(builder.Delay( {&#124; cexpr &#124;}), (fun () -> expr))</code>|
|<code>{&#124; cexpr1; cexpr2 &#124;}</code>|<code>builder.Combine({&#124;cexpr1 &#124;}, {&#124; cexpr2 &#124;})</code>|
|<code>{&#124; other-expr; cexpr &#124;}</code>|<code>expr; {&#124; cexpr &#124;}</code>|
|<code>{&#124; other-expr &#124;}</code>|`expr; builder.Zero()`|

上表中`other-expr`介绍一个表达式，否则不表中列出。 生成器类不需要实现的所有方法和支持所有前面的表中列出的翻译。 未实现这些构造不在该类型的计算表达式中可用。 例如，如果你不想要支持`use`中计算表达式的关键字，则可以省略的定义`Use`生成器类中。

下面的代码示例显示了一系列步骤，可以是计算一次一个步骤封装计算的计算表达式。 一个可区分联合类型`OkOrException`，到目前为止计算对表达式的错误状态进行编码。 此代码演示了可以在您的计算表达式，如生成器方法的一些样本实现中使用的几种典型模式。

```fsharp
// Computations that can be run step by step
type Eventually<'T> =
    | Done of 'T
    | NotYetDone of (unit -> Eventually<'T>)

module Eventually =
    // The bind for the computations. Append 'func' to the
    // computation.
    let rec bind func expr =
        match expr with
        | Done value -> func value
        | NotYetDone work -> NotYetDone (fun () -> bind func (work()))

    // Return the final value wrapped in the Eventually type.
    let result value = Done value

    type OkOrException<'T> =
        | Ok of 'T
        | Exception of System.Exception

    // The catch for the computations. Stitch try/with throughout
    // the computation, and return the overall result as an OkOrException.
    let rec catch expr =
        match expr with
        | Done value -> result (Ok value)
        | NotYetDone work ->
            NotYetDone (fun () ->
                let res = try Ok(work()) with | exn -> Exception exn
                match res with
                | Ok cont -> catch cont // note, a tailcall
                | Exception exn -> result (Exception exn))

    // The delay operator.
    let delay func = NotYetDone (fun () -> func())

    // The stepping action for the computations.
    let step expr =
        match expr with
        | Done _ -> expr
        | NotYetDone func -> func ()

    // The rest of the operations are boilerplate.
    // The tryFinally operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryFinally expr compensation =
        catch (expr)
        |> bind (fun res -> 
            compensation();
            match res with
            | Ok value -> result value
            | Exception exn -> raise exn)

    // The tryWith operator.
    // This is boilerplate in terms of "result", "catch", and "bind".
    let tryWith exn handler =
        catch exn
        |> bind (function Ok value -> result value | Exception exn -> handler exn)

    // The whileLoop operator.
    // This is boilerplate in terms of "result" and "bind".
    let rec whileLoop pred body =
        if pred() then body |> bind (fun _ -> whileLoop pred body)
        else result ()

    // The sequential composition operator.
    // This is boilerplate in terms of "result" and "bind".
    let combine expr1 expr2 =
        expr1 |> bind (fun () -> expr2)

    // The using operator.
    let using (resource: #System.IDisposable) func =
        tryFinally (func resource) (fun () -> resource.Dispose())

    // The forLoop operator.
    // This is boilerplate in terms of "catch", "result", and "bind".
    let forLoop (collection:seq<_>) func =
        let ie = collection.GetEnumerator()
        tryFinally 
            (whileLoop 
                (fun () -> ie.MoveNext()) 
                (delay (fun () -> let value = ie.Current in func value)))
            (fun () -> ie.Dispose())

// The builder class.
type EventuallyBuilder() =
    member x.Bind(comp, func) = Eventually.bind func comp
    member x.Return(value) = Eventually.result value
    member x.ReturnFrom(value) = value
    member x.Combine(expr1, expr2) = Eventually.combine expr1 expr2
    member x.Delay(func) = Eventually.delay func
    member x.Zero() = Eventually.result ()
    member x.TryWith(expr, handler) = Eventually.tryWith expr handler
    member x.TryFinally(expr, compensation) = Eventually.tryFinally expr compensation
    member x.For(coll:seq<_>, func) = Eventually.forLoop coll func
    member x.Using(resource, expr) = Eventually.using resource expr

let eventually = new EventuallyBuilder()

let comp = eventually {
    for x in 1..2 do
        printfn " x = %d" x
    return 3 + 4 }

// Try the remaining lines in F# interactive to see how this
// computation expression works in practice.
let step x = Eventually.step x

// returns "NotYetDone <closure>"
comp |> step

// prints "x = 1"
// returns "NotYetDone <closure>"
comp |> step |> step

// prints "x = 1"
// prints "x = 2"
// returns "Done 7"
comp |> step |> step |> step |> step 
```

计算表达式的表达式返回的基础类型。 基础类型可表示计算所得的结果或可以执行的延迟的计算或它可能会提供一种方法来循环访问某种类型的集合。 在上一示例中，基础类型是**最终**。 为序列表达式的基础类型是<xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType>。 对于查询表达式中，基础类型是<xref:System.Linq.IQueryable?displayProperty=nameWithType>。 对于异步工作流，基础类型是[ `Async` ](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7)。 `Async`对象都表示为计算的结果执行的工作。 例如，调用[ `Async.RunSynchronously` ](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b)执行计算并返回结果。

## <a name="custom-operations"></a>自定义操作

您可以定义上计算表达式的自定义操作和使用自定义操作作为计算表达式中的运算符。 例如，您可以在查询表达式中包含的查询运算符。 在定义自定义操作时，必须定义 Yield 和计算表达式中的方法。 若要定义自定义操作，将其放入一个生成器类，用于计算表达式，并将[ `CustomOperationAttribute` ](https://msdn.microsoft.com/library/199f3927-79df-484b-ba66-85f58cc49b19)。 此属性采用一个字符串作为参数，它是用于在自定义操作中使用的名称。 此名称发送到开头的计算表达式的左大括号的作用域中时。 因此，不应使用此块中具有相同名称作为自定义操作的标识符。 例如，例如避免使用的标识符`all`或`last`在查询表达式中。

### <a name="extending-existing-builders-with-new-custom-operations"></a>扩展现有生成器与新的自定义操作

如果您已有一个生成器类，其自定义操作可从此生成器类的外部进行扩展。 必须在模块中声明扩展。 命名空间不能包含除相同的文件和定义该类型的相同命名空间声明组中的扩展成员。

下面的示例演示的现有扩展`Microsoft.FSharp.Linq.QueryBuilder`类。

```fsharp
type Microsoft.FSharp.Linq.QueryBuilder with

    [<CustomOperation("existsNot")>]
    member __.ExistsNot (source: QuerySource<'T, 'Q>, predicate) =
        Enumerable.Any (source.Source, Func<_,_>(predicate)) |> not
```

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [异步工作流](asynchronous-workflows.md)
- [序列](https://msdn.microsoft.com/library/6b773b6b-9c9a-4af8-bd9e-d96585c166db)
- [查询表达式](query-expressions.md)
