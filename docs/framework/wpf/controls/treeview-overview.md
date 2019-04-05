---
title: TreeView 概述
ms.date: 03/30/2017
helpviewer_keywords:
- expanding node [WPF]
- TreeView control [WPF], about TreeView control
- Control class [WPF], TreeView
ms.assetid: 62212512-5a5c-4864-949e-b6a6a3a52c02
ms.openlocfilehash: 5758aead9811cdbaf7f61bbd710092f6b4474ad8
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369625"
---
# <a name="treeview-overview"></a>TreeView 概述
<xref:System.Windows.Controls.TreeView>控件提供了一种方法，通过使用可折叠节点在层次结构中显示的信息。 本主题介绍<xref:System.Windows.Controls.TreeView>和<xref:System.Windows.Controls.TreeViewItem>控件，并提供其用法的简单示例。  
  
  
<a name="Simple_TreeView_Control"></a>   
## <a name="what-is-a-treeview"></a>什么是 TreeView？  
 <xref:System.Windows.Controls.TreeView> 是<xref:System.Windows.Controls.ItemsControl>通过使用嵌套项<xref:System.Windows.Controls.TreeViewItem>控件。 下面的示例创建<xref:System.Windows.Controls.TreeView>。  
  
 [!code-xaml[TreeViewSnips#EmbeddedTVIs](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#embeddedtvis)]  
  
<a name="Creating_a_TreeView"></a>   
## <a name="creating-a-treeview"></a>创建 TreeView  
 <xref:System.Windows.Controls.TreeView>控件包含的层次结构<xref:System.Windows.Controls.TreeViewItem>控件。 一个<xref:System.Windows.Controls.TreeViewItem>控件是<xref:System.Windows.Controls.HeaderedItemsControl>具有<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>和<xref:System.Windows.Controls.ItemsControl.Items%2A>集合。  
  
 如果您要定义<xref:System.Windows.Controls.TreeView>通过使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，可以显式定义<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>内容的<xref:System.Windows.Controls.TreeViewItem>控件以及组成其集合的项。 上图演示了此方法。  
  
 此外可以指定<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>作为数据源，然后指定<xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A>并<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>可以定义<xref:System.Windows.Controls.TreeViewItem>内容。  
  
 若要定义的布局<xref:System.Windows.Controls.TreeViewItem>控件，您还可以使用<xref:System.Windows.HierarchicalDataTemplate>对象。 有关详细信息和示例，请参阅[使用 SelectedValue、SelectedValuePath 和 SelectedItem](how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)。  
  
 如果项不是<xref:System.Windows.Controls.TreeViewItem>控件，它将自动包括<xref:System.Windows.Controls.TreeViewItem>控制何时<xref:System.Windows.Controls.TreeView>显示控件。  
  
<a name="Expanding_and_Collapsing_a_TreeViewItem"></a>   
## <a name="expanding-and-collapsing-a-treeviewitem"></a>展开和折叠 TreeViewItem  
 如果在用户展开<xref:System.Windows.Controls.TreeViewItem>，则<xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A>属性设置为`true`。 您还可以展开或折叠<xref:System.Windows.Controls.TreeViewItem>而无需通过设置任何直接的用户操作<xref:System.Windows.Controls.TreeViewItem.IsExpanded%2A>属性设置为`true`（展开） 或`false`（折叠）。 此属性更改时，<xref:System.Windows.Controls.TreeViewItem.Expanded>或<xref:System.Windows.Controls.TreeViewItem.Collapsed>事件发生。  
  
 当<xref:System.Windows.FrameworkElement.BringIntoView%2A>上调用方法<xref:System.Windows.Controls.TreeViewItem>控件，<xref:System.Windows.Controls.TreeViewItem>及其父<xref:System.Windows.Controls.TreeViewItem>控件展开。 如果<xref:System.Windows.Controls.TreeViewItem>不可见或部分可见，<xref:System.Windows.Controls.TreeView>滚动以使其可见。  
  
<a name="TreeViewItem_Selection"></a>   
## <a name="treeviewitem-selection"></a>TreeViewItem 选择  
 当用户单击<xref:System.Windows.Controls.TreeViewItem>控件以选择它，<xref:System.Windows.Controls.TreeViewItem.Selected>发生事件时，并将其<xref:System.Windows.Controls.TreeViewItem.IsSelected%2A>属性设置为`true`。 <xref:System.Windows.Controls.TreeViewItem>也将变为<xref:System.Windows.Controls.TreeView.SelectedItem%2A>的<xref:System.Windows.Controls.TreeView>控件。 相反，所选内容由<xref:System.Windows.Controls.TreeViewItem>控件，其<xref:System.Windows.Controls.TreeViewItem.Unselected>发生事件并将其<xref:System.Windows.Controls.TreeViewItem.IsSelected%2A>属性设置为`false`。  
  
 <xref:System.Windows.Controls.TreeView.SelectedItem%2A>属性上的<xref:System.Windows.Controls.TreeView>控件是只读属性; 因此，您不能显式将其设置。 <xref:System.Windows.Controls.TreeView.SelectedItem%2A>属性设置在用户单击上<xref:System.Windows.Controls.TreeViewItem>控件时，或者当<xref:System.Windows.Controls.TreeViewItem.IsSelected%2A>属性设置为`true`上<xref:System.Windows.Controls.TreeViewItem>控件。  
  
 使用<xref:System.Windows.Controls.TreeView.SelectedValuePath%2A>属性来指定<xref:System.Windows.Controls.TreeView.SelectedValue%2A>的<xref:System.Windows.Controls.TreeView.SelectedItem%2A>。 有关详细信息，请参阅[使用 SelectedValue、SelectedValuePath 和 SelectedItem](how-to-use-selectedvalue-selectedvaluepath-and-selecteditem.md)。  
  
 可以在注册事件处理程序<xref:System.Windows.Controls.TreeView.SelectedItemChanged>事件，以确定当所选<xref:System.Windows.Controls.TreeViewItem>更改。 <xref:System.Windows.RoutedPropertyChangedEventArgs%601>提供对事件处理程序指定<xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A>，这是以前的选项，和<xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>，这是当前所选内容。 如果应用程序或用户未进行上一个或当前选择，则任一值都可能为 `null`。  
  
<a name="TreeView_Style"></a>   
## <a name="treeview-style"></a>TreeView 样式  
 默认样式<xref:System.Windows.Controls.TreeView>控件将其内部放置<xref:System.Windows.Controls.StackPanel>对象，其中包含<xref:System.Windows.Controls.ScrollViewer>控件。 当设置<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性<xref:System.Windows.Controls.TreeView>，这些值用于为大小<xref:System.Windows.Controls.StackPanel>显示的对象<xref:System.Windows.Controls.TreeView>。 如果要显示的内容大于显示区域中，<xref:System.Windows.Controls.ScrollViewer>自动显示，以便用户可以滚动浏览<xref:System.Windows.Controls.TreeView>内容。  
  
 若要自定义的外观<xref:System.Windows.Controls.TreeViewItem>控件，将<xref:System.Windows.FrameworkElement.Style%2A>属性设置为自定义<xref:System.Windows.Style>。  
  
 下面的示例演示如何设置<xref:System.Windows.Controls.Control.Foreground%2A>并<xref:System.Windows.Controls.Control.FontSize%2A>属性值的<xref:System.Windows.Controls.TreeViewItem>控件中的使用<xref:System.Windows.FrameworkElement.Style%2A>。  
  
 [!code-xaml[TreeViewSimple#8](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#8)]  
  
<a name="Adding_Images_and_oOther_Content_to_TreeView_Items"></a>   
## <a name="adding-images-and-other-content-to-treeview-items"></a>向 TreeView 项添加图像和其他内容  
 可以包含多个对象中的<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>内容的<xref:System.Windows.Controls.TreeViewItem>。 若要包括在多个对象<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>内容，如将括在布局控件内的对象<xref:System.Windows.Controls.Panel>或<xref:System.Windows.Controls.StackPanel>。  
  
 下面的示例演示如何定义<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>的<xref:System.Windows.Controls.TreeViewItem>作为<xref:System.Windows.Controls.CheckBox>并<xref:System.Windows.Controls.TextBlock>，括在<xref:System.Windows.Controls.DockPanel>控件。  
  
 [!code-xaml[TreeViewSnips#TVIHeader](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSnips/CSharp/Window1.xaml#tviheader)]  
  
 下面的示例演示如何定义<xref:System.Windows.DataTemplate>，其中包含<xref:System.Windows.Controls.Image>和一个<xref:System.Windows.Controls.TextBlock>括在<xref:System.Windows.Controls.DockPanel>控件。 可以使用<xref:System.Windows.DataTemplate>若要设置<xref:System.Windows.Controls.HeaderedItemsControl.HeaderTemplate%2A>或<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>为<xref:System.Windows.Controls.TreeViewItem>。  
  
 [!code-xaml[TreeViewDataBinding#6](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewDataBinding/CSharp/Window1.xaml#6)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.TreeView>
- <xref:System.Windows.Controls.TreeViewItem>
- [帮助主题](treeview-how-to-topics.md)
- [WPF 内容模型](wpf-content-model.md)
