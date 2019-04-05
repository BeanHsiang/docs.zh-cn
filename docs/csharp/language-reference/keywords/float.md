---
title: float 关键字 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- float
- float_CSharpKeyword
helpviewer_keywords:
- float keyword [C#]
- floating-point numbers [C#], float keyword
ms.assetid: 1e77db7b-dedb-48b7-8dd1-b055e96a9258
ms.openlocfilehash: 6bf8043b97d23fdb91ca5798ed46cdea783bad7e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54514115"
---
# <a name="float-c-reference"></a>float（C# 参考）

`float` 关键字表示存储 32 位浮点值的简单类型。 下表显示了 `float` 类型的精度和大致范围。

|类型|大致范围|精度|.NET 类型|  
|----------|-----------------------|---------------|-------------------------|  
|`float`|±1.5 x 10<sup>−45</sup> 至 ±3.4 x 10<sup>38</sup>|大约 6-9 位数字|<xref:System.Single?displayProperty=nameWithType>|  

## <a name="literals"></a>文本

默认情况下，赋值运算符右侧的实数被视为 [double](double.md)。 因此，若要初始化浮点型变量，请使用后缀 `f` 或 `F`，如以下示例中所示：

```csharp
float x = 3.5F;
```

如果不在前面的声明中使用后缀，则会收到编译错误，因为你正尝试将 [double](double.md) 值存储到 `float` 变量。

## <a name="conversions"></a>转换

可以在表达式中混合使用数值整型和浮点类型。 在这种情况下，整数类型将转换为浮点类型。 根据以下规则对表达式求值：

- 如果其中一个浮点类型是 [double](double.md)，该表达式在关系比较或相等比较中求值类型为 [double](double.md) 或 [bool](bool.md)。

- 如果表达式中没有 [double](double.md) 类型，则表达式在关系比较或相等比较中求值类型为 `float` 或 [bool](bool.md)。

浮点表达式可以包含下列值集：

- 正和负零

- 正和负无穷大

- 非数字值 (NaN)

- 一组有限的非零值

有关这些值的详细信息，请参阅 [IEEE](https://www.ieee.org) 网站中提供的二进制浮点算术的 IEEE 标准。

## <a name="example"></a>示例

在下面的示例中，提供 `float` 结果的数学表达式中包含 [int](int.md)、[short](short.md) 和 `float`。 （请记住，`float` 是 <xref:System.Single?displayProperty=nameWithType> 类型的别名。）请注意，表达式中没有任何 [double](double.md)。

[!code-csharp[csrefKeywordsTypes#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#13)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- <xref:System.Single>
- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [强制转换和类型转换](../../programming-guide/types/casting-and-type-conversions.md)
- [C# 关键字](index.md)
- [整型表](integral-types-table.md)
- [内置类型表](built-in-types-table.md)
- [隐式数值转换表](implicit-numeric-conversions-table.md)
- [显式数值转换表](explicit-numeric-conversions-table.md)
