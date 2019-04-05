---
title: 用于实现抽象的基类
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- abstractions [.NET Framework]
- base classes, abstractions
ms.assetid: 37a2d9a4-9721-482a-a40f-eee2c1d97875
author: KrzysztofCwalina
ms.openlocfilehash: 6811423258481fcbae24743c9b17f3f20c379c58
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54565808"
---
# <a name="base-classes-for-implementing-abstractions"></a>用于实现抽象的基类
严格地说，当一个类派生出另一个类时，它就成了一个基类。 但是，在本部分中，基类是一个主要用于提供公共抽象的类，或者是供其他类通过继承重用某些默认实现的类。 基类通常位于继承层次结构的中间位置，位于根部的层次结构抽象和末端的一些自定义实现之间。  
  
 它们可以为实现抽象提供帮助。 例如，框架中有序项集合的抽象之一是 <xref:System.Collections.Generic.IList%601> 接口。 实现 <xref:System.Collections.Generic.IList%601> 并不简单，因此框架提供了几个基类，例如 <xref:System.Collections.ObjectModel.Collection%601> 和 <xref:System.Collections.ObjectModel.KeyedCollection%602>，来为实现自定义集合提供帮助。  
  
 基类通常不适合作为抽象本身，因为它们往往包含太多的实现。 例如，`Collection<T>` 基类包含许多实现，这些实现与一些实际情况有关，即它实现了非泛型的 `IList` 接口（目的是更好地与非泛型集合集成），并且它是存储在某个字段的内存中的项的集合。  
  
 如前所述，基类可以为需要实现抽象的用户提供宝贵的帮助，但同时它们可能是一个重大的不利因素。 它们增加了继承层次结构的广度和深度，因此在概念上使框架更加复杂。 因此，只有在为框架用户提供巨大价值的时候才应使用基类。 如果它们仅对框架的实现者有用，则应该避免使用它们，在这种情况下，应该考虑委托到内部实现而不是从基类继承。  
  
 **✓ 考虑** 使基类抽象，即使它们不包含任何抽象成员。 这会清楚地告知用户该类根据设计只能用于继承。  
  
 **✓ 考虑** 将基类放在与主线场景类型不同的命名空间中。 根据定义，基类用于高级可扩展性场景，因此对大多数用户来说并没有意义。  
  
 **X AVOID** 命名为"基本"后缀的基类，如果类旨在用于在公共 Api 中使用。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
