---
title: DataGrid 控件中的调整大小选项
ms.date: 03/30/2017
helpviewer_keywords:
- DataGrid control [WPF], sizing
- size [WPF], DataGrid
- automatically size DataGrid [WPF]
ms.assetid: 96a0e47e-b010-4302-98ef-2daac446d8db
ms.openlocfilehash: 38cd29720a885f10d093bdb4617c503c16402e6c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54672183"
---
# <a name="sizing-options-in-the-datagrid-control"></a>DataGrid 控件中的调整大小选项
各种选项来控制如何<xref:System.Windows.Controls.DataGrid>调整自身大小。 <xref:System.Windows.Controls.DataGrid>，以及各个行和列中的<xref:System.Windows.Controls.DataGrid>，可以设置为其内容自动调整大小，也可以设置为特定值。 默认情况下，<xref:System.Windows.Controls.DataGrid>将放大或缩小以适合其内容的大小。  
  
## <a name="sizing-the-datagrid"></a>大小调整数据网格  
  
### <a name="cautions-when-using-automatic-sizing"></a>使用自动大小调整时的注意事项  
 默认情况下<xref:System.Windows.FrameworkElement.Height%2A>并<xref:System.Windows.FrameworkElement.Width%2A>的属性<xref:System.Windows.Controls.DataGrid>设置为<xref:System.Double.NaN?displayProperty=nameWithType>("`Auto`"在 XAML 中)，和<xref:System.Windows.Controls.DataGrid>将调整其内容的大小。  
  
 当放置在不限制及其子项的大小，如容器内<xref:System.Windows.Controls.Canvas>或<xref:System.Windows.Controls.StackPanel>，则<xref:System.Windows.Controls.DataGrid>将拉伸到容器的可见的边框之外并且不会显示滚动条。 这种情况会影响可用性和性能。  
  
 当绑定到数据集，如果<xref:System.Windows.FrameworkElement.Height%2A>的<xref:System.Windows.Controls.DataGrid>是不受限制，它将继续添加绑定数据集中的每个数据项的行。 这可能会导致<xref:System.Windows.Controls.DataGrid>添加行时增加到超过您的应用程序的可见边界。 <xref:System.Windows.Controls.DataGrid>将不显示滚动条在这种情况下由于其<xref:System.Windows.FrameworkElement.Height%2A>将继续增大以容纳新行。  
  
 中的每一行创建一个对象<xref:System.Windows.Controls.DataGrid>。 如果你正在使用的大型数据集并且您允许<xref:System.Windows.Controls.DataGrid>自动调整自身大小，请创建大量对象可能会影响应用程序的性能。  
  
 若要避免这些问题，在处理大型数据集时，建议您专门设置<xref:System.Windows.FrameworkElement.Height%2A>的<xref:System.Windows.Controls.DataGrid>或将其放在一个容器，它将限制其<xref:System.Windows.FrameworkElement.Height%2A>，如<xref:System.Windows.Controls.Grid>。 当<xref:System.Windows.FrameworkElement.Height%2A>受到限制，<xref:System.Windows.Controls.DataGrid>才会创建将适合其指定的行<xref:System.Windows.FrameworkElement.Height%2A>，并根据需要以显示新数据将回收这些行。  
  
### <a name="setting-the-datagrid-size"></a>数据网格大小设置  
 <xref:System.Windows.Controls.DataGrid>可以设置为自动指定边界内的大小或<xref:System.Windows.Controls.DataGrid>可以设置为特定大小。 下表显示了可以设置到控件的属性的<xref:System.Windows.Controls.DataGrid>大小。  
  
|属性|描述|  
|--------------|-----------------|  
|<xref:System.Windows.FrameworkElement.Height%2A>|设置为特定高度<xref:System.Windows.Controls.DataGrid>。|  
|<xref:System.Windows.FrameworkElement.MaxHeight%2A>|设置高度的上限<xref:System.Windows.Controls.DataGrid>。 <xref:System.Windows.Controls.DataGrid>将沿垂直方向增长，直到它达到此高度。|  
|<xref:System.Windows.FrameworkElement.MinHeight%2A>|设置高度的下限<xref:System.Windows.Controls.DataGrid>。 <xref:System.Windows.Controls.DataGrid>将垂直收缩，直到其达到此高度。|  
|<xref:System.Windows.FrameworkElement.Width%2A>|设置为特定宽度<xref:System.Windows.Controls.DataGrid>。|  
|<xref:System.Windows.FrameworkElement.MaxWidth%2A>|设置的宽度上限<xref:System.Windows.Controls.DataGrid>。 <xref:System.Windows.Controls.DataGrid>将水平增长，直到它达到此宽度。|  
|<xref:System.Windows.FrameworkElement.MinWidth%2A>|设置的宽度下限<xref:System.Windows.Controls.DataGrid>。 <xref:System.Windows.Controls.DataGrid>会水平缩小，直到它达到此宽度。|  
  
## <a name="sizing-rows-and-row-headers"></a>调整行和行标题  
  
### <a name="datagrid-rows"></a>DataGrid Rows  
 默认情况下<xref:System.Windows.Controls.DataGrid>行的<xref:System.Windows.FrameworkElement.Height%2A>属性设置为<xref:System.Double.NaN?displayProperty=nameWithType>("`Auto`"在 XAML 中)，和行的高度将扩展到其内容的大小。 中的所有行的高度<xref:System.Windows.Controls.DataGrid>可以通过设置指定<xref:System.Windows.Controls.DataGrid.RowHeight%2A?displayProperty=nameWithType>属性。 用户可以通过拖动行标题分隔符更改行的高度。  
  
### <a name="datagrid-row-headers"></a>DataGrid 行标题  
 若要显示行标题<xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A>属性必须设置为<xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType>或<xref:System.Windows.Controls.DataGridHeadersVisibility.All?displayProperty=nameWithType>。 默认情况下，显示行标题和自动调整大小以适合其内容。 行标题可以通过设置给定特定宽度<xref:System.Windows.Controls.DataGrid.RowHeaderWidth%2A?displayProperty=nameWithType>属性。  
  
## <a name="sizing-columns-and-column-headers"></a>大小调整列标题和列标题  
  
### <a name="datagrid-columns"></a>DataGrid 列  
 <xref:System.Windows.Controls.DataGrid>使用的值<xref:System.Windows.Controls.DataGridLength>和<xref:System.Windows.Controls.DataGridLengthUnitType>结构，以指定绝对或自动大小调整模式。  
  
 下表显示了由提供的值<xref:System.Windows.Controls.DataGridLengthUnitType>结构。  
  
|name|描述|  
|----------|-----------------|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Auto>|默认自动调整大小模式大小<xref:System.Windows.Controls.DataGrid>列基于单元格和列标题的内容。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToCells>|基于单元格的自动调整大小模式大小<xref:System.Windows.Controls.DataGrid>列基于的列，不包括列标题中的单元格的内容。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToHeader>|基于标头的自动调整大小模式大小<xref:System.Windows.Controls.DataGrid>列基于列标头的内容。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Pixel>|基于像素的大小调整模式大小<xref:System.Windows.Controls.DataGrid>列基于提供的数字值。|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Star>|星形调整大小模式用于根据加权比例分配可用空间。<br /><br /> 在 XAML 中，星号值表示为 n * 其中 n 表示的数字值。 1\*等效于\*。 例如，如果两个中的列<xref:System.Windows.Controls.DataGrid>具有的宽度\*和 2 个\*、 第一列将会收到的可用空间的一部分和第二列将会收到的可用空间的两个部分。|  
  
 <xref:System.Windows.Controls.DataGridLengthConverter>类可用于数字或字符串值之间转换数据和<xref:System.Windows.Controls.DataGridLength>值。  
  
 默认情况下<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>属性设置为<xref:System.Windows.Controls.DataGridLength.SizeToHeader%2A>，并<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType>属性设置为<xref:System.Windows.Controls.DataGridLength.Auto%2A>。 如果调整大小模式设置为<xref:System.Windows.Controls.DataGridLength.Auto%2A>或<xref:System.Windows.Controls.DataGridLength.SizeToCells%2A>，列会增长到其尽可能广泛的可见内容的宽度。 当滚动时，这些调整大小模式的将导致列进行扩展内容大于当前的列大小滚动到视图。 列不会收缩后的内容滚动到视图之外。  
  
 中的列<xref:System.Windows.Controls.DataGrid>还可以设置为自动仅在指定边界内的大小或列可设置为特定大小。 下表显示可以用来控制列的大小的属性。  
  
|属性|描述|  
|--------------|-----------------|  
|<xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType>|设置中的所有列的上限<xref:System.Windows.Controls.DataGrid>。|  
|<xref:System.Windows.Controls.DataGridColumn.MaxWidth%2A?displayProperty=nameWithType>|设置的单个列的上限。 重写 <xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType>。|  
|<xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType>|设置中的所有列的下限<xref:System.Windows.Controls.DataGrid>。|  
|<xref:System.Windows.Controls.DataGridColumn.MinWidth%2A?displayProperty=nameWithType>|设置的单个列的下限。 重写 <xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType>。|  
|<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>|设置中的所有列的特定宽度<xref:System.Windows.Controls.DataGrid>。|  
|<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType>|设置特定的单个列宽度。 重写 <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>。|  
  
### <a name="datagrid-column-headers"></a>DataGrid 列标题  
 默认情况下，<xref:System.Windows.Controls.DataGrid>显示列标题。 若要隐藏列标题<xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A>属性必须设置为<xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType>或<xref:System.Windows.Controls.DataGridHeadersVisibility.None?displayProperty=nameWithType>。 默认情况下，当显示列标题时，自动调整大小以适合其内容。 列标题可以通过设置指定特定高度<xref:System.Windows.Controls.DataGrid.ColumnHeaderHeight%2A?displayProperty=nameWithType>属性。  
  
### <a name="resizing-with-the-mouse"></a>使用鼠标调整大小  
 用户可以调整大小<xref:System.Windows.Controls.DataGrid>行和列通过拖动行或列标题分隔符。 <xref:System.Windows.Controls.DataGrid>还支持自动调整大小的行和列通过双击行或列标题分隔符。 若要防止用户调整特定列的大小，设置<xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType>属性设置为`false`为各个列。 若要阻止用户调整所有列，设置<xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType>属性设置为`false`。 若要阻止用户调整所有行，将设置<xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A?displayProperty=nameWithType>属性设置为`false`。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.DataGrid>
- <xref:System.Windows.Controls.DataGridColumn>
- <xref:System.Windows.Controls.DataGridLength>
- <xref:System.Windows.Controls.DataGridLengthConverter>
