---
title: 第一类函数
description: 了解有关的第一类函数，以及如何对函数式编程中的重要信息F#。
ms.date: 10/29/2018
ms.openlocfilehash: 505ad686614b53d779cb617fc04ac74c2a88b31b
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53148623"
---
# <a name="first-class-functions"></a>第一类函数

函数编程语言的决定性特征是提升至最优状态的函数。 您应能够执行的函数，任何您可以使用其他内置类型的值执行操作并将无法执行此操作与一般程度的工作量。

典型的第一类状态的度量值包括：

- 您可以将函数绑定到标识符？ 也就是说，可以在为其提供名称？

- 可以存储函数中的数据结构，如在列表中？

- 可以为函数调用中的自变量传递函数？

- 您可以从函数调用返回一个函数？

最后两个度量值定义所谓*高阶 operations*或*高阶函数*。 高阶函数接受作为参数的函数，并返回函数作为函数调用的值。 这些操作支持这种功能性编程作为映射函数和函数的组合。

## <a name="give-the-value-a-name"></a>为指定名称的值

如果函数是第一类值，您必须能够将其命名，就像可以命名整数、 字符串和其他内置类型。 这称为函数编程语言标识符绑定到的值中。 F#使用[`let`绑定](../language-reference/functions/let-bindings.md)要绑定到值的名称： `let <identifier> = <value>`。 下面的代码演示两个示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet20.fs)]

您可以命名很容易地函数。 下面的示例定义一个名为函数`squareIt`通过将标识符绑定`squareIt`到[lambda 表达式](../language-reference/functions/lambda-expressions-the-fun-keyword.md) `fun n -> n * n`。 函数`squareIt`具有一个参数、 `n`，它将返回该参数的平方和。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet21.fs)]

F#提供了以下更简洁的语法来实现相同的结果，少键入一些字符。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet22.fs)]

主要是下面的示例使用第一个样式， `let <function-name> = <lambda-expression>`，以强调函数的声明和其他类型的值的声明之间的相似之处。 但是，还可以使用简洁的语法编写所有命名的函数。 这两种方式编写的一些示例。

## <a name="store-the-value-in-a-data-structure"></a>应用商店中的数据结构的值

第一类值可以存储在一个数据结构。 下面的代码显示了将值存储在列表和元组中的示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet23.fs)]

若要验证存储元组中的函数名称的确会实际计算的函数，下面的示例，请使用`fst`并`snd`运算符从元组中提取的第一个和第二个元素`funAndArgTuple`。 元组中的第一个元素是`squareIt`和第二个元素是`num`。 标识符`num`绑定到的有效参数的整数 10 上, 一示例中`squareIt`函数。 第二个表达式所应用到的元组中的第二个元素的元组中的第一个元素： `squareIt num`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet24.fs)]

同样，就像标识符`num`整数 10 可以互换使用，因此可以标识符`squareIt`和 lambda 表达式`fun n -> n * n`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet25.fs)]

## <a name="pass-the-value-as-an-argument"></a>值作为参数传递

如果值有一种语言中的第一类的状态，则可以它作为参数传递给函数。 例如，它是常见整数和字符串作为参数传递。 下面的代码演示整数和字符串中作为参数传递F#。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet26.fs)]

如果函数的第一类的状态，您必须能够将它们作为参数传递相同的方式。 请记住，这是高阶函数的第一个特征。

在以下示例中，函数`applyIt`具有两个参数`op`和`arg`。 如果您将发送具有一个参数的函数`op`和到函数的相应参数`arg`，该函数返回应用的结果`op`到`arg`。 在以下示例中，函数参数和整数自变量将发送相同方式使用它们的名称。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet27.fs)]

能够将函数作为参数发送到另一个函数是函数编程语言，例如映射或筛选器操作中的常见抽象的基础。 映射操作，例如，是捕获共享单步执行列表、 对每个元素进行一些操作，然后返回结果的列表的函数的计算，高阶函数。 您可能想要递增的整数，列表中每个元素或正方形每个元素，或更改为大写的字符串列表中每个元素。 计算的易出错部分是递归过程的列表的步骤和生成的要返回的结果列表。 映射函数中捕获该部分。 你已将某个特定应用程序是你想要单独应用于每个列表元素的函数 （添加、 求平方、 更改大小写）。 函数作为参数发送到映射函数，就像`squareIt`发送到`applyIt`在前面的示例。

F#提供用于大多数集合类型，包括映射方法[列出了](../language-reference/lists.md)，[数组](../language-reference/arrays.md)，并[序列](../language-reference/sequences.md)。 下面的示例使用列表。 语法是`List.map <the function> <the list>`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet28.fs)]

有关详细信息，请参阅[列出了](../language-reference/lists.md)。

## <a name="return-the-value-from-a-function-call"></a>从函数调用返回值

最后，如果函数具有一种语言中的第一类的状态，您必须能够将其作为函数调用的值返回就像返回其他类型，如整数和字符串。

以下函数调用返回整数并将其显示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet29.fs)]

以下函数调用返回一个字符串。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet30.fs)]

以下函数调用中，声明为内联，返回一个布尔值。 显示的值是`True`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet31.fs)]

返回一个函数作为函数调用的值的功能是高阶函数的第二个特征。 在以下示例中，`checkFor`被定义为采用一个参数的函数`item`，并返回作为其值的新函数。 返回的函数采用一个列表作为其参数`lst`，并搜索`item`中`lst`。 如果`item`，则该函数将返回`true`。 如果`item`不存在，该函数将返回`false`。 上一节中，以下代码使用提供的列表函数[List.exists](https://msdn.microsoft.com/library/15a3ebd5-98f0-44c0-8220-7dedec3e68a8)，以在列表中搜索。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet32.fs)]

下面的代码使用`checkFor`若要创建新的函数采用一个自变量、 列表和 7 的搜索列表中。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet33.fs)]

下面的示例使用中的函数的第一类状态F#来声明一个函数， `compose`，返回两个函数参数的组合。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet34.fs)]

> [!NOTE]
> 更短的版本，请参阅以下部分中，"扩充函数。"

下面的代码将作为参数发送两个函数`compose`，这两个的这需要相同类型的单个参数。 返回值是一个新函数，则两个函数参数的组合。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet35.fs)]

> [!NOTE]
> F#提供了两个运算符`<<`和`>>`，组合函数。 例如，`let squareAndDouble2 = doubleIt << squareIt`等效于`let squareAndDouble = compose doubleIt squareIt`在前面的示例。

返回一个函数作为函数调用的值的以下示例创建一个简单的猜测游戏。 若要创建一个游戏，调用`makeGame`的值，希望有人猜测中发送`target`。 函数的返回值`makeGame`是接受一个参数 （猜测值），并报告猜测是正确的函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet36.fs)]

下面的代码调用`makeGame`，将值发送`7`为`target`。 标识符`playGame`绑定到返回的 lambda 表达式。 因此，`playGame`是一个函数，将作为它的一个参数值为`guess`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet37.fs)]

## <a name="curried-functions"></a>扩充的函数

可以通过利用隐式更简洁地编写的示例在上一节中的许多*科*中F#函数声明。 科是一个转换具有多个参数为一系列的嵌入功能，其中每个具有单个参数的函数的过程。 在F#，本质上是扩充具有多个参数的函数。 例如，`compose`从上一节可以编写以下简洁样式，带有三个参数中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet38.fs)]

但是，结果是返回一个参数，它又会返回一个参数的另一个函数的函数，如中所示的一个参数的函数`compose4curried`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet39.fs)]

您可以访问以下几种方式的此函数。 下面的示例的每个返回并显示 18。 您可以替换`compose4`与`compose4curried`中任何示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet40.fs)]

若要验证函数仍像以前一样工作，试一次原始测试用例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet41.fs)]

> [!NOTE]
> 你可以限制科参数括在元组中。 详细信息，请参阅"参数模式"中[形参和实参](../language-reference/parameters-and-arguments.md)。

下面的示例使用隐式扩充编写的简短版本`makeGame`。 如何的详细信息`makeGame`构造并返回`game`函数不太明确按以下格式，但你可以通过使用原始的结果是相同的测试用例验证。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet42.fs)]

科的详细信息，请参阅"的参数的部分应用程序"中[函数](../language-reference/functions/index.md)。

## <a name="identifier-and-function-definition-are-interchangeable"></a>是可互换的标识符和函数定义

变量名称`num`中的上一个示例的计算结果为整数 10，并不奇怪，因为`num`是有效，10 也是有效的。 这同样适用的函数标识符和它们的值： 可以随处可用的函数的名称，使用绑定到的 lambda 表达式。

下面的示例定义`Boolean`调用的函数`isNegative`，然后互换使用的函数的名称和函数的定义。 接下来三个示例都返回并显示`False`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet43.fs)]

若要进一步它一个步骤，替换为的值的`applyIt`为绑定到`applyIt`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet44.fs)]

## <a name="functions-are-first-class-values-in-f"></a>函数是 F 中的第一类值\#

前面几节中的示例演示中，函数F#满足的条件中的一类值F#:

- 可以绑定到函数定义的标识符。
[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet21.fs)]

- 您可以在数据结构存储函数。
[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet45.fs)]

- 可以将函数作为参数传递。
[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet46.fs)]

- 可以将函数作为函数调用的值返回。
[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet32.fs)]

有关详细信息F#，请参阅[F#语言参考](../language-reference/index.md)。

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的代码包含本主题中的所有示例。

### <a name="code"></a>代码

[!code-fsharp[Main](../../../samples/snippets/fsharp/contour/snippet47.fs)]

## <a name="see-also"></a>请参阅

- [列表](../language-reference/lists.md)
- [元组](../language-reference/tuples.md)
- [函数](../language-reference/functions/index.md)
- [`let` 绑定](../language-reference/functions/let-bindings.md)
- [Lambda 表达式：`fun`关键字](../language-reference/functions/lambda-expressions-the-fun-keyword.md)
