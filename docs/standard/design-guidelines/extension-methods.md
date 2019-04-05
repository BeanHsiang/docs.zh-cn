---
title: 扩展方法
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: 5de945cb-88f4-49d7-b0e6-f098300cf357
author: KrzysztofCwalina
ms.openlocfilehash: bd5f67c3bd766625e7c22b3ca9986cfbca8854bf
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54621755"
---
# <a name="extension-methods"></a>扩展方法
扩展方法是一种语言特性，允许使用实例方法调用语法来调用静态方法。 这些方法必须至少使用一个参数，该参数表示方法要操作的实例。  
  
 定义此类扩展方法的类称“sponsor”类，必须将其声明为静态。 要使用扩展方法，必须导入定义 sponsor 类的命名空间。  
  
 **X 避免** 轻率定义扩展方法，尤其是在你不拥有的类型上。  
  
 如果拥有某一类型的源代码，请考虑使用常规实例方法。 如果没有，并且想要添加方法，请务必小心。 随意使用扩展方法可能会使本来不具备这些方法的类型产生混乱的API。  
  
 **✓ 考虑**在以下任何一种情况下使用扩展方法：  
  
-   提供与接口的每个实现相关的辅助功能（如果上述功能可以根据核心接口编写）。 这是因为不能将具体实现分配给接口。 例如，`LINQ to Objects` 运算符作为所有 <xref:System.Collections.Generic.IEnumerable%601> 类型的扩展方法被实现。 因此，任何 `IEnumerable<>` 实现都会自动启用LINQ。  
  
-   当实例方法在某种类型上引入依赖关系，但这样的依赖关系会破坏依赖关系管理规则的时候。 例如，从 <xref:System.String> 到 <xref:System.Uri?displayProperty=nameWithType> 的依赖关系可能是不可取的，因此返回 `System.Uri` 的 `String.ToUri()` 实例方法从依赖关系管理的角度来看可能存在设计错误。 返回 `System.Uri` 的静态扩展方法 `Uri.ToUri(this string str)` 可能是更好的设计。  
  
 **X 避免**在 <xref:System.Object?displayProperty=nameWithType> 上定义扩展方法。  
  
 VB 用户将无法使用扩展方法语法在对象引用上调用此类方法。 VB 不支持调用这样的方法，因为在 VB 中，将引用声明为 Object 会强制对方法的所有方法调用进行延迟绑定（在运行时确定调用的实际成员），而在编译时确定对扩展方法的绑定（早期绑定）。  
  
 请注意，该准则适用于存在相同绑定行为的其他语言，或者不支持扩展方法的其他语言。  
  
 **X 切忌**将扩展方法放在与扩展类型相同的命名空间中，除非它用于向接口添加方法或用于依赖关系管理。  
  
 **X 避免**定义两个或多个具有相同签名的扩展方法，即使它们位于不同的命空间中。  
  
 **✓ 考虑**在与扩展类型相同的命名空间中定义扩展方法，前提是该类型是接口并且打算在大多数或所有情况下使用该扩展方法。  
  
 **X 请勿**定义在通常与其他功能相关联的命名空间中实现功能的扩展方法。 而是在与它们所属的功能相关联的命名空间中定义它们。  
  
 **X 避免**对专用于扩展方法的命名空间进行通用命名（例如，“扩展”）。 而是使用描述性名称（例如，“路由”）。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [成员设计准则](../../../docs/standard/design-guidelines/member.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
