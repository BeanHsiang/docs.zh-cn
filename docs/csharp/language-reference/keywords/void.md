---
title: void - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- void_CSharpKeyword
- void
helpviewer_keywords:
- void keyword [C#]
ms.assetid: 0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4
ms.openlocfilehash: ce52e4d19335db0e21637b87bbd1589c86c06ae1
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613123"
---
# <a name="void-c-reference"></a>void（C# 参考）

当用作一种方法的返回类型时，`void` 将指定该方法不返回值。

方法的参数列表中不允许有 `void`。 无参数且不返回值的方法的声明方式如下：

```csharp
public void SampleMethod()
{
    // Body of the method.
}
```

`void` 还可用于在不安全的上下文中将指针声明为未知类型。 有关详细信息，请参阅[指针类型](../../programming-guide/unsafe-code-pointers/pointer-types.md)。

`void` 是 .NET Framework <xref:System.Void?displayProperty=nameWithType> 类型的别名。

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [引用类型](reference-types.md)
- [值类型](value-types.md)
- [方法](../../programming-guide/classes-and-structs/methods.md)
- [不安全代码和指针](../../programming-guide/unsafe-code-pointers/index.md)