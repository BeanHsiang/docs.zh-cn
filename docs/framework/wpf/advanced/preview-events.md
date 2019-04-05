---
title: 预览事件
ms.date: 03/30/2017
helpviewer_keywords:
- Preview events [WPF]
- suppressing events [WPF]
- events [WPF], Preview
- events [WPF], suppressing
ms.assetid: b5032308-aa9c-4d02-af11-630ecec8df7e
ms.openlocfilehash: 95514cfce88764d92d690fb9c0a51c667a49683b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356333"
---
# <a name="preview-events"></a>预览事件
预览事件，也称为隧道事件，也是路由的路由的事件，在应用程序根元素引发该事件并报告为事件数据中的源间传递的方向。 并非所有事件方案支持或要求预览事件;本主题介绍的情况下，预览事件存在，应用程序或组件应如何处理它们和在其中创建自定义组件或类中的预览事件可能是适当的情况。  
  
## <a name="preview-events-and-input"></a>预览事件和输入  
 在处理事件一般情况下，则应注意的预览版时将事件标记在事件中处理数据。 而不处理任何元素上的预览事件引发它 （将被报告为中的事件数据源的元素） 的元素具有不提供机会处理产生的事件元素的效果。 有时这是所需的结果，尤其是在控件的该组合中的关系中存在所涉及的元素。  
  
 输入事件的具体来说，预览事件也共享事件数据实例与等效的浮升事件。 如果使用预览事件类处理程序将处理该输入的事件标记，将不会调用浮升输入的事件的类处理程序。 或者，如果使用预览事件实例处理程序将处理该事件标记，浮升事件的处理程序将不通常会调用。 类处理程序或实例处理程序可以注册或附加要调用即使事件被标记为已处理，但该技术不常使用的选项。  
  
 有关类处理并将它与预览事件的详细信息请参阅[路由事件标记为已处理，和类处理](marking-routed-events-as-handled-and-class-handling.md)。  
  
### <a name="working-around-event-suppression-by-controls"></a>通过控件解决事件禁止问题  
 通常用于预览事件的一个方案是，对于复合控件的输入事件的处理。 有时，控件作者禁止显示中的某些事件可能是为了替换上携带更多信息或者指示更具体的行为的组件定义事件源自其控件。 例如， [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.Button>取消<xref:System.Windows.UIElement.MouseLeftButtonDown>和<xref:System.Windows.UIElement.MouseRightButtonDown>引发浮升事件<xref:System.Windows.Controls.Button>或复合元素上的，以便支持捕获鼠标并引发<xref:System.Windows.Controls.Primitives.ButtonBase.Click>始终由引发的事件<xref:System.Windows.Controls.Button>本身。 事件和其数据仍继续沿路由，但由于<xref:System.Windows.Controls.Button>将标记作为事件数据<xref:System.Windows.RoutedEventArgs.Handled%2A>，仅用于明确指定它们应在处理该事件的处理程序`handledEventsToo`调用用例。  如果其他元素指向你的应用程序的根目录仍想要处理控件取消事件的机会，一种替代方法是将在代码中使用的处理程序附加`handledEventsToo`指定为`true`。 但通常更简单方法是更改处理输入事件的预览等效路由方向。 例如，如果一个控件，将禁止<xref:System.Windows.UIElement.MouseLeftButtonDown>，请尝试将附加的处理程序<xref:System.Windows.UIElement.PreviewMouseLeftButtonDown>改为。 此方法仅适用于基元素输入事件如<xref:System.Windows.UIElement.MouseLeftButtonDown>。 这些输入的事件使用隧道/冒泡对、 引发两个事件，并共享事件数据。  
  
 上述每种方法有负面影响或限制。 处理预览事件的副作用是在该点处理该事件可能会禁用为能够处理浮升事件的处理程序，并因此的限制是，它通常是不标记为已处理仍在使用 Previ 时一个好办法新路由的一部分。 限制`handledEventsToo`种方法是，不能指定`handledEventsToo`处理程序中的[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]作为属性，你必须注册事件处理程序代码中获取对该元素的对象引用，该处理程序附加后。  
  
## <a name="see-also"></a>请参阅
- [将路由事件标记为“已处理”和“类处理”](marking-routed-events-as-handled-and-class-handling.md)
- [路由事件概述](routed-events-overview.md)
