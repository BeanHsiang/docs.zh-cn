---
title: 类型推断
description: 了解如何F#编译器推断类型的值、 变量、 参数和返回值。
ms.date: 05/16/2016
ms.openlocfilehash: 3e61d5c81fde0a48af66a47745123a842dc04cb1
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612785"
---
# <a name="type-inference"></a>类型推断

本主题介绍如何将F#编译器推断类型的值、 变量、 参数和返回值。

## <a name="type-inference-in-general"></a>一般情况下，类型推理

类型推理的理念是，不需要指定类型的F#除时，编译器无法最终推断类型的构造。 省略显式类型信息并不意味着F#是动态类型化的语言或中的值F#是弱类型化。 F#是静态类型化的语言，这意味着编译器将在编译期间推导为每个构造的确切类型。 如果没有足够的信息供编译器推导出的每个构造的类型，则必须在代码中某个位置添加明确的类型注释通常提供附加类型信息。

## <a name="inference-of-parameter-and-return-types"></a>参数和返回类型推理

在参数列表中，无需指定每个参数的类型。 并且，F#是一种静态类型化的语言，并因此的每个值和表达式具有明确的类型在编译时。 对于不显式指定这些类型，编译器将推断基于上下文的类型。 如果类型不是以其他方式指定，它被推断为泛型。 如果代码使用一个值不一致，这样一种方式中是否有没有一推断满足的一个值，所有使用编译器会报告错误的类型。

一个函数的返回类型取决于在函数中的最后一个表达式的类型。

例如，在下面的代码中，参数类型`a`并`b`以及所有推断为返回类型`int`因为文本`100`属于类型`int`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet301.fs)]

您可以通过更改文本影响类型推理。 如果进行`100``uint32`通过追加后缀`u`，类型的`a`， `b`，并返回值会被推断为`uint32`。

也可以影响使用隐含的类型，如函数和方法适用于特定类型的限制的其他构造类型推理。

此外，您可以应用显式类型批注函数或方法参数或变量在表达式中，如以下示例所示。 不同的约束之间发生冲突时，将导致错误。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet302.fs)]

通过提供类型批注所有参数，可以显式指定函数的返回值。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet303.fs)]

类型批注的参数非常有用的常见情况是当该参数是一个对象类型，你想要使用成员。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet304.fs)]

## <a name="automatic-generalization"></a>自动泛化

如果函数代码并不依赖参数的类型，编译器会考虑要为泛型的参数。 这称为*自动泛化*，它可以是编写泛型代码，且不会增加复杂性大有帮助。

例如，以下函数将任何类型的元组的两个参数组合。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet305.fs)]

推断的类型为

```fsharp
'a -> 'b -> 'a * 'b
```

## <a name="additional-information"></a>其他信息

中更详细地介绍了类型推断F#语言规范。

## <a name="see-also"></a>请参阅

- [自动泛化](generics/automatic-generalization.md)