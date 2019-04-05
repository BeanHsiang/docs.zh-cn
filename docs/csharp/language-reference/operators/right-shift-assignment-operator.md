---
title: '>>= 运算符 - C# 参考'
ms.custom: seodec18
ms.date: 02/12/2019
f1_keywords:
- '>>=_CSharpKeyword'
helpviewer_keywords:
- right shift assignment operator (>>=) [C#]
- '>>= operator (right-shift assignment) [C#]'
ms.assetid: b593778c-b9b4-440d-8b29-c1ac22cb81c0
ms.openlocfilehash: 51914bb5e9ebffd5d868528b5a8d3072a956cea6
ms.sourcegitcommit: 30e2fe5cc4165aa6dde7218ec80a13def3255e98
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2019
ms.locfileid: "56220908"
---
# <a name="-operator-c-reference"></a>>>= 运算符（C# 参考）

右移赋值运算符。

使用 `>>=` 运算符的表达式，例如

```csharp
x >>= y
```

等效于

```csharp
x = x >> y
```

不同的是 `x` 只计算一次。

[`>>` 运算符](right-shift-operator.md) 将第一个操作数向右移动第二个操作数定义的位数。

下面的示例演示 `>>=` 运算符的用法：

[!code-csharp-interactive[right shift assignment](~/samples/snippets/csharp/language-reference/operators/ShiftOperatorsExamples.cs#RightShiftAssignment)]

## <a name="operator-overloadability"></a>运算符可重载性

如果用户定义类型[重载](../keywords/operator.md) [`>>` 运算符](right-shift-operator.md)，则隐式重载右移赋值运算符 `>>=`。 用户定义类型不得显式重载右移赋值运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[复合赋值](~/_csharplang/spec/expressions.md#compound-assignment)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)