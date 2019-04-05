---
title: double 关键字 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- double
- double_CSharpKeyword
helpviewer_keywords:
- double data type [C#]
ms.assetid: 0980e11b-6004-4102-abcf-cfc280fc6991
ms.openlocfilehash: 50e11e8547c2887ace677d2c86dcf055326ff9a4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54708150"
---
# <a name="double-c-reference"></a>double（C# 参考）

`double` 关键字表示存储 64 位浮点值的简单类型。 下表显示了 `double` 类型的精度和大致范围。

|类型|大致范围|精度|.NET 类型|
|----------|-----------------------|---------------|-------------------------|
|`double`|±5.0 × 10<sup>−324</sup> 到 ±1.7 × 10<sup>308</sup>|大约 15-17 位数字|<xref:System.Double?displayProperty=nameWithType>|

## <a name="literals"></a>文本

默认情况下，赋值运算符右侧的实数被视为 `double`。 但是，如果希望整数被视为 `double`，可使用后缀 d 或 D，例如：

```csharp
double x = 3D;
```

## <a name="conversions"></a>转换

可以在表达式中混合使用数值整型和浮点类型。 在这种情况下，整数类型将转换为浮点类型。 根据以下规则对表达式求值：

- 如果其中一个浮点类型是 `double`，该表达式在关系比较和相等比较中求值类型为 `double` 或 [bool](../../../csharp/language-reference/keywords/bool.md)。

- 如果表达式中没有 `double` 类型，则表达式在关系比较和相等比较中求值类型为[float](../../../csharp/language-reference/keywords/float.md) 或 [bool](../../../csharp/language-reference/keywords/bool.md)。

 浮点表达式可以包含下列值集：

- 正零和负零。

- 正无穷大和负无穷大。

- 非数字值 (NaN)。

- 一组有限的非零值。

有关这些值的详细信息，请参阅 [IEEE](https://www.ieee.org) 网站中提供的二进制浮点算术的 IEEE 标准。

## <a name="example"></a>示例

在下面的示例中，将 [int](../../../csharp/language-reference/keywords/int.md)、[short](../../../csharp/language-reference/keywords/short.md)、[float](../../../csharp/language-reference/keywords/float.md) 和 `double` 相加可得出 `double` 结果。

[!code-csharp[csrefKeywordsTypes#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#9)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](../../../csharp/language-reference/keywords/index.md)
- [默认值表](../../../csharp/language-reference/keywords/default-values-table.md)
- [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)
- [浮点型表](../../../csharp/language-reference/keywords/floating-point-types-table.md)
- [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)
- [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
