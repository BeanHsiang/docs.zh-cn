---
title: 显式数值转换表 - C# 参考
ms.custom: seodec18
ms.date: 09/06/2018
helpviewer_keywords:
- conversions [C#], explicit numeric
- numeric conversions [C#], explicit
- explicit numeric conversion [C#]
- numeric data types [C#]
- types [C#], explicit numeric conversions
- type conversion [C#], explicit numeric
ms.assetid: f3bb9e76-6b92-4df7-bc36-f866c24e1dfd
ms.openlocfilehash: 90691ae0d9de35831b7b3119493e4e9cd81720e6
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53236305"
---
# <a name="explicit-numeric-conversions-table-c-reference"></a>显式数值转换表（C# 参考）

下表显示没有[隐式转换](implicit-numeric-conversions-table.md)的 .NET 数值类型之间的预定义显式转换。

|From|到|  
|----------|--------|  
|[sbyte](sbyte.md)|`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[byte](byte.md)|`sbyte` 或 `char`|  
|[short](short.md)|`sbyte`、`byte`、`ushort`、`uint`、`ulong` 或 `char`|  
|[ushort](ushort.md)|`sbyte`、`byte`、`short` 或 `char`|  
|[int](int.md)|`sbyte`、`byte`、`short`、`ushort`、`uint`、`ulong` 或 `char`|  
|[uint](uint.md)|`sbyte`、`byte`、`short`、`ushort`、`int` 或 `char`|  
|[long](long.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`ulong` 或 `char`|  
|[ulong](ulong.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long` 或 `char`|  
|[char](char.md)|`sbyte`、`byte` 或 `short`|  
|[float](float.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char` 或 `decimal`|  
|[double](double.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `decimal`|  
|[decimal](decimal.md)|`sbyte`、`byte`、`short`、`ushort`、`int`、`uint`、`long`、`ulong`、`char`、`float` 或 `double`|  
  
## <a name="remarks"></a>备注  
  
- 显式数值转换可能会导致精度降低或导致引发异常，通常为 <xref:System.OverflowException>。  

- 将整数类型的值转换为另一个整数类型时，结果取决于溢出[检查上下文](checked-and-unchecked.md)。 在已检查的上下文中，如果源值在目标类型的范围内，则转换成功。 否则会引发 <xref:System.OverflowException>。 在未检查的上下文中，转换始终成功，并按如下方式进行：

  - 如果源类型大于目标类型，则通过放弃其“额外”最高有效位来截断源值。 结果会被视为目标类型的值。

  - 如果源类型小于目标类型，则源值是符号扩展或零扩展，以使其与目标类型的大小相同。 如果源类型带符号，则是符号扩展；如果源类型是无符号的，则是零扩展。 结果会被视为目标类型的值。

  - 如果源类型与目标类型的大小相同，则源值将被视为目标类型的值。
  
- 将 `decimal` 值转换为整型类型时，此值会向零舍入到最接近的整数值。 如果生成的整数值处于目标类型的范围之外，则会引发 <xref:System.OverflowException>。  
  
- 将 `double` 或 `float` 值转换为整型类型时，此值会向零舍入到最接近的整数值。 如果生成的整数值处于目标类型范围之外，则结果会取决于溢出[上下文](checked-and-unchecked.md)。 在已检查的上下文中，引发 <xref:System.OverflowException>；而在未检查的上下文中，结果是目标类型的未指定值。  
  
- 将 `double` 转换为 `float` 时，`double` 值舍入为最接近的 `float` 值。 如果 `double` 值太小或太大，无法匹配目标类型，结果将为零或无穷大。  
  
- 将 `float` 或 `double` 转换为 `decimal` 时，源值转换为 `decimal` 表示形式，并并五入到第 28 位小数后最接近的数（如果需要）。 根据源值的值，可能出现以下结果之一：  

  - 如果源值太小，无法表示为 `decimal`，结果则为零。  

  - 如果源值为 NaN（非数值）、无穷大或太大而无法表示为 `decimal`，则引发 <xref:System.OverflowException>。  
  
- 将 `decimal` 转换为 `float` 或 `double` 时，`decimal` 值舍入到最接近的 `double` 或 `float` 值。  
  
 有关显式转换的详细信息，请参阅 [C# 语言规范](../language-specification/index.md)的[显式转换](~/_csharplang/spec/conversions.md#explicit-conversions)章节。
  
## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [强制转换和类型转换](../../programming-guide/types/casting-and-type-conversions.md)
- [() 运算符](../operators/invocation-operator.md)
- [整型类型表](integral-types-table.md)
- [浮点型表](floating-point-types-table.md)
- [内置类型表](built-in-types-table.md)
- [隐式数值转换表](implicit-numeric-conversions-table.md)
