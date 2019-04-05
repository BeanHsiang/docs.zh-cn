---
title: 模式匹配
description: 了解如何在中使用模式F#若要比较的逻辑结构的数据，将数据分解为各个构成部分，或从数据中提取信息。
ms.date: 05/16/2016
ms.openlocfilehash: bb6b41f6d15612e4a65abd4a3d5d7291d84a8f3c
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613578"
---
# <a name="pattern-matching"></a>模式匹配

模式是用于转换输入的数据的规则。 在整个F#语言要比较数据的逻辑结构或结构，将数据分解为各个构成部分，或从以各种方式的数据中提取信息。

## <a name="remarks"></a>备注

在许多语言构造，如使用模式`match`表达式。 正在处理中的函数的参数时使用它们`let`绑定、 lambda 表达式和中与相关联的异常处理程序`try...with`表达式。 有关详细信息，请参阅[匹配表达式](match-expressions.md)， [let 绑定](functions/let-bindings.md)， [Lambda 表达式：`fun`关键字](functions/lambda-expressions-the-fun-keyword.md)，和[异常：`try...with`表达式](exception-handling/the-try-with-expression.md)。

例如，在`match`表达式中，*模式*是竖线的后面。

```fsharp
match expression with
| pattern [ when condition ] -> result-expression
...
```

每个模式都充当转换输入以某种方式的规则。 在`match`又检查表达式中，每个模式来查看输入的数据是否与模式兼容。 如果找到匹配项，则执行结果表达式。 如果找不到匹配项，则测试下一个模式规则。 可选 when*条件*一部分所述[匹配表达式](match-expressions.md)。

受支持的模式下表所示。 在运行时，对输入进行测试对每个表中列出的顺序中的以下模式和模式以递归方式应用，从第一次到最后一个出现在代码中，并从左到右的模式的每个行。

|name|描述|示例|
|----|-----------|-------|
|常量模式|任何数字、 字符或字符串文本、 枚举常量或定义的文本标识符|`1.0`, `"test"`, `30`, `Color.Red`|
|标识符模式|可区分的联合、 异常标签或活动模式用例的用例值|`Some(x)`<br /><br />`Failure(msg)`|
|变量模式|*identifier*|`a`|
|`as` 模式|*模式*作为*标识符*|`(a, b) as tuple1`|
|或模式|*pattern1* &#124; *pattern2 下*|<code>([h] &#124; [h; _])</code>|
|和模式|*pattern1* &amp; *pattern2 下*|`(a, b) & (_, "test")`|
|Cons 模式|*标识符*::*列表标识符*|`h :: t`|
|列表模式|[*模式 1*;...;*模式 n* ]|`[ a; b; c ]`|
|数组模式|[&#124; *模式 1*;..;*模式 n* &#124;]|<code>[&#124; a; b; c &#124;]</code>|
|带括号模式|(*模式*)|`( a )`|
|元组模式|(*模式 1*、...、*模式 n* )|`( a, b )`|
|记录模式|{ *identifier1* = *模式 1*;...;*标识符 n* = *模式 n* }|`{ Name = name; }`|
|通配符模式|_|`_`|
|带有类型批注的模式|*模式*:*类型*|`a : int`|
|类型测试模式|:? *类型*[作为*标识符*]|`:? System.DateTime as dt`|
|Null 模式|null|`null`|

## <a name="constant-patterns"></a>常量模式

常量模式是数值、 字符和字符串文本、 枚举常量 （包括枚举类型名称）。 一个`match`只有常量模式的表达式可以比作其他语言中的 case 语句。 输入与文本值进行比较，则模式匹配的值是否相等。 文字的类型必须与输入的类型兼容。

下面的示例演示如何使用文本模式，并还使用了变量模式和 OR 模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4801.fs)]

文本模式的另一个示例是基于枚举常量的模式。 使用枚举常量时，必须指定枚举类型名称。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4802.fs)]

## <a name="identifier-patterns"></a>标识符模式

如果模式是形成有效标识符字符的字符串，该标识符的形式确定如何匹配该模式。 如果标识符的长度超过一个字符和大写字符开头，编译器将尝试与标识符模式进行匹配。 此模式的标识符可以是标记为文本特性、 可区分联合用例、 异常标识符或活动模式用例的值。 如果不找到任何匹配的标识符，则匹配将失败下, 一个模式规则变量模式进行比较的输入。

可区分联合模式可以是简单的命名用例或它们可能有一个值或包含多个值的元组。 如果没有一个值，则必须指定值的标识符。 如果存在元组，必须提供一个元组模式与元组的每个元素的标识符或具有一个字段名称的标识符或多个命名联合的字段。 请参阅本部分中用于示例的代码示例。

`option`类型是具有两种情况下，一个可区分的联合`Some`和`None`。 一个用例 (`Some`) 的一个值，但其他 (`None`) 是只是命名用例。 因此，`Some`需要具有与关联的值的变量`Some`，但`None`必须单独出现。 在下面的代码中，变量`var1`都提供了通过到匹配值`Some`用例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4803.fs)]

在以下示例中，`PersonName`可区分的联合混合的字符串和表示可能的名称形式的字符。 可区分联合的情况下都`FirstOnly`， `LastOnly`，和`FirstLast`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4804.fs)]

对于具有命名字段的可区分联合，你可以使用等号 （=） 中提取命名字段的值。 例如，考虑具有如下所示的声明的可区分的联合。

```fsharp
type Shape =
    | Rectangle of height : float * width : float
    | Circle of radius : float
```

可以使用模式匹配表达式中的命名的字段，如下所示。

```fsharp
let matchShape shape =
    match shape with
    | Rectangle(height = h) -> printfn "Rectangle with length %f" h
    | Circle(r) -> printfn "Circle with radius %f" r
```

已命名字段的使用是可选的因此在上一示例中，同时`Circle(r)`和`Circle(radius = r)`具有相同的效果。

当指定多个字段时，请使用分号 （;） 作为分隔符。

```
match shape with
| Rectangle(height = h; width = w) -> printfn "Rectangle with height %f and width %f" h w
| _ -> ()
```

活动的模式，您可以定义更复杂的自定义模式匹配。 有关活动模式的详细信息，请参阅[活动模式](active-patterns.md)。

在其中标识符是异常的情况下用在模式匹配的异常处理程序上下文中。 有关异常处理中的模式匹配的信息，请参阅[异常：`try...with`表达式](exception-handling/the-try-with-expression.md)。

## <a name="variable-patterns"></a>变量模式

变量模式将与变量名称，然后可在右侧的执行表达式中使用该名称匹配的值分配`->`符号。 变量模式单独匹配任何输入，但变量模式通常出现在其他模式，从而更复杂的结构，例如元组和数组分解为变量中。

下面的示例演示一个元组模式内的变量模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4805.fs)]

## <a name="as-pattern"></a>as 模式

`as`模式是一种模式具有`as`子句附加到它。 `as`子句将匹配的值绑定到可用的执行表达式中的名称`match`表达式，或在此模式中的使用位置的情况下`let`绑定，将名称添加作为到局部范围的绑定。

下面的示例使用`as`模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4806.fs)]

## <a name="or-pattern"></a>或模式

输入的数据可以与匹配多个模式，并且想要作为结果执行相同代码时，则使用 OR 模式。 OR 模式两边的类型必须兼容。

下面的示例演示 OR 模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4807.fs)]

## <a name="and-pattern"></a>和模式

AND 模式要求的输入匹配两种模式。 AND 模式两边的类型必须兼容。

下面的示例就像`detectZeroTuple`中所示[元组模式](https://msdn.microsoft.com/library/#tuple)后面本主题中，但此处部分`var1`和`var2`通过使用 AND 模式获得作为值。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4808.fs)]

## <a name="cons-pattern"></a>Cons 模式

Cons 模式用于将列表分解为第一个元素， *head*，和一个列表，其中包含其余元素*结尾*。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4809.fs)]

## <a name="list-pattern"></a>列表模式

利用列表模式可将列表分解为多个元素。 在列表模式本身可以匹配特定数量的元素组成的列表。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4810.fs)]

## <a name="array-pattern"></a>数组模式

数组模式类似于列表模式，并且可用于将分解特定长度的数组。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4811.fs)]

## <a name="parenthesized-pattern"></a>带括号模式

可以围绕模式来实现所需的关联性分组括号。 在以下示例中，括号用于控制 AND 模式和 cons 模式之间的关联性。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4812.fs)]

## <a name="tuple-pattern"></a>元组模式

元组模式与元组形式的输入匹配，并启用要使用的模式匹配的元组中每个位置的变量分解为其构成元素的元组。

以下示例演示元组模式，并且还使用文本模式、 变量模式和通配符模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4813.fs)]

## <a name="record-pattern"></a>记录模式

记录模式用于分解记录以提取字段的值。 该模式不必引用记录; 该记录的所有字段任何忽略的字段仅不参与匹配，并且不会提取。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4814.fs)]

## <a name="wildcard-pattern"></a>通配符模式

通配符模式均由下划线 (`_`) 字符，并匹配任何输入，就像变量模式一样，不同之处在于输入丢弃而不是分配给一个变量。 通配符模式通常用于在其他模式内作为占位符在右侧的表达式中不需要的值`->`符号。 也经常模式的列表的末尾使用通配符模式匹配任何不匹配的输入。 本主题中的许多代码示例中演示的通配符模式。 请参阅前面的代码查看一个示例。

## <a name="patterns-that-have-type-annotations"></a>具有类型批注的模式

模式可以有类型批注。 这些行为类似于其他类型批注，指导推理等其他类型批注。 类型批注的模式的模式要求使用括号。 下面的代码演示具有类型批注的模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4815.fs)]

## <a name="type-test-pattern"></a>类型测试模式

类型测试模式用于匹配类型的输入。 如果输入的类型是与匹配的 （或派生的类型的） 成功的模式匹配中指定的类型。

下面的示例演示类型测试模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4816.fs)]

## <a name="null-pattern"></a>Null 模式

Null 模式匹配时你正在使用允许 null 值的类型，可能出现 null 值。 与.NET Framework 代码交互操作时，经常使用 null 模式。 例如，.NET API 的返回值可能是输入到`match`表达式。 您可以控制是否返回值为 null，并且也返回的值的其他特征上基于的程序流。 Null 模式可用于防止 null 值传播到应用程序的其余部分。

以下示例使用 null 模式和变量模式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4817.fs)]

## <a name="see-also"></a>请参阅

- [match 表达式](match-expressions.md)
- [活动模式](active-patterns.md)
- [F# 语言参考](index.md)