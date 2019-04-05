---
title: F# 编码约定
description: 编写 F# 代码时，了解一般指导原则和惯例。
ms.date: 05/14/2018
ms.openlocfilehash: 21119b6d69e00f359104bfb6eab7681bdbfb8d78
ms.sourcegitcommit: db8b83057d052c1f9f249d128b08d4423af0f7c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2018
ms.locfileid: "49087383"
---
# <a name="f-coding-conventions"></a>F# 编码约定

以下约定表述从体验使用大型 F# 代码库。 [优秀的 F# 代码的五个原则](index.md#five-principles-of-good-f-code)是每个建议的基础。 与相关[F# 组件设计准则](component-design-guidelines.md)，但适用于任何 F# 代码，而不仅仅是组件，例如库。

## <a name="organizing-code"></a>组织代码

F# 功能来组织代码的两种主要方式： 模块和命名空间。 这些相似，但存在以下差异：

* 命名空间被编译为.NET 命名空间。 静态类作为编译模块。
* 命名空间始终是最高级别。 模块可以是顶级和嵌套在其他模块。
* 命名空间可以跨多个文件。 模块不能。
* 模块可以使用修饰`[<RequireQualifiedAccess>]`和`[<AutoOpen>]`。

以下准则将帮助您使用这些来组织你的代码。

### <a name="prefer-namespaces-at-the-top-level"></a>更喜欢在顶层命名空间

对于任何公开使用的代码，命名空间是优先于模块的顶层。 作为.NET 命名空间对它们进行编译，因为它们是可使用 C# 中不存在问题。

```fsharp
// Good!
namespace MyCode

type MyClass() =
    ...
```

使用顶级模块可能不会显示不同时仅从 F# 中，但 C# 的使用者，调用方可能会惊讶于无需限定`MyClass`与`MyCode`模块。

```fsharp
// Bad!
module MyCode

type MyClass() =
    ...
```

### <a name="carefully-apply-autoopen"></a>请仔细应用 `[<AutoOpen>]`

`[<AutoOpen>]`构造可以污染，调用方提供的功能范围和内容来自的答案是"神奇"。 这通常不是一件好事。 此规则的例外是 F# 核心库本身 （尽管这一事实也是有点有争议的）。

但是，如果你有一个公共 API，你想要组织单独从该公共 API 帮助程序功能是提供了便利。

```fsharp
module MyAPI =
    [<AutoOpen>]
    module private Helpers =
        let helper1 x y z =
            ...


    let myFunction1 x =
        let y = ...
        let z = ...

        helper1 x y z
```

这样可以从一个函数的公共 API 完全不同的实现详细信息而无需完全限定程序的帮助程序每次调用它。

此外，公开的扩展方法和表达式生成器的命名空间级别可以巧妙地表示与`[<AutoOpen>]`。

### <a name="use-requirequalifiedaccess-whenever-names-could-conflict-or-you-feel-it-helps-with-readability"></a>使用`[<RequireQualifiedAccess>]`时可能发生名称冲突或您认为它有助于提高可读性

添加`[<RequireQualifiedAccess>]`对模块的特性指示模块不能打开，并且对模块的元素的引用需要显式限定访问权限。 例如，`Microsoft.FSharp.Collections.List`模块具有此属性。

当函数和模块中的值具有名称可能与其他模块中的名称发生冲突时，这很有用。 需要限定的访问可以极大地提高的长期可维护性和可进化性的库。

```fsharp
[<RequireQualifiedAccess>]
module StringTokenization =
    let parse s = ...

...

let s = getAString()
let parsed = StringTokenization.parse s // Must qualify to use 'parse'
```

### <a name="sort-open-statements-topologically"></a>排序`open`语句拓扑结构上

在 F# 中，声明的顺序非常重要，包括与`open`语句。 这是与 C# 中，其中的效果`using`和`using static`无关的文件中这些语句的顺序。

在 F# 中，打开到作用域的元素可以隐藏其他人已存在。 这意味着重新排序`open`语句无法更改代码的含义。 因此，任何任意排序的所有`open`语句 （例如，根据） 通常不建议，避免生成您所料的不同行为。

相反，我们建议，您对其进行排序[拓扑结构上](https://en.wikipedia.org/wiki/Topological_sorting); 即，排序你`open`语句中的顺序_层_系统的定义。 也可以考虑不同的拓扑图层内的排序字母数字。

例如，下面是 F# 编译器服务公共 API 文件的拓扑排序：

```fsharp
namespace Microsoft.FSharp.Compiler.SourceCodeServices

open System
open System.Collections.Generic
open System.Collections.Concurrent
open System.Diagnostics
open System.IO
open System.Reflection
open System.Text

open Microsoft.FSharp.Compiler
open Microsoft.FSharp.Compiler.AbstractIL
open Microsoft.FSharp.Compiler.AbstractIL.Diagnostics
open Microsoft.FSharp.Compiler.AbstractIL.IL
open Microsoft.FSharp.Compiler.AbstractIL.ILBinaryReader
open Microsoft.FSharp.Compiler.AbstractIL.Internal
open Microsoft.FSharp.Compiler.AbstractIL.Internal.Library

open Microsoft.FSharp.Compiler.AccessibilityLogic
open Microsoft.FSharp.Compiler.Ast
open Microsoft.FSharp.Compiler.CompileOps
open Microsoft.FSharp.Compiler.CompileOptions
open Microsoft.FSharp.Compiler.Driver
open Microsoft.FSharp.Compiler.ErrorLogger
open Microsoft.FSharp.Compiler.Infos
open Microsoft.FSharp.Compiler.InfoReader
open Microsoft.FSharp.Compiler.Lexhelp
open Microsoft.FSharp.Compiler.Layout
open Microsoft.FSharp.Compiler.Lib
open Microsoft.FSharp.Compiler.NameResolution
open Microsoft.FSharp.Compiler.PrettyNaming
open Microsoft.FSharp.Compiler.Parser
open Microsoft.FSharp.Compiler.Range
open Microsoft.FSharp.Compiler.Tast
open Microsoft.FSharp.Compiler.Tastops
open Microsoft.FSharp.Compiler.TcGlobals
open Microsoft.FSharp.Compiler.TypeChecker
open Microsoft.FSharp.Compiler.SourceCodeServices.SymbolHelpers

open Internal.Utilities
open Internal.Utilities.Collections
```

请注意，一个分行符将分开的拓扑图层，与正在排序根据之后每个层。 这完全可以将代码组织而不会意外地隐藏值中。

## <a name="use-classes-to-contain-values-that-have-side-effects"></a>使用类来包含具有副作用的值

有很多时候时初始化一个值，可能会有副作用，如实例化到的数据库或其他远程资源的上下文。 它很容易初始化模块这类问题，并将其用于后续函数：

```fsharp
// This is bad!
module MyApi =
    let dep1 = File.ReadAllText "/Users/{your name}/connectionstring.txt"
    let dep2 = Environment.GetEnvironmentVariable "DEP_2"

    let private r = Random()
    let dep3() = r.Next() // Problematic if multiple threads use this

    let function1 arg = doStuffWith dep1 dep2 dep3 arg
    let function2 arg = doSutffWith dep1 dep2 dep3 arg
```

这通常是一个好主意几个原因：

首先，应用程序配置推送到的基本代码`dep1`和`dep2`。 这将很难维护中较大代码库。

第二个，将以静态方式初始化数据不应包含不是线程安全，如果你的组件本身会使用多个线程的值。 显然，这违反了`dep3`。

最后，初始化模块编译到静态构造函数在整个编译单元。 如果该模块中的 let 绑定值初始化中出现任何错误，它表现为`TypeInitializationException`然后应用程序的整个生存期内缓存。 这可能很难诊断。 通常是内部异常，您可以尝试推断，但如果没有，则根本原因无法区分。

相反，只需使用一个简单的类来保存依赖项：

```fsharp
type MyParametricApi(dep1, dep2, dep3) =
    member __.Function1 arg1 = doStuffWith dep1 dep2 dep3 arg1
    member __.Function2 arg2 = doStuffWith dep1 dep2 dep3 arg2
```

这可实现以下目的：

1. 将推送 API 本身之外的任何依赖于状态。
2. 现在可以外部 API 完成配置。
3. 初始化为因变量值中的错误不是可能会表现为`TypeInitializationException`。
4. 该 API 是现在可以轻松地测试。

## <a name="error-management"></a>错误管理

大型系统中的错误管理是一项复杂且能体现细微差别工作，并且没有确保您的系统中的项目符号是容错的和的行为也没有 silver。 以下指南应提供导航此困难空间中的指导。

### <a name="represent-error-cases-and-illegal-state-in-types-intrinsic-to-your-domain"></a>表示错误情况和你的域中的内部类型中的非法状态

与[可区分联合](../language-reference/discriminated-unions.md)，F# 使你能够在类型系统中表示发生故障的程序状态。 例如：

```fsharp
type MoneyWithdrawalResult =
    | Success of amount:decimal
    | InsufficientFunds of balance:decimal
    | CardExpired of DateTime
    | UndisclosedFailure
```

在这种情况下，有三种已知的方式从银行帐户提取资金可能会失败。 每个错误用例表示在类型中，并因此地进行处理安全地在整个程序。

```fsharp
let handleWithdrawal amount =
    let w = withdrawMoney amount
    match w with
    | Success am -> printfn "Successfully withdrew %f" am
    | InsufficientFunds balance -> printfn "Failed: balance is %f" balance
    | CardExpired expiredDate -> printfn "Failed: card expired on %O" expiredDate
    | UndisclosedFailure -> printfn "Failed: unknown"
```

一般情况下，如果您可以建立模型的不同方法的内容可以**失败**中你的域，然后处理错误的代码不再视为必须处理常规程序流除了的内容。 它是只需正常程序流的一部分，不会被视为**异常**。 有这两个主要好处：

1. 更轻松地根据你的域更改随着时间的推移维护它。
2. 错误情况下是容易进行单元测试。

### <a name="use-exceptions-when-errors-cannot-be-represented-with-types"></a>当错误不能表示的类型时使用异常

并非所有的错误可表示问题域中。 这些类型的故障*异常*在本质上，因此能够引发和 F# 中捕获异常。

首先，建议先阅读[异常设计准则](../../standard/design-guidelines/exceptions.md)。 它们还适用于 F#。

可在 F# 中用于引发异常的目的的主要构造应考虑按以下顺序的首选项：

| 函数 | 语法 | 目标 |
|----------|--------|---------|
| `nullArg` | `nullArg "argumentName"` | 引发`System.ArgumentNullException`与指定的参数名称。 |
| `invalidArg` | `invalidArg "argumentName" "message"` | 引发`System.ArgumentException`使用指定的参数名称和消息。 |
| `invalidOp` | `invalidOp "message"` | 引发`System.InvalidOperationException`使用指定的消息。 |
|`raise`| `raise (ExceptionType("message"))` | 引发异常的通用机制。 |
| `failwith` | `failwith "message"` | 引发`System.Exception`使用指定的消息。 |
| `failwithf` | `failwithf "format string" argForFormatString` | 引发`System.Exception`由格式字符串和其输入一条消息。 |

使用`nullArg`，`invalidArg`并`invalidOp`作为机制引发`ArgumentNullException`，`ArgumentException`和`InvalidOperationException`在适当的时候。

`failwith`并`failwithf`应通常避免函数，因为它们会引发基`Exception`类型，不特定的异常。 为每个[异常设计准则](../../standard/design-guidelines/exceptions.md)，你想要时可以引发更具体的异常。

### <a name="using-exception-handling-syntax"></a>使用异常处理语法

F# 支持通过异常模式`try...with`语法：

```fsharp
try
    tryGetFileContents()
with
| :? System.IO.FileNotFoundException as e -> // Do something with it here
| :? System.Security.SecurityException as e -> // Do something with it here
```

协调遇到模式匹配的异常时执行的功能可能需要一些技巧，如果你想要保持代码干净。 一种此类方法来处理这种情况是使用[活动模式](../language-reference/active-patterns.md)作为一种方式对组功能围绕本身出现异常错误情况。 例如，您可能要使用的 API 时将引发异常，异常元数据中包含有价值的信息。 解包捕获的异常活动模式在正文中有用的值和返回值可以在某些情况下有用。

### <a name="do-not-use-monadic-error-handling-to-replace-exceptions"></a>不使用一元错误处理程序来替换异常

异常被视为某种程度上禁忌在函数式编程。 实际上，异常违反纯度，以便安全地将其视为不完全正常工作。 但是，这会忽略代码必须运行的位置和该运行时，可能会发生错误的实际的情况。 一般情况下，假定大多数内容都是纯和总，尽量少的意外事件都不编写代码。

请务必考虑以下核心优势/方面的异常相对于其相关性和.NET 运行时和跨语言生态系统中作为一个整体的适合程度：

1. 它们包含详细的诊断信息，这一点非常有用，调试问题时。
2. 它们是由运行时和其他.NET 语言易于理解。
3. 它们可以减少大量样板与超出其方法的代码相比*避免*通过 ad hoc 基础上实现它们的语义的某个子集的异常。

此第三个点至关重要。 对于重要的复杂操作，无法使用异常会导致处理此类结构：

```fsharp
Result<Result<MyType, string>, string list>
```

这很容易导致脆弱的模式匹配的"stringly 类型化"错误代码：

```fsharp
let result = doStuff()
match result with
| Ok r -> ...
| Error e ->
    if e.Contains "Error string 1" then ...
    elif e.Contains "Error string 2" then ...
    else ... // Who knows?
```

此外，它可以是很吸引人，但在返回的"更好"类型的"简单"函数所需的任何异常：

```fsharp
// This is bad!
let tryReadAllText (path : string) =
    try System.IO.File.ReadAllText path |> Some
    with _ -> None
```

遗憾的是，`tryReadAllText`可能会引发大量异常基于在文件系统中，可以发生的事情的各种和此代码会立即丢弃有关可能实际上发生哪些错误在您的环境中的任何信息。 如果此代码替换为结果类型，然后您返回到"stringly 类型化"错误消息分析：

```fsharp
// This is bad!
let tryReadAllText (path : string) =
    try System.IO.File.ReadAllText path |> Ok
    with e -> Error e.Message

let r = tryReadAllText "path-to-file"
match r with
| Ok text -> ...
| Error e ->
    if e.Contains "uh oh, here we go again..." then ...
    else ...
```

并将放入异常对象本身中`Error`构造函数只是强制您能够正确处理在调用站点，而不是在函数中的异常类型。 执行此操作有效地创建选中是众所周知 unfun 作为 API 的调用方处理的异常。

与上述示例的良好替代方法是捕捉*特定*异常并返回该异常的上下文中有意义的值。 如果你修改`tryReadAllText`函数，如下所示，`None`具有更多的含义：

```fsharp
let tryReadAllTextIfPresent (path : string) =
    try System.IO.File.ReadAllText path |> Some
    with :? FileNotFoundException -> None
```

而不是作为万法归宗正常运行，此函数现在正确地处理这种情况时文件找不到，并将该含义分配给返回。 此返回值可以将映射到错误这种情况下，不放弃任何上下文信息或强制调用方不得不面临可能无法在该点在代码中相关的用例时。

类型，如`Result<'Success, 'Error>`适用于基本操作，其中它们不嵌套和 F# 可选类型非常适合表示当内容无法返回时，*一些*或*nothing*. 它们也不能取代有关例外情况，但是，和参数不应尝试使用，以替换异常。 相反，它们应当应用明智地到地址的异常和错误管理策略的特定方面中目标的方式。

## <a name="partial-application-and-point-free-programming"></a>部分应用程序和无点的编程

F# 无点的方式，支持部分应用程序，因此，不同的方法来计划。 这会很有用的代码重用在模块或实现的操作，但它通常不是要公开的内容。 一般情况下，无点的编程有益本身并不是，并可以添加一个巨大的认知障碍不沉浸在样式中的人员。

### <a name="do-not-use-partial-application-and-currying-in-public-apis"></a>不要使用部分应用程序和科中的公共 Api

有一些例外，在公共 Api 中的部分应用程序的用法容易混淆的使用者。 通常情况下， `let`-F# 代码中的绑定的值为**值**，而非**函数值**。 值和函数值，将混合在一起可能会导致保存少量的几行代码来交换一小段认知开销，尤其是与运算符结合使用如`>>`编写函数。

### <a name="consider-the-tooling-implications-for-point-free-programming"></a>请考虑无点的编程的工具含义

扩充的函数未标记其参数。 这会产生工具产生影响。 请考虑以下两个函数：

```fsharp
let func name age =
    printfn "My name is %s and I am %d years old!" name age

let funcWithApplication =
    printfn "My name is %s and I am %d years old!"
```

两者都是有效的函数，但`funcWithApplication`是扩充的函数。 当鼠标悬停在其类型在编辑器中时，会看到此：

```fsharp
val func : name:string -> age:int -> unit

val funcWithApplication : (string -> int -> unit)
```

在调用站点，如 Visual Studio 工具中的工具提示将不提供有意义信息关于什么`string`和`int`实际上表示输入的类型。

如果遇到类似的点无代码`funcWithApplication`公开使用，建议执行完全的 η 扩展，以便工具可以选择在有意义的自变量的名称。

此外，调试无点的代码可能相当困难，如果不是不可能。 调试工具依赖于绑定到名称的值 (例如，`let`绑定)，以便您可以检查中间值中途执行。 当你的代码具有没有要检查的值时，要调试。 将来，调试工具可能会发展为合成基于以前执行路径，这些值，但并不在草木皆兵你一个好办法*潜在*调试功能。

### <a name="consider-partial-application-as-a-technique-to-reduce-internal-boilerplate"></a>请考虑部分应用程序作为一种技术来减少内部样本

与以前的点，部分应用程序是非常棒的工具减少内部应用程序或 API 的更深层次的内部的样本。 它可以是有用的单元测试更复杂的 Api，样板通常非常困难不得不面临的实现。 例如，下面的代码演示如何可以完成哪些最模拟框架为您提供无需在此类框架使外部依赖关系，而无需了解相关订购 API。

例如，考虑以下解决方案拓扑：

```
MySolution.sln
|_/ImplementationLogic.fsproj
|_/ImplementationLogic.Tests.fsproj
|_/API.fsproj
```

`ImplementationLogic.fsproj` 例如，可能会公开代码：

```fsharp
module Transactions =
    let doTransaction txnContext txnType balance =
        ...

type Transactor(ctx, currentBalance) =
    member __.ExecuteTransaction(txnType) =
        Transactions.doTransaction ctx txtType currentBalance
        ...
```

单元测试`Transactions.doTransaction`在`ImplementationLogic.Tests.fspoj`很简单：

```fsharp
namespace TransactionsTestingUtil

open Transactions

module TransactionsTestable =
    let getTestableTransactionRoutine mockContext = Transactions.doTransaction mockContext
```

部分应用`doTransaction`与模拟上下文对象，而无需每次构造模拟的上下文中的所有单元测试都调用该函数可以：

```fsharp
namespace TransactionTests

open Xunit
open TransactionTypes
open TransactionsTestingUtil
open TransactionsTestingUtil.TransactionsTestable

let testableContext =
    { new ITransactionContext with
        member __.TheFirstMember() = ...
        member __.TheSecondMember() = ... }

let transactionRoutine = getTestableTransactionRoutine testableContext

[<Fact>]
let ``Test withdrawal transaction with 0.0 for balance``() =
    let expected = ...
    let actual = transactionRoutine TransactionType.Withdraw 0.0
    Assert.Equal(expected, actual)
```

不应将此技术普遍应用到整个代码库，但它是以减少样本的复杂的内部机制和单元测试这些内部结构的好方法。

## <a name="access-control"></a>访问控制

F# 的多个选项[访问控制](../language-reference/access-control.md)继承从所用的.NET 运行时中可用。 这些不是只可用于类型-您也可以使用它们对于函数。

* 更喜欢非`public`类型和成员，直到需要它们是公开使用。 这还可以尽量降低到哪些使用者几。
* 尽量保证所有帮助器功能`private`。
* 请考虑使用`[<AutoOpen>]`上的帮助器函数，如果它们可以大量专用模块。

## <a name="type-inference-and-generics"></a>类型推断和泛型

类型推断可以将保存您键入了大量的样板。 在 F# 编译器自动泛化可帮助您编写更为通用的代码几乎没有任何额外的工作量。 但是，这些功能不是普遍很好的。

* 考虑标签与公共 Api 中的显式类型的参数名称并不依赖此类型推断。

    这样做的原因在于**您**应在你的 API，编译器不该形状的控制。 虽然编译器可以执行在推断类型为您的正常作业，就可能有的 API 更改形状，如果它依赖于内部已更改类型。 这可能是你想的但几乎可以肯定会导致重大 API 变化的下游使用者然后需要处理。 相反，如果您显式控制公共 API 的形状，则可以控制这些重大更改。 在 DDD 术语中，这可以认为的防损层。

* 请考虑为泛型参数指定有意义的名称。

    除非你正在编写不是特定于特定域的真正泛型代码，有意义的名称可帮助了解的域处于其他程序员。 例如，名为的类型参数`'Document`与文档交互的上下文中数据库中可更清晰通用文档类型，可以接受由函数或正在使用的成员。

* 请考虑命名使用 pascal 命名法的泛型类型参数。

    这是常规的方法进行某些操作在.NET 中，因此建议使用 pascal 命名法而不是 snake_case 或驼峰式大小写。

最后，自动泛化并不总是不熟悉 F# 或大型基本代码的人员的一大福音。 在使用都是泛型方法的组件则认知开销。 此外，如果自动对不同的输入类型 (let 单独如果他们要这种情况下使用) 不使用通用的函数，就是在该点在时间没有实际的好处。 应始终考虑是否你正在编写的代码将实际上是受益泛型。

## <a name="performance"></a>性能

F# 的值为默认情况下，你可以避免某些 bug （特别是那些涉及并发和并行度） 的类不可变。 但是，在某些情况下，为了实现最佳 （或甚至合理） 高效的执行时间或内存分配的工作范围可能最实现使用就地变化的状态。 这可在使用 F# 与选择的基础`mutable`关键字。

但是，使用的`mutable`在 F# 中可能会觉得促使功能纯度。 这是没问题，如果调整到纯度上的预期[引用透明度](https://en.wikipedia.org/wiki/Referential_transparency)。 引用透明度-不纯度-时编写 F# 函数中的最终目标。 这可以通过性能关键代码的变化基于实现编写功能的接口。

### <a name="wrap-mutable-code-in-immutable-interfaces"></a>可变代码包装在不可变接口

作为一个目标的引用透明度，与编写代码，不会公开性能关键功能可变 underbelly 至关重要。 例如，下面的代码实现`Array.contains`F# 核心库中的函数：

```fsharp
[<CompiledName("Contains")>]
let inline contains value (array:'T[]) =
    checkNonNull "array" array
    let mutable state = false
    let mutable i = 0
    while not state && i < array.Length do
        state <- value = array.[i]
        i <- i + 1
    state
```

多次调用此函数不会更改基础数组，也不要求您维护中使用它的任何可变状态。 它是引用透明的即使的几乎每行代码在其中使用变化。

### <a name="consider-encapsulating-mutable-data-in-classes"></a>请考虑封装在类中的可变数据

前面的示例使用单个函数来封装操作使用可变的数据。 这并不总是能够满足更复杂的数据集。 请考虑以下几组函数：

```fsharp
open System.Collections.Generic

let addToClosureTable (key, value) (t: Dictionary<_,_>) =
    if not (t.ContainsKey(key)) then
        t.Add(key, value)
    else
        t.[key] <- value

let closureTableCount (t: Dictionary<_,_>) = t.Count

let closureTableContains (key, value) (t: Dictionary<_, HashSet<_>>) =
    match t.TryGetValue(key) with
    | (true, v) -> v.Equals(value)
    | (false, _) -> false
```

此代码是高性能，但它会公开调用方负责维护基于变化的数据结构。 这可以不包含可以更改任何基础成员类内部包装：

```fsharp
open System.Collections.Generic

/// The results of computing the LALR(1) closure of an LR(0) kernel
type Closure1Table() =
    let t = Dictionary<Item0, HashSet<TerminalIndex>>()

    member __.Add(key, value) =
        if not (t.ContainsKey(key)) then
            t.Add(key, value)
        else
            t.[key] <- value

    member __.Count = t.Count

    member __.Contains(key, value) =
        match t.TryGetValue(key) with
        | (true, v) -> v.Equals(value)
        | (false, _) -> false
```

`Closure1Table` 封装基础的基于变化的数据结构，从而不强制调用方可以维护基础数据结构。 类是封装数据和例程，而无需公开给调用方的详细信息是基于变化的一种强大方法。

### <a name="prefer-let-mutable-to-reference-cells"></a>更喜欢`let mutable`到引用单元格

引用单元格是一种方法来表示对一个值，而不是值本身的引用。 虽然它们可以用于性能关键代码，但它们通常不建议。 请看下面的示例：

```fsharp
let kernels =
    let acc = ref Set.empty

    processWorkList startKernels (fun kernel ->
        if not ((!acc).Contains(kernel)) then
            acc := (!acc).Add(kernel)
        ...)

    !acc |> Seq.toList
```

使用引用单元格现在"破坏"与无需取消引用和重新引用基础数据的所有后续代码。 相反，应考虑`let mutable`:

```fsharp
let kernels =
    let mutable acc = Set.empty

    processWorkList startKernels (fun kernel ->
        if not (acc.Contains(kernel)) then
            acc <- acc.Add(kernel)
        ...)

    acc |> Seq.toList
```

除了在 lambda 表达式中间的变化的单个点，所有其他代码的接触`acc`可以在没有任何差别的普通的使用情况的方式操作`let`-绑定不变的值。 这将使更轻松地随时间而变化。

## <a name="object-programming"></a>对象编程

F# 具有对对象和面向对象的 (OO) 概念的完整支持。 尽管许多 OO 概念是功能强大且有用，但并非所有这些都使用的理想之选。 以下列表提供类别在高级别 OO 功能的指导。

**请考虑在许多情况下使用这些功能：**

* 点表示法 (`x.Length`)
* 实例成员
* 隐式构造函数
* 静态成员
* 索引器表示法 (`arr.[x]`)
* 命名实参和可选实参
* 接口和接口实现

**不会到达这些功能的第一次，但请谨慎应用它们时才可以方便地解决问题：**

* 方法重载
* 封装的可变数据
* 类型运算符
* 自动属性
* 实现`IDisposable`和 `IEnumerable`
* 类型扩展
* 事件
* 结构
* 委托
* 枚举

**除非您必须将它们通常避免这些功能：**

* 基于继承的类型层次结构和实现继承
* Null 值和 `Unchecked.defaultof<_>`

### <a name="prefer-composition-over-inheritance"></a>组合为首继承

[通过继承复合](https://en.wikipedia.org/wiki/Composition_over_inheritance)是良好的 F# 代码可以遵循一个长期惯例。 基本原则是，不应公开的基类，强制调用方继承该基类可以实现功能。

### <a name="use-object-expressions-to-implement-interfaces-if-you-dont-need-a-class"></a>使用对象表达式实现接口，如果您不需要一个类

[对象表达式](../language-reference/object-expressions.md)可用于快速实现接口在无需执行此操作类内部实现的接口绑定到的值。 这很方便，尤其是当您_仅_需要实现接口并不需要完整的类。

例如，下面是在中运行的代码[Ionide](http://ionide.io/)提供的代码修复操作，如果你已添加没有的符号`open`语句：

```fsharp
    let private createProvider () =
        { new CodeActionProvider with
            member this.provideCodeActions(doc, range, context, ct) =
                let diagnostics = context.diagnostics
                let diagnostic = diagnostics |> Seq.tryFind (fun d -> d.message.Contains "Unused open statement")
                let res =
                    match diagnostic with
                    | None -> [||]
                    | Some d ->
                        let line = doc.lineAt d.range.start.line
                        let cmd = createEmpty<Command>
                        cmd.title <- "Remove unused open"
                        cmd.command <- "fsharp.unusedOpenFix"
                        cmd.arguments <- Some ([| doc |> unbox; line.range |> unbox; |] |> ResizeArray)
                        [|cmd |]
                res
                |> ResizeArray
                |> U2.Case1
        }
```

由于没有为类无需与 Visual Studio Code API 进行交互时，对象表达式是对此的理想工具。 它们也是有价值的单元测试，如果想要进行存根处理出测试例程的接口中特别的方式。

## <a name="type-abbreviations"></a>类型缩写

[类型缩写，用](../language-reference/type-abbreviations.md)是要将标签分配到另一个类型，例如函数签名或更复杂类型的简便方法。 例如，以下别名将标签分配给所需定义与计算[CNTK](https://www.microsoft.com/en-us/cognitive-toolkit/)、 深度学习库：

```fsharp
open CNTK

// DeviceDescriptor, Variable, and Function all come from CNTK
type Computation = DeviceDescriptor -> Variable -> Function
```

`Computation`名称是以表示它是别名的签名匹配的任何函数的简便方法。 使用此类类型缩写方便，且允许更简洁的代码。

### <a name="avoid-using-type-abbreviations-to-represent-your-domain"></a>避免使用类型缩写来表示你的域

尽管类型缩写便于到函数签名中提供一个名称，但它们可以是令人困惑时缩写加上其他类型。 请考虑此缩写：

```fsharp
// Does not actually abstract integers.
type BufferSize = int
```

这可以是令人困惑，在多个方面：

* `BufferSize` 不是一个抽象概念。它是整数的只是另一个名称。
* 如果`BufferSize`公开在公共 API 中，它可以轻松地被错误地解释不止是表示`int`。 通常情况下，域类型具有多个属性到它们并不是基元类型，如`int`。 此缩写违反了这种假设。
* 大小写`BufferSize`（pascal 命名法） 意味着此类型包含更多的数据。
* 此别名不提供与提供的函数的命名的参数进行比较时会更加的明确。
* 缩写不将清单中已编译 IL;它是只是一个整数，此别名是编译时构造。

```fsharp
module Networking =
    ...
    let send data (bufferSize: int) =
        ...
```

总之，与类型缩写缺陷是它们**不**抽象概念通过它们缩写加上的类型。 在上一示例中，`BufferSize`只是`int`事实上，与任何其他数据，也不从除了什么类型系统的任何权益`int`已有。
