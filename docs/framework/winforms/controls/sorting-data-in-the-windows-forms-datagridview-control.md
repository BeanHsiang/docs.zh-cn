---
title: 对 Windows 窗体 DataGridView 控件中的数据进行排序
ms.date: 02/13/2018
helpviewer_keywords:
- data [Windows Forms], sorting in grids
- data grids [Windows Forms], sorting data
- DataGridView control [Windows Forms], sorting data
ms.assetid: c1d4f24c-d961-4181-809d-5a5caa6122e4
ms.openlocfilehash: 606ffc7bd6136b775adaaaa79cf5042cf1e2dd70
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724916"
---
# <a name="sorting-data-in-the-windows-forms-datagridview-control"></a>对 Windows 窗体 DataGridView 控件中的数据进行排序

默认情况下，用户可以对中的数据排序<xref:System.Windows.Forms.DataGridView>控件通过单击文本框列标题 （或通过按 f3 键时文本框单元格侧重于.NET Framework 4.7.2 及更高版本）。 您可以修改<xref:System.Windows.Forms.DataGridViewColumn.SortMode>要允许用户若要按其他列类型时最好这样做的特定列的属性。 您可以还对数据进行排序以编程方式按任何列，或按多个列。

## <a name="in-this-section"></a>本节内容

[Windows 窗体 DataGridView 控件中的列排序模式](column-sort-modes-in-the-windows-forms-datagridview-control.md)  
介绍了用于对控件中的数据进行排序。

[如何：设置 Windows 窗体 DataGridView 控件中的列排序模式](set-the-sort-modes-for-columns-wf-datagridview-control.md)  
介绍如何使用户能够按不是默认情况下可排序的列进行排序。

[如何：自定义 Windows 窗体 DataGridView 控件中的排序](how-to-customize-sorting-in-the-windows-forms-datagridview-control.md)  
介绍如何以编程方式对数据进行排序以及如何自定义使用的排序<xref:System.Windows.Forms.DataGridView.SortCompare?displayProperty=nameWithType>事件或通过实现<xref:System.Collections.IComparer>接口。

## <a name="reference"></a>参考

<xref:System.Windows.Forms.DataGridView>  
提供关于 <xref:System.Windows.Forms.DataGridView> 控件的参考文档。  

<xref:System.Windows.Forms.DataGridView.Sort%2A?displayProperty=nameWithType>  
为提供参考文档<xref:System.Windows.Forms.DataGridView.Sort%2A>方法。

<xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=nameWithType>  
为提供参考文档<xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A>属性。

<xref:System.Windows.Forms.DataGridViewColumnSortMode>  
为提供参考文档<xref:System.Windows.Forms.DataGridViewColumnSortMode>枚举。

## <a name="see-also"></a>请参阅

- [DataGridView 控件](datagridview-control-windows-forms.md)
- [Windows 窗体 DataGridView 控件中的列类型](column-types-in-the-windows-forms-datagridview-control.md)
