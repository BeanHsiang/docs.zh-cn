---
title: 固定大小的缓冲区 - C# 编程指南
ms.custom: seodec18
ms.date: 04/20/2018
helpviewer_keywords:
- fixed size buffers [C#]
- unsafe buffers [C#]
- unsafe code [C#], fixed size buffers
ms.openlocfilehash: 7c83b4819975f63c6fc19e5c4783603f37d2a885
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54700606"
---
# <a name="fixed-size-buffers-c-programming-guide"></a>固定大小的缓冲区（C# 编程指南）

在 C# 中，可以使用 [fixed](../../language-reference/keywords/fixed-statement.md) 语句来创建在数据结构中具有固定大小的数组的缓冲区。 当编写与其他语言或平台的数据源进行互操作的方法时，固定大小的缓冲区很有用。 固定的数组可以采用允许用于常规结构成员的任何属性或修饰符。 唯一的限制是数组类型必须为 `bool`、`byte`、`char`、`short`、`int`, `long`、`sbyte`、`ushort`、`uint`、`ulong`、`float` 或 `double`。

```csharp
private fixed char name[30];
```

## <a name="remarks"></a>备注

在安全代码中，包含数组的 C# 结构不包含该数组元素。 而该结构包含对元素的引用。 当在[不安全的](../../language-reference/keywords/unsafe.md)代码块中使用数组时，可以在[结构](../../language-reference/keywords/struct.md)中嵌入该固定大小的数组。

以下 `struct` 的大小为 8 字节。 `pathName` 数组是引用：

[!code-csharp[Struct with embedded array](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#6)]

`struct` 可以在不安全代码中包含嵌入的数组。 在下面的示例中，`fixedBuffer` 数组具有固定的大小。 使用 `fixed` 语句建立指向第一个元素的指针。 通过此指针访问数组的元素。 `fixed` 语句将 `fixedBuffer` 实例字段固定到内存中的特定位置。

[!code-csharp[Struct with embedded inline array](../../../../samples/snippets/csharp/keywords/FixedKeywordExamples.cs#7)]

包含 128 个元素的 `char` 数组的大小为 256 个字节。 固定大小的 [char](../../language-reference/keywords/char.md) 缓冲区每个字符始终占用两个字节，而不考虑编码。 甚至在将 char 缓冲区封送到 API 方法或具有 `CharSet = CharSet.Auto` 或 `CharSet = CharSet.Ansi` 的结构时，这也为 true。 有关更多信息，请参见<xref:System.Runtime.InteropServices.CharSet>。

前面的示例演示访问未固定的 `fixed` 字段，此功能从 C# 7.3 开始提供。

另一常见的固定大小的数组是 [bool](../../language-reference/keywords/bool.md) 数组。 `bool` 数组中的元素大小始终为一个字节。 `bool` 数组不适用于创建位数组或缓冲区。

> [!NOTE]
> 除了通过使用 [stackalloc](../../language-reference/keywords/stackalloc.md) 创建的内存外，C# 编译器和公共语言运行时 (CLR) 不执行任何安全缓冲区溢出检查。 与所有不安全代码一样，请谨慎使用。

不安全的缓冲区与常规数组的区别体现在以下方面：

- 只能在不安全的上下文中使用不安全的缓冲区。
- 不安全的缓冲区始终是矢量或一维数组。
- 数组的声明应包括计数，如 `char id[8]`。 不能使用 `char id[]`。
- 在不安全的上下文中，不安全的缓冲区只能是结构的实例字段。

## <a name="see-also"></a>请参阅

- [C# 编程指南](../index.md)
- [不安全代码和指针](index.md)
- [fixed 语句](../../language-reference/keywords/fixed-statement.md)
- [互操作性](../interop/index.md)
