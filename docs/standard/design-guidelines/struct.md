---
title: 结构设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], structures
- deallocating structures
- allocating structures
- value types, structures
- structure design
- type design guidelines, structures
- structures [.NET Framework], design guidelines
ms.assetid: 1f48b2d8-608c-4be6-9ba4-d8f203ed9f9f
author: KrzysztofCwalina
ms.openlocfilehash: cc5b8d7effda31b0236477b217bccf5cf2137f8c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54646602"
---
# <a name="struct-design"></a>结构设计
常规用途的值类型通常称为结构，其 C# 关键字。 本部分提供有关常规结构设计指导原则。  
  
 **X 切忌**为结构提供默认构造函数。  
  
 遵循此原则将允许创建结构数组，而无需对数组的每个项运行构造函数。 请注意，C# 不允许结构具有默认构造函数。  
  
 **X 切忌**定义可变值类型。  
  
 可变值类型有几个问题。 例如，当属性 getter 返回值类型时，调用者会收到一个副本。 由于该副本是隐式创建的，因此开发人员可能不会意识到他们正在改变副本，而不是原始值。 此外，某些语言（尤其是动态语言）在使用可变值类型时会遇到问题，因为即使局部变量在解除引用时也会导致生成副本。  
  
 **✓ 务必**确保所有实例数据设置为零、false 或 null（视情况而定）的状态是有效的。  
  
 这可以防止在创建结构数组时意外创建无效实例。  
  
 **✓ 务必**为值类型实现 <xref:System.IEquatable%601>。  
  
 值类型的 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 方法会导致装箱，并且其默认实现效率不高，因为它使用反射。 <xref:System.IEquatable%601.Equals%2A> 可以有更好的性能，并且可以进行实现，这样它就不会导致装箱。  
  
 X 请勿显式扩展 <xref:System.ValueType>。 实际上，大多数语言禁止此行为。  
  
 一般情况下，结构可能非常有用，但应仅用于不经常装箱的单个不可变的小值。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [类型设计准则](../../../docs/standard/design-guidelines/type.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [在类和结构之间选择](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)
