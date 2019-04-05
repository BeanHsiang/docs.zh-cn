---
title: 内联函数
description: 了解如何使用F#直接集成到调用代码的内联函数。
ms.date: 05/16/2016
ms.openlocfilehash: 12c175e3e46e12d978fe02d3e1fe83142e71a25d
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610562"
---
# <a name="inline-functions"></a>内联函数

*内联函数*是直接集成到调用代码的函数。

## <a name="using-inline-functions"></a>使用内联函数

当使用静态类型参数时，任何类型参数的参数化的函数必须是内联。 这可确保编译器可以解决这些类型参数。 当您使用普通的泛型类型参数时，没有任何此类限制。

不允许使用成员约束，内联函数可以帮助优化代码。 但是，过度使用的内联函数会导致编译器优化和库函数的实现变化不太本身也可以在代码。 出于此原因，应避免进行优化使用内联函数，除非您已尝试了所有其他优化技术。 使函数或方法的内联有时可以提高性能，但它并不总是这种情况。 因此，您应使用性能度量值以验证使任何给定的函数内联实际上产生积极的影响。

`inline`修饰符可以应用于函数的顶层，在模块级别，或在方法级别在类中。

下面的代码示例说明了在最高级别、 内联实例方法和内联静态方法的内联函数。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet201.fs)]

## <a name="inline-functions-and-type-inference"></a>内联函数和类型推理

是否存在`inline`影响类型推理。 这是因为内联函数可以具有静态解析的类型参数，而非内联函数不能。 下面的代码示例显示了一种情况其中`inline`十分有用，因为正在使用具有一个静态解析的类型参数的函数`float`转换运算符。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet202.fs)]

无需`inline`修饰符，类型推理强制函数以这种情况下采用特定的类型， `int`。 但与`inline`修饰符，该函数同样被推断为具有静态解析的类型参数。 使用`inline`修饰符，类型推断为以下：

```fsharp
^a -> unit when ^a : (static member op_Explicit : ^a -> float)
```

这意味着该函数接受任何类型的支持将转换为**float**。

## <a name="see-also"></a>请参阅

- [函数](index.md)
- [约束](../generics/constraints.md)
- [静态解析的类型参数](../generics/statically-resolved-type-parameters.md)