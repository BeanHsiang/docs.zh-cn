---
title: 接口 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- interface_CSharpKeyword
helpviewer_keywords:
- interface keyword [C#]
ms.assetid: 7da38e81-4f99-4bc5-b07d-c986b687eeba
ms.openlocfilehash: ce3cb95617c87d1bf66879f4a2432b4de4ac40f2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54586457"
---
# <a name="interface-c-reference"></a>接口（C# 参考）

接口只包含[方法](../../programming-guide/classes-and-structs/methods.md)、[属性](../../programming-guide/classes-and-structs/properties.md)、[事件](../../programming-guide/events/index.md)或[索引器](../../programming-guide/indexers/index.md)的签名。 实现接口的类或结构必须实现接口定义中指定的接口成员。 在以下示例中，类 `ImplementationClass` 必须实现一个不含参数但返回 `void` 的名为 `SampleMethod` 的方法。

有关详细信息和示例，请参阅[接口](../../programming-guide/interfaces/index.md)。

## <a name="example"></a>示例

[!code-csharp[csrefKeywordsTypes#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#14)]

接口可以是命名空间或类的成员，并且可以包含下列成员的签名：

- [方法](../../programming-guide/classes-and-structs/methods.md)

- [属性](../../programming-guide/classes-and-structs/using-properties.md)

- [索引器](../../programming-guide/indexers/using-indexers.md)

- [事件](event.md)

一个接口可从一个或多个基接口继承。

基类型列表包含基类和接口时，基类必须是列表中的第 1 项。

实现接口的类可以显式实现该接口的成员。 显式实现的成员不能通过类实例访问，而只能通过接口实例访问。

有关显式接口实现的更多详细信息和代码示例，请参阅[显式接口实现](../../programming-guide/interfaces/explicit-interface-implementation.md)。

## <a name="example"></a>示例

下例演示了接口实现。 在此示例中，接口包含属性声明，类包含实现。 实现 `IPoint` 的类的任何实例都具有整数属性 `x` 和 `y`。

[!code-csharp[csrefKeywordsTypes#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#15)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [引用类型](reference-types.md)
- [接口](../../programming-guide/interfaces/index.md)
- [使用属性](../../programming-guide/classes-and-structs/using-properties.md)
- [使用索引器](../../programming-guide/indexers/using-indexers.md)
- [class](class.md)
- [struct](struct.md)
- [接口](../../programming-guide/interfaces/index.md)
