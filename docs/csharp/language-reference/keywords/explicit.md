---
title: explicit 关键字 - C# 参考
ms.custom: seodec18
ms.date: 08/24/2018
f1_keywords:
- explicit_CSharpKeyword
- explicit
helpviewer_keywords:
- explicit keyword [C#]
ms.assetid: cfb8f42a-e411-4db2-af9b-796b05644846
ms.openlocfilehash: 4949b88a32dae2a727e623bb6e4db0a4f9d8418c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54557989"
---
# <a name="explicit-c-reference"></a>explicit（C# 参考）

`explicit` 关键字声明必须通过转换来调用的用户定义的类型转换运算符。

以下示例定义从 `Fahrenheit` 类转换为 `Celsius` 类的运算符。 必须在 `Fahrenheit` 类或 `Celsius` 类中定义运算符：

[!code-csharp[csrefKeywordsConversion#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsConversion/CS/csrefKeywordsConversion.cs#2)]

如以下示例所示，使用强制转换调用定义的转换运算符：

[!code-csharp[csrefKeywordsConversion#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsConversion/CS/csrefKeywordsConversion.cs#3)]

此转换运算符从源类型转换为目标类型。 源类型提供转换运算符。 不同于隐式转换，显式转换运算符必须通过转换的方式来调用。 如果转换操作会导致异常或丢失信息，则应将其标记为 `explicit`。 这可阻止编译器静默调用可能产生意外后果的转换操作。

省略转换将导致编译时错误 CS0266。

有关详细信息，请参阅[使用转换运算符](../../programming-guide/statements-expressions-operators/using-conversion-operators.md)。

## <a name="example"></a>示例

下面的示例提供了 `Fahrenheit` 和 `Celsius` 类，其中每个类均提供转换为其他类的显式转换运算符。

[!code-csharp[csrefKeywordsConversion#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsConversion/CS/csrefKeywordsConversion.cs#1)]

## <a name="example"></a>示例

下面的示例定义结构 `Digit`，它表示单个的十进制数字。 将运算符定义为从 `byte` 到 `Digit` 的转换，但由于并非所有字节都可转换为 `Digit`，因此该转换为显式。

[!code-csharp[csrefKeywordsConversion#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsConversion/CS/csrefKeywordsConversion.cs#4)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [implicit](implicit.md)
- [运算符（C# 参考）](operator.md)
- [如何：在结构之间实现用户定义的转换](../../programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)
- [Chained user-defined explicit conversions in C#](https://blogs.msdn.microsoft.com/ericlippert/2007/04/16/chained-user-defined-explicit-conversions-in-c/)（C# 中链接在一起的用户定义的显式转换）
