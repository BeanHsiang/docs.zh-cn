---
title: 如何：在 TreeView 中查找 TreeViewItem
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TreeView control [WPF], finding a TreeViewItem
- TreeViewItem [WPF], finding
ms.assetid: 72ecd40c-3939-4e01-b617-5e9daa6074d9
ms.openlocfilehash: c90db5312d58cfba18910f299386e2884fb36ce6
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360209"
---
# <a name="how-to-find-a-treeviewitem-in-a-treeview"></a>如何：在 TreeView 中查找 TreeViewItem
<xref:System.Windows.Controls.TreeView>控件提供了方便地显示分层数据。 如果你<xref:System.Windows.Controls.TreeView>绑定到数据源，<xref:System.Windows.Controls.TreeView.SelectedItem%2A>属性提供的简便方法，以便快速检索所选的数据对象。 通常，最好使用基础数据对象，但有时您可能需要以编程方式处理的数据包含<xref:System.Windows.Controls.TreeViewItem>。 例如，可能需要以编程方式展开<xref:System.Windows.Controls.TreeViewItem>，或选择不同的项在<xref:System.Windows.Controls.TreeView>。  
  
 若要查找<xref:System.Windows.Controls.TreeViewItem>，其中包含特定的数据对象，您必须遍历每个级别的<xref:System.Windows.Controls.TreeView>。 中的项<xref:System.Windows.Controls.TreeView>可以还虚拟化以提高性能。 在项可能虚拟化的情况下，您还必须认识到<xref:System.Windows.Controls.TreeViewItem>检查它是否包含数据对象。  
  
## <a name="example"></a>示例  
  
## <a name="description"></a>描述  
 以下示例将搜索<xref:System.Windows.Controls.TreeView>特定的对象并返回该对象的包含<xref:System.Windows.Controls.TreeViewItem>。 该示例确保每个<xref:System.Windows.Controls.TreeViewItem>实例化，以便可以搜索其子项。 如果此示例也适用于<xref:System.Windows.Controls.TreeView>不使用虚拟化的项。  
  
> [!NOTE]
>  下面的示例适用于任何<xref:System.Windows.Controls.TreeView>，而不考虑基础数据模型和搜索每个<xref:System.Windows.Controls.TreeViewItem>直到找到该对象。 具有更好的性能的另一个方法是搜索指定对象的数据模型、 跟踪的数据层次结构中的其位置，然后找到相应<xref:System.Windows.Controls.TreeViewItem>在<xref:System.Windows.Controls.TreeView>。 但是，具有更好的性能的技术需要了解数据模型，并且不能使用通用对于任何给定<xref:System.Windows.Controls.TreeView>。  
  
## <a name="code"></a>代码  
 [!code-csharp[TreeViewFindTVI#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[TreeViewFindTVI#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#1)]  
  
 前面的代码依赖于自定义<xref:System.Windows.Controls.VirtualizingStackPanel>公开一个名为方法`BringIntoView`。 下面的代码定义自定义<xref:System.Windows.Controls.VirtualizingStackPanel>。  
  
 [!code-csharp[TreeViewFindTVI#2](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml.cs#2)]
 [!code-vb[TreeViewFindTVI#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TreeViewFindTVI/VisualBasic/MainWindow.xaml.vb#2)]  
  
 以下 XAML 演示如何创建<xref:System.Windows.Controls.TreeView>，它使用自定义<xref:System.Windows.Controls.VirtualizingStackPanel>。  
  
 [!code-xaml[TreeViewFindTVI#3](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewFindTVI/CSharp/MainWindow.xaml#3)]  
  
## <a name="see-also"></a>请参阅
- [提升 TreeView 的性能](how-to-improve-the-performance-of-a-treeview.md)
