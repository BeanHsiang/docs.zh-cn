---
title: 代码引用
description: 了解如何F#的代码引号中，一种语言功能，可用于生成和使用F#以编程方式代码表达式。
ms.date: 05/16/2016
ms.openlocfilehash: aa8a17eb8f9837ca4023abc552a6aac063117e96
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614293"
---
# <a name="code-quotations"></a>代码引用

> [!NOTE]
> API 参考链接将转至 MSDN。  Docs.microsoft.com API 参考尚未完成。

本主题介绍*代码引用*，一种语言功能，可用于生成和使用F#以编程方式代码表达式。 此功能允许您生成一个表示的抽象语法树F#代码。 然后可以遍历并根据应用程序需要处理的抽象语法树。 例如，可以使用树来生成F#代码或一些其他语言生成代码。

## <a name="quoted-expressions"></a>带引号的表达式

一个*带引号的表达式*是F#在代码中的分隔方式作为应用程序的一部分不编译，但被编译为一个对象，表示表达式F#表达式。 您可以将标记引用的表达式有两种： 使用类型信息或不带类型信息。 如果你想要包括类型信息，则使用符号`<@`和`@>`来分隔带引号的表达式。 如果不需要类型信息，则使用符号`<@@`和`@@>`。 下面的代码显示了类型化和非类型化引用。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet501.fs)]

遍历一个大型的表达式树速度更快，如果不包括类型信息。 带引号的使用类型化的符号的表达式的结果类型是`Expr<'T>`，其中类型参数都有由表达式的类型F#编译器的类型推断算法。 当使用不含类型信息的代码引用时，带引号的表达式的类型为非泛型类型[Expr](https://msdn.microsoft.com/library/ed6a2caf-69d4-45c2-ab97-e9b3be9bce65)。 您可以调用[Raw](https://msdn.microsoft.com/library/47fb94f1-e77f-4c68-aabc-2b0ba40d59c2)属性的类型化`Expr`类来获取的非类型化`Expr`对象。

有多种，可以生成的静态方法F#表达式以编程方式在对象`Expr`类，而无需使用带引号的表达式。

请注意，代码引号必须包含完整的表达式。 有关`let`绑定，例如，您需要定义绑定的名称和使用该绑定的其他表达式。 在详细语法中，这是一个表达式，遵循`in`关键字。 在顶级模块中，这是只需在模块中下, 一个表达式，但在报价，它是明确要求。

因此，下面的表达式不是有效的。

```fsharp
// Not valid:
// <@ let f x = x + 1 @>
```

但以下表达式是有效的。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet502.fs)]

若要使用的代码引用，必须添加导入声明 (使用`open`关键字)，用于在打开[Microsoft.FSharp.Quotations](https://msdn.microsoft.com/library/e9ce8a3a-e00c-4190-bad5-cce52ee089b2)命名空间。

F# PowerPack 提供了评估和执行的支持F#表达式对象。

## <a name="expr-type"></a>Expr 类型

实例`Expr`表示类型F#表达式。 泛型和非泛型`Expr`类型均记录在F#库文档。 有关详细信息，请参阅[Microsoft.FSharp.Quotations Namespace](https://msdn.microsoft.com/visualfsharpdocs/conceptual/microsoft.fsharp.quotations-namespace-%5bfsharp%5d)并[Quotations.Expr 类](https://msdn.microsoft.com/visualfsharpdocs/conceptual/quotations.expr-class-%5bfsharp%5d)。

## <a name="splicing-operators"></a>拼接运算符

拼接可以合并使用而创建了以编程方式或从另一个代码引用的表达式的原义代码引用。 `%`并`%%`运算符，您可以添加F#表达式到代码引用的对象。 您使用`%`运算符将类型化的表达式对象插入类型化引起来; 您可以使用`%%`运算符以将非类型化的表达式对象插入非类型化引起来。 这两个运算符是一元前缀运算符。 因此如果`expr`类型的非类型化表达式`Expr`，以下代码是有效的。

```fsharp
<@@ 1 + %%expr @@>
```

如果`expr`是类型化的引用`Expr<int>`，以下代码是有效的。

```fsharp
<@ 1 + %expr @>
```

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例演示如何使用代码引用将F#到表达式对象的代码，然后打印F#表示表达式的代码。 一个函数`println`定义包含递归函数`print`显示F#表达式对象 (类型的`Expr`) 以友好格式。 有几种活动模式在[Microsoft.FSharp.Quotations.Patterns](https://msdn.microsoft.com/library/093944a9-c752-403a-8983-5fcd5dbf92a4)并[Microsoft.FSharp.Quotations.DerivedPatterns](https://msdn.microsoft.com/library/d2434a6e-ae7b-4f3d-b567-c162938bc9cd)模块，它们可以用于分析表达式对象。 此示例不包括所有可能的模式中可能出现的F#表达式。 任何无法识别的模式将触发与通配符模式匹配的项 (`_`) 和通过使用呈现`ToString`方法，而后者在`Expr`类型，可以知道要向匹配表达式中添加的活动模式。

### <a name="code"></a>代码

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet601.fs)]

### <a name="output"></a>输出

```fsharp
fun (x:System.Int32) -> x + 1
a + 1
let f = fun (x:System.Int32) -> x + 10 in f 10
```

## <a name="example"></a>示例

### <a name="description"></a>描述

此外可以使用中的三个活动模式[ExprShape 模块](https://msdn.microsoft.com/library/7685150e-2432-4d39-9338-57292eff18de)遍历表达式树，使用更少的活动模式。 如果想要遍历树，但不是需要大多数节点中的所有信息，这些活动模式会很有用。 当使用这些模式中，任何F#表达式匹配的以下三种模式之一：`ShapeVar`如果表达式是一个变量，`ShapeLambda`如果表达式为 lambda 表达式，或`ShapeCombination`如果表达式为任何其他操作。 如果通过使用如前面的代码示例中所示的活动模式遍历表达式树，你必须使用更多的模式来处理所有可能的F#的表达式类型，并且你的代码将会更加复杂。 有关详细信息，请参阅[ExprShape.ShapeVar&#124;ShapeLambda&#124;ShapeCombination 活动模式](https://msdn.microsoft.com/visualfsharpdocs/conceptual/exprshape.shapevarhshapelambdahshapecombination-active-pattern-%5bfsharp%5d)。

下面的代码示例可以用作更复杂的遍历基础。 在此代码中，为涉及函数调用的表达式创建表达式树`add`。 [SpecificCall](https://msdn.microsoft.com/library/05a77b21-20fe-4b9a-8e07-aa999538198d)活动的模式用于检测到的任何调用`add`表达式树中。 此活动的模式将分配到调用的参数`exprList`值。 在这种情况下，有只有两种，因此这些拉出且对自变量以递归方式调用该函数。 结果插入到表示对的调用的代码引用`mul`通过使用接合运算符 (`%%`)。 `println`上一示例中的函数用于显示结果。

其他活动的模式分支中的代码只是重新生成相同的表达式树，因此所生成的表达式中的唯一更改是从更改`add`到`mul`。

### <a name="code"></a>代码

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet701.fs)]

### <a name="output"></a>输出

```fsharp
1 + Module1.add(2,Module1.add(3,4))
1 + Module1.mul(2,Module1.mul(3,4))
```

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)