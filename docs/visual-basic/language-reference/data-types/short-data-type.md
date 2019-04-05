---
title: Short 数据类型 (Visual Basic)
ms.date: 01/31/2018
f1_keywords:
- vb.Short
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- S literal type character [Visual Basic]
- Short data type
- literal type characters [Visual Basic], S
ms.assetid: 65fcbcf3-a841-400e-885e-301497729a8b
ms.openlocfilehash: d4dab1a72d1e240bc428b2c6b83a722584e35ecc
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54587656"
---
# <a name="short-data-type-visual-basic"></a>Short 数据类型 (Visual Basic)
保存有符号 16 位 （2 个字节） 整数，值的范围从-32,768 到 32767 之间。  
  
## <a name="remarks"></a>备注  
 使用`Short`数据类型包含不需要的完整数据宽度的整数值`Integer`。 在某些情况下，公共语言运行时能够打包你`Short`变量紧密合作，以节省内存消耗。  
  
 `Short` 的默认值为 0。  
  
## <a name="literal-assignments"></a>文本分配

您可以声明并初始化`Short`变量由将其分配十进制文本、 十六进制文本八进制文本，或 （Visual Basic 从 2017年开始） 二进制文本。 如果整数文本在 `Short` 范围之外（即，如果它小于 <xref:System.Int16.MinValue?displayProperty=nameWithType> 或大于 <xref:System.Int16.MaxValue?displayProperty=nameWithType>），会发生编译错误。

在以下示例中，整数等于 1034、 表示为十进制、 十六进制和二进制文本隐式转换从[整数](integer-data-type.md)到`Short`值。

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Short)]

> [!NOTE]
> 使用前缀`&h`或`&H`来表示十六进制文本前缀`&b`或`&B`来表示二进制文本和前缀`&o`或`&O`来表示八进制文本。 十进制文本没有前缀。

从 Visual Basic 2017 开始，你还可以使用下划线字符， `_`，作为数字分隔符，以增强可读性，如以下示例所示。

[!code-vb[Short](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ShortS)]

从 Visual Basic 15.5 开始，你还可以使用下划线字符 (`_`) 作为前缀和十六进制、 二进制或八进制数字之间的前导分隔符。 例如：

```vb
Dim number As Short = &H_3264
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

此外可以包含数值`S`[键入字符](../../programming-guide/language-features/data-types/type-characters.md)来表示`Short`数据类型，如以下示例所示。

```vb
Dim number = &H_3264S
```

## <a name="programming-tips"></a>编程提示

-   **扩大转换。** `Short`数据类型加宽到`Integer`， `Long`， `Decimal`， `Single`，或`Double`。 这意味着，你可以将 `Short` 转换为这些类型中的任意类型，而不会遇到 <xref:System.OverflowException?displayProperty=nameWithType> 错误。  
  
-   **类型字符。** 将文本类型字符 `S` 追加到文本会将其强制转换为 `Short` 数据类型。 `Short` 有没有标识符类型字符。  
  
-   **Framework 类型。** .NET Framework 中的对应类型是 <xref:System.Int16?displayProperty=nameWithType> 结构。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Int16?displayProperty=nameWithType>
- [数据类型](../../../visual-basic/language-reference/data-types/index.md)
- [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)
- [Long 数据类型](../../../visual-basic/language-reference/data-types/long-data-type.md)
- [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
