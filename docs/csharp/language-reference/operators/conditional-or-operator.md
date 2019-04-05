---
title: '|| 运算符 - C# 参考'
ms.custom: seodec18
ms.date: 11/06/2018
f1_keywords:
- '||_CSharpKeyword'
helpviewer_keywords:
- logical OR operator [C#]
- conditional-OR operator (||) [C#]
- '|| operator [C#]'
ms.assetid: 7d442d8e-400d-421f-b4d2-034bf82bcbdc
ms.openlocfilehash: 079c021eb68ece097c7f644416f1e9469a82dcea
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2019
ms.locfileid: "54415424"
---
# <a name="-operator-c-reference"></a>|| 运算符（C# 参考）

条件逻辑 OR 运算符 `||`（也称为“短路”逻辑 OR 运算符）计算其 [bool](../keywords/bool.md) 操作数的逻辑 OR。 如果 `x` 或 `y` 的计算结果为 `true`，则 `x || y` 的结果为 `true`。 否则，结果为 `false`。 如果第一个操作数的计算结果为 `true`，则不会计算第二个操作数且运算结果为 `true`。 以下示例演示了该行为：

[!code-csharp-interactive[conditional logical OR](~/samples/snippets/csharp/language-reference/operators/ConditionalLogicalOperatorsExamples.cs#Or)]

[逻辑 OR 运算符](or-operator.md) `|` 也会计算其 `bool` 操作数的逻辑 OR，但始终会计算两个操作数。

## <a name="operator-overloadability"></a>运算符可重载性

用户定义类型不能重载条件逻辑 OR 运算符。 不过，如果用户定义类型以某种方式重载[逻辑 OR](or-operator.md) 以及 [true 和 false 运算符](../keywords/true-false-operators.md)，可以对相应类型的操作数执行 `||` 运算。 有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)的[用户定义条件逻辑运算符](~/_csharplang/spec/expressions.md#user-defined-conditional-logical-operators)部分。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)的[条件逻辑运算符](~/_csharplang/spec/expressions.md#conditional-logical-operators)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [&& 运算符](conditional-and-operator.md)
- [\! 运算符](logical-negation-operator.md)
- [| 运算符](or-operator.md)
