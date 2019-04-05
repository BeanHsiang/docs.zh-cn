---
title: < 运算符 - C# 参考
ms.custom: seodec18
ms.date: 12/18/2018
f1_keywords:
- <_CSharpKeyword
helpviewer_keywords:
- less than operator (<) [C#]
- < operator [C#]
ms.assetid: 38cb91e6-79a6-48ec-9c1e-7b71fd8d2b41
ms.openlocfilehash: ab21e32b7609bc0c8753b42ccf8b6091bf3ad57b
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55286632"
---
# <a name="-operator-c-reference"></a>\< 运算符（C# 参考）

如果第一操作数小于第二操作数，“小于”关系运算符 `<` 返回 `true`，否则返回 `false`。 所有数值和枚举类型都支持 `<` 运算符。 对于相同[枚举](../keywords/enum.md)类型的操作数，基础整数类型的相应值会进行比较。

> [!NOTE]
> 对于关系运算符 `==`、`>`、`<`、`>=` 和 `<=`，如果任何操作数不是数字 (<xref:System.Double.NaN?displayProperty=nameWithType> 或 <xref:System.Single.NaN?displayProperty=nameWithType>)，操作数的结果为 `false`。 这意味着 `NaN` 值不大于、小于或等于任何其他 `double` （或 `float`）值。 有关更多信息和示例，请参阅 <xref:System.Double.NaN?displayProperty=nameWithType> 或 <xref:System.Single.NaN?displayProperty=nameWithType> 参考文章。

下面的示例演示 `<` 运算符的用法：

[!code-csharp-interactive[less than example](~/samples/snippets/csharp/language-reference/operators/GreaterAndLessOperatorsExamples.cs#Less)]

## <a name="operator-overloadability"></a>运算符可重载性

用户定义的类型可以[重载](../keywords/operator.md) `<` 运算符。 如果类型重载“小于”运算符 `<`，它必须也重载[“大于”运算符](greater-than-operator.md) `>`。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[关系和类型测试运算符](~/_csharplang/spec/expressions.md#relational-and-type-testing-operators)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [<= 运算符](less-than-equal-operator.md)
- <xref:System.IComparable%601?displayProperty=nameWithType>
