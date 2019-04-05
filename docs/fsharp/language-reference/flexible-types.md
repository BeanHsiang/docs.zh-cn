---
title: 可变类型
description: 了解如何使用F#可变类型批注，该值指示参数、 变量或值具有与指定的类型兼容的类型。
ms.date: 05/16/2016
ms.openlocfilehash: 32857cc317bc6b4b7baf53b623b551e8e0733e41
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613669"
---
# <a name="flexible-types"></a>可变类型

一个*可变类型批注*指示参数、 变量或值具有兼容类型的具有指定类型，其兼容性由面向对象的层次结构中的类或接口的位置。 可变类型非常有用，特别是，当自动转换为类型层次结构中级别更高的类型不会发生，但你仍想要启用您要使用在层次结构中的任何类型或实现接口的任何类型的功能。

## <a name="syntax"></a>语法

```fsharp
#type
```

## <a name="remarks"></a>备注

在上述语法中，*类型*表示基类型或接口。

灵活的类型是等效的泛型类型，有一个约束，限制为与 base 或接口类型相兼容的类型允许的类型。 也就是说，以下两行代码是等效的。

```fsharp
#SomeType

'T when 'T :> SomeType
```

可变类型是在多种类型的情况下很有用。 例如，如果具有更高版本的 order 函数 （采用函数作为参数的函数），通常很函数返回灵活类型很有用。 在下面的示例中，包含序列参数中的灵活类型使用`iterate2`使高阶函数用于生成序列、 数组、 列表和其他任何可枚举类型的函数。

请考虑以下两个函数，其中一个的哪些返回一个序列，这些其他返回可变类型。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4101.fs)]

作为另一个示例，请考虑[Seq.concat](https://msdn.microsoft.com/library/2eeb69a9-fc2f-4b7d-8dee-101fa2b00712)库函数：

```fsharp
val concat: sequences:seq<#seq<'T>> -> seq<'T>
```

可以将任何以下的可枚举序列传递给此函数：

- 列表的列表
- 数组列表
- 列表的数组
- 序列的数组
- 可枚举序列的任何其他组合

下面的代码使用`Seq.concat`来演示您可以通过使用可变类型支持的方案。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4102.fs)]

输出如下所示。

```
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
seq [1; 2; 3; 4; ...]
```

在F#，如下所示的面向对象的其他语言中，有的上下文中的派生类型或实现接口的类型自动转换为基类型或接口类型。 在直接自变量，但不是在该类型位于从属的位置，例如函数类型的返回类型的更复杂类型的一部分或作为类型参数时，会发生这些自动转换。 因此，灵活类型表示法时，主要是要将应用到的类型是更复杂类型的一部分。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [泛型](generics/index.md)