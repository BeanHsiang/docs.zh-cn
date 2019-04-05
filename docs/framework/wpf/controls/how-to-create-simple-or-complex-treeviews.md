---
title: 如何：创建简单或复杂的 TreeView
ms.date: 03/30/2017
helpviewer_keywords:
- TreeView control [WPF], creating
- Control class [WPF], TreeView [WPF], creating
ms.assetid: 1defbb78-b8e7-4c0e-b650-576453ac828d
ms.openlocfilehash: 9b19443c80818809122b0bbfc7c7dae7b4b40da5
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368903"
---
# <a name="how-to-create-simple-or-complex-treeviews"></a>如何：创建简单或复杂的 TreeView
此示例演示如何创建简单或复杂<xref:System.Windows.Controls.TreeView>控件。  
  
 一个<xref:System.Windows.Controls.TreeView>包含的层次结构<xref:System.Windows.Controls.TreeViewItem>控件，它们可以包含简单文本字符串和也更复杂的内容，如<xref:System.Windows.Controls.Button>控件或<xref:System.Windows.Controls.StackPanel>与嵌入的内容。 您可以显式定义<xref:System.Windows.Controls.TreeView>内容或数据源可以提供内容。 本主题提供了这些概念的示例。  
  
## <a name="example"></a>示例  
 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>的属性<xref:System.Windows.Controls.TreeViewItem>包含的内容的<xref:System.Windows.Controls.TreeView>显示该项。 一个<xref:System.Windows.Controls.TreeViewItem>还可以<xref:System.Windows.Controls.TreeViewItem>控件作为其子元素，您可以通过使用定义这些子元素<xref:System.Windows.Controls.ItemsControl.Items%2A>属性。  
  
 下面的示例演示如何显式定义<xref:System.Windows.Controls.TreeViewItem>通过设置内容<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>属性设置为文本字符串。  
  
 [!code-xaml[TreeViewSimple#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#1)]  
  
 下面的示例演示如何定义的子元素<xref:System.Windows.Controls.TreeViewItem>通过定义<xref:System.Windows.Controls.ItemsControl.Items%2A>的<xref:System.Windows.Controls.Button>控件。  
  
 [!code-xaml[TreeViewSimple#3](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#3)]  
  
 下面的示例演示如何创建<xref:System.Windows.Controls.TreeView>其中<xref:System.Windows.Data.XmlDataProvider>提供<xref:System.Windows.Controls.TreeViewItem>内容和<xref:System.Windows.HierarchicalDataTemplate>定义内容的外观。  
  
 [!code-xaml[TreeViewSimple#6](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#6)]  
  
 [!code-xaml[TreeViewSimple#7](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#7)]  
  
 [!code-xaml[TreeViewSimple#5](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#5)]  
  
 下面的示例演示如何创建<xref:System.Windows.Controls.TreeView>其中<xref:System.Windows.Controls.TreeViewItem>内容包含<xref:System.Windows.Controls.DockPanel>嵌入内容的控件。  
  
 [!code-xaml[TreeViewSimple#9](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewSimple/CS/Window1.xaml#9)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.TreeView>
- <xref:System.Windows.Controls.TreeViewItem>
- [TreeView 概述](treeview-overview.md)
- [帮助主题](treeview-how-to-topics.md)
