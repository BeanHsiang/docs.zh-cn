---
title: <<= 运算符 - C# 参考
ms.custom: seodec18
ms.date: 02/12/2019
f1_keywords:
- <<=_CSharpKeyword
helpviewer_keywords:
- <<= operator (left-shift assignment) [C#]
- left shift assignment operator (<<=) [C#]
ms.assetid: 3bc99c78-1edb-4827-86fc-bce6c3048871
ms.openlocfilehash: d2105fbee4ddfe1b2cb3325d82b0f2f8c5559297
ms.sourcegitcommit: 30e2fe5cc4165aa6dde7218ec80a13def3255e98
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2019
ms.locfileid: "56219444"
---
# <a name="-operator-c-reference"></a>\<\<= 运算符（C# 参考）

左移赋值运算符。

使用 `<<=` 运算符的表达式，例如

```csharp
x <<= y
```

等效于

```csharp
x = x << y
```

不同的是 `x` 只计算一次。

[`<<` 运算符](left-shift-operator.md) 将第一个操作数向左移动第二个操作数定义的位数。

下面的示例演示 `<<=` 运算符的用法：

[!code-csharp-interactive[left shift assignment](~/samples/snippets/csharp/language-reference/operators/ShiftOperatorsExamples.cs#LeftShiftAssignment)]

## <a name="operator-overloadability"></a>运算符可重载性

如果用户定义类型[重载](../keywords/operator.md) [`<<` 运算符](left-shift-operator.md)，则会隐式重载左移赋值运算符 `<<=`。 用户定义类型不得显式重载左移赋值运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[复合赋值](~/_csharplang/spec/expressions.md#compound-assignment)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
