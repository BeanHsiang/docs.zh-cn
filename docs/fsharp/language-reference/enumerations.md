---
title: 枚举
description: 了解如何使用F#枚举来代替文本以使代码更具可读性且更易于维护。
ms.date: 05/16/2016
ms.openlocfilehash: a8839b73de074f62606b70ffe969a53b3db753bf
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53611723"
---
# <a name="enumerations"></a>枚举

*枚举*，也称为*枚举*、 是整型类型的标签分配到值的子集。 可以使用它们来代替文本，使代码更具可读性且更易维护。

## <a name="syntax"></a>语法

```fsharp
type enum-name =
| value1 = integer-literal1
| value2 = integer-literal2
...
```

## <a name="remarks"></a>备注

一个枚举，看上去像可区分联合具有简单的值，只不过可以指定的值。 这些值通常是从 0 或 1，开始的整数或整数，用于表示位位置。 如果一个枚举，用于表示位位置，还应使用[标志](xref:System.FlagsAttribute)属性。

枚举的基础类型由文本使用，以便，例如，您可以使用文本带有后缀，如`1u`， `2u`，依此类推，对于无符号整数 (`uint32`) 类型。

如果是指已命名值时，您必须使用枚举类型本身的名称用作限定符，，即`enum-name.value1`，而不是`value1`。 此行为有何不同的可区分联合。 这是因为枚举始终具有[RequireQualifiedAccess](https://msdn.microsoft.com/library/8b9b6ade-0471-4413-ac5d-638cd0de5f15)属性。

下面的代码演示声明和使用的枚举。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2101.fs)]

您可以轻松地转换为枚举的基础类型通过使用相应的运算符，如下面的代码中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2102.fs)]

枚举的类型可以具有以下基础类型之一： `sbyte`， `byte`， `int16`， `uint16`， `int32`， `uint32`， `int64`， `uint16`， `uint64`，和`char`。 枚举类型在.NET Framework 中表示为从继承的类型`System.Enum`，其又继承自`System.ValueType`。 因此，它们是位于堆栈或内联的包含对象中的值类型，任何值的基础类型是枚举的有效值。 这很重要时模式匹配枚举值，因为您必须提供一种模式可捕获未命名的值。

`enum`函数，在F#库可用于生成一个枚举值，甚至之外的预定义的值命名值。 您使用`enum`函数，如下所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2103.fs)]

默认值`enum`函数适用于类型`int32`。 因此，它不能用于具有其他的基础类型的枚举类型。 相反，使用以下命令。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2104.fs)]

此外，情况下，对于枚举时，始终发出作为`public`。 这是以使它们与 C# 和.NET 平台的其余部分保持一致。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [强制转换和转换](casting-and-conversions.md)