---
title: 墨迹线程处理模型
ms.date: 03/30/2017
helpviewer_keywords:
- application user interface thread [WPF]
- stylus plug-in
- ink threading model [WPF]
- ink [WPF], rendering
- pen thread [WPF]
- threading model [WPF]
- rendering ink [WPF]
- dynamic rendering thread [WPF]
- ink collection plug-in
- plug-ins [WPF], for ink
ms.assetid: c85fcad1-cb50-4431-847c-ac4145a35c89
ms.openlocfilehash: 8089c857d2406f8cfb357ba2efe188ad84605541
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377020"
---
# <a name="the-ink-threading-model"></a>墨迹线程处理模型
Tablet PC 上的优势之一是墨迹的，它极为相似书写一样使用普通的笔和纸。  若要实现此目的，触笔收集输入的数据以高得多的速度比鼠标将手写内容呈现为用户写入。  应用程序的用户界面 (UI) 线程是不够的笔数据和呈现墨迹收集，因为它可能被阻止。  若要解决此问题，问题[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序使用两个其他线程，当用户将墨迹。  
  
 以下列表描述了在收集和呈现数字墨迹了相应的线程：  
  
-   笔线程的触笔输入的线程。  （实际上，这是一个线程池，但本主题会将其称为笔线程。）  
  
-   应用程序用户界面线程的线程，用于控制应用程序的用户界面。  
  
-   动态呈现线程的线程呈现墨迹时用户绘制笔划。 动态呈现线程是不同于呈现的应用程序，其他 UI 元素的线程窗口 Presentation Foundation 中所述[线程模型](threading-model.md)。  
  
 墨迹模型都是相同的应用程序使用是否<xref:System.Windows.Controls.InkCanvas>或自定义控件中的一个类似[创建墨迹输入控件](creating-an-ink-input-control.md)。  尽管本主题讨论了线程处理的<xref:System.Windows.Controls.InkCanvas>，在创建自定义控件时应用相同的概念。  
  
## <a name="threading-overview"></a>线程处理概述  
 下图说明了线程模型，当用户绘制笔划时：  
  
 ![绘制笔画时的线程处理模型。](./media/inkthreading-drawingink.png "InkThreading_DrawingInk")  
  
1.  用户绘制笔划时发生的操作  
  
    1.  当用户绘制笔划时，触笔接触点在笔线程上。  在触笔插件，包括<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>，接受在笔线程上的触笔接触点，并有机会修改之前已对其<xref:System.Windows.Controls.InkCanvas>接收它们。  
  
    2.  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>呈现动态呈现线程上的触笔接触点。 发生这种情况在同时作为在上一步。  
  
    3.  <xref:System.Windows.Controls.InkCanvas>接收在 UI 线程上的触笔接触点。  
  
2.  用户结束笔画后发生的操作  
  
    1.  在用户完成绘制笔画<xref:System.Windows.Controls.InkCanvas>创建<xref:System.Windows.Ink.Stroke>对象，并将其添加到<xref:System.Windows.Controls.InkPresenter>，它将以静态方式呈现它。  
  
    2.  UI 线程通知<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>静态呈现笔划，因此<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>删除笔画其可视表示形式。  
  
## <a name="ink-collection-and-stylus-plug-ins"></a>墨迹收集和触笔插件  
 每个<xref:System.Windows.UIElement>具有<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>。  <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>中的对象<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>接收，并可以修改在笔线程上的触笔接触点。 <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>对象接收根据其在顺序触笔接触点<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>。  
  
 下图演示了一个假想的场景其中<xref:System.Windows.UIElement.StylusPlugIns%2A>的集合<xref:System.Windows.UIElement>包含`stylusPlugin1`即<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>，和`stylusPlugin2`按顺序。  
  
 ![在触笔插件的顺序会影响输出。](./media/inkthreading-pluginorder.png "InkThreading_PluginOrder")  
  
 在上图中，以下行为会发生：  
  
1.  `StylusPlugin1` 修改的 x 值和 y。  
  
2.  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> 接收已修改的触笔接触点，并将它们呈现在动态呈现线程。  
  
3.  `StylusPlugin2` 接收已修改的触笔接触点，并进一步修改的 x 值和 y。  
  
4.  应用程序收集触笔接触点，并在用户完成笔画，以静态方式呈现笔划。  
  
 假设`stylusPlugin1`限制对矩形的触笔接触点和`stylusPlugin2`转换到右侧触笔接触点。  在前面的方案，<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>收到受限制的触笔点，但是不翻译后的触笔接触点。  时用户绘制笔划，笔划的呈现的矩形的边界内，但不会对笔画用户提起笔之前转换。  
  
### <a name="performing-operations-with-a-stylus-plug-in-on-the-ui-thread"></a>使用触笔插件在 UI 线程上执行操作  
 由于不能在笔线程上执行准确的命中测试，因此某些元素可能会偶尔收到适用于其他元素的触笔输入。 如果你需要确保输入已正确路由正在执行的操作之前，订阅并执行中的操作<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusDownProcessed%2A>， <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusMoveProcessed%2A>，或<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn.OnStylusUpProcessed%2A>方法。 在执行准确的命中测试后，应用程序线程将调用这些方法。 若要订阅对这些方法，调用<xref:System.Windows.Input.StylusPlugIns.RawStylusInput.NotifyWhenProcessed%2A>在笔线程发生的方法中的方法。  
  
 下图说明了在笔线程和 UI 线程方面的触笔事件之间的关系<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>。  
  
 ![墨迹线程模型&#40;UI 和 Pen&#41;](./media/inkthreading-plugincallbacks.png "InkThreading_PluginCallbacks")  
  
## <a name="rendering-ink"></a>呈现墨迹  
 用户绘制笔划，如<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>呈现单独的线程上的墨迹，因此墨迹看上去"流"从笔即使 UI 线程正忙。  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>动态呈现线程上生成可视化树，因为它收集触笔接触点。  在用户完成描边，<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>要求应用程序执行下一次呈现时收到通知。  应用程序完成下一次呈现的之后,<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>清理其可视化树。  下图说明了此过程。  
  
 ![墨迹线程处理示意图](./media/inkthreading-visualtree.png "InkThreading_VisualTree")  
  
1.  用户开始笔画。  
  
    1.  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>创建可视化树。  
  
2.  用户绘制笔划。  
  
    1.  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>构建可视化树。  
  
3.  用户结束笔画。  
  
    1.  <xref:System.Windows.Controls.InkPresenter>笔画添加到其可视化树。  
  
    2.  媒体集成层 (MIL) 以静态方式呈现笔划。  
  
    3.  <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>清理视觉对象。
