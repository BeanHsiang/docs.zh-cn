---
title: 如何：处理 ContextMenuOpening 事件
ms.date: 03/30/2017
helpviewer_keywords:
- ContextMenuOpening properties [WPF]
ms.assetid: 789652fb-1951-4217-934a-7843e355adf4
ms.openlocfilehash: 077a28f345b886fd9ec183b5828c0535ce688cb4
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364835"
---
# <a name="how-to-handle-the-contextmenuopening-event"></a>如何：处理 ContextMenuOpening 事件
<xref:System.Windows.FrameworkElement.ContextMenuOpening>应用程序可以调整现有的上下文菜单之前来显示或禁止显示本应通过设置中显示的菜单中，可以处理事件<xref:System.Windows.RoutedEventArgs.Handled%2A>属性设置为`true`事件数据中。 设置的典型原因<xref:System.Windows.RoutedEventArgs.Handled%2A>到`true`在事件数据将替换为菜单完全新<xref:System.Windows.Controls.ContextMenu>对象，这有时需要取消该操作并启动新打开的。 如果您编写的处理程序<xref:System.Windows.FrameworkElement.ContextMenuOpening>事件，您应注意的计时问题之间<xref:System.Windows.Controls.ContextMenu>控件和服务，它负责打开和一般情况下定位控件的上下文菜单。 本主题演示了其中一些各种上下文菜单打开方案的代码技术，并说明了计时问题派上用场的事例。  
  
 有几种方案用于处理<xref:System.Windows.FrameworkElement.ContextMenuOpening>事件：  
  
-   调整之前显示的菜单项。  
  
-   替换为在显示之前的整个菜单。  
  
-   完全禁止显示任何现有的上下文菜单，并不显示任何上下文菜单。  
  
## <a name="example"></a>示例  
  
## <a name="adjusting-the-menu-items-before-display"></a>调整之前显示的菜单项  
 调整现有的菜单项是相当简单，可能是最常见的方案。 您可以这样做才能添加或减少以响应在应用程序中的当前状态信息或可用作其中请求的上下文菜单的对象的属性的特定状态信息的上下文菜单选项。  
  
 一般的方法是获取事件的来源，这是我们右键单击特定控件，并获取<xref:System.Windows.FrameworkElement.ContextMenu%2A>从它的属性。 你通常想要检查<xref:System.Windows.Controls.ItemsControl.Items%2A>集合，以查看哪些上下文菜单项已存在在菜单中，然后添加或删除相应的新<xref:System.Windows.Controls.MenuItem>到或从集合中的项。  
  
 [!code-csharp[ContextMenuOpeningHandlers#AddItemNoHandle](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#additemnohandle)]  
  
## <a name="replacing-the-entire-menu-before-display"></a>替换为在显示之前的整个菜单  
 另一种方案是如果你想要替换整个上下文菜单。 您无法当然也使用上述代码中，一种变体删除每个现有的上下文菜单项并添加新的从零项开始。 但更直观的方法，用于更换的上下文菜单中的所有项是创建一个新<xref:System.Windows.Controls.ContextMenu>，其中填充项，并将<xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType>为这个新的控件属性<xref:System.Windows.Controls.ContextMenu>。  
  
 以下是用于替换的简单的处理程序代码<xref:System.Windows.Controls.ContextMenu>。 该代码引用自定义`BuildMenu`方法，它分隔出这是因为多个示例处理程序之一。  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceNoReopen](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacenoreopen)]  
  
 [!code-csharp[ContextMenuOpeningHandlers#BuildMenu](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#buildmenu)]  
  
 但是，如果使用的处理程序的此样式<xref:System.Windows.FrameworkElement.ContextMenuOpening>，您可能可以公开计时问题，如果您设置的对象<xref:System.Windows.Controls.ContextMenu>没有预先存在的上下文菜单。 在用户右键单击一个控件，当<xref:System.Windows.FrameworkElement.ContextMenuOpening>引发即使现有<xref:System.Windows.Controls.ContextMenu>为空或 null。 但在这种情况下，任何新<xref:System.Windows.Controls.ContextMenu>对源设置元素太晚到达要显示。 此外，如果用户要用鼠标右键单击第二次，这一次新<xref:System.Windows.Controls.ContextMenu>出现，则该值为非 null 和您的处理程序将正确替换和第二次运行该处理程序时显示菜单。 这表明两个可能的解决方法：  
  
1.  确保<xref:System.Windows.FrameworkElement.ContextMenuOpening>处理程序对具有至少一个占位符控件始终运行<xref:System.Windows.Controls.ContextMenu>可用，其中你想要替换为处理程序代码。 在这种情况下，仍可以使用上一示例所示的处理程序，但你通常想要分配一个占位符<xref:System.Windows.Controls.ContextMenu>初始标记中：  
  
     [!code-xaml[ContextMenuOpeningHandlers#XAMLWithInitCM](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml#xamlwithinitcm)]  
  
2.  假设初始<xref:System.Windows.Controls.ContextMenu>值可能为 null，根据一些初步的逻辑。 你可以选中复选<xref:System.Windows.Controls.ContextMenu>为 null 或使用代码以检查是否已被您的处理程序中的标志至少运行一次。 因为你假设<xref:System.Windows.Controls.ContextMenu>有关是要显示，您的处理程序，然后设置<xref:System.Windows.RoutedEventArgs.Handled%2A>到`true`事件数据中。 向<xref:System.Windows.Controls.ContextMenuService>，它负责显示上下文菜单中，`true`值<xref:System.Windows.RoutedEventArgs.Handled%2A>数据在事件表示取消的显示上下文菜单 / 控件组合，用于引发事件的请求。  
  
 现在，你已阻止的潜在可疑的上下文菜单下, 一步是提供一个新的活动，然后将其显示。 设置新的其中一个是基本上与上一个处理程序相同： 生成一个新<xref:System.Windows.Controls.ContextMenu>，然后设置控制源<xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType>与它的属性。 其他步骤是您现在必须强制显示的上下文菜单中，因为禁止显示第一次尝试。 若要强制显示，则设置<xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A?displayProperty=nameWithType>属性设置为`true`处理程序中。 谨慎执行此操作，因为在处理程序中打开上下文菜单引发<xref:System.Windows.FrameworkElement.ContextMenuOpening>再次事件。 如果你重新输入您的处理程序，它将无限递归。 这就是原因，始终需要检查`null`或使用一个标志，如果在打开一个上下文菜单<xref:System.Windows.FrameworkElement.ContextMenuOpening>事件处理程序。  
  
## <a name="suppressing-any-existing-context-menu-and-displaying-no-context-menu"></a>禁止显示任何现有的上下文菜单，不显示任何上下文菜单  
 最后一种情况下，编写完全，禁止显示菜单处理程序并不常见。 如果给定的控件不应显示上下文菜单，有可能更合适的方法，以确保这比只是当用户请求其禁止显示菜单。 但如果你想要使用的处理程序来取消上下文菜单，并不显示任何内容，则只需将您的处理程序应设置<xref:System.Windows.RoutedEventArgs.Handled%2A>到`true`事件数据中。 <xref:System.Windows.Controls.ContextMenuService> ，负责显示上下文菜单将检查它在控件引发的事件的事件数据。 如果事件被标记为<xref:System.Windows.RoutedEventArgs.Handled%2A>任意位置路由，然后启动了事件的上下文菜单打开操作被取消。  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceReopen](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacereopen)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.ContextMenu>
- <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType>
- [基元素概述](base-elements-overview.md)
- [ContextMenu 概述](../controls/contextmenu-overview.md)
