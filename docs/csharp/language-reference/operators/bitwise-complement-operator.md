---
title: ~ 运算符 - C# 参考
ms.custom: seodec18
ms.date: 11/05/2018
f1_keywords:
- ~_CSharpKeyword
helpviewer_keywords:
- tilde (~) one's complement operator [C#]
- ~ operator [C#]
- ~ [C#], bitwise complement operator
- bitwise complement operator [C#]
ms.assetid: 11bc078a-50e2-4d7e-9896-67ef669dc602
ms.openlocfilehash: 57e5baee423c0b5d9292d0ad4cbf909646eb3a38
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53235712"
---
# <a name="-operator-c-reference"></a>~ 运算符（C# 参考）

按位求补运算符 `~` 是一元运算符，通过反转每个位生成其操作数的按位求补。 所有整数类型都支持 `~` 运算符。

> [!NOTE]
> `~` 符号还用于声明终结器。 有关详细信息，请参阅[终结器](../../programming-guide/classes-and-structs/destructors.md)。

下面的示例演示 `~` 运算符的用法：

[!code-csharp-interactive[bitwise NOT](~/samples/snippets/csharp/language-reference/operators/BitwiseComplementExamples.cs#Example)]

> [!NOTE]
> 之前的示例使用[在 C# 7.0 中引入](../../whats-new/csharp-7.md#numeric-literal-syntax-improvements)并[在 C# 7.2 中增强](../../whats-new/csharp-7-2.md#leading-underscores-in-numeric-literals)的二进制文本。

## <a name="operator-overloadability"></a>运算符可重载性

用户定义的类型可以[重载](../keywords/operator.md) `~` 运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)的[按位求补运算符](~/_csharplang/spec/expressions.md#bitwise-complement-operator)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [终结器](../../programming-guide/classes-and-structs/destructors.md)
- [& 运算符](and-operator.md)
- [| 运算符](or-operator.md)
- [^ 运算符](xor-operator.md)
