---
title: 优化性能：其他建议
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Terminal Services rendering [WPF]
- opacity [WPF]
- hit-test objects [WPF]
- ScrollBarVisibility enumeration [WPF]
- brushes [WPF], performance
ms.assetid: d028cc65-7e97-4a4f-9859-929734eaf40d
ms.openlocfilehash: 05fe4ba4e2125b01637bc9066d23b5738d81f98d
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57358933"
---
# <a name="optimizing-performance-other-recommendations"></a>优化性能：其他建议
<a name="introduction"></a>本主题提供[优化 WPF 应用程序性能](optimizing-wpf-application-performance.md)这一节中各主题内容之外的性能改进建议。  
  
 本主题包含以下各节：  
  
-   [画笔的不透明度与元素的不透明度](#Opacity)  
  
-   [导航到对象](#Navigation_Objects)  
  
-   [对大型 3D 图面进行命中测试](#Hit_Testing)  
  
-   [CompositionTarget.Rendering 事件](#CompositionTarget_Rendering_Event)  
  
-   [避免使用 ScrollBarVisibility=Auto](#Avoid_Using_ScrollBarVisibility)  
  
-   [配置字体缓存服务以缩短启动时间](#FontCache)  
  
<a name="Opacity"></a>   
## <a name="opacity-on-brushes-versus-opacity-on-elements"></a>画笔的不透明度与元素的不透明度  
 当你使用<xref:System.Windows.Media.Brush>若要设置<xref:System.Windows.Shapes.Shape.Fill%2A>或<xref:System.Windows.Shapes.Shape.Stroke%2A>的元素，则最好设置<xref:System.Windows.Media.Brush.Opacity%2A?displayProperty=nameWithType>值比设置元素的<xref:System.Windows.UIElement.Opacity%2A>属性。 修改元素的<xref:System.Windows.UIElement.Opacity%2A>属性可能会导致[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]创建临时图面。  
  
<a name="Navigation_Objects"></a>   
## <a name="navigation-to-object"></a>导航到对象  
 <xref:System.Windows.Navigation.NavigationWindow>对象派生<xref:System.Windows.Window>并将其扩展并用内容导航支持，主要是通过聚合<xref:System.Windows.Navigation.NavigationService>和日志。 您可以更新的工作区<xref:System.Windows.Navigation.NavigationWindow>通过指定[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]或对象。 以下示例演示了这两种方法：  
  
 [!code-csharp[Performance#PerformanceSnippet14](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/TestNavigation.xaml.cs#performancesnippet14)]
 [!code-vb[Performance#PerformanceSnippet14](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/testnavigation.xaml.vb#performancesnippet14)]  
  
 每个<xref:System.Windows.Navigation.NavigationWindow>对象都有一个日志记录在该窗口中的用户的导航历史记录。 日志的作用之一是允许用户回溯他们执行的步骤。  
  
 使用 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 导航时，日志只存储[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 引用。 这意味着，每次重新访问该页时都会动态地重新构造该页，根据页面的复杂程度，此过程可能会非常耗时。 在这种情况下，虽然占用的日志存储较少，但用于重建该页的时间可能会较长。  
  
 使用对象进行导航时，日志会存储对象的整个可视化树。 这意味着，每次重新访问该页时，无需重新构造即可立即呈现该页。 在这种情况下，虽然占用的日志存储较多，但重建页面所用的时间较短。  
  
 当你使用<xref:System.Windows.Navigation.NavigationWindow>对象，将需要记住日志支持是如何影响应用程序的性能。 有关详细信息，请参阅[导航概述](../app-development/navigation-overview.md)。  
  
<a name="Hit_Testing"></a>   
## <a name="hit-testing-on-large-3d-surfaces"></a>对大型 3D 图面进行命中测试  
 就 CPU 消耗而言，对大型 3D 图面进行命中测试是一项非常占用资源的操作。 3D 图面显示动画效果时更是如此。 如果不需要对这些图面进行命中测试，请禁用命中测试。 派生自的对象<xref:System.Windows.UIElement>可以禁用命中测试通过设置<xref:System.Windows.UIElement.IsHitTestVisible%2A>属性设置为`false`。  
  
<a name="CompositionTarget_Rendering_Event"></a>   
## <a name="compositiontargetrendering-event"></a>CompositionTarget.Rendering 事件  
 <xref:System.Windows.Media.CompositionTarget.Rendering?displayProperty=nameWithType>事件会导致[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]连续显示动画效果。 使用此事件时，应尽可能将其分离。  
  
<a name="Avoid_Using_ScrollBarVisibility"></a>   
## <a name="avoid-using-scrollbarvisibilityauto"></a>避免使用 ScrollBarVisibility=Auto  
 只要有可能，避免使用<xref:System.Windows.Controls.ScrollBarVisibility.Auto?displayProperty=nameWithType>值`HorizontalScrollBarVisibility`和`VerticalScrollBarVisibility`属性。 这些属性定义为<xref:System.Windows.Controls.RichTextBox>， <xref:System.Windows.Controls.ScrollViewer>，并<xref:System.Windows.Controls.TextBox>对象，并作为附加属性的<xref:System.Windows.Controls.ListBox>对象。 与此相反，设置<xref:System.Windows.Controls.ScrollBarVisibility>到<xref:System.Windows.Controls.ScrollBarVisibility.Disabled>， <xref:System.Windows.Controls.ScrollBarVisibility.Hidden>，或<xref:System.Windows.Controls.ScrollBarVisibility.Visible>。  
  
 <xref:System.Windows.Controls.ScrollBarVisibility.Auto>空间有限制，并在必要时，应仅显示滚动条时，将值适用于用例。 例如，可能会使用此选项很有用<xref:System.Windows.Controls.ScrollBarVisibility>具有值<xref:System.Windows.Controls.ListBox>30 个项目而不是<xref:System.Windows.Controls.TextBox>与具有数百行文本。  
  
<a name="FontCache"></a>   
## <a name="configure-font-cache-service-to-reduce-start-up-time"></a>配置字体缓存服务以缩短启动时间  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 字体缓存服务会在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序之间共享字体数据。 如果该服务尚未运行，则首个运行的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序将启动此服务。 如果使用的[!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)]，可以设置从"手动"（默认值）"Windows Presentation Foundation (WPF) 字体缓存 3.0.0.0"服务为"自动 （延迟启动）"，以减少的初始启动时间[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]应用程序。  
  
## <a name="see-also"></a>请参阅
- [规划应用程序性能](planning-for-application-performance.md)
- [利用硬件](optimizing-performance-taking-advantage-of-hardware.md)
- [布局和示例](optimizing-performance-layout-and-design.md)
- [2D 图形和图像处理](optimizing-performance-2d-graphics-and-imaging.md)
- [对象行为](optimizing-performance-object-behavior.md)
- [应用程序资源](optimizing-performance-application-resources.md)
- [文本](optimizing-performance-text.md)
- [数据绑定](optimizing-performance-data-binding.md)
- [动画提示和技巧](../graphics-multimedia/animation-tips-and-tricks.md)
