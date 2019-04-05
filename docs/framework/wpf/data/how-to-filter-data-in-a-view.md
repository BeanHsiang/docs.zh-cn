---
title: 如何：筛选视图中的数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- views [WPF], filtering data
- filtering data in views [WPF]
- data binding [WPF], filtering data in views
ms.assetid: c76e8606-4cc4-45a8-9110-e2ec66dc6afd
ms.openlocfilehash: 51f95834556153448d416157460cf63da0d409e1
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373941"
---
# <a name="how-to-filter-data-in-a-view"></a>如何：筛选视图中的数据
此示例演示如何对视图中的数据进行筛选。  
  
## <a name="example"></a>示例  
 若要创建筛选器，需要定义提供筛选逻辑的方法。 该方法用作回调，接受 `object` 类型的参数。 以下方法将返回所有 `filled` 属性设置为"No"的 `Order` 对象，同时过滤掉其他的对象。  
  
 [!code-csharp[SortFilter#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#2)]
 [!code-vb[SortFilter#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#2)]  
  
 然后可以应用筛选器，如下面的示例中所示。 在此示例中，`myCollectionView`是 <xref:System.Windows.Data.ListCollectionView> 对象。  
  
 [!code-csharp[SortFilter#Filter](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#filter)]
 [!code-vb[SortFilter#Filter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#filter)]  
  
 若要撤销筛选，可以将 <xref:System.Windows.Data.CollectionView.Filter%2A> 属性设置为 `null`：  
  
 [!code-csharp[SortFilter#Unfilter](~/samples/snippets/csharp/VS_Snippets_Wpf/SortFilter/CSharp/Page1.xaml.cs#unfilter)]
 [!code-vb[SortFilter#Unfilter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SortFilter/VisualBasic/Page1.xaml.vb#unfilter)]  
  
 有关如何创建或获取视图的信息，请参阅[获取数据集合的默认视图](how-to-get-the-default-view-of-a-data-collection.md)。 有关完整示例，请参阅[对视图中的项目进行排序和筛选的示例](https://go.microsoft.com/fwlink/?LinkID=160040)。  
  
 如果视图对象是一个 <xref:System.Windows.Data.CollectionViewSource> 对象，可以通过设置 <xref:System.Windows.Data.CollectionViewSource.Filter> 事件的事件处理程序来应用筛选逻辑。 在以下示例中，`listingDataView` 是 <xref:System.Windows.Data.CollectionViewSource> 的一个实例。  
  
 [!code-csharp[DataBindingLab#10](~/samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#10)]
 [!code-vb[DataBindingLab#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#10)]  
  
 下面展示了如何实现示例筛选器 `ShowOnlyBargainsFilter` 的事件处理程序。 此事件处理程序使用 <xref:System.Windows.Data.FilterEventArgs.Accepted%2A> 属性来过滤掉 `CurrentPrice` 至少为 25 美元的 `AuctionItem` 对象。  
  
 [!code-csharp[DataBindingLab#5](~/samples/snippets/csharp/VS_Snippets_Wpf/DataBindingLab/CSharp/MainWindow.xaml.cs#5)]
 [!code-vb[DataBindingLab#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataBindingLab/VisualBasic/MainWindow.xaml.vb#5)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Data.CollectionView.CanFilter%2A>
- <xref:System.Windows.Data.BindingListCollectionView.CustomFilter%2A>
- [数据绑定概述](data-binding-overview.md)
- [在视图中对数据进行排序](how-to-sort-data-in-a-view.md)
- [帮助主题](data-binding-how-to-topics.md)
