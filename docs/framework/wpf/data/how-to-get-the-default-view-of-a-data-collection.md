---
title: 如何：获取数据集合的默认视图
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data collections [WPF], creating views of
- data binding [WPF], creating views of data collections
ms.assetid: b641e96c-c2f6-42ea-9c5d-bac81176ad65
ms.openlocfilehash: 28a21aae7f8a08efebfd16bacd2a2d82b04de0c1
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360064"
---
# <a name="how-to-get-the-default-view-of-a-data-collection"></a>如何：获取数据集合的默认视图
可以通过视图以不同的方式查看同一数据集合，具体取决于排序、筛选或分组规则。 每个集合都有一个共享的默认视图，在绑定指定一个集合作为其源时用作实际绑定源。 此示例演示如何获取集合的默认视图。  
  
## <a name="example"></a>示例  
 若要创建视图，需要一个针对该集合的对象引用。 可以通过引用自己的代码隐藏对象、获取数据上下文、获取数据源属性、获取绑定属性的方式来获得该数据对象。 此示例演示如何获取数据对象的 <xref:System.Windows.FrameworkElement.DataContext%2A> 并使用它来直接获取该集合的默认集合视图。  
  
 [!code-csharp[CollectionView#2](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml.cs#2)]
 [!code-vb[CollectionView#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionView/VisualBasic/Page1.xaml.vb#2)]  
  
 在此示例中，根元素是 <xref:System.Windows.Controls.StackPanel>。 <xref:System.Windows.FrameworkElement.DataContext%2A> 设置为 *myDataSource*，它引用的数据提供程序是 *Order* 对象的 <xref:System.Collections.ObjectModel.ObservableCollection%601>。  
  
 [!code-xaml[CollectionView#CollectionViewDataContext](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionView/CSharp/Page1.xaml#collectionviewdatacontext)]  
  
 也可使用 <xref:System.Windows.Data.CollectionViewSource> 类实例化你自己的集合视图并将内容绑定到它。 此集合视图仅由直接绑定到它的控件共享。 有关示例，请参阅[数据绑定概述](data-binding-overview.md)中的“如何创建视图”部分。  
  
 有关集合视图提供的功能的示例，请参阅[在视图中对数据进行排序](how-to-sort-data-in-a-view.md)、[在视图中筛选数据](how-to-filter-data-in-a-view.md)和[在数据 CollectionView 中的对象之间导航](how-to-navigate-through-the-objects-in-a-data-collectionview.md)。  
  
## <a name="see-also"></a>请参阅
- [在 XAML 中使用视图对数据进行排序和分组](how-to-sort-and-group-data-using-a-view-in-xaml.md)
- [帮助主题](data-binding-how-to-topics.md)
