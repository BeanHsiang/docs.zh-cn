---
title: '&amp; 运算符 - C# 参考'
ms.custom: seodec18
ms.date: 10/29/2018
f1_keywords:
- '&_CSharpKeyword'
helpviewer_keywords:
- bitwise AND operator [C#]
- ampersand operator (&) [C#]
- '& operator [C#]'
- AND operator (&) [C#]
ms.assetid: afa346d5-90ec-4b1f-a2c8-3881f018741d
ms.openlocfilehash: a799c0e37d6607e8ff72ab984ff5e540a4e11063
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53236370"
---
# <a name="amp-operator-c-reference"></a>&amp; 运算符（C# 参考）

以下两种形式支持 `&` 运算符：一元 address-of 运算符或二元逻辑运算符。

## <a name="unary-address-of-operator"></a>一元 address-of 运算符

一元 `&` 运算符返回其操作数的地址。 有关详细信息，请参阅[如何：获取变量的地址](../../programming-guide/unsafe-code-pointers/how-to-obtain-the-address-of-a-variable.md)。

Address-of 运算符 `&` 需要 [不安全](../keywords/unsafe.md)上下文。

## <a name="integer-logical-bitwise-and-operator"></a>整型逻辑按位 AND 运算符

对于整数类型，`&` 运算符对其操作数执行逻辑按位 AND 运算：

[!code-csharp-interactive[integer logical bitwise AND](~/samples/snippets/csharp/language-reference/operators/AndOperatorExamples.cs#IntegerOperands)]

> [!NOTE]
> 之前的示例使用[在 C# 7.0 中引入](../../whats-new/csharp-7.md#numeric-literal-syntax-improvements)并[在 C# 7.2 中增强](../../whats-new/csharp-7-2.md#leading-underscores-in-numeric-literals)的二进制文本。

由于针对整数类型的运算通常也允许针对枚举类型进行，因此 `&` 运算符也支持[枚举](../keywords/enum.md)操作数。

## <a name="boolean-logical-and-operator"></a>布尔逻辑 AND 运算符

对于 [bool](../keywords/bool.md) 操作数，`&` 运算符对其操作数执行逻辑 AND 运算。 如果 `x` 和 `y` 都为 `true`，则 `x & y` 的结果为 `true`。 否则，结果为 `false`。

即使第一个操作数计算结果为 `false`，`&` 运算符也会计算这两个操作数，而在这种情况下，无论第二个操作数的值为何，结果都肯定为 `false`。 以下示例演示了该行为：

[!code-csharp-interactive[bool logical AND](~/samples/snippets/csharp/language-reference/operators/AndOperatorExamples.cs#BooleanOperands)]

[条件 AND 运算符](conditional-and-operator.md) `&&` 也会计算其操作数的逻辑 AND，但只有在第一个操作数的计算结果为 `true` 时，才会计算第二个操作数。

对于可为 null 的 bool 操作数，`&` 操作数的行为与 SQL 的三值逻辑一致。 有关详细信息，请参阅[使用可以为 null 的类型](../../programming-guide/nullable-types/using-nullable-types.md)一文的 [bool? 类型](../../programming-guide/nullable-types/using-nullable-types.md#the-bool-type)部分。

## <a name="operator-overloadability"></a>运算符可重载性

用户定义类型可以[重载](../keywords/operator.md)二元 `&` 运算符。 重载二元 `&` 运算符后，也会隐式重载 [AND 赋值运算符](and-assignment-operator.md) `&=`。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)的 [address-of 运算符](~/_csharplang/spec/unsafe-code.md#the-address-of-operator)和[逻辑运算符](~/_csharplang/spec/expressions.md#logical-operators)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [指针类型](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [| 运算符](or-operator.md)
- [^ 运算符](xor-operator.md)
- [~ 运算符](bitwise-complement-operator.md)
- [&& 运算符](conditional-and-operator.md)
