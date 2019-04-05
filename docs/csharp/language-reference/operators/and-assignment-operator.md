---
title: '&amp;= 运算符 - C# 参考'
ms.custom: seodec18
ms.date: 10/29/2018
f1_keywords:
- '&=_CSharpKeyword'
helpviewer_keywords:
- AND assignment operator (&=) [C#]
- '&= operator [C#]'
ms.assetid: e8d58f3f-72dd-4b5a-b995-452fcce7e6bb
ms.openlocfilehash: 223d2f30ee77457e1f9d5304ec299517932499d0
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53237020"
---
# <a name="amp-operator-c-reference"></a>&amp;= 运算符（C# 参考）

AND 赋值运算符。

使用 `&=` 运算符的表达式，例如

```csharp
x &= y
```

等效于

```csharp
x = x & y
```

不同的是 `x` 只计算一次。

对于整数操作数，[`&` 运算符](and-operator.md)对其操作数执行按位逻辑 AND 运算；而对于 [bool](../keywords/bool.md) 操作数，该运算符对其操作数执行逻辑 AND 运算。

下面的示例演示 `&=` 运算符的用法：

[!code-csharp-interactive[AND assignment example](~/samples/snippets/csharp/language-reference/operators/AndOperatorExamples.cs#AndAssignmentExample)]

## <a name="operator-overloadability"></a>运算符可重载性

如果用户定义类型[重载](../keywords/operator.md) [`&` 运算符](and-operator.md)，则 AND 赋值运算符 `&=` 为隐式重载。 用户定义类型不能显式重载 AND 赋值运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[复合赋值](~/_csharplang/spec/expressions.md#compound-assignment)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
