---
title: 嵌套类型
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- types, nested
- public nested types
- type design guidelines, nested types
- nested types
- members [.NET Framework], type
- class library design guidelines [.NET Framework], nested types
ms.assetid: 12feb7f0-b793-4d96-b090-42d6473bab8c
author: KrzysztofCwalina
ms.openlocfilehash: 22c14d05105154ff642cb8a44eda8e7c5d0575e4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54559536"
---
# <a name="nested-types"></a>嵌套类型
嵌套的类型是另一种类型，称为封闭类型的范围内定义的类型。 嵌套的类型有权访问其封闭类型的所有成员。 例如，它有权访问在封闭类型和受保护的封闭类型的所有祖先中定义的字段定义的私有字段。  
  
 一般情况下，应谨慎使用嵌套的类型。 其原因有若干： 一些开发人员不完全熟悉这一概念。 这些开发人员，例如，可能与声明的嵌套类型的变量的语法问题。 嵌套的类型与其封闭类型时，还非常紧密耦合，并且这种情况下为通用类型不适合。  
  
 嵌套的类型是最适合用于建模的其封闭类型的实现详细信息。 最终用户应几乎不需要声明嵌套类型的变量和几乎永远不能进行显式实例化嵌套的类型。 例如，集合的枚举器可以为该集合的嵌套的类型。 枚举器通常通过其封闭类型实例化，因为许多语言都支持 foreach 语句，枚举器变量几乎不需要最终用户声明。  
  
 **✓ 务必** 使用嵌套的类型，从而使成员可访问性语义都需要的嵌套的类型和其外部类型之间的关系时。  
  
 **X 切忌** 使用公共嵌套的类型作为自己的逻辑分组构造; 为此使用命名空间。  
  
 **X 避免** 公共公开嵌套的类型。 唯一的例外是嵌套类型的变量需要声明仅在极少数情况下，如生成子类或其他高级自定义方案。  
  
 **X 切忌** 使用嵌套的类型，如果类型为可能包含类型的外部引用。  
  
 例如，传递给方法的类上定义的枚举应未定义为类中的嵌套类型。  
  
 **X 切忌** 使用嵌套的类型，如果他们需要通过客户端代码来实例化。  如果类型具有公共构造函数，它可能不应进行嵌套。  
  
 如果可以实例化一个类型，这种方法似乎以指示该类型具有上其自己的框架中的位置 （你可以创建它，使用它，和销毁而完全不必使用外部类型），并因此不应嵌套。 不应内部类型广泛重用之外没有任何关系的外部类型都为外部类型。  
  
 **X 切忌** 定义为接口成员的嵌套的类型。 许多语言不支持此类构造。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [类型设计准则](../../../docs/standard/design-guidelines/type.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
