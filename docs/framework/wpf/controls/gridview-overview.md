---
title: GridView 概述
ms.date: 03/30/2017
helpviewer_keywords:
- GridView view mode [WPF]
- ListView controls [WPF], GridView view mode
- controls [WPF], ListView
ms.assetid: b2d02267-32b3-40ce-8e9f-06972d8749d9
ms.openlocfilehash: 9457430ab61681ad154aba98d72850f19d30280d
ms.sourcegitcommit: 462dc41a13942e467984e48f4018d1f79ae67346
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58185436"
---
# <a name="gridview-overview"></a>GridView 概述
<xref:System.Windows.Controls.GridView> 视图模式是一种视图模式的<xref:System.Windows.Controls.ListView>控件。 <xref:System.Windows.Controls.GridView>类和及其支持类使您和您的用户能够查看通常使用按钮作为交互式列标题的表中的项集合。 本主题介绍<xref:System.Windows.Controls.GridView>类，并概述了其用途。  
  
  
  
<a name="DefiningaListViewthatusesGridViewView"></a>   
## <a name="what-is-a-gridview-view"></a>什么是 GridView 视图？  
 <xref:System.Windows.Controls.GridView>模式通过将数据字段绑定到列以及显示列标题，可标识的字段显示的数据项列表的视图。 默认值<xref:System.Windows.Controls.GridView>样式实现按钮作为列标题。 通过使用列标题按钮，可以实现重要的用户交互功能;例如，用户可以单击要排序的列标题<xref:System.Windows.Controls.GridView>根据特定列的内容的数据。  
  
> [!NOTE]
>  按钮控件<xref:System.Windows.Controls.GridView>用于列标题派生自<xref:System.Windows.Controls.Primitives.ButtonBase>。  
  
 如下图所示<xref:System.Windows.Controls.GridView>查看的<xref:System.Windows.Controls.ListView>内容。  
    
 ![显示 ListView 内容的 GridView 视图的屏幕截图。](./media/gridview-overview/styled-listview-content.png)  
  
 <xref:System.Windows.Controls.GridView> 列由<xref:System.Windows.Controls.GridViewColumn>对象，可以对其内容自动调整大小。 （可选） 可以显式设置<xref:System.Windows.Controls.GridViewColumn>为一个特定宽度。 可通过拖动列标题之间的手柄重设列的大小。 您可以还可以动态地添加、 删除、 替换和对列重新排序，因为此功能内置到<xref:System.Windows.Controls.GridView>。 但是，<xref:System.Windows.Controls.GridView>不能直接更新它显示的数据。  
  
 下面的示例演示如何定义<xref:System.Windows.Controls.GridView>显示员工数据。 在此示例中，<xref:System.Windows.Controls.ListView>定义`EmployeeInfoDataSource`作为<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>。 属性定义<xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>绑定<xref:System.Windows.Controls.GridViewColumn>内容到`EmployeeInfoDataSource`数据类别。  
  
 [!code-xaml[ListViewCode#ListViewEmployee](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 下图显示了上一示例创建的表格。 GridView 控件显示 ItemsSource 对象中的数据：
    
 ![显示具有 GridView 输出的 ListView 的屏幕截图。](./media/gridview-overview/listview-gridview-output.jpg)  
  
<a name="GridViewLayoutandStyle"></a>   
## <a name="gridview-layout-and-style"></a>GridView 布局和样式  
 列单元格和列标题的<xref:System.Windows.Controls.GridViewColumn>具有相同的宽度。 默认情况下，每一列都根据其内容来调整宽度大小。 也可以选择将列设置为固定宽度。  
  
 相关的数据内容显示在水平行中。 例如，在上图中，每个员工的姓氏、名字和 ID 号显示为一组，因为它们显示在一个水平行中。  
  
<a name="DefiningandStylingColumnsinaGridView"></a>   
### <a name="defining-and-styling-columns-in-a-gridview"></a>在 GridView 中定义列并设置其样式  
 定义要在中显示的数据字段时<xref:System.Windows.Controls.GridViewColumn>，使用<xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>， <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>，或<xref:System.Windows.Controls.GridViewColumn.CellTemplateSelector%2A>属性。 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>属性优先于任何模板属性。  
  
 若要指定的列中的内容的对齐方式<xref:System.Windows.Controls.GridView>，定义<xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>。 不要使用<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>并<xref:System.Windows.Controls.Control.VerticalContentAlignment%2A>属性<xref:System.Windows.Controls.ListView>通过使用显示的内容<xref:System.Windows.Controls.GridView>。  
  
 若要指定列标题的模板和样式属性，请使用<xref:System.Windows.Controls.GridView>， <xref:System.Windows.Controls.GridViewColumn>，和<xref:System.Windows.Controls.GridViewColumnHeader>类。 有关详细信息，请参阅 [GridView 列标题的样式和模板概述](gridview-column-header-styles-and-templates-overview.md)。  
  
<a name="AddingVisualElementstoaGridViewView"></a>   
### <a name="adding-visual-elements-to-a-gridview"></a>将可视元素添加到 GridView  
 添加可视元素，例如<xref:System.Windows.Controls.CheckBox>并<xref:System.Windows.Controls.Button>控件，为<xref:System.Windows.Controls.GridView>视图模式中，使用模板或样式。  
  
 如果您显式定义为数据项的可视元素，它可以只出现一次在<xref:System.Windows.Controls.GridView>。 之所以存在此限制，是因为元素只能有一个父级，因此，只能在可视化树中出现一次。  
  
<a name="StylingRowsinaGridViewView"></a>   
### <a name="styling-rows-in-a-gridview"></a>设置 GridView 中的行的样式  
 使用<xref:System.Windows.Controls.GridViewRowPresenter>并<xref:System.Windows.Controls.GridViewHeaderRowPresenter>类来格式化和显示的行<xref:System.Windows.Controls.GridView>。 有关如何的示例中的样式行<xref:System.Windows.Controls.GridView>查看模式，请参阅[的行设置样式中 ListView，实现 GridView](how-to-style-a-row-in-a-listview-that-implements-a-gridview.md)。  
  
<a name="AlignmentIssuesWhenUsingItemContainerStyle"></a>   
### <a name="alignment-issues-when-you-use-itemcontainerstyle"></a>使用 ItemContainerStyle 时的对齐问题  
 若要防止列标题和单元格之间对齐问题，未设置属性或指定模板中的项的宽度有影响<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>。 例如，未设置<xref:System.Windows.FrameworkElement.Margin%2A>属性，或者指定<xref:System.Windows.Controls.ControlTemplate>，它将<xref:System.Windows.Controls.CheckBox>到<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A>上定义<xref:System.Windows.Controls.ListView>控件。 而是指定的属性和影响列宽度，直接在定义的类上的模板<xref:System.Windows.Controls.GridView>视图模式。  
  
 例如，若要添加<xref:System.Windows.Controls.CheckBox>对中的行<xref:System.Windows.Controls.GridView>视图模式中，添加<xref:System.Windows.Controls.CheckBox>到<xref:System.Windows.DataTemplate>，然后设置<xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>属性设置为的<xref:System.Windows.DataTemplate>。  
  
<a name="InteractingwithaGridViewControl"></a>   
## <a name="user-interactions-with-a-gridview"></a>与 GridView 的用户交互  
 当你使用<xref:System.Windows.Controls.GridView>用户可以在应用程序中与之交互和修改的格式设置<xref:System.Windows.Controls.GridView>。 例如，用户可以对列重新排序、重设列的大小、选择表中的项以及滚动查看内容。 还可定义当用户单击列标题按钮时响应的事件处理程序。 事件处理程序可以执行操作，如显示在对数据进行排序<xref:System.Windows.Controls.GridView>根据列的内容。  
  
 以下列表更详细地讨论使用的功能<xref:System.Windows.Controls.GridView>进行用户交互：  
  
-   **使用拖放方法对列重新排序。**  
  
     用户可以对中的列重新排序<xref:System.Windows.Controls.GridView>由列标题上时按鼠标左键，然后将该列拖动到新位置。 当用户拖动列标题时，将显示标题的浮动版本以及显示列的插入位置的黑色实线。  
  
     如果你想要修改的浮动版本的标头的默认样式，指定<xref:System.Windows.Controls.ControlTemplate>有关<xref:System.Windows.Controls.GridViewColumnHeader>，它是键入触发时<xref:System.Windows.Controls.GridViewColumnHeader.Role%2A>属性设置为<xref:System.Windows.Controls.GridViewColumnHeaderRole.Floating>。 有关详细信息，请参阅[为拖动的 GridView 列标题创建样式](how-to-create-a-style-for-a-dragged-gridview-column-header.md)。  
  
-   **根据列的内容重设其大小。**  
  
     用户可双击列标题右侧的手柄来根据列的内容重设其大小。  
  
    > [!NOTE]
    >  可以设置<xref:System.Windows.Controls.GridViewColumn.Width%2A>属性设置为`Double.NaN`以生成相同的效果。  
  
-   **选择行项目。**  
  
     用户可以选择中的一个或多个项<xref:System.Windows.Controls.GridView>。  
  
     如果你想要更改<xref:System.Windows.Style>选定项，请参阅[使用触发器为 ListView 中选定项设置样式](how-to-use-triggers-to-style-selected-items-in-a-listview.md)。  
  
-   **滚动查看最初未显示在屏幕上的内容。**  
  
     如果的大小<xref:System.Windows.Controls.GridView>是不足够大以显示所有项，用户可以滚动浏览水平或垂直通过使用滚动条，其中提供的<xref:System.Windows.Controls.ScrollViewer>控件。 一个<xref:System.Windows.Controls.Primitives.ScrollBar>处于隐藏状态，如果所有内容都是在特定方向中可见。 列标题不会随着垂直滚动条滚动，但可水平滚动。  
  
-   **通过单击列标题按钮与列交互。**  
  
     如果提供了排序算法，则当用户单击列标题按钮时，可以对列中显示的数据进行排序。  
  
     您可以处理<xref:System.Windows.Controls.Primitives.ButtonBase.Click>以便提供类似排序算法的功能的列标题按钮的事件。 若要处理<xref:System.Windows.Controls.Primitives.ButtonBase.Click>一个列标题，为事件设置事件处理程序上<xref:System.Windows.Controls.GridViewColumnHeader>。 若要设置的事件处理程序处理<xref:System.Windows.Controls.Primitives.ButtonBase.Click>的所有列标题，为事件设置处理程序上<xref:System.Windows.Controls.ListView>控件。  
  
<a name="Obtaining_Other_Custom_Views"></a>   
## <a name="obtaining-other-custom-views"></a>获取其他自定义视图  
 <xref:System.Windows.Controls.GridView>类，该类派生自<xref:System.Windows.Controls.ViewBase>抽象类，只是可能视图模式的一个<xref:System.Windows.Controls.ListView>类。 可以创建其他自定义视图<xref:System.Windows.Controls.ListView>通过派生自<xref:System.Windows.Controls.ViewBase>类。 有关自定义视图模式的示例，请参阅[为 ListView 创建自定义视图模式](how-to-create-a-custom-view-mode-for-a-listview.md)。  
  
<a name="GridViewSupportingClasses"></a>   
## <a name="gridview-supporting-classes"></a>GridView 支持类  
 下面的类支持<xref:System.Windows.Controls.GridView>视图模式。  
  
-   <xref:System.Windows.Controls.GridViewColumn>  
  
-   <xref:System.Windows.Controls.GridViewColumnHeader>  
  
-   <xref:System.Windows.Controls.GridViewRowPresenter>  
  
-   <xref:System.Windows.Controls.GridViewHeaderRowPresenter>  
  
-   <xref:System.Windows.Controls.GridViewColumnCollection>  
  
-   <xref:System.Windows.Controls.GridViewColumnHeaderRole>  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.ListViewItem>
- <xref:System.Windows.Controls.GridViewColumn>
- <xref:System.Windows.Controls.GridViewColumnHeader>
- <xref:System.Windows.Controls.GridViewRowPresenter>
- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>
- <xref:System.Windows.Controls.ViewBase>
- [ListView 概述](listview-overview.md)
- [在单击标题时对 GridView 列进行排序](how-to-sort-a-gridview-column-when-a-header-is-clicked.md)
- [帮助主题](listview-how-to-topics.md)
