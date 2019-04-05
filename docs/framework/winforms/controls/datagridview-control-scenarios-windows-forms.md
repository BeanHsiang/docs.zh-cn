---
title: DataGridView 控件方案（Windows 窗体）
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], displaying in tabular format
- data grids [Windows Forms], about data grids
- DataGridView control [Windows Forms], scenarios
ms.assetid: 09a5fd05-3447-47ec-a4ec-6082a2b7f0dd
ms.openlocfilehash: 882b210a19f1ec5515bd7f37ccc55343f84767bc
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57721298"
---
# <a name="datagridview-control-scenarios-windows-forms"></a>DataGridView 控件方案（Windows 窗体）
使用<xref:System.Windows.Forms.DataGridView>控件，可以显示来自各种数据源的表格格式数据。 有关简单用法，您可以手动填充<xref:System.Windows.Forms.DataGridView>和操作直接通过控件的数据。 通常情况下，但是，您将外部数据源中存储数据并将控件绑定到它通过<xref:System.Windows.Forms.BindingSource>组件。  
  
 本主题介绍了一些常见方案涉及<xref:System.Windows.Forms.DataGridView>控件。  
  
## <a name="scenario-1-displaying-small-amounts-of-data"></a>方案 1:显示较少的数据  
 无需将数据存储在外部数据源使其显示在<xref:System.Windows.Forms.DataGridView>控件。 如果您正在使用的少量数据，可以自行填充控件和操作通过控件的数据。 这称为*取消绑定的模式*。 有关详细信息，请参阅[如何：创建未绑定的 Windows 窗体 DataGridView 控件](how-to-create-an-unbound-windows-forms-datagridview-control.md)。  
  
### <a name="scenario-key-points"></a>方案的关键点：  
  
-   在未绑定模式下，您手动填充控件。  
  
-   取消绑定的模式是特别适合较少的只读数据。  
  
-   取消绑定的模式也适用于类似电子表格或稀疏填充的表。  
  
## <a name="scenario-2-viewing-and-updating-data-stored-in-an-external-data-source"></a>方案 2:查看和更新的外部数据源中存储的数据  
 可以使用<xref:System.Windows.Forms.DataGridView>作为用户界面 (UI) 控制哪些用户可通过访问保留在数据源，例如数据库表或业务对象的集合中的数据。 有关详细信息，请参阅[如何：将数据绑定到 Windows 窗体 DataGridView 控件](how-to-bind-data-to-the-windows-forms-datagridview-control.md)。  
  
### <a name="scenario-key-points"></a>方案的关键点：  
  
-   绑定的模式允许您连接到数据源、 自动生成基于数据源属性或数据库列的列和自动填充该控件。  
  
-   绑定的模式适合大量用户与数据交互。 在设置数据格式进行显示，和用户指定的数据可以解析为数据源所需的格式。 可以检测到格式设置错误和数据库约束错误的数据输入，以便用户可以收到警告，可以更正错误的单元格。  
  
-   附加功能，例如列排序，冻结和重新排序使用户能够查看其工作流的最方便的方法中的数据。  
  
-   剪贴板支持使用户能够将数据复制到其他应用程序的应用程序中。  
  
## <a name="scenario-3-advanced-data"></a>方案 3:高级的数据  
 如果你有标准数据绑定模型不能解决的特殊需求，可以通过实现来管理控件与你的数据之间的交互*的虚拟模式*。 需要实现虚拟模式是指实现一个或多个事件处理程序允许控件请求的信息有关的单元格的信息。  
  
 例如，如果要使用的数据量大，可能想要实现虚拟模式，以确保最佳的效率。 虚拟模式下也是用于维护，以及从另一个数据源检索的列显示未绑定列的值。  
  
 有关虚拟模式的详细信息，请参阅[演练：在 Windows 中实现虚拟模式窗体 DataGridView 控件](implementing-virtual-mode-wf-datagridview-control.md)。  
  
### <a name="scenario-key-points"></a>方案的关键点：  
  
-   虚拟模式适合用于需要进行精细调整性能时显示的数据量非常大。  
  
## <a name="scenario-4-automatically-resizing-rows-and-columns"></a>方案 4:自动调整行和列的大小  
 时显示的定期更新数据，可以自动调整行和列，以确保所有内容可见。 <xref:System.Windows.Forms.DataGridView>控件提供了几个选项，可以启用或禁用手动调整大小，在特定时间，以编程方式调整大小或调整大小自动内容发生更改时。 有关详细信息，请参阅[Windows 窗体 DataGridView 控件中调整大小选项](sizing-options-in-the-windows-forms-datagridview-control.md)。  
  
### <a name="scenario-key-points"></a>方案的关键点：  
  
-   手动调整大小，用户可以调整单元格的高度和宽度。  
  
-   自动调整大小，可维护单元格的大小，以便永远不会剪切单元格内容。  
  
-   以编程方式调整大小，可在特定时间以避免对性能影响持续自动调整大小的调整大小的单元格。  
  
## <a name="scenario-5-simple-customization"></a>方案 5:简单的自定义  
 <xref:System.Windows.Forms.DataGridView>控件提供了许多方法来更改其基本外观和行为。 有关详细信息，请参阅[Windows 窗体 DataGridView 控件中的单元格样式](cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
### <a name="scenario-key-points"></a>方案的关键点：  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle> 对象，只需提供颜色、 字体、 格式设置和多个级别和控件的各个元素的定位信息。  
  
-   可以分层和共享的多个元素，从而允许重用代码的单元格样式。  
  
## <a name="scenario-6-advanced-customization"></a>方案 6:高级自定义  
 <xref:System.Windows.Forms.DataGridView>控件提供了多种用于自定义其外观和行为。  
  
### <a name="scenario-key-points"></a>方案的关键点：  
  
-   您可以提供自己的单元格的绘制代码。 有关详细信息，请参阅[如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](customize-the-appearance-of-cells-in-the-datagrid.md)。  
  
-   你可以提供自己的行绘制。 这很有用，例如，若要创建具有跨多个列的内容的行。 有关详细信息，请参阅[如何：自定义 Windows 窗体 DataGridView 控件中的行的外观](customize-the-appearance-of-rows-in-the-datagrid.md)。  
  
-   您可以实现自己的单元格和列类自定义单元格的外观。 有关详细信息，请参阅[如何：自定义单元格和列在 Windows 窗体 DataGridView 控件通过扩展行为和外观](customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md)。  
  
-   您可以实现承载控件而不是通过内置的列类型提供您自己单元格和列的类。 有关详细信息，请参阅[如何：Windows 窗体 DataGridView 单元格中承载控件](how-to-host-controls-in-windows-forms-datagridview-cells.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- [DataGridView 控件概述](datagridview-control-overview-windows-forms.md)
