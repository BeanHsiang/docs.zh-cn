---
title: 密封
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- limiting extensibility
- classes [.NET Framework], sealing
- preventing customization
- sealed classes
ms.assetid: cc42267f-bb7a-427a-845e-df97408528d4
author: KrzysztofCwalina
ms.openlocfilehash: c8aeb5ce3d93755f30bf68732592a08d7af54957
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54646654"
---
# <a name="sealing"></a>密封
面向对象的框架的一个特性是开发人员可以以框架设计者未曾预料到的方式扩展和定制它们。 这是可扩展设计的强大和危险之处。 因此，在设计框架时，必须根据需要仔细设计可扩展性并在不安全的情况下对其进行限制。  
  
 防止可扩展性的强大机制是密封。 可以密封类或单个成员。 密封类会阻止用户继承该类。 密封成员可阻止用户重写特定成员。  
  
 **X 切忌** 在没有充分理由的情况下密封类。  
  
 因为无法预料到可扩展性场景而密封一个类并不是一个充分的理由。 框架用户喜欢因各种非显而易见的原因继承类，比如添加一些便利的成员。 有关用户希望从类型进行继承的非显而易见的原因的示例，请参阅[未密封类](../../../docs/standard/design-guidelines/unsealed-classes.md)。  
  
 对类进行密封的充足理由包括：  
  
-   该类是一个静态类。 请参阅[静态类设计](../../../docs/standard/design-guidelines/static-class.md)。  
  
-   该类在继承的受保护成员中存储了对安全敏感的机密。  
  
-   该类继承了许多虚拟成员，单独密封它们的成本将超过使该类未密封的益处。  
  
-   该类是一个需要极快速运行时查找的属性。 密封属性的性能水平略高于未密封的属性。 请参阅[属性](../../../docs/standard/design-guidelines/attributes.md)。  
  
 **X 切忌** 在密封类型上声明受保护成员或虚拟成员。  
  
 根据定义，不能从密封类型继承。 这意味着无法调用密封类型上的受保护成员，并且无法重写密封类型上的虚拟方法。  
  
 **✓ 考虑** 密封重写的成员。  
  
 引入虚拟成员可能导致的问题（在[虚拟成员](../../../docs/standard/design-guidelines/virtual-members.md)中讨论）也适用于重写，尽管程度较低。 密封重写可以防止这些继承层次结构中的问题。  
  
 *部分版权 © 2005，2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
- [未密封类](../../../docs/standard/design-guidelines/unsealed-classes.md)
