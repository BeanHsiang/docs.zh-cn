---
title: 成员重载
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- default arguments
- members [.NET Framework], overloaded
- member design guidelines [.NET Framework], overloading
- overloaded members
- signatures, members
ms.assetid: 964ba19e-8b94-4b5b-b1e3-5a0b531a0bb1
author: KrzysztofCwalina
ms.openlocfilehash: b13f9e1551aec7e53ba1ac2ed0b9049d46b0a756
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54636646"
---
# <a name="member-overloading"></a>成员重载
成员重载意味着创建两个或多个成员上的相同类型的区别只体现在数量或类型参数，但具有相同的名称。 例如，在以下内容，`WriteLine`重载方法：  
  
```  
public static class Console {  
    public void WriteLine();  
    public void WriteLine(string value);  
    public void WriteLine(bool value);  
    ...  
}  
```  
  
 方法、 构造函数和索引的属性可以具有参数，因为只有这些成员可以进行重载。  
  
 重载是用于提高可用性、 生产力和可重用库的可读性最重要的技术之一。 重载的参数数量，使可能提供更简单的构造函数和方法的版本。 重载参数类型，使得可以使用相同的成员执行相同操作在所选的一组不同类型的成员名称。  
  
 **✓ 务必** 尝试使用描述性的参数名称以指示较短的重载使用的默认值。  
  
 **X 避免** 随意更改重载中的参数名称。 如果某一重载中的参数表示相同的输入中的另一个重载的参数，参数应具有相同的名称。  
  
 **X 避免** 在排序中的参数中不一致状态重载成员。 具有相同名称的参数应出现在相同位置中所有重载。  
  
 **✓ 务必** 使只有最长的重载成为虚方法 （如果可扩展性是必需的）。 只需较短的重载应调用通过到较长的重载。  
  
 **X 切忌** 使用`ref`或`out`修饰符来重载成员。  
  
 某些语言无法解析对此类重载的调用。 此外，此类重载通常具有完全不同的语义，可能不应重载，但两个单独的方法相反。  
  
 **X 切忌** 具有重载随着在相同的位置以及相似类型的参数，而使用不同的语义。  
  
 **✓ 务必** 允许`null`要为可选自变量传递。  
  
 **✓ 务必** 使用重载，而不是定义具有默认自变量的成员的成员。  
  
 默认自变量不符合 CLS。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [成员设计准则](../../../docs/standard/design-guidelines/member.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
