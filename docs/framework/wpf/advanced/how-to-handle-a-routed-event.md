---
title: 如何：处理路由事件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- routed events [WPF], handling
- bubbling events [WPF]
ms.assetid: 157787b4-f469-4047-8777-5b034145f32e
ms.openlocfilehash: 42f5f247e775fbf0bd323fc693a74d6149c87bb3
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368189"
---
# <a name="how-to-handle-a-routed-event"></a>如何：处理路由事件
本示例演示了浮升事件的工作原理，以及如何编写可处理路由事件数据的处理程序。  
  
## <a name="example"></a>示例  
 在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中，元素以元素树结构形式排列。 父元素可以参与处理最初由元素树中的子元素引发的事件。 这都是因为事件路由。  
  
 路由事件通常遵循以下两个路由策略之一：浮升和隧道。 此示例重点介绍浮升事件，并使用<xref:System.Windows.Controls.Primitives.ButtonBase.Click?displayProperty=nameWithType>事件可显示路由的工作原理。  
  
 下面的示例创建两个<xref:System.Windows.Controls.Button>控制，并使用[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]特性语法将事件处理程序附加到公用父元素，它在此示例中为<xref:System.Windows.Controls.StackPanel>。 而不是将单个事件处理程序附加每个<xref:System.Windows.Controls.Button>子元素，该示例使用特性语法将附加到的事件处理程序<xref:System.Windows.Controls.StackPanel>父元素。 此事件处理模式展示了如何使用事件路由技术来减少附加处理程序的元素数。 每个的所有浮升事件<xref:System.Windows.Controls.Button>通过父元素路由。  
  
 请注意，在父<xref:System.Windows.Controls.StackPanel>元素中，<xref:System.Windows.Controls.Primitives.ButtonBase.Click>指定为该属性进行部分限定的命名的事件名称<xref:System.Windows.Controls.Button>类。 <xref:System.Windows.Controls.Button>类是<xref:System.Windows.Controls.Primitives.ButtonBase>派生的类具有<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件在其成员列表中的。 如果要处理的事件不在附加路由事件处理程序的元素的成员列表中，则有必要使用这种部分限定技术来附加事件处理程序。  
  
 [!code-xaml[RoutedEventHandle#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml#xaml)]  
  
 下面的示例处理<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件。  该示例会报告哪个元素处理事件以及哪个元素引发事件。 用户单击任一按钮时都将执行事件处理程序。  
  
 [!code-csharp[RoutedEventHandle#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventHandle#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventHandle/VisualBasic/MainWindow.xaml.vb#handler)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.RoutedEvent>
- [输入概述](input-overview.md)
- [路由事件概述](routed-events-overview.md)
- [帮助主题](events-how-to-topics.md)
- [XAML 语法详述](xaml-syntax-in-detail.md)
