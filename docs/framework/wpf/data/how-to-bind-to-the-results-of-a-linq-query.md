---
title: 如何：绑定到 LINQ 查询的结果
ms.date: 03/30/2017
helpviewer_keywords:
- running a LINQ query [WPF], bind to results
- binding to LINQ query results [WPF]
ms.assetid: ff2844d9-17ed-4ea6-aab1-5111af0bc684
ms.openlocfilehash: 9be0f95824c97456b50996f9cd6f010442b523f2
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355943"
---
# <a name="how-to-bind-to-the-results-of-a-linq-query"></a>如何：绑定到 LINQ 查询的结果
此示例演示如何运行 LINQ 查询，然后绑定到结果。  
  
## <a name="example"></a>示例  
 以下示例创建两个列表框。 第一个列表框包含三个列表项。  
  
 [!code-xaml[LinqExample#UI](~/samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml#ui)]  
  
 从第一个列表框中选择一项即可调用以下事件处理程序。 在此示例中，`Tasks` 是一系列 `Task` 对象。 `Task` 类有一个名为 `Priority` 的属性。 此事件处理程序会运行 LINQ 查询，返回具有所选优先级值的 `Task` 对象集合，然后将其设置为 <xref:System.Windows.FrameworkElement.DataContext%2A>:  
  
 [!code-csharp[LinqExample#Using](~/samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#using)]  
[!code-csharp[LinqExample#Tasks](~/samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#tasks)]  
[!code-csharp[LinqExample#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/LinqExample/CSharp/Window1.xaml.cs#handler)]  
  
 第二个列表框将绑定到该集合，因为其 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 值设置为 `{Binding}`。 因此，它将显示返回的集合（基于 `myTaskTemplate` <xref:System.Windows.DataTemplate>）。  
  
## <a name="see-also"></a>请参阅
- [让数据可供 XAML 中的绑定使用](how-to-make-data-available-for-binding-in-xaml.md)
- [绑定到集合并根据选择的内容显示信息](how-to-bind-to-a-collection-and-display-information-based-on-selection.md)
- [WPF 版本 4.5 中的新增功能](../getting-started/whats-new.md)
- [数据绑定概述](data-binding-overview.md)
- [帮助主题](data-binding-how-to-topics.md)
