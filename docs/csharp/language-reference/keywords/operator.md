---
title: operator 关键字 - C# 参考
ms.custom: seodec18
description: 了解如何重载内置 C# 运算符
ms.date: 08/27/2018
f1_keywords:
- operator_CSharpKeyword
- operator
helpviewer_keywords:
- operator keyword [C#]
ms.assetid: 59218cce-e90e-42f6-a6bb-30300981b86a
ms.openlocfilehash: cdc052da4457a59cc66848780e944ccf203acf39
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53235578"
---
# <a name="operator-c-reference"></a>运算符（C# 参考）

使用 `operator` 关键字重载内置运算符，或在类或结构声明中提供用户定义的转换。

若要在自定义类或结构上重载运算符，可以在相应的类型中创建运算符声明。 重载内置 C# 运算符的运算符声明必须满足以下规则：

- 同时包含 `public` 和 `static` 修饰符。
- 包含 `operator X`，其中 `X` 是被重载运算符的名称或符号。
- 一元运算符具有一个参数，二元运算符具有两个参数。 在每种情况下，都必须至少有一个参数与声明运算符的类或结构的类型相同。

有关如何定义转换运算符的信息，请参阅[显式](explicit.md)和[隐式](implicit.md)关键字文章。

有关可重载 C# 运算符的概述，请参阅[可重载运算符](../../programming-guide/statements-expressions-operators/overloadable-operators.md)一文。

## <a name="example"></a>示例

以下示例定义了表示小数的 `Fraction` 类型。 此类重载 `+` 和 `*` 运算符以执行分数加法和乘法，并提供转换运算符将 `Fraction` 类型转换为 `double` 类型。

[!code-csharp[csrefKeywordsConversion#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsConversion/CS/csrefKeywordsConversion.cs#6)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [implicit](implicit.md)
- [explicit](explicit.md)
- [可重载运算符](../../programming-guide/statements-expressions-operators/overloadable-operators.md)
- [如何：在结构之间实现用户定义的转换](../../programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)
