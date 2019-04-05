---
title: 自动泛化
description: 了解如何F#自动泛化的参数和类型的函数，以便它们适用于多个类型在可能的情况。
ms.date: 05/16/2016
ms.openlocfilehash: 15ecf8e6f07da19bb015fd028a7465ba8b837190
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53611706"
---
# <a name="automatic-generalization"></a>自动泛化

F#使用类型推理评估的函数和表达式的类型。 本主题介绍如何F#自动泛化的参数和类型的函数，使它们工作的多个类型时做到这一点。

## <a name="automatic-generalization"></a>自动泛化

F#编译器，它执行上一个函数，类型推理时确定是否为给定的参数可以为泛型。 编译器检查每个参数，并确定该函数是否具有该参数的特定类型的依赖关系。 如果未显示，类型推断为泛型。

下面的代码示例演示编译器将推断是通用的函数。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet101.fs)]

类型被推断为`'a -> 'a -> 'a`。

该类型指示这是采用相同的未知类型的两个参数并返回相同类型的值的函数。 可以是上一个函数的原因之一泛型是： 大于-运算符 (`>`) 本身是泛型。 更高版本-不是运算符具有签名`'a -> 'a -> bool`。 并非所有运算符都是泛型，并在函数中的代码使用与非泛型函数或运算符的参数类型，如果该参数类型不能使用通用。

因为`max`是泛型类型，它可用于类型如`int`， `float`，依此类推，如以下示例所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet102.fs)]

但是，两个参数必须属于同一类型。 该签名是`'a -> 'a -> 'a`，而不`'a -> 'b -> 'a`。 因此，下面的代码生成错误，因为类型不匹配。

```fsharp
// Error: type mismatch.
let biggestIntFloat = max 2.0 3
```

`max`函数也可用于支持较大的任何类型的运算符。 因此，你无法使用它在一个字符串，如下面的代码中所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet104.fs)]

## <a name="value-restriction"></a>值限制

编译器会执行自动泛化仅在具有显式参数的完整函数定义和简单的不可变值。

这意味着编译器发出错误，如果您尝试编译代码未充分约束为特定的类型，但也不是可归纳。 此问题的错误消息是指此限制的值作为自动泛化*值限制*。

通常情况下，值限制错误发生时所需的构造是通用，但编译器没有足够的信息进行通用化处理，或在无意中省略足够在非泛型构造函数中的类型信息时。 值限制错误的解决方案是提供更明确的信息，以更全面地约束类型推理问题，通过以下方式之一：

- 将通过将显式类型批注添加到值或参数为非泛型类型约束。

- 如果使用问题不可泛化构造来定义如函数组合或不完整的泛型函数应用的扩充的函数自变量，请尝试重写为普通函数定义的函数。

- 如果问题是太复杂，无法进行一般化，通过添加额外的未使用参数来使到函数的表达式。

- 添加显式泛型类型参数。 很少使用此选项。

- 下面的代码示例说明了每种方案。

案例 1:表达式太复杂。 在此示例中，列表`counter`用于`int option ref`，但它不定义为一个简单的不可变值。

```fsharp
let counter = ref None
// Adding a type annotation fixes the problem:
let counter : int option ref = ref None
```

案例 2:使用不可泛化构造定义的泛型函数。 在此示例中，构造是不可泛化，因为它涉及到部分应用函数自变量。

```fsharp
let maxhash = max << hash
// The following is acceptable because the argument for maxhash is explicit:
let maxhash obj = (max << hash) obj
```

案例 3:添加一个额外的、 未使用的参数。 此表达式不是简单的泛化，因为编译器会发出值限制错误。

```fsharp
let emptyList10 = Array.create 10 []
// Adding an extra (unused) parameter makes it a function, which is generalizable.
let emptyList10 () = Array.create 10 []
```

情形 4:添加类型参数。

```fsharp
let arrayOf10Lists = Array.create 10 []
// Adding a type parameter and type annotation lets you write a generic value.
let arrayOf10Lists<'T> = Array.create 10 ([]:'T list)
```

在最后一种情况下，值将成为类型函数，可用于创建许多不同类型的值为例，如下：

```fsharp
let intLists = arrayOf10Lists<int>
let floatLists = arrayOf10Lists<float>
```

## <a name="see-also"></a>请参阅

- [类型推断](../type-inference.md)
- [泛型](index.md)
- [静态解析的类型参数](statically-resolved-type-parameters.md)
- [约束](constraints.md)