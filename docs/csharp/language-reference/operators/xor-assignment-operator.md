---
title: ^= 运算符 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- ^=_CSharpKeyword
helpviewer_keywords:
- ^= operator [C#]
ms.assetid: 3658ff9a-61cd-467e-ad6b-8fbf1cfbaae4
ms.openlocfilehash: 12189d6469a9716d3b7ebcffef23423a75692d1a
ms.sourcegitcommit: 5c36aaa8299a2437c155700c810585aff19edbec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2019
ms.locfileid: "54333546"
---
# <a name="-operator-c-reference"></a>^= 运算符（C# 参考）

异或赋值运算符。

## <a name="remarks"></a>备注

形式如下的表达式

```csharp
x ^= y
```

计算结果为

```csharp
x = x ^ y
```

不同的是 `x` 只计算一次。 [^ 运算符](xor-operator.md) 对整型操作数执行按位异或运算，对 [bool](../keywords/bool.md) 操作数执行逻辑异或运算。

不能直接重载 ^= 运算符，但用户定义的类型可重载 [^ 运算符](xor-operator.md)（请参阅[运算符](../keywords/operator.md)）。

## <a name="example"></a>示例

[!code-csharp[csRefOperators#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefOperators/CS/csrefOperators.cs#23)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)