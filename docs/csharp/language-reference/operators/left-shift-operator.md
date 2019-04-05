---
title: << 运算符 - C# 参考
ms.custom: seodec18
ms.date: 02/12/2019
f1_keywords:
- <<_CSharpKeyword
helpviewer_keywords:
- left shift operator (<<) [C#]
- << operator [C#]
ms.assetid: a654eb56-1ff7-4bf3-9064-b631be0cdccc
ms.openlocfilehash: deea2d0f720ba7f096e65c67378586bc88f24673
ms.sourcegitcommit: 30e2fe5cc4165aa6dde7218ec80a13def3255e98
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2019
ms.locfileid: "56219428"
---
# <a name="-operator-c-reference"></a>\<\< 运算符（C# 参考）

左移运算符 `<<` 将第一个操作数向左移动第二个操作数定义的位数。 所有整数类型都支持 `<<` 运算符。 但是，第二个操作数的类型必须为 [int](../keywords/int.md) 或[预定义隐式数值转换](../keywords/implicit-numeric-conversions-table.md)为 `int` 的类型。

放弃结果类型范围之外的高顺序位，将低顺序空位位置设置为零，如下例所示：

[!code-csharp-interactive[left shift example](~/samples/snippets/csharp/language-reference/operators/ShiftOperatorsExamples.cs#LeftShift)]

## <a name="shift-count"></a>移位计数

对于表达式 `x << count`，实际移位计数取决于 `x` 的类型，如下所示：

- 如果 `x` 的类型是 [int](../keywords/int.md) 或 [uint](../keywords/uint.md)，则移位计数由第二个操作数的低顺序五位给定。 也就是说，移位计数通过 `count & 0x1F`（或 `count & 0b_1_1111`）计算得出。

- 如果 `x` 的类型是 [long](../keywords/long.md) 或 [ulong](../keywords/ulong.md)，则移位计数由第二个操作数的低顺序六位给定。 也就是说，移位计数通过 `count & 0x3F`（或 `count & 0b_11_1111`）计算得出。

以下示例演示了该行为：

[!code-csharp-interactive[shift count example](~/samples/snippets/csharp/language-reference/operators/ShiftOperatorsExamples.cs#LeftShiftByLargeCount)]

## <a name="remarks"></a>备注

移位运算绝对不会导致溢出并在[选中和未选中](../keywords/checked-and-unchecked.md)上下文中产生相同结果。

## <a name="operator-overloadability"></a>运算符可重载性

用户定义的类型可以[重载](../keywords/operator.md) `<<` 运算符。 如果用户定义类型 `T` 重载 `<<` 运算符，则第一个操作数的类型必须是 `T`，第二个操作数的类型必须是 `int`。 在重载 `<<` 运算符后，还会隐式重载[左移赋值运算符](left-shift-assignment-operator.md) `<<=`。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[移位运算符](~/_csharplang/spec/expressions.md#shift-operators)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [>> 运算符](right-shift-operator.md)
