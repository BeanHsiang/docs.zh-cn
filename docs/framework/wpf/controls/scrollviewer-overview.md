---
title: ScrollViewer 概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [WPF], ScrollViewer
- ScrollViewer control [WPF], about ScrollViewer control
ms.assetid: 94a13b94-cfdf-4b12-a1aa-90cb50c6e9b9
ms.openlocfilehash: 2685be197d6b47cf174c5fbd062bd3c37a19f5eb
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356905"
---
# <a name="scrollviewer-overview"></a>ScrollViewer 概述
用户界面中的内容通常比计算机屏幕的显示区域大。 <xref:System.Windows.Controls.ScrollViewer>控件提供了方便地启用中的内容滚动[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]应用程序。 本主题介绍<xref:System.Windows.Controls.ScrollViewer>元素，并提供了几个用法示例。  
  
<a name="what_is_a_scrollviewer_element"></a>   
## <a name="the-scrollviewer-control"></a>ScrollViewer 控件  
 有两个预定义的元素启用滚动[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序：<xref:System.Windows.Controls.Primitives.ScrollBar>和<xref:System.Windows.Controls.ScrollViewer>。 <xref:System.Windows.Controls.ScrollViewer>控件封装水平滚动条和垂直<xref:System.Windows.Controls.Primitives.ScrollBar>元素和内容的容器 (如<xref:System.Windows.Controls.Panel>元素) 以便在可滚动区域中显示其他可见元素。 若要使用必须生成自定义对象<xref:System.Windows.Controls.Primitives.ScrollBar>元素实现内容滚动。 但是，可以使用<xref:System.Windows.Controls.ScrollViewer>元素本身，因为它是一个复合控件封装<xref:System.Windows.Controls.Primitives.ScrollBar>功能。  
  
 <xref:System.Windows.Controls.ScrollViewer>控件响应鼠标和键盘命令，并定义用于按预设的增量滚动内容的许多方法。 可以使用<xref:System.Windows.Controls.ScrollViewer.ScrollChanged>事件来检测更改<xref:System.Windows.Controls.ScrollViewer>状态。  
  
 一个<xref:System.Windows.Controls.ScrollViewer>只能有一个子级，通常<xref:System.Windows.Controls.Panel>元素，可承载<xref:System.Windows.Controls.Panel.Children%2A>元素的集合。 <xref:System.Windows.Controls.ContentPresenter.Content%2A>属性定义的唯一子级<xref:System.Windows.Controls.ScrollViewer>。  
  
<a name="scrollviewer_physical_vs_logical"></a>   
## <a name="physical-vs-logical-scrolling"></a>物理滚动与逻辑滚动  
 物理滚动用于按预设的物理增量（通常按以像素为单位声明的值）滚动内容。 逻辑滚动用于滚动到逻辑树中的下一项。 物理滚动是大多数的默认滚动行为<xref:System.Windows.Controls.Panel>元素。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 同时支持这两种类型的滚动。  
  
#### <a name="the-iscrollinfo-interface"></a>IScrollInfo 接口  
 <xref:System.Windows.Controls.Primitives.IScrollInfo>接口表示的主滚动区域内<xref:System.Windows.Controls.ScrollViewer>或派生的控件。 该接口定义的滚动属性和方法，可由实现<xref:System.Windows.Controls.Panel>需要按逻辑单元，而不按物理增量滚动元素。 实例转换<xref:System.Windows.Controls.Primitives.IScrollInfo>到派生<xref:System.Windows.Controls.Panel>，然后使用其滚动方法提供了一种滚动到下一个逻辑单位子集合，而不是按像素增量有效方式。 默认情况下，<xref:System.Windows.Controls.ScrollViewer>控件支持按物理单位滚动。  
  
 <xref:System.Windows.Controls.StackPanel> 并<xref:System.Windows.Controls.VirtualizingStackPanel>都可实现<xref:System.Windows.Controls.Primitives.IScrollInfo>和本身支持逻辑滚动。 对于布局控件，本身支持逻辑滚动，您仍可以完成通过包装主机物理滚动<xref:System.Windows.Controls.Panel>中的元素<xref:System.Windows.Controls.ScrollViewer>并设置<xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A>属性设置为`false`。  
  
 下面的代码示例演示如何强制转换的实例<xref:System.Windows.Controls.Primitives.IScrollInfo>到<xref:System.Windows.Controls.StackPanel>，并使用内容滚动方法 (<xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A>和<xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A>) 的接口定义。  
  
 [!code-csharp[IScrollInfoMethods#3](~/samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
<a name="scrollviewer_markup_syntax_and_sample"></a>   
## <a name="defining-and-using-a-scrollviewer-element"></a>定义和使用 ScrollViewer 元素  
 下面的示例创建<xref:System.Windows.Controls.ScrollViewer>包含一些文本和一个矩形的窗口中。 <xref:System.Windows.Controls.Primitives.ScrollBar> 元素出现仅当它们是必需的。 当调整窗口大小时<xref:System.Windows.Controls.Primitives.ScrollBar>元素将出现然后消失的值已更新由于<xref:System.Windows.Controls.ScrollViewer.ComputedHorizontalScrollBarVisibility%2A>和<xref:System.Windows.Controls.ScrollViewer.ComputedVerticalScrollBarVisibility%2A>属性。  
  
 [!code-cpp[ScrollViewer#1](~/samples/snippets/cpp/VS_Snippets_Wpf/ScrollViewer/CPP/ScrollViewer_wcp.cpp#1)]
 [!code-csharp[ScrollViewer#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewer/CSharp/ScrollViewer_wcp.cs#1)]
 [!code-vb[ScrollViewer#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewer/VisualBasic/ScrollViewer.vb#1)]
 [!code-xaml[ScrollViewer#1](~/samples/snippets/xaml/VS_Snippets_Wpf/ScrollViewer/XAML/Pane1.xaml#1)]  
  
<a name="scrollviewer_styling_scrollviewer"></a>   
## <a name="styling-a-scrollviewer"></a>设置 ScrollViewer 的样式  
 Windows Presentation foundation 中的所有控件都一样<xref:System.Windows.Controls.ScrollViewer>可以设置要更改默认呈现行为的控件的样式。 有关控件样式设置的其他信息，请参阅[样式设置和模板化](styling-and-templating.md)。  
  
<a name="scrollviewer_scroll_vs_paginate"></a>   
## <a name="paginating-documents"></a>对文档进行分页  
 对于文档内容，一种替代滚动的方法是选择支持分页的文档容器。 <xref:System.Windows.Documents.FlowDocument> 对于旨在中查看控件，如托管的文档是<xref:System.Windows.Controls.FlowDocumentPageViewer>，内容分页支持跨多个页面，从而无需进行滚动。 <xref:System.Windows.Controls.DocumentViewer> 提供一种解决方案，用于查看<xref:System.Windows.Documents.FixedDocument>的内容，它使用传统的滚动来显示超出显示区域的领域。  
  
 有关文档格式和演示选项的其他信息，请参阅 [WPF 中的文档](../advanced/documents-in-wpf.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.Primitives.ScrollBar>
- <xref:System.Windows.Controls.Primitives.IScrollInfo>
- [如何：创建滚动查看器](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752352(v=vs.90))
- [WPF 中的文档](../advanced/documents-in-wpf.md)
- [ScrollBar 样式和模板](scrollbar-styles-and-templates.md)
- [控件](../advanced/optimizing-performance-controls.md)
