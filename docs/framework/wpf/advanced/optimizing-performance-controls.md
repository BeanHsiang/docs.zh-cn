---
title: 优化性能：控件的 WPF
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], improving performance
- container recycling [WPF]
- user interface virtualization [WPF]
ms.assetid: 45a31c43-ea8a-4546-96c8-0631b9934179
ms.openlocfilehash: 20b2b20c2f7f37b4ae01159e70bc8c0945777152
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55286424"
---
# <a name="optimizing-performance-controls"></a>优化性能：Controls

Windows Presentation Foundation (WPF) 包含许多使用的常见用户界面 (UI) 组件在大多数 Windows 应用程序。 本主题包含提高 UI 性能的技术。

## <a name="displaying-large-data-sets"></a>显示大型数据集

WPF 控件，如<xref:System.Windows.Controls.ListView>和<xref:System.Windows.Controls.ComboBox>用于应用程序中显示的项列表。 如果要显示的列表较大，则应用程序性能可能受到影响。 这是因为标准布局系统会为每个与列表控件关联的项创建布局容器，并计算其布局大小和位置。 通常，无需同时显示所有项，而是显示子集，然后用户滚动浏览列表。 这种情况下，使用 UI 虚拟化具有意义，这意味着生成项容器，且项的关联布局计算会推迟，直到项可见时。

UI 虚拟化是列表控件的一个重要方面。 不应混淆 UI 虚拟化和数据虚拟化。 UI 虚拟化在内存中仅存储可见项，但在数据绑定方案中会存储内存中的整个数据结构。 相反，数据虚拟化仅存储内存中屏幕上可见的数据项。

默认情况下，为启用 UI 虚拟化<xref:System.Windows.Controls.ListView>和<xref:System.Windows.Controls.ListBox>控制其列表项绑定到数据时。 <xref:System.Windows.Controls.TreeView> 可以通过设置启用虚拟化<xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=nameWithType>附加属性设置为`true`。 如果你想要启用 UI 虚拟化的自定义控件派生自<xref:System.Windows.Controls.ItemsControl>或现有项控件使用<xref:System.Windows.Controls.StackPanel>类，如<xref:System.Windows.Controls.ComboBox>，可以设置<xref:System.Windows.Controls.ItemsControl.ItemsPanel%2A>到<xref:System.Windows.Controls.VirtualizingStackPanel>并设置<xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizing%2A>到`true`. 遗憾的是，可对没有实现虚拟化的控件禁用 UI 虚拟化。 以下为禁用 UI 虚拟化的条件列表。

- 项容器直接添加到<xref:System.Windows.Controls.ItemsControl>。 例如，如果应用程序显式添加<xref:System.Windows.Controls.ListBoxItem>对象添加到<xref:System.Windows.Controls.ListBox>，则<xref:System.Windows.Controls.ListBox>不会虚拟<xref:System.Windows.Controls.ListBoxItem>对象。

- 中的项容器<xref:System.Windows.Controls.ItemsControl>类型不同。 例如， <xref:System.Windows.Controls.Menu> ，它使用<xref:System.Windows.Controls.Separator>对象无法实现项回收，因为<xref:System.Windows.Controls.Menu>包含类型的对象<xref:System.Windows.Controls.Separator>和<xref:System.Windows.Controls.MenuItem>。

- 设置<xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A>到`false`。

- 设置<xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A>到`false`。

虚拟化项容器时需要考虑到一个重要因素，即是否具有与属于项的项容器相关联的其他状态信息。 这种情况下，必须保存其他状态。 例如，可能有中包含的项<xref:System.Windows.Controls.Expander>控件和<xref:System.Windows.Controls.Expander.IsExpanded%2A>状态绑定到项的容器，而不是项目本身。 容器的新项目的当前值的重用时间<xref:System.Windows.Controls.Expander.IsExpanded%2A>用于新项。 此外，旧项会丢失正确<xref:System.Windows.Controls.Expander.IsExpanded%2A>值。

当前，无任何 WPF 控件提供对数据虚拟化的内置支持。

## <a name="container-recycling"></a>容器回收

一种优化方式 UI 虚拟化在.NET Framework 3.5 SP1 的继承的控件添加到<xref:System.Windows.Controls.ItemsControl>是*容器回收，* 这样还可提高滚动性能。 当<xref:System.Windows.Controls.ItemsControl>填充使用 UI 虚拟化，它会创建每个项，滚动到视图中，并销毁滚动出视野之外的每个项的项容器的项容器。 *容器回收*使得控件可以重用不同的数据项，将现有项容器，以便无需经常创建和销毁当用户滚动项容器<xref:System.Windows.Controls.ItemsControl>。 您可以选择启用项回收通过设置<xref:System.Windows.Controls.VirtualizingPanel.VirtualizationMode%2A>附加属性设置为<xref:System.Windows.Controls.VirtualizationMode.Recycling>。

任何<xref:System.Windows.Controls.ItemsControl>支持虚拟化可以使用容器回收。 有关如何启用容器回收上的示例<xref:System.Windows.Controls.ListBox>，请参阅[提高 ListBox 的滚动性能](../controls/how-to-improve-the-scrolling-performance-of-a-listbox.md)。

## <a name="supporting-bidirectional-virtualization"></a>支持双向虚拟化

<xref:System.Windows.Controls.VirtualizingStackPanel> 提供对在一个方向的 UI 虚拟化的内置支持水平或垂直。 如果你想要使用双向虚拟化您的控件，则必须实现扩展的自定义面板<xref:System.Windows.Controls.VirtualizingStackPanel>类。 <xref:System.Windows.Controls.VirtualizingStackPanel>类公开的虚拟方法，如<xref:System.Windows.Controls.VirtualizingStackPanel.OnViewportSizeChanged%2A>， <xref:System.Windows.Controls.VirtualizingStackPanel.LineUp%2A>， <xref:System.Windows.Controls.VirtualizingStackPanel.PageUp%2A>，和<xref:System.Windows.Controls.VirtualizingStackPanel.MouseWheelUp%2A>。这些虚拟方法，可检测列表可见部分中的更改并相应地处理。

## <a name="optimizing-templates"></a>优化模板

可视化树包含应用程序中所有可视元素。 除直接创建的对象外，它还包括由于模板扩展而产生的对象。 例如，创建<xref:System.Windows.Controls.Button>，您还可以获得<xref:Microsoft.Windows.Themes.ClassicBorderDecorator>和<xref:System.Windows.Controls.ContentPresenter>可视化树中的对象。 如果尚未优化模板控件，则要在可视化树中创建大量不必要的额外对象。 有关可视化树的详细信息，请参见 [WPF 图形呈现概述](../graphics-multimedia/wpf-graphics-rendering-overview.md)。

## <a name="deferred-scrolling"></a>延迟滚动

默认情况下，用户拖动滚动条上的滚动块时，内容视图会不断更新。 如果控件中滚动较慢，请考虑使用延迟滚动。 在延迟滚动中，仅在用户释放滚动块时才会更新内容。

若要实现延迟滚动，设置<xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A>属性设置为`true`。 <xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A> 是一个附加的属性和可以设置<xref:System.Windows.Controls.ScrollViewer>并具有任何控件<xref:System.Windows.Controls.ScrollViewer>其控件模板中。

## <a name="controls-that-implement-performance-features"></a>控件可实现性能功能

下表列出了显示数据的常见控件及其性能功能支持。 有关如何启用这些功能的信息，请参阅先前章节。

|控件|虚拟化|容器回收|延迟滚动|
|-------------|--------------------|-------------------------|------------------------|
|<xref:System.Windows.Controls.ComboBox>|可启用|可启用|可启用|
|<xref:System.Windows.Controls.ContextMenu>|可启用|可启用|可启用|
|<xref:System.Windows.Controls.DocumentViewer>|不可用|不可用|可启用|
|<xref:System.Windows.Controls.ListBox>|默认|可启用|可启用|
|<xref:System.Windows.Controls.ListView>|默认|可启用|可启用|
|<xref:System.Windows.Controls.TreeView>|可启用|可启用|可启用|
|<xref:System.Windows.Controls.ToolBar>|不可用|不可用|可启用|

> [!NOTE]
> 有关如何启用虚拟化和容器上回收的示例<xref:System.Windows.Controls.TreeView>，请参阅[提高 TreeView 的性能](../controls/how-to-improve-the-performance-of-a-treeview.md)。

## <a name="see-also"></a>请参阅

- [布局](layout.md)
- [布局和示例](optimizing-performance-layout-and-design.md)
- [数据绑定](optimizing-performance-data-binding.md)
- [控件](../controls/index.md)
- [样式设置和模板化](../controls/styling-and-templating.md)
- [演练：缓存在 WPF 应用程序的应用程序数据](walkthrough-caching-application-data-in-a-wpf-application.md)