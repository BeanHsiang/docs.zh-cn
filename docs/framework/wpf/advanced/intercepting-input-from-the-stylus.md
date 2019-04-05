---
title: 截获触笔输入
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 'architecture [WPF], '
- ', '
- ', '
- ', '
ms.assetid: 791bb2f0-4e5c-4569-ac3c-211996808d44
ms.openlocfilehash: 0568e72e6d686ce08e6bd802f273e45dd623524b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374305"
---
# <a name="intercepting-input-from-the-stylus"></a>截获触笔输入
<xref:System.Windows.Input.StylusPlugIns>体系结构提供了用于通过实现低级别控制的机制<xref:System.Windows.Input.Stylus>输入和数字墨迹创建<xref:System.Windows.Ink.Stroke>对象。 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>类提供了一种机制，以实现自定义行为，并将其应用到从触笔设备以获得最佳性能的数据的流。  
  
 本主题包含以下小节：  
  
-   [体系结构](#Architecture)  
  
-   [实现触笔插件](#ImplementingStylusPlugins)  
  
-   [将插件添加到 InkCanvas](#AddingYourPluginToAnInkCanvas)  
  
-   [结束语](#Conclusion)  
  
<a name="Architecture"></a>   
## <a name="architecture"></a>体系结构  
 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>的演进[StylusInput](https://go.microsoft.com/fwlink/?LinkId=50753&clcid=0x409)中所述的 Api[访问和操作笔输入](https://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)中[Microsoft Windows XP Tablet PC Edition 软件Kit 1.7](https://go.microsoft.com/fwlink/?linkid=11782&clcid=0x409)。  
  
 每个<xref:System.Windows.UIElement>已<xref:System.Windows.UIElement.StylusPlugIns%2A>是属性<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>。 您可以添加<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>的元素<xref:System.Windows.UIElement.StylusPlugIns%2A>属性来操作<xref:System.Windows.Input.StylusPoint>生成作为它的数据。 <xref:System.Windows.Input.StylusPoint> 数据包含的所有系统数字化器，包括支持的属性<xref:System.Windows.Input.StylusPoint.X%2A>并<xref:System.Windows.Input.StylusPoint.Y%2A>点数据，以及<xref:System.Windows.Input.StylusPoint.PressureFactor%2A>数据。  
  
 你<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>对象插入到流中的数据来自直接<xref:System.Windows.Input.Stylus>设备添加时<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>到<xref:System.Windows.UIElement.StylusPlugIns%2A>属性。 管理单元添加到中的顺序<xref:System.Windows.UIElement.StylusPlugIns%2A>集合的顺序指定将收到<xref:System.Windows.Input.StylusPoint>数据。 例如，如果您添加筛选器插件，将输入限制为特定的区域，以及如何将写入时识别的笔势的插件，识别的笔势插件将接收已筛选<xref:System.Windows.Input.StylusPoint>数据。  
  
<a name="ImplementingStylusPlugins"></a>   
## <a name="implementing-stylus-plug-ins"></a>实现触笔插件  
 若要将插件实现，派生的类从<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>。 此类是应用的 o 数据的流，因为它来自<xref:System.Windows.Input.Stylus>。 在此类可以通过修改的值<xref:System.Windows.Input.StylusPoint>数据。  
  
> [!CAUTION]
>  如果<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>引发或导致异常，应用程序将关闭。 您应该全面测试使用的控件<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>并且只使用一个控件，如果您确信<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>不会引发异常。  
  
 下面的示例演示一个插件，通过修改限制触笔输入<xref:System.Windows.Input.StylusPoint.X%2A>并<xref:System.Windows.Input.StylusPoint.Y%2A>中的值<xref:System.Windows.Input.StylusPoint>作为它的数据来自<xref:System.Windows.Input.Stylus>设备。  
  
 [!code-csharp[AdvancedInkTopicsSamples#19](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#19)]
 [!code-vb[AdvancedInkTopicsSamples#19](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#19)]  
[!code-csharp[AdvancedInkTopicsSamples#3](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/DynamicRenderer.cs#3)]
[!code-vb[AdvancedInkTopicsSamples#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AdvancedInkTopicsSamples/VisualBasic/DynamicRenderer.vb#3)]  
  
<a name="AddingYourPluginToAnInkCanvas"></a>   
## <a name="adding-your-plug-in-to-an-inkcanvas"></a>将插件添加到 InkCanvas  
 若要使用自定义插件的最简单方法是实现从 InkCanvas 派生而来的类并将其添加到<xref:System.Windows.UIElement.StylusPlugIns%2A>属性。  
  
 下面的示例演示自定义<xref:System.Windows.Controls.InkCanvas>对墨迹进行筛选。  
  
 [!code-csharp[AdvancedInkTopicsSamples#4](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#4)]  
  
 如果添加`FilterInkCanvas`到应用程序并运行它，你会注意到在用户完成一个笔画后手写内容并不局限于之前的区域。 这是因为<xref:System.Windows.Controls.InkCanvas>已<xref:System.Windows.Controls.InkCanvas.DynamicRenderer%2A>属性，即<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>已经是成员的和<xref:System.Windows.UIElement.StylusPlugIns%2A>集合。 自定义<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>你添加到<xref:System.Windows.UIElement.StylusPlugIns%2A>集合接收<xref:System.Windows.Input.StylusPoint>之后，数据<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>接收数据。 因此，<xref:System.Windows.Input.StylusPoint>数据在用户抬起笔结束笔画后不会直到筛选。 若要筛选用户将其绘制手写内容，必须插入`FilterPlugin`之前<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>。  
  
 下面的 C# 代码演示一个自定义<xref:System.Windows.Controls.InkCanvas>是绘制筛选手写内容。  
  
 [!code-csharp[AdvancedInkTopicsSamples#5](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/Window1.xaml.cs#5)]  
  
<a name="Conclusion"></a>   
## <a name="conclusion"></a>结束语  
 通过派生您自己<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>类并将它们到插入<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>集合，可以极大地提高你数字墨迹的行为。 你有权<xref:System.Windows.Input.StylusPoint>生成数据时，您可以自定义<xref:System.Windows.Input.Stylus>输入。 因为此类低级别访问<xref:System.Windows.Input.StylusPoint>数据，可以为你的应用程序实现墨迹收集和呈现具有优化性能。  
  
## <a name="see-also"></a>请参阅
- [高级墨迹处理](advanced-ink-handling.md)
- [访问和操作笔输入](https://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)
