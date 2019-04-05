---
title: 如何：在数据网格中的数据进行分组、 排序和筛选器控制
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], sort
- DataGrid [WPF], group
- DataGrid [WPF], filter
ms.assetid: 03345e85-89e3-4aec-9ed0-3b80759df770
ms.openlocfilehash: 81fdb0a6d5602f612c55d7e790ca9a0fe56c144e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365043"
---
# <a name="how-to-group-sort-and-filter-data-in-the-datagrid-control"></a>如何：分组、 排序和筛选的 DataGrid 控件中的数据

通常很有用，若要查看中的数据<xref:System.Windows.Controls.DataGrid>分组、 排序和筛选的数据通过不同的方式。 若要进行分组、 排序和筛选器中的数据<xref:System.Windows.Controls.DataGrid>，你将其绑定到<xref:System.Windows.Data.CollectionView>支持这些函数。 然后可以使用中的数据<xref:System.Windows.Data.CollectionView>而不会影响基础数据源。 集合视图中的更改会反映在<xref:System.Windows.Controls.DataGrid>用户界面 (UI)。

<xref:System.Windows.Data.CollectionView>类提供了分组和排序功能，实现为数据源<xref:System.Collections.IEnumerable>接口。 <xref:System.Windows.Data.CollectionViewSource>类，可设置的属性<xref:System.Windows.Data.CollectionView>从 XAML。

在此示例中，一系列`Task`对象绑定到<xref:System.Windows.Data.CollectionViewSource>。 <xref:System.Windows.Data.CollectionViewSource>用作<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>为<xref:System.Windows.Controls.DataGrid>。 在执行分组、 排序和筛选<xref:System.Windows.Data.CollectionViewSource>，并显示在<xref:System.Windows.Controls.DataGrid>UI。

![数据网格中的数据进行分组](././media/wpf-datagridgroups.png "WPF_DataGridGroups")分组数据网格中的数据

## <a name="using-a-collectionviewsource-as-an-itemssource"></a>CollectionViewSource 用作 ItemsSource

为进行分组、 排序和筛选器中的数据<xref:System.Windows.Controls.DataGrid>控件，您将绑定<xref:System.Windows.Controls.DataGrid>到<xref:System.Windows.Data.CollectionView>支持这些函数。 在此示例中，<xref:System.Windows.Controls.DataGrid>绑定到<xref:System.Windows.Data.CollectionViewSource>，它提供有关这些函数<xref:System.Collections.Generic.List%601>的`Task`对象。

### <a name="to-bind-a-datagrid-to-a-collectionviewsource"></a>若要将 DataGrid 绑定到 CollectionViewSource，

1. 创建的数据集合的实现<xref:System.Collections.IEnumerable>接口。

    如果您使用<xref:System.Collections.Generic.List%601>若要创建你的集合，应创建的新类继承自<xref:System.Collections.Generic.List%601>而不是实例化的实例<xref:System.Collections.Generic.List%601>。 这可以将数据绑定到 XAML 中的集合。

    > [!NOTE]
    > 集合中的对象必须实现<xref:System.ComponentModel.INotifyPropertyChanged>已更改的接口和<xref:System.ComponentModel.IEditableObject>接口，以便<xref:System.Windows.Controls.DataGrid>以正确响应属性更改和编辑。 有关详细信息，请参阅[实现属性更改通知](../data/how-to-implement-property-change-notification.md)。

    [!code-csharp[DataGrid_GroupSortFilter#101](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#101)]
    [!code-vb[DataGrid_GroupSortFilter#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#101)]

2. 在 XAML 中，创建集合类的实例并设置[X:key 指令](../../xaml-services/x-key-directive.md)。

3. 在 XAML 中，创建的实例<xref:System.Windows.Data.CollectionViewSource>类中，设置[X:key 指令](../../xaml-services/x-key-directive.md)，并将设置为你的集合类的实例<xref:System.Windows.Data.CollectionViewSource.Source%2A>。

    [!code-xaml[DataGrid_GroupSortFilter#201](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml#201)]

4. 创建的实例<xref:System.Windows.Controls.DataGrid>类，并设置<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>属性设置为<xref:System.Windows.Data.CollectionViewSource>。

    [!code-xaml[DataGrid_GroupSortFilter#002](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#002)]

5. 访问<xref:System.Windows.Data.CollectionViewSource>在代码中，使用<xref:System.Windows.Data.CollectionViewSource.GetDefaultView%2A>方法以获取对引用<xref:System.Windows.Data.CollectionViewSource>。

    [!code-csharp[DataGrid_GroupSortFilter#102](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#102)]
    [!code-vb[DataGrid_GroupSortFilter#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#102)]

## <a name="grouping-items-in-a-datagrid"></a>对数据网格中的项进行分组

若要指定项中的分组方式<xref:System.Windows.Controls.DataGrid>，则使用<xref:System.Windows.Data.PropertyGroupDescription>类型在源视图中的项进行分组。

### <a name="to-group-items-in-a-datagrid-using-xaml"></a>使用 XAML 的 DataGrid 中的项

1. 创建<xref:System.Windows.Data.PropertyGroupDescription>指定分组所依据的属性。 在 XAML 或代码中，可以指定属性。

   1. 在 XAML 中，设置<xref:System.Windows.Data.PropertyGroupDescription.PropertyName%2A>分组所依据的属性的名称。

   2. 在代码中，将传递到构造函数分组依据的属性的名称。

2. 添加<xref:System.Windows.Data.PropertyGroupDescription>到<xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A?displayProperty=nameWithType>集合。

3. 添加的其他实例<xref:System.Windows.Data.PropertyGroupDescription>到<xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A>集合添加更多级别的分组。

    [!code-xaml[DataGrid_GroupSortFilter#012](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#012)]
    [!code-csharp[DataGrid_GroupSortFilter#112](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#112)]
    [!code-vb[DataGrid_GroupSortFilter#112](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#112)]

4. 若要删除某个组，请删除<xref:System.Windows.Data.PropertyGroupDescription>从<xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A>集合。

5. 若要删除的所有组，请调用<xref:System.Collections.ObjectModel.Collection%601.Clear%2A>方法的<xref:System.Windows.Data.CollectionViewSource.GroupDescriptions%2A>集合。

    [!code-csharp[DataGrid_GroupSortFilter#114](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#114)]
    [!code-vb[DataGrid_GroupSortFilter#114](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#114)]

项中的分组时<xref:System.Windows.Controls.DataGrid>，可以定义<xref:System.Windows.Controls.GroupStyle>，它指定每个组的外观。 您将应用<xref:System.Windows.Controls.GroupStyle>通过将其添加到<xref:System.Windows.Controls.ItemsControl.GroupStyle%2A>DataGrid 的集合。 如果有多个级别的分组，可以将不同的样式应用到每个分组级别。 样式中定义的顺序应用。 例如，如果定义了两种样式，第一个将应用于顶级行组。 第二个样式将应用于在第二个级别的所有行组和更低版本。 <xref:System.Windows.FrameworkElement.DataContext%2A>的<xref:System.Windows.Controls.GroupStyle>是<xref:System.Windows.Data.CollectionViewGroup>组表示。

### <a name="to-change-the-appearance-of-row-group-headers"></a>若要更改的行组标题的外观

1. 创建<xref:System.Windows.Controls.GroupStyle>定义行组的外观。

2. 将放<xref:System.Windows.Controls.GroupStyle>内`<DataGrid.GroupStyle>`标记。

    [!code-xaml[DataGrid_GroupSortFilter#003](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#003)]

## <a name="sorting-items-in-a-datagrid"></a>数据网格中的项进行排序

若要指定项中的排序方式<xref:System.Windows.Controls.DataGrid>，则使用<xref:System.ComponentModel.SortDescription>类型在源视图中的项进行排序。

### <a name="to-sort-items-in-a-datagrid"></a>数据网格中的项进行排序

1. 创建<xref:System.ComponentModel.SortDescription>，它指定要作为排序依据的属性。 在 XAML 或代码中，可以指定属性。

    1. 在 XAML 中，设置<xref:System.ComponentModel.SortDescription.PropertyName%2A>为要作为排序依据的属性的名称。

    2. 在代码中，传递要作为排序依据的属性名称和<xref:System.ComponentModel.ListSortDirection>到构造函数。

2. 添加<xref:System.ComponentModel.SortDescription>到<xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A?displayProperty=nameWithType>集合。

3. 添加的其他实例<xref:System.ComponentModel.SortDescription>到<xref:System.Windows.Data.CollectionViewSource.SortDescriptions%2A>若要按其他属性的集合。

    [!code-xaml[DataGrid_GroupSortFilter#011](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#011)]
    [!code-csharp[DataGrid_GroupSortFilter#211](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/WindowSnips1.xaml.cs#211)]
    [!code-vb[DataGrid_GroupSortFilter#211](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#211)]

## <a name="filtering-items-in-a-datagrid"></a>筛选数据网格中的项

筛选器中的项<xref:System.Windows.Controls.DataGrid>使用<xref:System.Windows.Data.CollectionViewSource>，提供的处理程序中的筛选逻辑<xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=nameWithType>事件。

### <a name="to-filter-items-in-a-datagrid"></a>若要筛选数据网格中的项

1. 添加的处理程序<xref:System.Windows.Data.CollectionViewSource.Filter?displayProperty=nameWithType>事件。

2. 在<xref:System.Windows.Data.CollectionViewSource.Filter>事件处理程序，定义筛选逻辑。

    每次刷新该视图时，将应用筛选器。

    [!code-xaml[DataGrid_GroupSortFilter#013](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#013)]
    [!code-csharp[DataGrid_GroupSortFilter#113](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#113)]
    [!code-vb[DataGrid_GroupSortFilter#113](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#113)]

或者，可以筛选中的项<xref:System.Windows.Controls.DataGrid>通过创建提供筛选逻辑和设置方法<xref:System.Windows.Data.CollectionView.Filter%2A?displayProperty=nameWithType>应用该筛选器的属性。 若要查看此方法的示例，请参阅[视图中的筛选器数据](../data/how-to-filter-data-in-a-view.md)。

## <a name="example"></a>示例

下面的示例演示分组、 排序和筛选`Task`中的数据<xref:System.Windows.Data.CollectionViewSource>并显示经过分组、 排序和筛选`Task`中的数据<xref:System.Windows.Controls.DataGrid>。 <xref:System.Windows.Data.CollectionViewSource>用作<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>为<xref:System.Windows.Controls.DataGrid>。 在执行分组、 排序和筛选<xref:System.Windows.Data.CollectionViewSource>，并显示在<xref:System.Windows.Controls.DataGrid>UI。

若要测试此示例中，你将需要调整 DGGroupSortFilterExample 名称以匹配你的项目名称。 如果使用的 Visual Basic，您需要更改的类名<xref:System.Windows.Window>所示。

`<Window x:Class="MainWindow"`

[!code-xaml[DataGrid_GroupSortFilter#000](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml#000)]
[!code-csharp[DataGrid_GroupSortFilter#100](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_GroupSortFilter/CS/MainWindow.xaml.cs#100)]
[!code-vb[DataGrid_GroupSortFilter#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_GroupSortFilter/VB/MainWindow.xaml.vb#100)]

## <a name="see-also"></a>请参阅

- [数据绑定概述](../data/data-binding-overview.md)
- [创建和绑定到 ObservableCollection](../data/how-to-create-and-bind-to-an-observablecollection.md)
- [在视图中筛选数据](../data/how-to-filter-data-in-a-view.md)
- [在视图中对数据进行排序](../data/how-to-sort-data-in-a-view.md)
- [在 XAML 中使用视图对数据进行排序和分组](../data/how-to-sort-and-group-data-using-a-view-in-xaml.md)
