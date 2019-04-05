---
title: 如何：确定可以为 null 的类型 - C# 编程指南
ms.custom: seodec18
description: 了解如何确定类型是否是可以为 null 的类型或实例是否是可以为 null 的类型
ms.date: 09/24/2018
helpviewer_keywords:
- nullable types [C#], identifying
ms.assetid: d4b67ee2-66e8-40c1-ae9d-545d32c71387
ms.openlocfilehash: 33169315f8bef45aba52f0696d4acac031584817
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54582622"
---
# <a name="how-to-identify-a-nullable-type-c-programming-guide"></a>如何：确定可以为 null 的类型（C# 编程指南）

下面的示例演示如何确定 <xref:System.Type?displayProperty=nameWithType> 实例是否表示可以为 null 的封闭式泛型类型，即，具有指定类型参数 `T` 的 <xref:System.Nullable%601?displayProperty=nameWithType> 类型：

[!code-csharp-interactive[whether Type is nullable](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#1)]

如示例所示，使用 [typeof](../../language-reference/keywords/typeof.md) 运算符来创建 <xref:System.Type?displayProperty=nameWithType> 对象。  
  
如果要确定实例是否是可以为 null 的类型，请不要使用 <xref:System.Object.GetType%2A?displayProperty=nameWithType> 方法获取要通过前面的代码测试的 <xref:System.Type> 实例。 如果对可以为 null 的类型的实例调用 <xref:System.Object.GetType%2A?displayProperty=nameWithType> 方法，该实例将[装箱](using-nullable-types.md#boxing-and-unboxing)到 <xref:System.Object>。 由于对可以为 null 的类型的非 NULL 实例的装箱等效于对基础类型的值的装箱，因此 <xref:System.Object.GetType%2A> 返回表示可以为 null 的类型的基础类型的 <xref:System.Type> 对象：

[!code-csharp-interactive[GetType example](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#2)]

请勿使用 [is](../../language-reference/keywords/is.md) 运算符来确定实例是否是可以为 null 的类型。 如以下示例所示，无法使用 `is` 运算符区分可以为 null 的类型的实例类型和其基础类型：

[!code-csharp-interactive[is operator example](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#3)]

可使用以下示例中提供的代码来确定实例是否是可以为 null 的类型：

[!code-csharp-interactive[whether an instance is of a nullable type](../../../../samples/snippets/csharp/programming-guide/nullable-types/IdentifyNullableType.cs#4)]
  
## <a name="see-also"></a>请参阅

- [可以为 null 的类型](index.md)
- [使用可以为 null 的类型](using-nullable-types.md)
- <xref:System.Nullable.GetUnderlyingType%2A>
