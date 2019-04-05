---
title: -> 运算符 - C# 参考
ms.custom: seodec18
ms.date: 11/26/2018
f1_keywords:
- ->_CSharpKeyword
helpviewer_keywords:
- member access operator (->) [C#]
- -> operator [C#]
ms.assetid: e39ccdc1-f1ff-4a92-bf1d-ac2c8c11316a
ms.openlocfilehash: be74f02a85aa05cdab32768ed38222fc4d9289b1
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55255362"
---
# <a name="--operator-c-reference"></a>-> 运算符（C# 参考）

指针成员访问运算符 `->` 结合了指针间接和成员访问。

如果 `x` 是类型为 `T*` 的指针而 `y` 是 `T` 的可访问成员，则这种形式的表达式

```csharp
x->y
```

等效于

```csharp
(*x).y
```

`->` 运算符需要[不安全](../keywords/unsafe.md)上下文。

有关详细信息，请参阅[如何：使用指针访问成员](../../programming-guide/unsafe-code-pointers/how-to-access-a-member-with-a-pointer.md)。

## <a name="operator-overloadability"></a>运算符可重载性

不能重载 `->` 运算符。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[指针成员访问](~/_csharplang/spec/unsafe-code.md#pointer-member-access)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [指针类型](../../programming-guide/unsafe-code-pointers/pointer-types.md)
