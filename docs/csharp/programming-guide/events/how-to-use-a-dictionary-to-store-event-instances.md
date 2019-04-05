---
title: 操作说明：使用字典存储事件实例 - C# 编程指南
ms.custom: seodec18
ms.date: 03/11/2019
helpviewer_keywords:
- events [C#], storing instances in a Dictionary
ms.assetid: 9512c64d-5aaf-40cd-b941-ca2a592f0064
ms.openlocfilehash: f8522e499887398402f63c7788bbc6c6c4f57782
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "57845264"
---
# <a name="how-to-use-a-dictionary-to-store-event-instances-c-programming-guide"></a>操作说明：使用字典存储事件实例（C# 编程指南）

`add` 和 `remove` 自定义事件访问器的一个用途是，公开多个事件，但不为每个事件分配字段，而是改用 <xref:System.Collections.Generic.Dictionary%602> 实例来存储事件实例，如下面的示例所示。 这仅在一个类型有多个事件，但预计不会订阅大多数事件时有用。

[!code-csharp[csProgGuideEvents#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEvents/CS/Events.cs#9)]

此实现符合 C# 语言规范中的[添加和删除委托](~/_csharplang/spec/delegates.md#delegate-invocation)行为。

请注意，[lock](../../language-reference/keywords/lock-statement.md) 语句仅用于通过事件处理程序访问字典。 不要在 `lock` 语句的主体内调用事件处理程序，因为它可能会导致死锁或锁争用。

## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [事件](../../../csharp/programming-guide/events/index.md)
- [委托](../../../csharp/programming-guide/delegates/index.md)
