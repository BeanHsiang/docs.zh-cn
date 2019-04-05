---
title: ULong 数据类型 (Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.ulong
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- literal type characters [Visual Basic], UL
- ULong data type
- UL literal type characters [Visual Basic]
ms.assetid: 017e0702-774e-44ae-bedc-786b424ca84e
ms.openlocfilehash: 82a2badc1bb22a55f753c9075562db3a5ee0d234
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54522955"
---
# <a name="ulong-data-type-visual-basic"></a>ULong 数据类型 (Visual Basic)

保存取值范围为 0 到 18446744073709551615 的无符号的 64 位 （8 字节） 整数 (多个 1.84 倍 10 ^19)。  
  
## <a name="remarks"></a>备注

使用`ULong`数据类型来包含二进制数据太大， `UInteger`，或可能的最大无符号整数值。  
  
`ULong` 的默认值为 0。

## <a name="literal-assignments"></a>文本分配

您可以声明并初始化`ULong`变量由将其分配十进制文本、 十六进制文本八进制文本，或 （Visual Basic 从 2017年开始） 二进制文本。 如果整数文本在 `ULong` 范围之外（即，如果它小于 <xref:System.UInt64.MinValue?displayProperty=nameWithType> 或大于 <xref:System.UInt64.MaxValue?displayProperty=nameWithType>），会发生编译错误。

在以下示例中，表示为十进制、十六进制和二进制文本且等于 7,934,076,125 的整数被分配给 `ULong` 值。
  
[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ULong)]

> [!NOTE] 
> 使用前缀`&h`或`&H`来表示十六进制文本前缀`&b`或`&B`来表示二进制文本和前缀`&o`或`&O`来表示八进制文本。 十进制文本没有前缀。

从 Visual Basic 2017 开始，你还可以使用下划线字符， `_`，作为数字分隔符，以增强可读性，如以下示例所示。

[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

从 Visual Basic 15.5 开始，你还可以使用下划线字符 (`_`) 作为前缀和十六进制、 二进制或八进制数字之间的前导分隔符。 例如：

```vb
Dim number As ULong = &H_F9AC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

此外可以包含数值`UL`或`ul`[键入字符](../../programming-guide/language-features/data-types/type-characters.md)来表示`ULong`数据类型，如以下示例所示。

```vb
Dim number = &H_00_00_0A_96_2F_AC_14_D7ul
```

## <a name="programming-tips"></a>编程提示
  
-   **负号。** 因为`ULong`是无符号的类型，它不能表示为负数。 如果使用一元负 (`-`) 运算符的表达式的计算结果为类型`ULong`，Visual Basic 将转换为表达式`Decimal`第一个。  
  
-   **CLS 遵从性。** `ULong`数据类型不属于[公共语言规范](https://www.ecma-international.org/publications/standards/Ecma-335.htm)(CLS)，因此符合 cls 的代码不能使用使用它的组件。  
  
-   **互操作注意事项。** 如果你与不是为.NET Framework 中，如自动化或 COM 对象，编写组件交互请记住，类型，如`ulong`可以在其他环境中具有不同的数据宽度 （32 位）。 如果您将 32 位自变量传递给此类组件，将其作为声明`UInteger`而不是`ULong`中托管的 Visual Basic 代码。  
  
     此外，自动化不支持在 Windows 95、 Windows 98、 Windows ME 或 Windows 2000 上 64 位整数。 不能将传递一个 Visual Basic`ULong`到这些平台上自动化组件的参数。  
  
-   **扩大转换。** `ULong`数据类型加宽到`Decimal`， `Single`，和`Double`。 这意味着可以将转换`ULong`而不会遇到这些类型的任何<xref:System.OverflowException?displayProperty=nameWithType>错误。  
  
-   **类型字符。** 追加文本类型字符`UL`为文本将其强制转换到`ULong`数据类型。 `ULong` 有没有标识符类型字符。
  
-   **Framework 类型。** .NET Framework 中的对应类型是 <xref:System.UInt64?displayProperty=nameWithType> 结构。  
  
## <a name="see-also"></a>请参阅

- <xref:System.UInt64>
- [数据类型](../../../visual-basic/language-reference/data-types/index.md)
- [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [如何：调用需要使用无符号类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
