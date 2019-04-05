---
title: 抽象类设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, abstract classes
- abstract classes, design guidelines
- class library design guidelines [.NET Framework], classes
- classes [.NET Framework], abstract
- classes [.NET Framework], design guidelines
- type design guidelines, classes
ms.assetid: d3646e6d-5c1f-4922-8fb0-ec5effb30d60
author: KrzysztofCwalina
ms.openlocfilehash: 6eec3bb4575b89c6476e6c3410050c705141777f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54550405"
---
# <a name="abstract-class-design"></a>抽象类设计
**X** 请勿在抽象类型中定义公共或受保护的内部构造函数。  
  
 只有在用户需要创建该类型的实例时，构造函数才应该是公共构造函数。
 由于无法创建抽象类型的实例，因此带有公共构造函数的抽象类型设计不正确，会误导用户。  
  
 **✓** 请在抽象类中定义受保护的或内部构造函数  
  
 受保护的构造函数更常见，并且只允许基类在创建子类型时自行初始化。  
  
 内部构造函数可用于将抽象类的具体实现限制为定义该类的程序集。  
  
 **✓** 请提供至少一种继承自你交付的每个抽象类的具体类型。  
  
 这些措施有助于验证抽象类的设计。 例如，<xref:System.IO.FileStream?displayProperty=nameWithType> 是 <xref:System.IO.Stream?displayProperty=nameWithType> 抽象类的实现。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [类型设计准则](../../../docs/standard/design-guidelines/type.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
