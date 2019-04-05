---
title: 如何：将 TreeView 绑定到深度无法确定的数据
ms.date: 03/30/2017
helpviewer_keywords:
- TreeView control [WPF], binding to data of indeterminate depth
ms.assetid: daddcd74-1b0f-4ffd-baeb-ec934c5e0f53
ms.openlocfilehash: 6c0361674c4f6f740784a7657e018d5257c6edac
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377231"
---
# <a name="how-to-bind-a-treeview-to-data-that-has-an-indeterminable-depth"></a>如何：将 TreeView 绑定到深度无法确定的数据
可能存在你想要将绑定<xref:System.Windows.Controls.TreeView>与数据源不知道其深度。  这可能的数据时递归性质，例如文件系统，其中的文件夹可以包含文件夹或公司的组织结构，其中员工具有作为直接下属的其他员工。  
  
 数据源必须具有一个分层对象模型。 例如，`Employee`类可能包含一系列 Employee 对象的直接下属的员工。 如果不是分层的方式表示数据，则必须生成数据的分层表示形式。  
  
 当您将设置<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A?displayProperty=nameWithType>属性，如果<xref:System.Windows.Controls.ItemsControl>生成<xref:System.Windows.Controls.ItemsControl>每个子项，则子<xref:System.Windows.Controls.ItemsControl>使用相同<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>作为父级。 例如，如果您设置<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>属性数据绑定<xref:System.Windows.Controls.TreeView>，则每个<xref:System.Windows.Controls.TreeViewItem>，它是生成的使用<xref:System.Windows.DataTemplate>的已分配给<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>属性<xref:System.Windows.Controls.TreeView>。  
  
 <xref:System.Windows.HierarchicalDataTemplate> ，可指定<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>有关<xref:System.Windows.Controls.TreeViewItem>，或任何<xref:System.Windows.Controls.HeaderedItemsControl>，数据模板。 当您将设置<xref:System.Windows.HierarchicalDataTemplate.ItemsSource%2A?displayProperty=nameWithType>属性的值时使用<xref:System.Windows.HierarchicalDataTemplate>应用。 通过使用<xref:System.Windows.HierarchicalDataTemplate>，你可以以递归方式集<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>每个<xref:System.Windows.Controls.TreeViewItem>中<xref:System.Windows.Controls.TreeView>。  
  
## <a name="example"></a>示例  
 下面的示例演示如何将绑定<xref:System.Windows.Controls.TreeView>到层次结构数据，使用<xref:System.Windows.HierarchicalDataTemplate>来指定<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>为每个<xref:System.Windows.Controls.TreeViewItem>。  <xref:System.Windows.Controls.TreeView>将绑定到表示员工的公司中的 XML 数据。  每个`Employee`元素可以包含其他`Employee`元素，以指示隶属关系。 由于数据是递归的<xref:System.Windows.HierarchicalDataTemplate>可以应用于每个级别。  
  
 [!code-xaml[TreeViewWithUnknownDepth#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewWithUnknownDepth/CS/Window1.xaml#1)]  
  
## <a name="see-also"></a>请参阅
- [数据绑定概述](../data/data-binding-overview.md)
- [数据模板化概述](../data/data-templating-overview.md)
