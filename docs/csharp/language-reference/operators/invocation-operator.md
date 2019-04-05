---
title: () 运算符 - C# 参考
ms.custom: seodec18
ms.date: 01/15/2019
f1_keywords:
- ()_CSharpKeyword
helpviewer_keywords:
- type conversion [C#], () operator
- cast operator [C#]
- () operator [C#]
ms.assetid: 846e1f94-8a8c-42fc-a42c-fbd38e70d8cc
ms.openlocfilehash: 3a0af33739c9cb4d090842219eba4ece9700ef89
ms.sourcegitcommit: 542aa405b295955eb055765f33723cb8b588d0d0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2019
ms.locfileid: "54362777"
---
# <a name="-operator-c-reference"></a>() 运算符（C# 参考）

括号 `()` 通常用于方法或委托调用或用于强制转换表达式。

此外可以使用括号来指定表达式中计算操作的顺序。 有关详细信息，请参阅[运算符](../../programming-guide/statements-expressions-operators/operators.md)一文中的[添加括号](../../programming-guide/statements-expressions-operators/operators.md#adding-parentheses)部分。 对于按优先级排序的运算符列表，请参阅 [C# 运算符](index.md)。

## <a name="method-invocation"></a>方法调用

下面的示例演示如何调用方法（带或不带参数）和委托：

[!code-csharp-interactive[use for invocation](~/samples/snippets/csharp/language-reference/operators/InvocationOperatorExamples.cs#Invocation)]

在调用带 [`new`](../keywords/new-operator.md) 运算符的[构造函数](../../programming-guide/classes-and-structs/constructors.md)时，还可以使用括号。

有关这些方法的详细信息，请参阅[方法](../../programming-guide/classes-and-structs/methods.md)。 有关委托的详细信息，请参阅[委托](../../programming-guide/delegates/index.md)。

## <a name="cast-expression"></a>强制转换表达式

`(T)E` 形式的强制转换表达式调用转换运算符以将表达式 `E` 的值转换为类型 `T`。 如果不存在从类型 `E` 到类型 `T` 的显式转换，则发生编译时错误。 有关如何定义转换运算符的信息，请参阅[显式](../keywords/explicit.md)和[隐式](../keywords/implicit.md)关键字文章。

下面的示例演示了数值类型之间的类型转换：

[!code-csharp-interactive[use for cast](~/samples/snippets/csharp/language-reference/operators/InvocationOperatorExamples.cs#Cast)]

若要详细了解数值类型之间的预定义显式转换，请参阅[显式数值转换表](../keywords/explicit-numeric-conversions-table.md)。

有关详细信息，请参阅[强制转换和类型转换](../../programming-guide/types/casting-and-type-conversions.md)以及[转换运算符](../../programming-guide/statements-expressions-operators/conversion-operators.md)。

## <a name="operator-overloadability"></a>运算符可重载性

不能重载 `()` 运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的 [调用表达式](~/_csharplang/spec/expressions.md#invocation-expressions)和[强制转换表达式](~/_csharplang/spec/expressions.md#cast-expressions)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)