---
title: -= 运算符 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- -=_CSharpKeyword
helpviewer_keywords:
- subtraction assignment operator (-=) [C#]
- -= operator (subtraction assignment ) [C#]
ms.assetid: 05c7d68a-423f-4de8-891b-cf24e8fb6ed7
ms.openlocfilehash: 3b6890be4460a599a5d2f5f5f6ee1627be933f0b
ms.sourcegitcommit: 5c36aaa8299a2437c155700c810585aff19edbec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2019
ms.locfileid: "54333325"
---
# <a name="--operator-c-reference"></a>-= 运算符（C# 参考）

减法赋值运算符。

## <a name="remarks"></a>备注

使用 `-=` 赋值运算符的表达式，如

```csharp
x -= y
```

 等效于

```csharp
x = x - y
```

不同的是 `x` 只计算一次。 [- 运算符](subtraction-operator.md)的含义取决于 `x` 和 `y` 的类型（例如，对于数值操作数，其含义为相减；对于委托操作数，其含义为移除委托）。

不能直接重载 `-=` 运算符，但用户定义的类型可重载 [- 运算符](subtraction-operator.md)（请参阅[运算符](../keywords/operator.md)）。

C# 中也使用 -= 运算符来取消订阅事件。 有关详细信息，请参阅[如何：订阅和取消订阅事件](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)。

## <a name="example"></a>示例

[!code-csharp[csRefOperators#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefOperators/CS/csrefOperators.cs#6)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
