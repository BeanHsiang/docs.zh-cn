---
title: 如何：将行详细信息添加到 DataGrid 控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataTemplate [WPF], DataGrid
- row details [WPF], DataGrid
- DataGrid [WPF], row details
ms.assetid: 0bdc6f50-9b4c-483f-9df6-a47a1fde998b
ms.openlocfilehash: 5976e834ca984a257e5562b2a3c8051f45575f5b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372186"
---
# <a name="how-to-add-row-details-to-a-datagrid-control"></a>如何：将行详细信息添加到 DataGrid 控件
当使用<xref:System.Windows.Controls.DataGrid>控件，您可以自定义数据表示通过添加行详细信息部分。 添加行详细信息部分，可根据需要可见还是折叠的模板中的某些数据进行分组。 例如，可以添加到行详细信息<xref:System.Windows.Controls.DataGrid>表示仅在每个行的数据的摘要<xref:System.Windows.Controls.DataGrid>，但当用户选择某一行时带来了更多数据字段。 定义用于行详细信息部分中的模板<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>属性。 下图显示行详细信息部分的示例。  
  
 ![显示行详细信息的 DataGrid](./media/ndp-rowdetails.png "NDP_RowDetails")  
  
 定义行详细信息模板为任一内联 XAML 或作为资源。 这两种方法所示的以下过程。 可以在整个项目使用一个数据模板，作为资源添加，而无需重新创建该模板。 一个数据模板，添加为内联 XAML 才可访问从控件定义位置。  
  
### <a name="to-display-row-details-by-using-inline-xaml"></a>若要使用内联 XAML 显示行详细信息  
  
1.  创建<xref:System.Windows.Controls.DataGrid>显示来自数据源的数据。  
  
2.  在 <xref:System.Windows.Controls.DataGrid> 元素内，添加一个 <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 元素。  
  
3.  创建<xref:System.Windows.DataTemplate>定义行详细信息部分的外观。  
  
     下面的 XAML 演示<xref:System.Windows.Controls.DataGrid>以及如何定义<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>内联。 <xref:System.Windows.Controls.DataGrid>显示三个值中的每一行和第三个更多的值时选择的行。  
  
     [!code-xaml[DataGrid_RowDetails#1](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml#1)]  
  
     下面的代码显示了用于选择中显示的数据的查询<xref:System.Windows.Controls.DataGrid>。 在此示例中，该查询从包含客户信息的实体选择数据。  
  
     [!code-csharp[DataGrid_RowDetails#2](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml.cs#2)]
     [!code-vb[DataGrid_RowDetails#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_rowdetails/vb/mainwindow.xaml.vb#2)]  
  
### <a name="to-display-row-details-by-using-a-resource"></a>若要使用资源显示行详细信息  
  
1.  创建<xref:System.Windows.Controls.DataGrid>显示来自数据源的数据。  
  
2.  添加<xref:System.Windows.FrameworkElement.Resources%2A>元素到根元素，如<xref:System.Windows.Window>控制或<xref:System.Windows.Controls.Page>控件，或添加<xref:System.Windows.Application.Resources%2A>元素<xref:System.Windows.Application>App.xaml （或 Application.xaml） 文件中的类。  
  
3.  在资源元素中，创建<xref:System.Windows.DataTemplate>定义行详细信息部分的外观。  
  
     下面的 XAML 演示<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>中定义<xref:System.Windows.Application>类。  
  
     [!code-xaml[DataGrid_RowDetails#3](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/app.xaml#3)]  
  
4.  上<xref:System.Windows.DataTemplate>，将[X:key 指令](../../xaml-services/x-key-directive.md)唯一标识数据模板的值。  
  
5.  在中<xref:System.Windows.Controls.DataGrid>元素中，设置<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>属性设置为前面步骤中定义的资源。 分配给资源作为静态资源。  
  
     下面的 XAML 演示<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A>属性设置为该资源上一示例中。  
  
     [!code-xaml[DataGrid_RowDetails#4](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/window2.xaml#4)]  
  
### <a name="to-set-visibility-and-prevent-horizontal-scrolling-for-row-details"></a>若要设置可见性并禁止水平滚动行详细信息  
  
1.  如果需要设置<xref:System.Windows.Controls.DataGrid.RowDetailsVisibilityMode%2A>属性设置为<xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode>值。  
  
     默认情况下，值设置为<xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.VisibleWhenSelected>。 可以将其设置为<xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Visible>若要显示的所有行的详细信息或<xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Collapsed>隐藏所有行的详细信息。  
  
2.  如果需要设置<xref:System.Windows.Controls.DataGrid.AreRowDetailsFrozen%2A>属性设置为`true`禁止行详细信息中水平滚动的部分。
