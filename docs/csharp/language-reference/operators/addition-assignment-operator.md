---
title: += 运算符 - C# 参考
ms.custom: seodec18
ms.date: 10/29/2018
f1_keywords:
- +=_CSharpKeyword
helpviewer_keywords:
- += operator [C#]
- addition assignment operator (+=) [C#]
- event subscription [C#]
ms.assetid: 9cdf97e6-331d-492b-85e1-3ec3171484e9
ms.openlocfilehash: 5d48f2fe53a9bb6f781f8d35f1e0983bcaa30f88
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53240926"
---
# <a name="-operator-c-reference"></a>+= 运算符（C# 参考）

加法赋值运算符。

使用 `+=` 运算符的表达式，例如

```csharp
x += y
```

等效于

```csharp
x = x + y
```

不同的是 `x` 只计算一次。
  
对于数字类型，[加法运算符](addition-operator.md) `+`计算其操作数的和。 如果其中的一个操作数是 [string](../keywords/string.md) 类型或两个操作数都是该类型，它会将操作数的字符串表示形式串联在一起。 对于委托类型，`+` 运算符返回一个新的委托实例，该实例是其操作数的组合。

在订阅[事件](../keywords/event.md)时，还可以使用 `+=` 运算符来指定事件处理程序方法。 有关更多信息，请参见[如何：订阅和取消订阅事件](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)。

下面的示例演示 `+=` 运算符的用法：

[!code-csharp-interactive[+= examples](~/samples/snippets/csharp/language-reference/operators/AdditionExamples.cs#AddAndAssign)]

## <a name="operator-overloadability"></a>运算符可重载性

如果用户定义类型[重载](../keywords/operator.md)[加法运算符](addition-operator.md) `+`，则加法赋值运算符 `+=` 为隐式重载。 用户定义类型不能显式重载加法赋值运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[复合赋值](~/_csharplang/spec/expressions.md#compound-assignment)和[事件赋值](~/_csharplang/spec/expressions.md#event-assignment)部分。
  
## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [事件](../../programming-guide/events/index.md)
- [委托](../../programming-guide/delegates/index.md)
