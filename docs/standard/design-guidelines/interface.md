---
title: 接口设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- interfaces [.NET Framework], design guidelines
- type design guidelines, interfaces
- class library design guidelines [.NET Framework], interfaces
ms.assetid: a016bd18-6710-4358-9438-9f190a295392
author: KrzysztofCwalina
ms.openlocfilehash: 1f982aa37f92b7270725574d949989ca120297d5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54660136"
---
# <a name="interface-design"></a>接口设计
虽然大多数 API 最好使用类和结构进行建模，但有些情况下接口更合适或是唯一的选择。  
  
 CLR 不支持多重继承（即，CLR 类不能从多个基类继承），但它允许类型除了继承基类之外还实现一个或多个接口。 因此，通常使用接口来实现多重继承的效果。 例如，<xref:System.IDisposable>是一个接口，允许类型支持可释放性，而不依赖于他们想要参与的任何其他继承层次结构。  
  
 适合定义接口的另一种情况是创建一个可以由多种类型支持的公共接口，包括一些值类型。 值类型不能继承 <xref:System.ValueType> 之外的其他类型，但是它们可以实现接口，因此使用接口是提供公共基类型的唯一选择。  
  
 **✓ 务必**定义一个接口，如果需要某些通用 API 受到包含值类型的一组类型的支持。  
  
 **✓ 考虑**定义一个接口，如果需要在已继承自其他类型的类型上支持其功能。  
  
 **X 避免**使用标记接口（不包含任何成员的接口）。  
  
 如果需要将类标记为具有特定特征（标记），通常使用自定义特性而不是接口。  
  
 **✓ 务必**至少提供一种作为接口的实现的类型。  
  
 此做法有助于验证接口的设计。 例如，<xref:System.Collections.Generic.List%601> 是 <xref:System.Collections.Generic.IList%601> 接口的实现。  
  
 **✓ 务必**为你定义的每个接口提供至少一个使用它的 API（将接口作为类型化为接口的参数或属性的方法）。  
  
 此做法有助于验证接口设计。 例如，<xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> 使用 <xref:System.Collections.Generic.IComparer%601?displayProperty=nameWithType> 接口。  
  
 **X 切忌**将成员添加到之前发布的接口中。  
  
 这样做会破坏接口的实现。 应创建一个新接口以避免版本控制问题。  
  
 除了这些指南中描述的情况之外，一般情况下，应该在设计托管代码的可重用库时选择类而不是接口。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [类型设计准则](../../../docs/standard/design-guidelines/type.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
