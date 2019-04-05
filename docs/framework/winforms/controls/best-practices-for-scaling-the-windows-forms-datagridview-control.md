---
title: 缩放 Windows 窗体 DataGridView 控件的最佳做法
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], row sharing
- data grids [Windows Forms], best practices
- DataGridView control [Windows Forms], shared rows
- DataGridView control [Windows Forms], best practices
- best practices [Windows Forms], dataGridView control
- DataGridView control [Windows Forms], scaling
ms.assetid: 8321a8a6-6340-4fd1-b475-fa090b905aaf
ms.openlocfilehash: 895dd132c070157355c28a935e43240f2750159e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57706411"
---
# <a name="best-practices-for-scaling-the-windows-forms-datagridview-control"></a>缩放 Windows 窗体 DataGridView 控件的最佳做法
<xref:System.Windows.Forms.DataGridView>控件旨在提供最大可伸缩性。 如果需要显示大量的数据，则应遵循本主题，以避免消耗大量的内存或降低响应能力的用户界面 (UI) 中所述的准则。 本主题讨论下列问题：  
  
-   有效地使用的单元格样式  
  
-   有效地使用快捷菜单  
  
-   使用自动调整大小高效  
  
-   有效使用所选的单元格、 行和列集合  
  
-   使用共享的行  
  
-   防止行成为非共享行  
  
 如果你有特殊性能需求，可以实现虚拟模式并提供你自己的数据管理操作。 有关详细信息，请参阅[Windows 窗体 DataGridView 控件中的数据显示模式](data-display-modes-in-the-windows-forms-datagridview-control.md)。  
  
## <a name="using-cell-styles-efficiently"></a>有效地使用的单元格样式  
 每个单元格、 行和列可以具有其自己的样式信息。 样式的信息存储在<xref:System.Windows.Forms.DataGridViewCellStyle>对象。 创建多个独立单元格样式对象<xref:System.Windows.Forms.DataGridView>元素可以是效率不高，尤其在使用大量的数据时。 若要避免对性能产生影响，请使用以下准则：  
  
-   避免设置单元格样式属性为各个<xref:System.Windows.Forms.DataGridViewCell>或<xref:System.Windows.Forms.DataGridViewRow>对象。 这包括指定的行对象<xref:System.Windows.Forms.DataGridView.RowTemplate%2A>属性。 每个新行的行模板从克隆会收到其自己的模板的单元格样式对象副本。 最大可伸缩性，设置在单元格样式属性<xref:System.Windows.Forms.DataGridView>级别。 例如，设置<xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>属性而不是<xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>属性。  
  
-   如果某些单元格需要比默认格式设置的其他格式，使用相同<xref:System.Windows.Forms.DataGridViewCellStyle>跨单元格、 行或列组的实例。 避免直接设置属性类型的<xref:System.Windows.Forms.DataGridViewCellStyle>上各个单元格、 行和列。 单元格样式共享的示例，请参阅[如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)。 通过处理单独设置单元格样式时，也可以避免对性能产生负面影响<xref:System.Windows.Forms.DataGridView.CellFormatting>事件处理程序。 有关示例，请参见 [如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)。  
  
-   在确定单元格的样式，使用<xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=nameWithType>属性而不是<xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>属性。 访问<xref:System.Windows.Forms.DataGridViewCell.Style%2A>属性创建的新实例<xref:System.Windows.Forms.DataGridViewCellStyle>类如果尚未使用该属性。 此外，此对象可能不包含该单元格的完整的样式信息，如果某些样式继承自行、 列或控件。 有关单元格的样式继承的详细信息，请参阅[Windows 窗体 DataGridView 控件中的单元格样式](cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
## <a name="using-shortcut-menus-efficiently"></a>有效地使用快捷菜单  
 每个单元格、 行和列可以具有其自己的快捷菜单。 中的快捷菜单<xref:System.Windows.Forms.DataGridView>控制由<xref:System.Windows.Forms.ContextMenuStrip>控件。 只需与单元格样式对象一样，为许多单个创建快捷方式菜单<xref:System.Windows.Forms.DataGridView>元素会对性能产生负面影响。 若要避免这种下降，请使用以下准则：  
  
-   避免创建各个单元格和行的快捷菜单。 这包括行模板，新行添加到控件时，会克隆以及其快捷菜单。 最大可伸缩性，使用仅该控件的<xref:System.Windows.Forms.Control.ContextMenuStrip%2A>属性可以指定整个控件的一个快捷方式菜单。  
  
-   如果您需要针对多个行或单元格的多个快捷菜单，处理<xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded>或<xref:System.Windows.Forms.DataGridView.RowContextMenuStripNeeded>事件。 这些事件使您可以管理快捷方式菜单对象自己，从而可以优化性能。  
  
## <a name="using-automatic-resizing-efficiently"></a>使用自动调整大小高效  
 行、 列和标头可以自动调整大小作为单元格的内容更改，以便完整地显示单元格的全部内容。 更改大小调整模式还可以调整行、 列和标头。 若要确定正确的大小，<xref:System.Windows.Forms.DataGridView>控件必须检查必须适应每个单元格的值。 当处理大型数据集，此分析会降低该控件的性能，自动调整大小发生时。 若要避免性能损失，使用以下准则：  
  
-   避免使用自动调整大小<xref:System.Windows.Forms.DataGridView>与大量的行的控件。 如果使用自动调整大小，调整大小，根据所显示的行。 处于虚拟模式下以及使用显示的行。  
  
    -   行和列，请使用`DisplayedCells`或`DisplayedCellsExceptHeaders`字段<xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>， <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>，和<xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>枚举。  
  
    -   对于行标题，请使用<xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode.AutoSizeToDisplayedHeaders>或<xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode.AutoSizeToFirstHeader>字段<xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>枚举。  
  
-   最大可伸缩性，关闭自动调整大小和使用以编程方式调整大小。  
  
 有关详细信息，请参阅[Windows 窗体 DataGridView 控件中调整大小选项](sizing-options-in-the-windows-forms-datagridview-control.md)。  
  
## <a name="using-the-selected-cells-rows-and-columns-collections-efficiently"></a>有效使用选定的单元格、 行和列集合  
 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>集合不会使用大型选择有效地执行。 <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>并<xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>集合还可能效率很低，尽管到一定程度上因为有许多较少行，比在典型的单元格<xref:System.Windows.Forms.DataGridView>控制和许多较少的列比行。 若要避免性能损失，使用这些集合时，使用以下准则：  
  
-   若要确定是否中的所有单元格<xref:System.Windows.Forms.DataGridView>访问的内容之前选择了<xref:System.Windows.Forms.DataGridView.SelectedCells%2A>集合中，检查返回值的<xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>方法。 但请注意，此方法可能会导致行变为非共享。 有关更多信息，请参见下一节。  
  
-   避免使用<xref:System.Collections.ICollection.Count%2A>属性的<xref:System.Windows.Forms.DataGridViewSelectedCellCollection?displayProperty=nameWithType>来确定选定的单元格的数目。 请改用<xref:System.Windows.Forms.DataGridView.GetCellCount%2A?displayProperty=nameWithType>方法并传入<xref:System.Windows.Forms.DataGridViewElementStates.Selected?displayProperty=nameWithType>值。 同样，使用<xref:System.Windows.Forms.DataGridViewRowCollection.GetRowCount%2A?displayProperty=nameWithType>和<xref:System.Windows.Forms.DataGridViewColumnCollection.GetColumnCount%2A?displayProperty=nameWithType>方法来确定选定的元素，而不是访问所选的行和列集合的数目。  
  
-   避免基于单元格的选择模式。 与此相反，设置<xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType>属性设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType>或<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect?displayProperty=nameWithType>。  
  
## <a name="using-shared-rows"></a>使用共享行  
 在实现高效的内存使用<xref:System.Windows.Forms.DataGridView>控制通过共享行。 行将通过共享的实例来共享尽可能多的信息有关其外观和行为可能<xref:System.Windows.Forms.DataGridViewRow>类。  
  
 虽然共享行实例节省内存，行可以轻松地成为非共享行。 例如，每当用户交互直接与单元格时，其行变为非共享。 由于不能避免此操作，此主题中的准则十分有用，仅当使用的数据量非常大并且仅当用户将与相对较小部分数据交互每次运行程序时。  
  
 不能共享行中未绑定<xref:System.Windows.Forms.DataGridView>控制是否有任何其单元格包含值。 当<xref:System.Windows.Forms.DataGridView>控件绑定到外部数据源或外部控件而不是在单元格对象，允许要共享的行时实现虚拟模式并提供您自己的数据源时，存储单元格的值。  
  
 如果可以从行的状态和包含的单元格的列的状态确定所有单元格的状态，可以仅共享行对象。 如果您更改单元格的状态，以便从其行和列的状态可以不再推导，不能共享行。  
  
 例如，不能在任何以下情况下共享行：  
  
-   包含一个所选的单元格不在所选列中的行。  
  
-   行包含具有的单元格及其<xref:System.Windows.Forms.DataGridViewCell.ToolTipText%2A>或<xref:System.Windows.Forms.DataGridViewCell.ContextMenuStrip%2A>属性集。  
  
-   包含的行<xref:System.Windows.Forms.DataGridViewComboBoxCell>使用其<xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A>属性集。  
  
 在绑定的模式或虚拟模式下，可以提供工具提示和快捷菜单为单个单元通过处理<xref:System.Windows.Forms.DataGridView.CellToolTipTextNeeded>和<xref:System.Windows.Forms.DataGridView.CellContextMenuStripNeeded>事件。  
  
 <xref:System.Windows.Forms.DataGridView>控件将自动尝试使用共享的行，只要行添加到<xref:System.Windows.Forms.DataGridViewRowCollection>。 使用以下准则以确保共享行：  
  
-   避免调用`Add(Object[])`的重载<xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>方法并`Insert(Object[])`重载<xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A>方法<xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType>集合。 这些重载自动创建非共享的行。  
  
-   务必中指定的行<xref:System.Windows.Forms.DataGridView.RowTemplate%2A?displayProperty=nameWithType>可在以下情况下共享属性：  
  
    -   调用时`Add()`或`Add(Int32)`的重载<xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>方法或`Insert(Int32,Int32)`重载<xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A>方法<xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType>集合。  
  
    -   增加的值时<xref:System.Windows.Forms.DataGridView.RowCount%2A?displayProperty=nameWithType>属性。  
  
    -   设置时<xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=nameWithType>属性。  
  
-   请确保所指示的行`indexSource`调用时，可以共享参数<xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A>， <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>， <xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopy%2A>，并<xref:System.Windows.Forms.DataGridViewRowCollection.InsertCopies%2A>方法<xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType>集合。  
  
-   确保在调用时，可共享的指定的行`Add(DataGridViewRow)`的重载<xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>方法，<xref:System.Windows.Forms.DataGridViewRowCollection.AddRange%2A>方法，`Insert(Int32,DataGridViewRow)`重载<xref:System.Windows.Forms.DataGridViewRowCollection.Insert%2A>方法，和<xref:System.Windows.Forms.DataGridViewRowCollection.InsertRange%2A>方法<xref:System.Windows.Forms.DataGridView.Rows%2A?displayProperty=nameWithType>集合。  
  
 若要确定是否共享行，请使用<xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=nameWithType>方法以检索行对象，然后查看该对象的<xref:System.Windows.Forms.DataGridViewBand.Index%2A>属性。 共享的行始终具有<xref:System.Windows.Forms.DataGridViewBand.Index%2A>属性值为 – 1。  
  
## <a name="preventing-rows-from-becoming-unshared"></a>防止行成为非共享行  
 共享的行可以成为非共享行代码或用户操作的结果。 若要避免对性能产生影响，应避免使行成为非共享行。 应用程序在开发期间，可以处理<xref:System.Windows.Forms.DataGridView.RowUnshared>事件以确定当行成为非共享行。 调试行共享问题时，这很有用。  
  
 若要防止行成为非共享行，请使用以下准则：  
  
-   避免对创建索引<xref:System.Windows.Forms.DataGridView.Rows%2A>集合或循环访问其与`foreach`循环。 您将通常不需要直接访问的行。 <xref:System.Windows.Forms.DataGridView> 对行执行操作的方法接受行索引参数而不是行实例。 此外，与行相关的事件处理程序收到具有可用于操作而不会导致它们成为非共享行的行的行属性的事件参数对象。  
  
-   如果需要访问行对象，使用<xref:System.Windows.Forms.DataGridViewRowCollection.SharedRow%2A?displayProperty=nameWithType>方法并传入行的实际索引。 但是，请注意，修改通过此方法检索到一个共享的行对象，将修改共享此对象的所有行。 用于新记录的行不与共享其他行，但是，因此它不会受到影响时修改任何其他行。 另请注意共享行所表示的不同行可能有不同的快捷方式菜单。 若要从共享的行实例中检索正确的快捷菜单，请使用<xref:System.Windows.Forms.DataGridViewRow.GetContextMenuStrip%2A>方法并传入行的实际索引。 如果访问共享的行<xref:System.Windows.Forms.DataGridViewRow.ContextMenuStrip%2A>属性相反，它将使用共享的行索引-1 并将不检索正确的快捷菜单。  
  
-   避免索引<xref:System.Windows.Forms.DataGridViewRow.Cells%2A?displayProperty=nameWithType>集合。 直接访问一个单元格将导致其父行取消共享，并实例化新<xref:System.Windows.Forms.DataGridViewRow>。 与单元格相关的事件处理程序收到具有可用于对行执行操作而不会导致行变为非共享的单元属性的事件参数对象。 此外可以使用<xref:System.Windows.Forms.DataGridView.CurrentCellAddress%2A>属性来检索当前的单元格的行和列索引而无需直接访问该单元格。  
  
-   避免基于单元格的选择模式。 这些模式使行成为非共享行。 与此相反，设置<xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType>属性设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect?displayProperty=nameWithType>或<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect?displayProperty=nameWithType>。  
  
-   不处理<xref:System.Windows.Forms.DataGridViewRowCollection.CollectionChanged?displayProperty=nameWithType>或<xref:System.Windows.Forms.DataGridView.RowStateChanged?displayProperty=nameWithType>事件。 这些事件会导致行变为非共享。 此外，不要调用<xref:System.Windows.Forms.DataGridViewRowCollection.OnCollectionChanged%2A?displayProperty=nameWithType>或<xref:System.Windows.Forms.DataGridView.OnRowStateChanged%2A?displayProperty=nameWithType>引发这些事件的方法。  
  
-   不会访问<xref:System.Windows.Forms.DataGridView.SelectedCells%2A?displayProperty=nameWithType>集合时<xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType>属性值是<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>， <xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>， <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect>，或<xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect>。 这将导致所有所选的行变为非共享。  
  
-   不要调用<xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A?displayProperty=nameWithType>方法。 此方法会导致行成为非共享行。  
  
-   不要调用<xref:System.Windows.Forms.DataGridView.SelectAll%2A?displayProperty=nameWithType>方法时<xref:System.Windows.Forms.DataGridView.SelectionMode%2A?displayProperty=nameWithType>属性值是<xref:System.Windows.Forms.DataGridViewSelectionMode.CellSelect>。 这将导致所有行都成为非共享行。  
  
-   未设置<xref:System.Windows.Forms.DataGridViewCell.ReadOnly%2A>或<xref:System.Windows.Forms.DataGridViewCell.Selected%2A>到单元格的属性`false`时在其列中的相应属性设置为`true`。 这将导致所有行都成为非共享行。  
  
-   不会访问<xref:System.Windows.Forms.DataGridViewRowCollection.List%2A?displayProperty=nameWithType>属性。 这将导致所有行都成为非共享行。  
  
-   不要调用`Sort(IComparer)`重载<xref:System.Windows.Forms.DataGridView.Sort%2A>方法。 使用自定义比较器进行排序会导致所有行都成为非共享行。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- [Windows 窗体 DataGridView 控件中的性能调整](performance-tuning-in-the-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的虚拟模式](virtual-mode-in-the-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的数据显示模式](data-display-modes-in-the-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的单元格样式](cell-styles-in-the-windows-forms-datagridview-control.md)
- [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的重设大小选项](sizing-options-in-the-windows-forms-datagridview-control.md)
