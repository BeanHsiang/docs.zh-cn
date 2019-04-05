---
title: 如何：在视图中对数据进行排序
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], sorting data in views
- data binding [WPF], grouping data in views
- grouping data in views [WPF]
- views [WPF], sorting data
- views [WPF], grouping data
- sorting data in views [WPF]
ms.assetid: f4c43578-01b7-4774-a953-acb95a13b94a
ms.openlocfilehash: 41ee5cded04559acac5e7270c5e1a2450c70a5aa
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377114"
---
# <a name="how-to-sort-data-in-a-view"></a>如何：在视图中对数据进行排序
本示例介绍如何在视图中对数据进行排序。  
  
## <a name="example"></a>示例  
 下面的示例创建了一个简单的 <xref:System.Windows.Controls.ListBox> 和一个 <xref:System.Windows.Controls.Button>:  
  
 [!code-xaml[ListBoxSort_snip#HowTo](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml#howto)]  
  
 按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序包含对 <xref:System.Windows.Controls.ListBox> 中的项进行降序排序的逻辑。 之所以可以这样做是因为以这种方式将对象添加到 <xref:System.Windows.Controls.ListBox> 实际是将它们添加到了 <xref:System.Windows.Controls.ListBox> 的 <xref:System.Windows.Controls.ItemCollection>，而 <xref:System.Windows.Controls.ItemCollection> 派生自 <xref:System.Windows.Data.CollectionView> 类。 如果用 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性将<xref:System.Windows.Controls.ListBox> 绑定到一个集合，也可以使用相同的技术进行排序。  
  
 [!code-csharp[ListBoxSort_snip#HowToCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml.cs#howtocode)]
 [!code-vb[ListBoxSort_snip#HowToCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxSort_snip/visualbasic/window1.xaml.vb#howtocode)]  
  
 只要有视图对象的引用，就可以使用相同的技术对其他集合视图的内容进行排序。 有关如何获取视图的示例，请参阅[获取数据集合的默认视图](how-to-get-the-default-view-of-a-data-collection.md)。 另一个示例请参阅[在单击标题时对 GridView 列进行排序](../controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)。 有关视图的详细信息，请参阅 [数据绑定概述](data-binding-overview.md)中的“绑定到集合”。  
  
 有关如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]中应用排序逻辑的示例，请参阅[在 XAML 中使用视图对数据进行排序和分组](how-to-sort-and-group-data-using-a-view-in-xaml.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Data.ListCollectionView.CustomSort%2A>
- [在单击标题时对 GridView 列进行排序](../controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)
- [数据绑定概述](data-binding-overview.md)
- [在视图中筛选数据](how-to-filter-data-in-a-view.md)
- [帮助主题](data-binding-how-to-topics.md)
