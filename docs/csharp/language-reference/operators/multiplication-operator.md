---
title: '* 运算符 - C# 参考'
ms.custom: seodec18
ms.date: 02/26/2019
f1_keywords:
- '*_CSharpKeyword'
helpviewer_keywords:
- multiplication operator (*) [C#]
- '* operator [C#]'
ms.assetid: abd9a5f0-9b24-431e-971a-09ee1c45c50e
ms.openlocfilehash: a5e120d26614f1e38cc2f2db02949552140b594e
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56977339"
---
# <a name="-operator-c-reference"></a>* 运算符（C# 参考）

支持以下两种形式的 `*` 运算符：一元指针间接运算符或二元乘法运算符。

## <a name="pointer-indirection-operator"></a>指针间接运算符

使用一元 `*` 运算符获取指针类型的操作数指向的变量。 有关详细信息，请参阅[如何：获取指针变量的值](../../programming-guide/unsafe-code-pointers/how-to-obtain-the-value-of-a-pointer-variable.md)。

指针间接运算符 `*` 需要 [unsafe](../keywords/unsafe.md) 上下文。

## <a name="multiplication-operator"></a>乘法运算符

对于数字类型，`*` 运算符计算其操作数的乘积：

[!code-csharp-interactive[multiplication](~/samples/snippets/csharp/language-reference/operators/MultiplicationExamples.cs#Multiply)]

## <a name="operator-overloadability"></a>运算符可重载性

用户定义类型可以[重载](../keywords/operator.md)二元 `*` 运算符。 重载二元 `*` 运算符后，也会隐式重载[乘法赋值运算符](multiplication-assignment-operator.md) `*=`。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅[C# 语言规范](../language-specification/index.md)的[指针间接](~/_csharplang/spec/unsafe-code.md#pointer-indirection)和[乘法运算符](~/_csharplang/spec/expressions.md#multiplication-operator)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [指针类型](../../programming-guide/unsafe-code-pointers/pointer-types.md)