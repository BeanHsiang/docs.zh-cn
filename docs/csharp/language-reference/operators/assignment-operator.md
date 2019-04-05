---
title: = 运算符 - C# 参考
ms.custom: seodec18
ms.date: 11/26/2018
f1_keywords:
- =_CSharpKeyword
helpviewer_keywords:
- = operator [C#]
ms.assetid: d802a6d5-32f0-42b8-b180-12f5a081bfc1
ms.openlocfilehash: 40dc844f2a4b6411ea82aa2f029b36d7dd8f6e5a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716305"
---
# <a name="-operator-c-reference"></a>= 运算符（C# 参考）

赋值运算符 `=` 将其右操作数的值赋给变量、[属性](../../programming-guide/classes-and-structs/properties.md)或由其左操作数给出的[索引器](../../../csharp/programming-guide/indexers/index.md)元素。 赋值表达式的结果是分配给左操作数的值。 右操作数类型必须与左操作数类型相同，或可隐式转换为左操作数的类型。

赋值运算符为右联运算符，即形式的表达式

```csharp
a = b = c
```

计算结果为

```csharp
a = (b = c)
```

以下示例演示赋值运算符将值分配给局部变量、属性和索引器元素的用法：

[!code-csharp-interactive[assignment operator](~/samples/snippets/csharp/language-reference/operators/AssignmentExamples.cs#Assignments)]

## <a name="ref-assignment-operator"></a>ref 赋值运算符

从 C# 7.3 开始，可以使用 ref 赋值运算符 `= ref` 重新分配 [ref local](../keywords/ref.md#ref-locals) 或 [ref readonly local](../keywords/ref.md#ref-readonly-locals) 变量。 下面的示例演示 ref 赋值运算符的用法：

[!code-csharp[ref assignment operator](~/samples/snippets/csharp/language-reference/operators/AssignmentExamples.cs#RefAssignment)]

对于 ref 赋值运算符，左操作数和右操作数的类型必须相同。

有关详细信息，请参阅[功能建议说明](../../../../_csharplang/proposals/csharp-7.3/ref-local-reassignment.md)。

## <a name="operator-overloadability"></a>运算符可重载性

用户定义类型不能重载赋值运算符。 但是，用户定义类型可以定义到其他类型的隐式转换。 这样，可以将用户定义类型的值分配给其他类型的变量、属性或索引器元素。 有关详细信息，请参阅[隐式](../keywords/implicit.md)关键字一文。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[简单赋值](~/_csharplang/spec/expressions.md#simple-assignment)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [ref 关键字](../keywords/ref.md)
