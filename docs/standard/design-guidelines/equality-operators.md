---
title: 相等运算符
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], Equals method
- class library design guidelines [.NET Framework], equality operator
- equality operator (==) [.NET Framework]
- Equals method
- == operator (equality) [.NET Framework]
ms.assetid: bc496a91-fefb-4ce0-ab4c-61f09964119a
author: KrzysztofCwalina
ms.openlocfilehash: ef1a0aff1ac59434d9d9a6f0371bf236f637050e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54572677"
---
# <a name="equality-operators"></a>相等运算符
本部分讨论了重载相等运算符并将 `operator==` 和 `operator!=` 引用为相等运算符。  
  
 **X 请勿**重载这两个相等运算符的任意一个。  
  
 **✓ 请确**保 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 和相等运算符具有完全相同的语义和类似的性能特性。  
  
 这通常意味着，在重载相等运算符时需要替代 `Object.Equals`。  
  
 **X 避免**从等式运算符中引发异常。  
  
 例如，如果其中一个参数为 null，则返回 false，而不是引发 `NullReferenceException`。  
  
## <a name="equality-operators-on-value-types"></a>值类型的等式运算符  
 **✓ 如果**等式有意义，请对值类型重载等式运算符。  
  
 在大多数编程语言中，值类型没有 `operator==` 的默认实现。  
  
## <a name="equality-operators-on-reference-types"></a>引用类型的等式运算符  
 **X 避免**对可变引用类型重载等式运算符。  
  
 许多语言都具有针对引用类型的内置等式运算符。 内置运算符通常实现引用等式，当默认行更改为值等式时，许多开发人员都会感到惊讶。  
  
 对于不可变的引用类型来说，此问题可得到缓解，因为不可变性使得引用等式和值等式之间的区别更难以被注意到。  
  
 **X 如果**实现速度明显慢于引用等式，请避免对引用类型重载等式运算符。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [使用准则](../../../docs/standard/design-guidelines/usage-guidelines.md)
