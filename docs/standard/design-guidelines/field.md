---
title: 字段设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- fields, design guidelines
- read-only fields
- member design guidelines, fields
ms.assetid: 7cb4b0f3-7a10-4c93-b84d-733f7134fcf8
author: KrzysztofCwalina
ms.openlocfilehash: 3ab8fe279605c4795bb3a26557d0241b186b273a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54690444"
---
# <a name="field-design"></a>字段设计
封装原则是面向对象的设计中最重要的概念之一。 该原则规定，存储在对象内的数据只能由该对象访问。  
  
 解释该原则的一种有效的方式是，设计一种可在不破坏类型成员以外的代码的情况下对类型的字段（名称或类型更改）进行更改的类型。 这种解释随即表明所有字段必须为专用。  
  
 我们将常量和静态只读字段排除在了这一严格限制之外，因为根据定义，此类字段几乎从不需要更改。  
  
 X 请勿提供公共或受保护的实例字段。  
  
 应提供用于访问字段而非使其成为公共或受保护字段的属性。  
  
 **✓ 务必** 使用常量字段表示永不改变的常量。  
  
 编译器将 const 字段的值直接烧写到调用代码中。 因此，在没有破坏兼容性的风险的情况下，永远不能更改const值。  
  
 **✓ 务必** 对预定义的对象实例使用公共的静态的 `readonly` 字段。  
  
 如果存在该类型的预定义实例，则将它们声明为该类型本身的公共只读静态字段。  
  
 **X 切忌** 将可变类型的实例分配给 `readonly` 字段。  
  
 可变类型是具有可在实例化后修改的实例的类型。 例如，数组，大多数集合和流都是可变类型，但是 <xref:System.Int32?displayProperty=nameWithType>、<xref:System.Uri?displayProperty=nameWithType>、和 <xref:System.String?displayProperty=nameWithType> 都是不变的。 引用类型字段上的只读修饰符可防止存储在字段中的实例被替换，但它不会阻止通过调用更改实例的员来修改字段的实例数据。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [成员设计准则](../../../docs/standard/design-guidelines/member.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
