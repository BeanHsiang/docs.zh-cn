---
title: F#代码格式设置准则
description: 了解有关格式设置准则F#代码。
ms.date: 02/08/2019
ms.openlocfilehash: 7cbd8e4dd1f58cd974a8a12fc8a8c9ee92c546b4
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56093614"
---
# <a name="f-code-formatting-guidelines"></a>F#代码格式设置准则

本文提供有关如何设置代码的格式的指导原则，以便在F#代码是：

* 通常以更清晰的形式查看
* 符合应用的 Visual Studio 中的工具和其他编辑器格式设置约定
* 类似于其他代码联机

这些指导基于[的全面指南F#格式设置约定](https://github.com/dungpa/fantomas/blob/master/docs/FormattingConventions.md)通过[Anh Dung Phan](https://github.com/dungpa)。

## <a name="general-rules-for-indentation"></a>缩进的一般规则

F#默认情况下使用有意义的空白。 以下指南旨在提供指导如何能够同时处理这可以施加一些挑战。

### <a name="using-spaces"></a>使用的空间

需要缩进时，您必须使用空格，不是制表符。 至少一个空间是必需的。 你的组织可以创建以指定要用于缩进; 的空格数的编码标准典型的缩进发生每个级别的缩进的两个、 三个或四个空格。

**我们建议每个缩进的 4 个空格。**

也就是说，缩进的程序是一个主观问题。 变体是好的但应遵循的第一个规则*缩进的一致性*。 选择一种普遍接受的缩进样式，并在整个代码库系统地使用它。

## <a name="formatting-white-space"></a>格式设置的空白区域

F#是敏感的空白区域。 尽管正确缩进涵盖空白的大多数语义，有一些需要考虑的其他事项。

### <a name="formatting-operators-in-arithmetic-expressions"></a>算术表达式中的格式设置运算符

始终使用二进制算术表达式周围的空白区域：

```fsharp
let subtractThenAdd x = x - 1 + 3
```

一元`-`运算符应始终具有它们传递的值在后面紧跟：

```fsharp
// OK
let negate x = -x

// Bad
let negateBad x = - x
```

添加空白字符后的`-`运算符可能会导致其他人混淆。

总之，务必始终：

* 含空白区域的外侧代码二元运算符
* 一元运算符后没有尾随空格

二进制算术运算符准则是尤为重要。 失败来包围二进制`-`运算符，与特定格式设置选项结合使用时可能会导致它解释为一元`-`。

### <a name="surround-a-custom-operator-definition-with-white-space"></a>外侧代码具有空白的自定义运算符的定义

始终使用空格来包围运算符定义：

```fsharp
// OK
let ( !> ) x f = f x

// Bad
let (!>) x f = f x
```

对于任何自定义的运算符开头`*`，将需要添加到的要避免编译器不明确的定义开头的空白区域。 因此，建议您只需括起来的单个空白字符的所有运算符的定义。

### <a name="surround-function-parameter-arrows-with-white-space"></a>环绕含空白区域的函数参数箭头

在定义函数的签名时，使用周围的空白区域`->`符号：

```fsharp
// OK
type MyFun = int -> int -> string

// Bad
type MyFunBad = int->int->string
```

## <a name="formatting-blank-lines"></a>格式设置的空行

* 单独顶级函数和类定义包含两个空白行。
* 方法定义的类的内部由一个空行分隔。
* 可能会 （谨慎） 使用额外的空白行到单独的组相关的函数。 一系列相关一行式命令 （例如，一组虚拟实现） 之间，可以忽略空白行。
* 使用空白行在函数中，尽量少，以指示逻辑部分。

## <a name="formatting-comments"></a>格式设置的注释

通常将多个双斜杠注释为首 ML 样式块注释。

```fsharp
// Prefer this style of comments when you want
// to express written ideas on multiple lines.

(*
    ML-style comments are fine, but not a .NET-ism.
    They are useful when needing to modify multi-line comments, though.
*)
```

内联注释应的首字母大写。

```fsharp
let f x = x + 1 // Increment by one.
```

## <a name="naming-conventions"></a>命名约定

### <a name="use-camelcase-for-class-bound-expression-bound-and-pattern-bound-values-and-functions"></a>使用驼峰式大小写的类绑定、 表达式绑定和绑定模式的值和函数

通常会接受F#的绑定作为本地变量或在模式匹配的所有名称和函数定义采用驼峰式大小写样式。

```fsharp
// OK
let addIAndJ i j = i + j

// Bad
let addIAndJ I J = I+J

// Bad
let AddIAndJ i j = i + j
```

本地绑定类中的函数还应使用驼峰式大小写。

```fsharp
type MyClass() =

    let doSomething () =

    let firstResult = ...

    let secondResult = ...

    member x.Result = doSomething()
```

### <a name="use-camelcase-for-module-bound-public-functions"></a>有关绑定到模块的公共函数使用驼峰式大小写

当模块绑定函数是一个公共 API 的一部分时，它应使用驼峰式大小写：

```fsharp
module MyAPI =
    let publicFunctionOne param1 param2 param2 = ...

    let publicFunctionTwo param1 param2 param3 = ...
```

### <a name="use-camelcase-for-internal-and-private-module-bound-values-and-functions"></a>使用驼峰式大小写的内部和专用模块绑定值和函数

对于专用模块绑定值，其中包括使用驼峰式大小写：

* 在脚本中的即席函数

* 值组成的模块或类型的内部实现

```fsharp
let emailMyBossTheLatestResults =
    ...
```

### <a name="use-camelcase-for-parameters"></a>对参数使用驼峰式大小写

所有参数应都使用驼峰式大小写，根据.NET 命名约定。

```fsharp
module MyModule =
    let myFunction paramOne paramTwo = ...

type MyClass() =
    member this.MyMethod(paramOne, paramTwo) = ...
```

### <a name="use-pascalcase-for-modules"></a>模块使用 pascal 命名法

（顶级、 内部、 专用、 嵌套） 的所有模块都应都使用 pascal 命名法。

```fsharp
module MyTopLevelModule

module Helpers =
    module private SuperHelpers =
        ...

    ...
```

### <a name="use-pascalcase-for-type-declarations-members-and-labels"></a>类型声明、 成员和标签的使用 pascal 命名法

类、 接口、 结构、 枚举、 委托、 记录和可区分的联合所有的命名应当使用 pascal 命名法。 类型和标签的记录和可区分的联合中的成员还应使用 pascal 命名法。

```fsharp
type IMyInterface =
    abstract Something: int

type MyClass() =
    member this.MyMethod(x, y) = x + y

type MyRecord = { IntVal: int; StringVal: string }

type SchoolPerson =
    | Professor
    | Student
    | Advisor
    | Administrator
```

### <a name="use-pascalcase-for-constructs-intrinsic-to-net"></a>为.NET 中的内部构造使用 pascal 命名法

命名空间、 异常、 事件和项目 /`.dll`名称还应使用 pascal 命名法。 不仅这会使来自其他.NET 语言的消耗感觉更自然向使用者，也是与你可能会遇到的.NET 命名约定保持一致。

### <a name="avoid-underscores-in-names"></a>避免在名称中的下划线

从历史上看，一些F#库的名称中使用下划线。 但是，这是不能再广受认可，部分原因是因为它与.NET 命名约定冲突。 话虽如此，一些F#程序员出于历史原因，很大程度、 一定程度上使用下划线和容差和方面非常重要。 但是，请注意样式通常会不喜欢的其他用户可以选择要使用它。

一些例外情况包括与本机组件交互下划线很常见。

### <a name="use-standard-f-operators"></a>使用标准F#运算符

以下运算符定义中F#标准库，应使用而不是定义等效项。 建议使用这些运算符，因为它往往会使代码更具可读性且惯用。 具有背景的 OCaml 或其他功能的编程语言的开发人员可能习惯于不同编程惯例。 以下列表总结了推荐的F#运算符。

```fsharp
x |> f // Forward pipeline
f >> g // Forward composition
x |> ignore // Discard away a value
x + y // Overloaded addition (including string concatenation)
x - y // Overloaded subtraction
x * y // Overloaded multiplication
x / y // Overloaded division
x % y // Overloaded modulus
x && y // Lazy/short-cut "and"
x || y // Lazy/short-cut "or"
x <<< y // Bitwise left shift
x >>> y // Bitwise right shift
x ||| y // Bitwise or, also for working with “flags” enumeration
x &&& y // Bitwise and, also for working with “flags” enumeration
x ^^^ y // Bitwise xor, also for working with “flags” enumeration
```

### <a name="use-prefix-syntax-for-generics-foot-in-preference-to-postfix-syntax-t-foo"></a>前缀语法用于泛型 (`Foo<T>`) 优先于后缀语法 (`T Foo`)

F#继承这两个后缀机器学习的样式命名泛型类型 (例如， `int list`) 以及.NET 样式的前缀 (例如， `list<int>`)。 .NET 样式，除了四种特定类型为首选项：

1. 有关F#列表中，使用后缀形式：`int list`而非`list<int>`。
2. 有关F#选项，请使用后缀形式：`int option`而非`option<int>`。
3. 有关F#数组，使用语法名称`int[]`而非`int array`或`array<int>`。
4. 对于引用单元格，请使用`int ref`而非`ref<int>`或`Ref<int>`。

对于所有其他类型，请使用前缀形式。

## <a name="formatting-tuples"></a>格式设置的元组

元组实例化应该是用圆括号括起来，和中分隔的逗号应后跟一个空格，例如： `(1, 2)`， `(x, y, z)`。

它通常被接受以忽略在模式匹配的元组中的括号：

```fsharp
let (x, y) = z // Destructuring
let x, y = z // OK

// OK
match x, y with
| 1, _ -> 0
| x, 1 -> 0
| x, y -> 1
```

它通常也接受可以省略括号，如果元组是一个函数的返回值：

```fsharp
// OK
let update model msg =
    match msg with
    | 1 -> model + 1, []
    | _ -> model, [ msg ]
```
总之，更喜欢用圆括号括起来的元组实例化，但当使用模式匹配或返回值元组，它被视为可以避免括号。

## <a name="formatting-discriminated-union-declarations"></a>格式设置可区分联合声明

缩进`|`由 4 个空格的类型定义中：

```fsharp
// OK
type Volume =
    | Liter of float
    | FluidOunce of float
    | ImperialPint of float

// Not OK
type Volume =
| Liter of float
| USPint of float
| ImperialPint of float
```

## <a name="formatting-discriminated-unions"></a>格式设置可区分联合

将拆分到多个行的实例化的可区分联合应为包含的数据提供具有缩进的新作用域：

```fsharp
let tree1 =
    BinaryNode
        (BinaryNode(BinaryValue 1, BinaryValue 2),
         BinaryNode(BinaryValue 3, BinaryValue 4))
```

右括号还可以在新的一行：

```fsharp
let tree1 =
    BinaryNode(
        BinaryNode(BinaryValue 1, BinaryValue 2),
        BinaryNode(BinaryValue 3, BinaryValue 4)
    )
```

## <a name="formatting-record-declarations"></a>格式设置的记录声明

缩进`{`类型中定义由 4 空格和同一行上开始的字段列表：

```fsharp
// OK
type PostalAddress =
    { Address: string
      City: string
      Zip: string }
    member x.ZipAndCity = sprintf "%s %s" x.Zip x.City

// Not OK
type PostalAddress =
  { Address: string
    City: string
    Zip: string }
    member x.ZipAndCity = sprintf "%s %s" x.Zip x.City
    
// Unusual in F#
type PostalAddress =
    { 
        Address: string
        City: string
        Zip: string
    }
```

将打开标记放置在一个新行和新行中的右令牌是更可取，如果要声明接口实现或成员的记录：

```fsharp
// Declaring additional members on PostalAddress
type PostalAddress =
    { 
        Address: string
        City: string
        Zip: string
    } with
    member x.ZipAndCity = sprintf "%s %s" x.Zip x.City
    
type MyRecord =
    {
        SomeField: int
    }
    interface IMyInterface
```

## <a name="formatting-records"></a>格式设置的记录

可以在一行中编写短记录：

```fsharp
let point = { X = 1.0; Y = 0.0 }
```

较长的记录标签应使用新行：

```fsharp
let rainbow =
    { Boss = "Jeffrey"
      Lackeys = ["Zippy"; "George"; "Bungle"] }
```

放置在打开令牌在新的一行，内容选项卡式通过一个作用域，并置于新行的结束标记是如果您是更可取：

* 四处移动记录，在代码中使用不同的缩进作用域
* 通过管道将它们传递到函数

```fsharp
let rainbow =
    {
        Boss1 = "Jeffrey"
        Boss2 = "Jeffrey"
        Boss3 = "Jeffrey"
        Boss4 = "Jeffrey"
        Boss5 = "Jeffrey"
        Boss6 = "Jeffrey"
        Boss7 = "Jeffrey"
        Boss8 = "Jeffrey"
        Lackeys = ["Zippy"; "George"; "Bungle"]
    }
    
type MyRecord =
    {
        SomeField: int
    }
    interface IMyInterface

let foo a =
    a
    |> Option.map (fun x ->
        {
            MyField = x
        })
```

相同的规则适用于列表和数组元素。

## <a name="formatting-copy-and-update-record-expressions"></a>设置复制更新记录表达式格式

复制更新记录表达式仍然是一条记录，因此类似的准则适用于。

短表达式可以适合某个行：

```fsharp
let point2 = { point with X = 1; Y = 2 }
```

较长的表达式应使用新行：

```fsharp
let rainbow2 =
    { rainbow with
        Boss = "Jeffrey"
        Lackeys = ["Zippy"; "George"; "Bungle"] }
```

和记录的指导，您可能想要将专用的大括号的单独的行和缩进到右侧的表达式的一个作用域。 请注意，在某些特殊情况，例如 wrapping 具有不带括号，可选的值中你可能需要保留在同一行的大括号：

```fsharp    
type S = { F1: int; F2: string }
type State = { F:  S option }

let state = { F = Some { F1 = 1; F2 = "Hello" } }
let newState = 
    {
        state with
            F = Some {
                    F1 = 0
                    F2 = ""
                }
    }
```

## <a name="formatting-lists-and-arrays"></a>格式设置的列表和数组

编写`x :: l`与周围的空格`::`运算符 (`::`为中缀运算符，因此由空格括起来)。

列表和在单个行上声明的数组应具有一个空格后的左括号和右括号之间：

```fsharp
let xs = [ 1; 2; 3 ]
let ys = [| 1; 2; 3; |]
```

始终使用两个不同的大括号类似于运算符之间至少一个空格。 例如，将保留之间有空格`[`和一个`{`。

```fsharp
// OK
[ { IngredientName = "Green beans"; Quantity = 250 }
  { IngredientName = "Pine nuts"; Quantity = 250 }
  { IngredientName = "Feta cheese"; Quantity = 250 }
  { IngredientName = "Olive oil"; Quantity = 10 }
  { IngredientName = "Lemon"; Quantity = 1 } ]

// Not OK
[{ IngredientName = "Green beans"; Quantity = 250 }
 { IngredientName = "Pine nuts"; Quantity = 250 }
 { IngredientName = "Feta cheese"; Quantity = 250 }
 { IngredientName = "Olive oil"; Quantity = 10 }
 { IngredientName = "Lemon"; Quantity = 1 }]
```

相同原则也适用于列表或数组的元组。

列表和拆分到多个行的数组记录一样遵循类似的规则：

```fsharp
let pascalsTriangle =
    [|
        [| 1 |]
        [| 1; 1 |]
        [| 1; 2; 1 |]
        [| 1; 3; 3; 1 |]
        [| 1; 4; 6; 4; 1 |]
        [| 1; 5; 10; 10; 5; 1 |]
        [| 1; 6; 15; 20; 15; 6; 1 |]
        [| 1; 7; 21; 35; 35; 21; 7; 1 |]
        [| 1; 8; 28; 56; 70; 56; 28; 8; 1 |]
    |]
```

和与记录，在自己的行上声明左、 右括号将简化移动代码和到函数中的管道。

## <a name="formatting-if-expressions"></a>如果格式设置表达式

条件语句的缩进取决于把它们组合起来的表达式的大小。 如果`cond`，`e1`和`e2`简短，只需将它们写在同一行中：

```fsharp
if cond then e1 else e2
```

如果任一`cond`，`e1`或`e2`更长时间，但不多的行：

```fsharp
if cond
then e1
else e2
```

如果是多行的任何表达式：

```fsharp
if cond then
    e1
else
    e2
```

使用多个条件语句`elif`并`else`都在同一作用域为缩进`if`:

```fsharp
if cond1 then e1
elif cond2 then e2
elif cond3 then e3
else e4
```

### <a name="pattern-matching-constructs"></a>模式匹配构造

使用`|`无缩进匹配项的每个子句。 如果表达式很短，则可以考虑使用单独的一行，如果每一子表达式也非常简单。

```fsharp
// OK
match l with
| { him = x; her = "Posh" } :: tail -> x
| _ :: tail -> findDavid tail
| [] -> failwith "Couldn't find David"

// Not OK
match l with
    | { him = x; her = "Posh" } :: tail -> x
    | _ :: tail -> findDavid tail
    | [] -> failwith "Couldn't find David"
```

如果在模式匹配箭头右侧的表达式太大，则将其移动到以下行，缩进一个步骤，从`match` / `|`。

```fsharp
match lam with
| Var v -> 1
| Abs(x, body) ->
    1 + sizeLambda body
| App(lam1, lam2) ->
    sizeLambda lam1 + sizeLambda lam2

```

模式匹配的匿名函数，通过启动`function`，应通常不缩进太远。 例如，按如下所示缩进一个作用域是没问题：

```fsharp
lambdaList
|> List.map (function
    | Abs(x, body) -> 1 + sizeLambda 0 body
    | App(lam1, lam2) -> sizeLambda (sizeLambda 0 lam1) lam2
    | Var v -> 1)
```

通过定义的函数中的模式匹配`let`或`let rec`应在启动后的缩进的 4 个空格`let`，即使`function`使用关键字：

```fsharp
let rec sizeLambda acc = function
    | Abs(x, body) -> sizeLambda (succ acc) body
    | App(lam1, lam2) -> sizeLambda (sizeLambda acc lam1) lam2
    | Var v -> succ acc
```

我们不建议对齐箭头。

## <a name="formatting-trywith-expressions"></a>格式设置 try / with 表达式

模式匹配异常类型应为相同的级别缩进`with`。

```fsharp
try
    if System.DateTime.Now.Second % 3 = 0 then
        raise (new System.Exception())
    else
        raise (new System.ApplicationException())
with
| :? System.ApplicationException ->
    printfn "A second that was not a multiple of 3"
| _ ->
    printfn "A second that was a multiple of 3"
```

## <a name="formatting-function-parameter-application"></a>格式设置函数参数应用程序

一般情况下，大多数函数参数应用程序可在同一行。

如果你想要应用到新行上的函数的参数，将它们缩进按一个作用域。

```fsharp
// OK
sprintf "\t%s - %i\n\r"
     x.IngredientName x.Quantity

// OK
sprintf
     "\t%s - %i\n\r"
     x.IngredientName x.Quantity

// OK
let printVolumes x =
    printf "Volume in liters = %f, in us pints = %f, in imperial = %f"
        (convertVolumeToLiter x)
        (convertVolumeUSPint x)
        (convertVolumeImperialPint x)
```

适用的 lambda 表达式作为函数参数相同的准则。 如果 lambda 表达式，主体的主体可以拥有另一个行，缩进一个作用域

```fsharp
let printListWithOffset a list1 =
    List.iter
        (fun elem -> printfn "%d" (a + elem))
        list1

// OK if lambda body is long enough
let printListWithOffset a list1 =
    List.iter
        (fun elem ->
            printfn "%d" (a + elem))
        list1
```

但是，如果 lambda 表达式的主体是多个行，请考虑一下分离到单独的函数而不是具有多行构造为单个参数应用于函数。

### <a name="formatting-infix-operators"></a>格式设置中缀运算符

由空格的单独运算符。 是此规则的例外明显`!`和`.`运算符。

中缀表达式是同一列上的配置列表确定:

```fsharp
acc +
(sprintf "\t%s - %i\n\r"
     x.IngredientName x.Quantity)

let function1 arg1 arg2 arg3 arg4 =
    arg1 + arg2 +
    arg3 + arg4
```

### <a name="formatting-pipeline-operators"></a>格式设置管道运算符

管道`|>`运算符应发送到下对它们进行操作的表达式。

```fsharp
// Preferred approach
let methods2 =
    System.AppDomain.CurrentDomain.GetAssemblies()
    |> List.ofArray
    |> List.map (fun assm -> assm.GetTypes())
    |> Array.concat
    |> List.ofArray
    |> List.map (fun t -> t.GetMethods())
    |> Array.concat

// Not OK
let methods2 = System.AppDomain.CurrentDomain.GetAssemblies()
            |> List.ofArray
            |> List.map (fun assm -> assm.GetTypes())
            |> Array.concat
            |> List.ofArray
            |> List.map (fun t -> t.GetMethods())
            |> Array.concat
```

### <a name="formatting-modules"></a>格式设置模块

本地模块中的代码必须将缩进，相对于该模块，但顶级模块中的代码不应缩进。 Namespace 元素无需将缩进。

```fsharp
// A is a top-level module.
module A

let function1 a b = a - b * b
```

```fsharp
// A1 and A2 are local modules.
module A1 =
    let function1 a b = a*a + b*b

module A2 =
    let function2 a b = a*a - b*b
```

### <a name="formatting-object-expressions-and-interfaces"></a>格式设置对象表达式和接口

应使用相同的方式对齐对象表达式和接口`member`要缩进后 4 个空格。

```fsharp
let comparer =
    { new IComparer<string> with
          member x.Compare(s1, s2) =
              let rev (s: String) =
                  new String (Array.rev (s.ToCharArray()))
              let reversed = rev s1
              reversed.CompareTo (rev s2) }
```

### <a name="formatting-white-space-in-expressions"></a>格式表达式中的空白区域

避免多余空白区域，在F#表达式。

```fsharp
// OK
spam (ham.[1])

// Not OK
spam ( ham.[ 1 ] )
```

命名的参数也不应具有空间周围`=`:

```fsharp
// OK
let makeStreamReader x = new System.IO.StreamReader(path=x)

// Not OK
let makeStreamReader x = new System.IO.StreamReader(path = x)
```

## <a name="formatting-attributes"></a>格式设置特性

[属性](../language-reference/attributes.md)位于上方构造：

```fsharp
[<SomeAttribute>]
type MyClass() = ...

[<RequireQualifiedAccess>]
module M =
    let f x = x

[<Struct>]
type MyRecord =
    { Label1: int
      Label2: string }
```

### <a name="formatting-attributes-on-parameters"></a>参数格式设置特性

属性也可以是参数上的位置。 在这种情况下，将它们放置在作为参数并在名称前在同一行上：

```fsharp
// Defines a class that takes an optional value as input defaulting to false.
type C() =
    member __.M([<Optional; DefaultParameterValue(false)>] doSomething: bool)
```

### <a name="formatting-multiple-attributes"></a>格式设置多个属性

当多个属性应用于一个构造，它不是参数时，应将它们放，只有每行一个特性：

```fsharp
[<Struct>]
[<IsByRefLike>]
type MyRecord =
    { Label1: int
      Label2: string }
```

应用于参数时，它们必须在同一行，分隔`;`分隔符。

## <a name="formatting-literals"></a>设置文本的格式

[F#文字](../language-reference/literals.md)使用`Literal`属性应置于各自的行的属性，然后使用驼峰式大小写命名：

```fsharp
[<Literal>]
let path = __SOURCE_DIRECTORY__ + "/" + __SOURCE_FILE__

[<Literal>]
let myUrl = "www.mywebsitethatiamworkingwith.com"
```

避免在值所在的同一行上放置属性。
