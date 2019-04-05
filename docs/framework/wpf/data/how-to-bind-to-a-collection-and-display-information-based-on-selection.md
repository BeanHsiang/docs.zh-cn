---
title: 如何：绑定到集合并基于选择显示信息
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data collections [WPF], selecting data for views
- data binding [WPF], creating views of data collections
- data binding [WPF], selecting data for views
- data binding [WPF], binding to collections
ms.assetid: 952a7d76-dd29-49e5-86f5-32c4530e70eb
ms.openlocfilehash: 5ceda723ad982fc788e8d0b81e6cf92975790682
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360389"
---
# <a name="how-to-bind-to-a-collection-and-display-information-based-on-selection"></a>如何：绑定到集合并基于选择显示信息
在简单的母版-详细信息方案中，具有数据绑定<xref:System.Windows.Controls.ItemsControl>如<xref:System.Windows.Controls.ListBox>。 基于用户所选内容上，显示有关选定项的详细信息。 此示例演示如何实现此方案。  
  
## <a name="example"></a>示例  
 在此示例中，`People` 是 `Person` 类的 <xref:System.Collections.ObjectModel.ObservableCollection%601>。 `Person` 类包含三个属性：`FirstName`、`LastName` 和 `HomeTown`，类型均为 `string`。  
  
 [!code-xaml[CollectionBinding#Source](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#source)]  
[!code-xaml[CollectionBinding#UI](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#ui)]  
  
 <xref:System.Windows.Controls.ContentControl> 使用以下 <xref:System.Windows.DataTemplate>，它定义了 `Person` 信息的显示方式：  
  
 [!code-xaml[CollectionBinding#DetailTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Window1.xaml#detailtemplate)]  
  
 下面是该示例生成的屏幕截图。 <xref:System.Windows.Controls.ContentControl> 显示选中人员的其他属性。  
  
 ![绑定到集合](./media/databinding-collectionbindingsample.png "DataBinding_CollectionBindingSample")  
  
 在此示例中，需要注意两个事项：  
  
1.  <xref:System.Windows.Controls.ListBox> 和 <xref:System.Windows.Controls.ContentControl> 将绑定到相同的源。 两个绑定的 <xref:System.Windows.Data.Binding.Path%2A> 属性都没有指定，因为这两个控件都绑定到整个集合对象。  
  
2.  必须将 <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> 属性设置为 `true` 才能使其生效。 设置此属性可确保所选的项始终设置为 <xref:System.Windows.Controls.ItemCollection.CurrentItem%2A>。 或者，如果 <xref:System.Windows.Controls.ListBox> 从 <xref:System.Windows.Data.CollectionViewSource> 获取数据，它将自动同步所选内容和货币。  
  
 需要注意，`Person` 类将按以下方式重写 `ToString` 方法。 默认情况下，<xref:System.Windows.Controls.ListBox> 会调用 `ToString` 并以字符串形式显示绑定集合中的每个对象。 这就是每个 `Person` 在 <xref:System.Windows.Controls.ListBox> 中显示为名字的原因。  
  
 [!code-csharp[CollectionBinding#ToString](~/samples/snippets/csharp/VS_Snippets_Wpf/CollectionBinding/CSharp/Data.cs#tostring)]
 [!code-vb[CollectionBinding#ToString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CollectionBinding/VisualBasic/Person.vb#tostring)]  
  
## <a name="see-also"></a>请参阅
- [将主-详细模式与分层数据结合使用](how-to-use-the-master-detail-pattern-with-hierarchical-data.md)
- [将主-详细模式与分层 XML 数据结合使用](how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)
- [数据绑定概述](data-binding-overview.md)
- [数据模板化概述](data-templating-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
