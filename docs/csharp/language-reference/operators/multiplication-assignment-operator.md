---
title: '*= 运算符 - C# 参考'
ms.custom: seodec18
ms.date: 02/26/2019
f1_keywords:
- '*=_CSharpKeyword'
helpviewer_keywords:
- '*= operator [C#]'
- binary multiplication assignment operator (*=) [C#]
ms.assetid: 2e472155-59db-4dbf-bb94-bcccfa1a794d
ms.openlocfilehash: 70461f79e714e44354fe4137e5360769fa048d3e
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56967381"
---
# <a name="-operator-c-reference"></a>\*= 运算符（C# 参考）

乘法赋值运算符。

使用 `*=` 运算符的表达式，例如

```csharp
x *= y
```

等效于

```csharp
x = x * y
```

不同的是 `x` 只计算一次。

对于数字类型，[\* 运算符](multiplication-operator.md)计算其操作数的乘积。

下面的示例演示 `*=` 运算符的用法：

[!code-csharp-interactive[multiply and assign](~/samples/snippets/csharp/language-reference/operators/MultiplicationExamples.cs#MultiplyAndAssign)]

## <a name="operator-overloadability"></a>运算符可重载性

如果用户定义类型[重载](../keywords/operator.md)[乘法运算符](multiplication-operator.md) `*`，则乘法赋值运算符 `*=` 为隐式重载。 用户定义类型不能显式重载乘法赋值运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[复合赋值](~/_csharplang/spec/expressions.md#compound-assignment)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
