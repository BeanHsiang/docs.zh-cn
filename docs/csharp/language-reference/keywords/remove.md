---
title: remove 上下文关键字 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- remove_CSharpKeyword
helpviewer_keywords:
- remove event accessor [C#]
ms.assetid: c8223426-c17b-4fe2-8406-01564cf1dd2b
ms.openlocfilehash: fc6f310e17841349d476f35214ac17100e81d76f
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53236721"
---
# <a name="remove-c-reference"></a>remove（C# 参考）

`remove` 上下文关键字用于定义自定义事件访问器，当客户端代码订阅你的[事件](event.md)时将调用该访问器。 如果提供自定义 `remove` 访问器，还必须提供 [add](add.md) 访问器。

## <a name="example"></a>示例

以下示例显示具有自定义 [add](add.md) 和 `remove` 访问器的事件。 有关完整示例，请参阅[操作说明：实现接口事件](../../programming-guide/events/how-to-implement-interface-events.md)。

 [!code-csharp[csrefKeywordsContextual#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsContextual/CS/csrefKeywordsContextual.cs#15)]

通常不需要提供自己的自定义事件访问器。 大多数情况下，使用声明事件时由编译器自动生成的访问器就足够了。

## <a name="see-also"></a>请参阅

- [事件](../../programming-guide/events/index.md)