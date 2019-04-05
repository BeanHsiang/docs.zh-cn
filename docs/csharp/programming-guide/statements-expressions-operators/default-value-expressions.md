---
title: 默认值表达式 - C# 编程指南
ms.custom: seodec18
description: 默认值表达式生成任何引用类型或值类型的默认值
ms.date: 04/25/2018
helpviewer_keywords:
- generics [C#], default keyword
- default keyword [C#], generic programming
ms.openlocfilehash: 8e10a5de73e8d49f1a380fb8945b98ac797ef270
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54575536"
---
# <a name="default-value-expressions-c-programming-guide"></a>默认值表达式（C# 编程指南）

默认值表达式 `default(T)` 生成 `T` 类型的默认值。 下表显示为各种类型生成的值：

|类型|默认值|
|---------|---------|
|任何引用类型|`null`|
|数值类型|零|
|[bool](../../language-reference/keywords/bool.md)|`false`|
|[char](../../language-reference/keywords/char.md)|`'\0'`|
|[enum](../../language-reference/keywords/enum.md)|表达式 `(E)0` 生成的值，其中 `E` 是枚举标识符。|
|[struct](../../language-reference/keywords/struct.md)|通过如下设置生成的值：将所有值类型的字段设置为其默认值，将所有引用类型的字段设置为 `null`。|
|可以为 null 的类型|<xref:System.Nullable%601.HasValue%2A> 属性为 `false` 且 <xref:System.Nullable%601.Value%2A> 属性未定义的实例。|

默认值表达式在泛型类和泛型方法中非常有用。 使用泛型类和泛型方法时出现的一个问题是，如何在无法提前知道以下内容的情况下将默认值赋值给参数化类型 `T`：

- `T` 是引用类型还是值类型。
- 如果 `T` 是值类型，它是数值还是结构。

 已知参数化类型 `T` 的变量 `t`，仅当 `T` 为引用类型时，语句 `t = null` 才有效。 赋值 `t = 0` 仅对数值类型有效，对结构无效。 若要解决此问题，请使用默认值表达式：

```csharp
T t = default(T);
```

`default(T)` 表达式不限于泛型类和泛型方法。 默认值表达式可用于任何托管类型。 以下任一表达式都是有效的：

 [!code-csharp[csProgGuideGenerics#1](../../../../samples/snippets/csharp/programming-guide/statements-expressions-operators/default-value-expressions.cs)]

 `GenericList<T>` 类的以下示例演示如何在泛型类中使用 `default(T)` 运算符。 有关详细信息，请参阅[泛型介绍](../generics/introduction-to-generics.md)。

 [!code-csharp[csProgGuideGenerics#2](../../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#Snippet41)]

## <a name="default-literal-and-type-inference"></a>默认文本和类型推理

从 C# 7.1 开始，当编译器可以推断表达式的类型时，文本 `default` 可用于默认值表达式。 文本 `default` 生成与等效项 `default(T)`（其中，`T` 是推断的类型）相同的值。 这可减少多次声明类型的冗余，从而使代码更加简洁。 文本 `default` 可用于以下任一位置：

- 变量初始值设定项
- 变量赋值
- 声明可选参数的默认值
- 为方法调用参数提供值
- 返回语句（或 expression bodied 成员中的表达式）

以下示例展示了文本 `default` 在默认值表达式中的多种用法：

[!code-csharp[csProgGuideGenerics#3](../../../../samples/snippets/csharp/programming-guide/statements-expressions-operators/default-literal.cs)]

## <a name="see-also"></a>请参阅

- <xref:System.Collections.Generic>
- [C# 编程指南](../index.md)
- [泛型（C# 编程指南）](../generics/index.md)
- [泛型方法](../generics/generic-methods.md)
- [.NET 中的泛型](~/docs/standard/generics/index.md)
- [默认值表](../../language-reference/keywords/default-values-table.md)
