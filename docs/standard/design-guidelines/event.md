---
title: 事件设计
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- pre-events
- events [.NET Framework], design guidelines
- member design guidelines, events
- event handlers [.NET Framework], event design guidelines
- post-events
- signatures, event handling
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
author: KrzysztofCwalina
ms.openlocfilehash: 530c68ea5342263acd07f8dc8a8c8ce889652503
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54632018"
---
# <a name="event-design"></a>事件设计
事件是最常用的回叫（允许框架调用用户代码的结构）。 其他回叫机制包括接受委托的成员、虚拟成员和基于接口的插件。来自可用性研究的数据表明，相比使用其他回叫机制，大多数开发人员更习惯使用事件。 事件能与 Visual Studio 和许多语言很好地集成。  
  
 值得注意的是，有两组事件：在系统状态发生变化之前引发的事件，称为事前事件，以及状态更改后引发的事件，称为事后事件。 事前事件的一个例子是 `Form.Closing`，它是在窗体关闭之前引发的。 事后事件的一个例子是 `Form.Closed`，它是在窗体关闭后引发的。  
  
 **✓ 务必** 对事件使用术语 “raise” 而不是 “fire” 或 “trigger”。  
  
 **✓ 务必** 使用<xref:System.EventHandler%601?displayProperty=nameWithType>而不是手动创建新的委托以用作事件处理程序。  
  
 **✓ 考虑** 使用 <xref:System.EventArgs> 的子类作为事件参数，除非您完全确定事件永远不需要将任何数据传递给事件处理方法，在这种情况下您可以直接使用 `EventArgs` 类型。  
  
 如果直接使用 `EventArgs` 发布API，您将永远无法在不破坏兼容性的情况下添加任何要随事件携带的数据。 如果使用子类，即使最初完全为空，也可以在需要时向子类添加属性。  
  
 **✓ 务必** 使用受保护的虚拟方法来引发每个事件。 这仅适用于非密封类的非静态事件，而不适用于结构、密封类或静态事件。  
  
 该方法的目的是为派生类提供一种使用重写来处理事件的方法。 重写是一种更灵活、更快、更自然的方式来处理派生类中的基类事件。 按照惯例，方法的名称应以 “On” 开头，并跟随事件的名称。  
  
 派生类可以选择在其重写中不调用方法的基本实现。 要做到这点，需要在方法中不包括使基类正常工作所需的任何处理过程。  
  
 **✓ 务必** 为引发事件的受保护方法采用一个参数。  
  
 该参数应命名为 `e`，其类型应为事件参数类。  
  
 **X 切忌** 在引发非静态事件时传递 null 值作为 sender。  
  
 **✓ 务必** 在引发静态事件时传递 null 值作为 sender。  
  
 **X 切忌** 在引发事件时传递 null 值作为事件数据参数。  
  
 如果不想将任何数据传递给事件处理方法，则应传递 `EventArgs.Empty`。 开发人员希望此参数不为 null。  
  
 **✓ 考虑** 引发最终用户可以取消的事件。 这仅适用于事前事件。  
  
 使用 <xref:System.ComponentModel.CancelEventArgs?displayProperty=nameWithType> 或其子类作为事件参数，以允许最终用户取消事件。  
  
### <a name="custom-event-handler-design"></a>自定义事件处理程序设计  
 某些情况下不能使用 `EventHandler<T>`，例如当框架需要使用早期版本的 CLR（不支持泛型）时。 在这种情况下，可能需要设计和开发自定义事件处理程序委托。  
  
 **✓ DO** 对于事件处理程序使用返回类型为 void。  
  
 事件处理程序可以调用多个事件处理方法，可能在多个对象上。 如果允许事件处理方法返回一个值，则会为每个事件调用多个返回值。  
  
 **✓ DO** 使用`object`作为事件处理程序的第一个参数的类型和调用它`sender`。  
  
 **✓ 务必** 使用 <xref:System.EventArgs?displayProperty=nameWithType> 作为事件处理程序的第一个参数的类型，并将其命名为`e`。  
  
 **X DO NOT** 对事件处理程序的两个以上参数。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [成员设计准则](../../../docs/standard/design-guidelines/member.md)
- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
