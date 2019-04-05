---
title: 事件和回调
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], extensibility
- methods [.NET Framework], callback
- callback methods
- callbacks
ms.assetid: 48b55c60-495f-4089-9396-97f9122bba7c
author: KrzysztofCwalina
ms.openlocfilehash: 3609d6ac4847cb081740fd698869df4976f83f8f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54525477"
---
# <a name="events-and-callbacks"></a>事件和回调
回调允许框架通过委托回调用户代码来实现可扩展性。 这些委托通常通过方法的参数传递给框架。  
  
 事件是回调的一种特殊情况，它支持通过便捷且一致的语法来提供委托（事件处理程序）。 此外，可以借助 Visual Studio 的语句完成和设计器功能来使用基于事件的 API。 (请参阅[事件设计](../../../docs/standard/design-guidelines/event.md)。)  
  
 **✓ 考虑** 使用回调来允许用户提供框架要执行的自定义代码。  
  
 **✓ 考虑** 使用事件允许用户自定义框架的行为，而无需理解面向对象的设计。  
  
 **✓ 务必** 更愿意使用事件而纯回调，因为它们是广泛的开发人员更熟悉，与 Visual Studio 语句完成集成。  
  
 **X 避免** 性能敏感的 Api 中使用回调。  
  
 **✓ 务必** 使用新`Func<...>`， `Action<...>`，或`Expression<...>`而不是定义回调的 Api 时的自定义委托的类型。  
  
 `Func<...>` 和`Action<...>`表示泛型委托。 `Expression<...>` 表示函数定义，可以编译并随后还调用在运行时，但可进行序列化和传递到远程进程。  
  
 **✓ 务必** 测量和了解使用性能影响的`Expression<...>`，而不是使用`Func<...>`和`Action<...>`委托。  
  
 `Expression<...>` 类型是在逻辑上等同于大多数情况下`Func<...>`和`Action<...>`委托。 主要区别是，委托应将用于的本地进程方案;表达式适用于的情况下十分有益和无法计算表达式中的远程进程或计算机。  
  
 **✓ 务必** 了解，通过调用委托，正在执行任意代码，且无法具有安全、 正确性和兼容性影响。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
