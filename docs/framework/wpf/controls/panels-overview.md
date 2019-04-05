---
title: 面板概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Panel control [WPF], about Panel control
- controls [WPF], Panel
ms.assetid: f73644af-9941-4611-8754-6d4cef03fc44
ms.openlocfilehash: 2648296d01f0e237847fc16535b01dbd8e9c5b62
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377086"
---
# <a name="panels-overview"></a>面板概述
<xref:System.Windows.Controls.Panel> 元素是控制呈现元素的组件，其大小和维度，其位置和子内容的排列方式。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供了许多预定义<xref:System.Windows.Controls.Panel>元素，以及构造自定义的功能<xref:System.Windows.Controls.Panel>元素。  
  
 本主题包含以下各节：  
  
-   [Panel 类](#Panels_view_from_10000_feet)  
  
-   [Panel 元素公共成员](#Panels_declared_members)  
  
-   [派生 Panel 元素](#Panels_derived_elements)  
  
-   [用户界面 Panel](#Panels_main_UI_elements)  
  
-   [嵌套 Panel 元素](#Panels_nested_panel_elements)  
  
-   [自定义 Panel 元素](#Panels_custom_panel_elements)  
  
-   [本地化/全球化支持](#Panels_global_localization)  
  
<a name="Panels_view_from_10000_feet"></a>   
## <a name="the-panel-class"></a>Panel 类  
 <xref:System.Windows.Controls.Panel> 是类的基类，用于支持中的所有元素提供布局[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]。 派生<xref:System.Windows.Controls.Panel>元素用于放置和排列中的元素[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]和代码。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包含一套全面的派生面板实现，可支持许多复杂的布局。 这些派生类公开可实现大部分标准 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 方案的属性和方法。 开发人员找不到满足其需求的子排列行为可以通过重写创建新的布局<xref:System.Windows.FrameworkElement.ArrangeOverride%2A>和<xref:System.Windows.FrameworkElement.MeasureOverride%2A>方法。 有关自定义布局行为的详细信息，请参阅[自定义 Panel 元素](#Panels_custom_panel_elements)。  
  
<a name="Panels_declared_members"></a>   
## <a name="panel-common-members"></a>Panel 公共成员  
 所有<xref:System.Windows.Controls.Panel>元素支持大小和位置定义的属性的基<xref:System.Windows.FrameworkElement>，其中包括<xref:System.Windows.FrameworkElement.Height%2A>， <xref:System.Windows.FrameworkElement.Width%2A>， <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>， <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>， <xref:System.Windows.FrameworkElement.Margin%2A>，和<xref:System.Windows.FrameworkElement.LayoutTransform%2A>。 有关定义的位置属性的更多信息<xref:System.Windows.FrameworkElement>，请参阅[Alignment、 Margin 和 Padding 概述](../advanced/alignment-margins-and-padding-overview.md)。  
  
 <xref:System.Windows.Controls.Panel> 公开至关重要的一点是了解和使用布局中的其他的属性。 <xref:System.Windows.Controls.Panel.Background%2A>属性用于填充派生的面板元素使用的边界之间的区域<xref:System.Windows.Media.Brush>。 <xref:System.Windows.Controls.Panel.Children%2A> 表示元素的子集合的<xref:System.Windows.Controls.Panel>组成。 <xref:System.Windows.Controls.Panel.InternalChildren%2A> 表示内容的<xref:System.Windows.Controls.Panel.Children%2A>集合以及通过数据绑定生成的成员。 同时组成<xref:System.Windows.Controls.UIElementCollection>承载父项中的子元素<xref:System.Windows.Controls.Panel>。  
  
 面板还公开<xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType>附加属性可用于实现在派生的分层的顺序<xref:System.Windows.Controls.Panel>。 面板的成员<xref:System.Windows.Controls.Panel.Children%2A>集合具有较高<xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType>值显示在具有较低<xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType>值。 这是特别适合面板如<xref:System.Windows.Controls.Canvas>和<xref:System.Windows.Controls.Grid>这使子级共享相同的坐标空间。  
  
 <xref:System.Windows.Controls.Panel> 此外定义了<xref:System.Windows.Controls.Panel.OnRender%2A>方法，可用于重写的默认呈现行为的<xref:System.Windows.Controls.Panel>。  
  
#### <a name="attached-properties"></a>附加属性  
 派生面板元素广泛使用附加属性。 附加属性是没有常规 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性“包装器”的依赖属性的特殊化形式。 附加属性在 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中具有特殊化的语法，可在后面的几个示例中看到。  
  
 附加属性的一个用途是允许子元素存储实际上由父元素定义的属性的唯一值。 此功能的一项应用是让子元素通知父级它们希望如何在 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中呈现，这对应用程序布局非常有用。 有关详细信息，请参阅[附加属性概述](../advanced/attached-properties-overview.md)。  
  
<a name="Panels_derived_elements"></a>   
## <a name="derived-panel-elements"></a>派生 Panel 元素  
 许多对象派生<xref:System.Windows.Controls.Panel>，但不是所有这些旨在使用作为根布局提供程序。 有六个定义的面板类 (<xref:System.Windows.Controls.Canvas>， <xref:System.Windows.Controls.DockPanel>， <xref:System.Windows.Controls.Grid>， <xref:System.Windows.Controls.StackPanel>， <xref:System.Windows.Controls.VirtualizingStackPanel>，并且<xref:System.Windows.Controls.WrapPanel>)，专为创建应用程序[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 每个面板元素都封装自己的特殊功能，如下表所示。  
  
|元素名称|是否为 UI 面板？|描述|  
|------------------|---------------|-----------------|  
|<xref:System.Windows.Controls.Canvas>|是|定义一个区域，在其中可以显式定位子元素的坐标相对于<xref:System.Windows.Controls.Canvas>区域。|  
|<xref:System.Windows.Controls.DockPanel>|是|定义一个区域，可在其中使子元素相互水平或垂直排列。|  
|<xref:System.Windows.Controls.Grid>|是|定义一个由列和行组成的灵活网格区域。 子元素<xref:System.Windows.Controls.Grid>可以精确地使用定位<xref:System.Windows.FrameworkElement.Margin%2A>属性。|  
|<xref:System.Windows.Controls.StackPanel>|是|将子元素排列成水平或垂直的一行。|  
|<xref:System.Windows.Controls.Primitives.TabPanel>|否|处理中的选项卡按钮的布局<xref:System.Windows.Controls.TabControl>。|  
|<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|否|排列中的内容<xref:System.Windows.Controls.ToolBar>控件。|  
|<xref:System.Windows.Controls.Primitives.UniformGrid>|否|<xref:System.Windows.Controls.Primitives.UniformGrid> 用于与所有相等的单元格大小排列在网格中的子级。|  
|<xref:System.Windows.Controls.VirtualizingPanel>|否|为可以“虚拟化”其子级集合的面板提供基类。|  
|<xref:System.Windows.Controls.VirtualizingStackPanel>|是|在水平或垂直方向上将内容排列为一行并使其虚拟化。|  
|<xref:System.Windows.Controls.WrapPanel>|是|<xref:System.Windows.Controls.WrapPanel> 从顺序位置定位子元素的从左到右，将内容切换到下一行上包含框的边缘。 后续排序按照按顺序从上到下还是从右到左，具体取决于值<xref:System.Windows.Controls.WrapPanel.Orientation%2A>属性。|  
  
<a name="Panels_main_UI_elements"></a>   
## <a name="user-interface-panels"></a>用户界面 Panel  
 中提供了六个面板类[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]进行了优化以支持[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]方案： <xref:System.Windows.Controls.Canvas>， <xref:System.Windows.Controls.DockPanel>， <xref:System.Windows.Controls.Grid>， <xref:System.Windows.Controls.StackPanel>， <xref:System.Windows.Controls.VirtualizingStackPanel>，和<xref:System.Windows.Controls.WrapPanel>。 这些面板元素易于使用、功能齐全并且可扩展，足以适用于大多数应用程序。  
  
 每个派生<xref:System.Windows.Controls.Panel>元素以不同方式处理大小调整约束。 了解如何<xref:System.Windows.Controls.Panel>中水平或垂直方向的句柄约束可以使布局更可预测。  
  
|**Panel 名称**|**x 维度**|**y 维度**|  
|--------------------|----------------------|----------------------|  
|<xref:System.Windows.Controls.Canvas>|按内容约束|按内容约束|  
|<xref:System.Windows.Controls.DockPanel>|约束|约束|  
|<xref:System.Windows.Controls.StackPanel> （垂直方向）|约束|按内容约束|  
|<xref:System.Windows.Controls.StackPanel> （水平方向）|按内容约束|约束|  
|<xref:System.Windows.Controls.Grid>|约束|在情况下的约束，除非其中<xref:System.Windows.GridUnitType.Auto>适用于行和列|  
|<xref:System.Windows.Controls.WrapPanel>|按内容约束|按内容约束|  
  
 可在下方找到其中每种元素的更多详细说明和使用示例。  
  
<a name="Panels_overview_Canvas_subsection"></a>   
### <a name="canvas"></a>Canvas  
 <xref:System.Windows.Controls.Canvas>元素允许的内容根据绝对定位*x 轴*并*y-* 坐标。 元素可以在唯一位置绘制；或者，如果元素占用了相同坐标，则这些元素在标记中显示的顺序决定它们的绘制顺序。  
  
 <xref:System.Windows.Controls.Canvas> 提供最灵活布局支持的任何<xref:System.Windows.Controls.Panel>。 Height 和 Width 属性用于定义在画布的区域和内部的元素分配相对于父区域的绝对坐标<xref:System.Windows.Controls.Canvas>。 四个附加的属性， <xref:System.Windows.Controls.Canvas.Left%2A?displayProperty=nameWithType>， <xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=nameWithType>，<xref:System.Windows.Controls.Canvas.Right%2A?displayProperty=nameWithType>并<xref:System.Windows.Controls.Canvas.Bottom%2A?displayProperty=nameWithType>，允许内的对象放置进行精细控制<xref:System.Windows.Controls.Canvas>，允许开发人员放置和排列在屏幕上精确的元素。  
  
#### <a name="cliptobounds-within-a-canvas"></a>Canvas 内 ClipToBounds  
 <xref:System.Windows.Controls.Canvas> 可在屏幕上，即使在坐标位于其自己定义之外的任何位置定位子元素<xref:System.Windows.FrameworkElement.Height%2A>和<xref:System.Windows.FrameworkElement.Width%2A>。 此外，<xref:System.Windows.Controls.Canvas>不受其子级的大小。 因此，很可能要过度绘制父级的边框之外的其他元素的子元素<xref:System.Windows.Controls.Canvas>。 默认行为<xref:System.Windows.Controls.Canvas>是允许的父边界外绘制子级<xref:System.Windows.Controls.Canvas>。 如果不需要，此行为<xref:System.Windows.UIElement.ClipToBounds%2A>属性可以设置为`true`。 这将导致<xref:System.Windows.Controls.Canvas>向剪辑到其自身的大小。 <xref:System.Windows.Controls.Canvas> 是唯一的布局元素，允许其边界外绘制子级。  
  
 [宽度属性比较示例](https://go.microsoft.com/fwlink/?LinkID=160050)中以图形方式展示了此行为。  
  
#### <a name="defining-and-using-a-canvas"></a>定义和使用 Canvas  
 一个<xref:System.Windows.Controls.Canvas>可以只需通过使用实例化[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]或代码。 下面的示例演示如何使用<xref:System.Windows.Controls.Canvas>以绝对方式定位内容。 此代码生成三个 100 像素正方形。 第一个正方形为红色，其左上角的 (*x, y*) 位置指定为 (0, 0)。 第二个正方形为绿色，其左上角位置为 (100, 100)，在第一个正方形的右下方。 第三个正方形为蓝色，其左上角为 (50, 50)，因此包含了第一个正方形的右下四分之一部分和第二个正方形的左上四分之一部分。 由于第三个正方形最后布置，因此它看起来在另外两个正方形上方，即，重叠部分采用第三个正方形的颜色。  
  
 [!code-csharp[CanvasOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasOvwSample/CSharp/Canvas_Ovw_Sample.cs#1)]
 [!code-vb[CanvasOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasOvwSample/VisualBasic/canvas_vb.vb#1)]
 [!code-xaml[CanvasOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/CanvasOvwSample/XAML/default.xaml#1)]  
  
 经编译的应用程序产生新的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，外观如下。  
  
 ![典型的 Canvas 元素。](./media/panel-intro-canvas.PNG "panel_intro_canvas")  
  
<a name="Panels_overview_DockPanel_subsection"></a>   
### <a name="dockpanel"></a>DockPanel  
 <xref:System.Windows.Controls.DockPanel>元素使用<xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>子内容元素来定位内容沿容器的边缘中设置附加属性。 当<xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>设置为<xref:System.Windows.Controls.Dock.Top>或<xref:System.Windows.Controls.Dock.Bottom>，它将子元素的上方或下方相互定位。 当<xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>设置为<xref:System.Windows.Controls.Dock.Left>或<xref:System.Windows.Controls.Dock.Right>，它将定位到左侧或右侧的每个其他子元素。 <xref:System.Windows.Controls.DockPanel.LastChildFill%2A>属性确定作为子级添加的最后一个元素的位置<xref:System.Windows.Controls.DockPanel>。  
  
 可以使用<xref:System.Windows.Controls.DockPanel>定位一组相关控件，如一组按钮。 或者，可以使用它创建“平移”的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，类似于 [!INCLUDE[TLA#tla_outlook](../../../../includes/tlasharptla-outlook-md.md)] 中的 UI。  
  
#### <a name="sizing-to-content"></a>按内容调整大小  
 如果其<xref:System.Windows.FrameworkElement.Height%2A>并<xref:System.Windows.FrameworkElement.Width%2A>未指定属性，<xref:System.Windows.Controls.DockPanel>其内容的大小。 大小可以增大或减小以容纳其子元素的大小。 但是，当已指定这些属性，并且不再为下一步指定的子元素，留出空间<xref:System.Windows.Controls.DockPanel>不显示该子元素或后续子元素，且不测量后续子元素。  
  
#### <a name="lastchildfill"></a>LastChildFill  
 默认情况下的最后一个子级<xref:System.Windows.Controls.DockPanel>元素将"填充"剩余的未分配空间。 如果不需要此行为，请设置<xref:System.Windows.Controls.DockPanel.LastChildFill%2A>属性设置为`false`。  
  
#### <a name="defining-and-using-a-dockpanel"></a>定义和使用 DockPanel  
 下面的示例演示如何进行分区的空间使用<xref:System.Windows.Controls.DockPanel>。 五<xref:System.Windows.Controls.Border>元素添加为父级的子级<xref:System.Windows.Controls.DockPanel>。 每个使用不同的位置属性来<xref:System.Windows.Controls.DockPanel>对空间进行分区。 最后一个元素"填充"剩余的未分配空间。  
  
 [!code-cpp[DockPanelOvwSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xaml[DockPanelOvwSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
 经编译的应用程序产生新的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，外观如下。  
  
 ![典型的 DockPanel 方案。](./media/panel-intro-dockpanel.PNG "panel_intro_dockpanel")  
  
<a name="Panels_overview_Grid_subsection"></a>   
### <a name="grid"></a>Grid  
 <xref:System.Windows.Controls.Grid>元素合并绝对定位和表格数据控件的功能。 一个<xref:System.Windows.Controls.Grid>使你能够轻松地位置和样式元素。 <xref:System.Windows.Controls.Grid> 允许你定义灵活的行和列分组，并甚至还提供了一种机制来共享大小调整信息之间多<xref:System.Windows.Controls.Grid>元素。  
  
#### <a name="how-is-grid-different-from-table"></a>网格与表格有何不同？  
 <xref:System.Windows.Documents.Table> 和<xref:System.Windows.Controls.Grid>共享某些通用功能，但每个都是最适用于不同的方案。 一个<xref:System.Windows.Documents.Table>专为流内容内使用 (请参阅[流文档概述](../advanced/flow-document-overview.md)有关流内容的详细信息)。 网格最适合在表单内（主要在流内容以外的任意位置）使用。 内<xref:System.Windows.Documents.FlowDocument>，<xref:System.Windows.Documents.Table>支持流内容行为，如分页、 列重排和内容时选择<xref:System.Windows.Controls.Grid>却没有。 一个<xref:System.Windows.Controls.Grid>另一方面最好使用之外<xref:System.Windows.Documents.FlowDocument>包括的原因有很多<xref:System.Windows.Controls.Grid>根据行和列索引添加元素<xref:System.Windows.Documents.Table>却没有。 <xref:System.Windows.Controls.Grid>元素可对子内容，从而允许多个元素共存于单个"单元格。"内进行分层 <xref:System.Windows.Documents.Table> 不支持分层。 子元素的<xref:System.Windows.Controls.Grid>相对于其"单元格"边界区域进行绝对定位。 <xref:System.Windows.Documents.Table> 不支持此功能。 最后，<xref:System.Windows.Controls.Grid>比更轻<xref:System.Windows.Documents.Table>。  
  
#### <a name="sizing-behavior-of-columns-and-rows"></a>列和行的大小调整行为  
 列和行中定义<xref:System.Windows.Controls.Grid>可以充分利用<xref:System.Windows.GridUnitType.Star>为了按比例分配剩余空间大小调整。 当<xref:System.Windows.GridUnitType.Star>被选为的高度或宽度的行或列，该列或行将收到剩余的可用空间的加权的比例。 这是与<xref:System.Windows.GridUnitType.Auto>，这会将分发均匀地根据中的列或行的内容的大小的空间。 在使用 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 时，此值以 `*` 或 `2*` 的形式表示。 在第一种情况下，行或列将得到一倍的可用空间，在第二种情况下，将得到两倍的可用空间，依此类推。 通过将此技术来按比例分配空间的组合<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>并<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>的值`Stretch`是可能的布局空间分区的屏幕空间的百分比。 <xref:System.Windows.Controls.Grid> 是唯一的布局面板，可以将分发在这种方式中的空间。  
  
#### <a name="defining-and-using-a-grid"></a>定义和使用 Grid  
 以下示例演示如何生成 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，该 UI 类似于 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)]“开始”菜单上提供的“运行”对话框上的 UI。  
  
 [!code-csharp[GridRunDialog#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridRunDialog/CSharp/window1.xaml.cs#1)]
 [!code-vb[GridRunDialog#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GridRunDialog/VisualBasic/grid_vb.vb#1)]  
  
 经编译的应用程序产生新的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，外观如下。  
  
 ![典型的 Grid 元素。](./media/avalon-run-dialog.PNG "avalon_run_dialog")  
  
<a name="Panels_overview_StackPanel_subsection"></a>   
### <a name="stackpanel"></a>StackPanel  
 一个<xref:System.Windows.Controls.StackPanel>可以"堆叠"在指定方向的元素。 默认堆叠方向为垂直方向。 <xref:System.Windows.Controls.StackPanel.Orientation%2A>属性可用于控制内容流。  
  
#### <a name="stackpanel-vs-dockpanel"></a>StackPanel 与 DockPanel  
 尽管<xref:System.Windows.Controls.DockPanel>也可以"堆叠"子元素<xref:System.Windows.Controls.DockPanel>和<xref:System.Windows.Controls.StackPanel>不产生一些应用场景中的类似结果。 例如，子元素的顺序可能会影响在其大小<xref:System.Windows.Controls.DockPanel>但不能在<xref:System.Windows.Controls.StackPanel>。 这是因为<xref:System.Windows.Controls.StackPanel>度量值中的堆叠在方向<xref:System.Double.PositiveInfinity>，而<xref:System.Windows.Controls.DockPanel>测量仅的可用大小。  
  
 以下示例演示此主要区别。  
  
 [!code-cpp[StackPanelOvw4#1](~/samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xaml[StackPanelOvw4#1](~/samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
 通过此图像可以看到呈现行为的区别。  
  
 ![屏幕快照：StackPanel 与 DockPanel 屏幕截图](./media/layout-smiley-stackpanel.PNG "layout_smiley_stackpanel")  
  
#### <a name="defining-and-using-a-stackpanel"></a>定义和使用 StackPanel  
 下面的示例演示如何使用<xref:System.Windows.Controls.StackPanel>创建一组垂直定位的按钮。 对于水平定位，设置<xref:System.Windows.Controls.StackPanel.Orientation%2A>属性设置为<xref:System.Windows.Controls.Orientation.Horizontal>。  
  
 [!code-csharp[StackPanel_ovw2#1](~/samples/snippets/csharp/VS_Snippets_Wpf/StackPanel_ovw2/CSharp/StackPanel_Ovw_Sample2.cs#1)]
 [!code-vb[StackPanel_ovw2#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanel_ovw2/VisualBasic/StackPanelOvw.vb#1)]  
  
 经编译的应用程序产生新的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，外观如下。  
  
 ![典型的 StackPanel 元素。](./media/panel-intro-stackpanel.PNG "panel_intro_stackpanel")  
  
<a name="Panels_overview_VirtualizingStackPanel_subsection"></a>   
#### <a name="virtualizingstackpanel"></a>VirtualizingStackPanel  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 此外提供了一种变体的<xref:System.Windows.Controls.StackPanel>自动"虚拟化"数据绑定子级内容的元素。 在此上下文中，“虚拟化”一词指的是一种技术：通过此技术根据屏幕上哪些项可见，从较多的数据项中生成一个元素子集。 如果在指定时刻只有少量 UI 元素位于屏幕上，则此时生成大量 UI 元素需要占用大量内存和处理器。 <xref:System.Windows.Controls.VirtualizingStackPanel> (通过提供的功能<xref:System.Windows.Controls.VirtualizingPanel>) 计算可见项，并处理<xref:System.Windows.Controls.ItemContainerGenerator>从<xref:System.Windows.Controls.ItemsControl>(如<xref:System.Windows.Controls.ListBox>或<xref:System.Windows.Controls.ListView>) 仅创建为可见项的元素。  
  
 <xref:System.Windows.Controls.VirtualizingStackPanel>元素会自动设置为承载的项控件如<xref:System.Windows.Controls.ListBox>。 当承载数据绑定集合时，内容自动虚拟化，只要内容的边界内<xref:System.Windows.Controls.ScrollViewer>。 在承载许多子项时，这将大幅提高性能。  
  
 以下标记演示如何使用<xref:System.Windows.Controls.VirtualizingStackPanel>作为项宿主。 <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizingProperty?displayProperty=nameWithType>附加的属性必须设置为`true`（默认值） 才能进行虚拟化。  
  
 [!code-xaml[VirtualizingStackPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/VirtualizingStackPanel_Intro/CS/default.xaml#1)]  
  
<a name="Panels_overview_WrapPanel"></a>   
### <a name="wrappanel"></a>WrapPanel  
 <xref:System.Windows.Controls.WrapPanel> 用于从左到右，将内容切换到下一步的行时到达其父容器边缘的顺序位置定位子元素。 内容可以设置为水平或垂直方向。 <xref:System.Windows.Controls.WrapPanel> 可用于简单流[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]方案。 它还可以用来将统一大小调整应用于其所有子元素。  
  
 下面的示例演示如何创建<xref:System.Windows.Controls.WrapPanel>以显示<xref:System.Windows.Controls.Button>当到达容器边缘时换行的控件。  
  
 [!code-cpp[WrapPanel_Intro#1](~/samples/snippets/cpp/VS_Snippets_Wpf/WrapPanel_Intro/CPP/WrapPanel_Code.cpp#1)]
 [!code-csharp[WrapPanel_Intro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/WrapPanel_Intro/CSharp/WrapPanel_Code.cs#1)]
 [!code-vb[WrapPanel_Intro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WrapPanel_Intro/VisualBasic/WrapPanel_vb.vb#1)]
 [!code-xaml[WrapPanel_Intro#1](~/samples/snippets/xaml/VS_Snippets_Wpf/WrapPanel_Intro/XAML/default.xaml#1)]  
  
 经编译的应用程序产生新的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，外观如下。  
  
 ![典型 WrapPanel 元素。](./media/wrappanel-element.PNG "WrapPanel_Element")  
  
<a name="Panels_nested_panel_elements"></a>   
## <a name="nested-panel-elements"></a>嵌套 Panel 元素  
 <xref:System.Windows.Controls.Panel> 若要生成复杂的布局，可以相互嵌套元素。 这可以证明非常有用的一个<xref:System.Windows.Controls.Panel>非常适合的一部分[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，但不是满足的其他部分需求[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
 对于应用程序可以支持的嵌套数量，并没有实际限制，但通常最好限制应用程序仅使用预期布局实际所需的面板。 在许多情况下，<xref:System.Windows.Controls.Grid>元素可用来代替嵌套面板，因为它用作布局容器的灵活性。 这可以通过将不必要的元素排除在树以外来提高应用程序的性能。  
  
 下面的示例演示如何创建[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]充分利用嵌套<xref:System.Windows.Controls.Panel>元素，以实现特定的布局。 在此特定情况下<xref:System.Windows.Controls.DockPanel>元素用于提供[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]结构，而嵌套<xref:System.Windows.Controls.StackPanel>元素， <xref:System.Windows.Controls.Grid>，和一个<xref:System.Windows.Controls.Canvas>用来定位子元素精确地在父级内的<xref:System.Windows.Controls.DockPanel>。  
  
 [!code-csharp[Nested_Panels#1](~/samples/snippets/csharp/VS_Snippets_Wpf/Nested_Panels/CSharp/nestedpanels.cs#1)]
 [!code-vb[Nested_Panels#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Nested_Panels/VisualBasic/nestedpanels.vb#1)]  
  
 经编译的应用程序产生新的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，外观如下。  
  
 ![充分利用嵌套面板的 UI。](./media/nested-panels.PNG "nested_panels")  
  
<a name="Panels_custom_panel_elements"></a>   
## <a name="custom-panel-elements"></a>自定义 Panel 元素  
 虽然[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供了一系列灵活的布局控件，也可以通过重写实现行为的自定义布局<xref:System.Windows.FrameworkElement.ArrangeOverride%2A>和<xref:System.Windows.FrameworkElement.MeasureOverride%2A>方法。 可以通过在这些重写方法内定义新的位置行为来实现自定义大小调整和位置。  
  
 同样，自定义布局行为基于派生类 (如<xref:System.Windows.Controls.Canvas>或<xref:System.Windows.Controls.Grid>) 可以定义通过重写其<xref:System.Windows.FrameworkElement.ArrangeOverride%2A>和<xref:System.Windows.FrameworkElement.MeasureOverride%2A>方法。  
  
 以下标记演示如何创建自定义<xref:System.Windows.Controls.Panel>元素。 这一新<xref:System.Windows.Controls.Panel>，其定义如下`PlotPanel`，支持通过使用硬编码的子元素定位*x 轴*并*y-* 坐标。 在此示例中，<xref:System.Windows.Shapes.Rectangle>元素 （未显示） 都位于绘图点 50 (*x*)，到 50 个 (*y*)。  
  
 [!code-cpp[PlotPanel#1](~/samples/snippets/cpp/VS_Snippets_Wpf/PlotPanel/CPP/PlotPanel.cpp#1)]
 [!code-csharp[PlotPanel#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PlotPanel/CSharp/PlotPanel.cs#1)]
 [!code-vb[PlotPanel#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PlotPanel/VisualBasic/PlotPanel.vb#1)]  
  
 若要查看更复杂的自定义面板实现，请参阅[创建自定义内容换行面板示例](https://go.microsoft.com/fwlink/?LinkID=159979)。  
  
<a name="Panels_global_localization"></a>   
## <a name="localizationglobalization-support"></a>本地化/全球化支持  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 支持多种有助于创建可本地化的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的功能。  
  
 所有面板元素本身都支持<xref:System.Windows.FrameworkElement.FlowDirection%2A>属性，可用于动态地重排内容基于用户的区域设置或语言设置。 有关详细信息，请参阅 <xref:System.Windows.FrameworkElement.FlowDirection%2A>。  
  
 <xref:System.Windows.Window.SizeToContent%2A>属性提供了一种机制，使应用程序开发人员要预测的需求本地化[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。 使用<xref:System.Windows.SizeToContent.WidthAndHeight>此属性，父值<xref:System.Windows.Window>始终动态调整大小以适应内容和不受人为的高度或宽度限制。  
  
 <xref:System.Windows.Controls.DockPanel><xref:System.Windows.Controls.Grid>，并<xref:System.Windows.Controls.StackPanel>所有选择适合的可本地化[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。 <xref:System.Windows.Controls.Canvas> 但是，是不是一个不错的选择，因为其内容以绝对方式定位，使其难以本地化。  
  
 有关创建带有可本地化 [!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)] 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的其他信息，请参阅[使用自动布局概述](../advanced/use-automatic-layout-overview.md)。  
  
## <a name="see-also"></a>请参阅
- [演练：我的第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
- [WPF 布局库示例](https://go.microsoft.com/fwlink/?LinkID=160054)
- [布局](../advanced/layout.md)
- [WPF 控件库示例](https://go.microsoft.com/fwlink/?LinkID=160053)
- [对齐、边距和填充概述](../advanced/alignment-margins-and-padding-overview.md)
- [创建自定义内容换行面板示例](https://go.microsoft.com/fwlink/?LinkID=159979)
- [附加属性概述](../advanced/attached-properties-overview.md)
- [使用自动布局概述](../advanced/use-automatic-layout-overview.md)
- [布局和示例](../advanced/optimizing-performance-layout-and-design.md)
