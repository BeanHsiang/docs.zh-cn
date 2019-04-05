---
title: ToolTip 概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolTip control [WPF], about ToolTip control
- controls [WPF], ToolTip
ms.assetid: f06c1603-e9cb-4809-8a62-234607fc52f7
ms.openlocfilehash: 745ac23d65248302940eed6db3b8b19748dfc00d
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57376320"
---
# <a name="tooltip-overview"></a>ToolTip 概述
工具提示，则用户将鼠标指针悬停在元素，通过上时，将显示一个小型弹出窗口<xref:System.Windows.Controls.Button>。 本主题介绍工具提示，并讨论如何创建和自定义工具提示内容。  
  
 
  
<a name="what_is_a_tooltip"></a>   
## <a name="what-is-a-tooltip"></a>什么是工具提示？  
 当用户将鼠标指针移动到具有工具提示的元素上时，将在一段指定的时间内显示一个包含工具提示内容（例如，介绍控件功能的文本内容）的窗口。 如果用户将鼠标指针从控件上移开，该窗口将消失，因为工具提示内容无法接收焦点。  
  
 工具提示的内容可以包含一行或多行文本、图像、形状或其他可视内容。 通过将以下属性之一设置为工具提示内容来定义控件的工具提示。  
  
-   <xref:System.Windows.FrameworkContentElement.ToolTip%2A?displayProperty=nameWithType>  
  
-   <xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=nameWithType>  
  
 所使用的属性取决于是否定义了工具提示控件继承自<xref:System.Windows.FrameworkContentElement>或<xref:System.Windows.FrameworkElement>类。  
  
<a name="create_tooltip"></a>   
## <a name="creating-a-tooltip"></a>创建工具提示  
 下面的示例演示如何通过设置创建简单的工具提示<xref:System.Windows.FrameworkElement.ToolTip%2A>属性<xref:System.Windows.Controls.Button>为文本字符串的控件。  
  
 [!code-xaml[GroupBoxSnippet#ToolTipString](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipstring)]  
  
 您还可以定义为工具提示<xref:System.Windows.Controls.ToolTip>对象。 下面的示例使用[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]来指定<xref:System.Windows.Controls.ToolTip>对象的工具提示<xref:System.Windows.Controls.TextBox>元素。 请注意，该示例指定<xref:System.Windows.Controls.ToolTip>通过设置<xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=nameWithType>属性。  
  
 [!code-xaml[ToolTipSimple#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#tooltip)]  
  
 以下示例使用代码来生成<xref:System.Windows.Controls.ToolTip>对象。 此示例将创建<xref:System.Windows.Controls.ToolTip>(`tt`) 并将其与<xref:System.Windows.Controls.Button>。  
  
 [!code-csharp[ToolTipSimple#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ToolTipSimple#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipSimple/VisualBasic/Window1.xaml.vb#2)]  
  
 此外可以创建未定义为工具提示内容<xref:System.Windows.Controls.ToolTip>括起的工具提示内容的布局元素，如对象<xref:System.Windows.Controls.DockPanel>。 下面的示例演示如何设置<xref:System.Windows.FrameworkElement.ToolTip%2A>的属性<xref:System.Windows.Controls.TextBox>括在内容<xref:System.Windows.Controls.DockPanel>控件。  
  
 [!code-xaml[GroupBoxSnippet#ToolTipDockPanel](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipdockpanel)]  
  
<a name="Using_the_ToolTip_and_ToolTipService_Properties"></a>   
## <a name="using-the-properties-of-the-tooltip-and-tooltipservice-classes"></a>使用 ToolTipd 和 ToolTipService 类的属性  
 可以通过设置视觉属性和应用样式来自定义工具提示内容。 如果定义的工具提示内容作为<xref:System.Windows.Controls.ToolTip>对象，可以设置的视觉属性<xref:System.Windows.Controls.ToolTip>对象。 否则，必须上设置等效的附加的属性<xref:System.Windows.Controls.ToolTipService>类。  
  
 有关如何设置属性，以便使用指定的工具提示内容位置的示例<xref:System.Windows.Controls.ToolTip>并<xref:System.Windows.Controls.ToolTipService>属性，请参阅[定位 ToolTip](how-to-position-a-tooltip.md)。  
  
<a name="StylingToolTip"></a>   
## <a name="styling-a-tooltip"></a>设置工具提示样式  
 你可以设置样式<xref:System.Windows.Controls.ToolTip>通过定义一个自定义<xref:System.Windows.Style>。 下面的示例定义<xref:System.Windows.Style>称为`Simple`，演示如何偏移量的位置<xref:System.Windows.Controls.ToolTip>并通过设置更改其外观<xref:System.Windows.Controls.Control.Background%2A>， <xref:System.Windows.Controls.Control.Foreground%2A>， <xref:System.Windows.Controls.Control.FontSize%2A>，和<xref:System.Windows.Controls.Control.FontWeight%2A>。  
  
 [!code-xaml[ToolTipSimple#Style](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#style)]  
  
<a name="UsingtheToolTipServiceTimeIntervalProperties"></a>   
## <a name="using-the-time-interval-properties-of-tooltipservice"></a>使用 ToolTipService 的 Time Interval 属性  
 <xref:System.Windows.Controls.ToolTipService>类提供了以下属性用于设置工具提示显示时间： <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A>， <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A>，和<xref:System.Windows.Controls.ToolTipService.ShowDuration%2A>。  
  
 使用<xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A>并<xref:System.Windows.Controls.ToolTipService.ShowDuration%2A>属性指定的延迟通常很短，之前<xref:System.Windows.Controls.ToolTip>将显示，还指定的时间<xref:System.Windows.Controls.ToolTip>保持可见。 有关详细信息，请参阅[如何：延迟的工具提示显示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms747264(v=vs.90))。  
  
 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A>属性确定了快速移动时鼠标指针它们之间不同控件的工具提示是否显示没有初始延迟。 有关详细信息<xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A>属性，请参阅[使用 BetweenShowDelay 属性](how-to-use-the-betweenshowdelay-property.md)。  
  
 以下示例演示如何为工具提示设置这些属性。  
  
 [!code-xaml[ToolTipService#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.ToolTipService>
- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipEventArgs>
- <xref:System.Windows.Controls.ToolTipEventHandler>
- [帮助主题](tooltip-how-to-topics.md)
