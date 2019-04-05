---
title: Windows 窗体 DataGridView 控件中的大小调整选项
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], row sizing
- data grids [Windows Forms], column sizing
- DataGridView control [Windows Forms], column sizing
- DataGridView control [Windows Forms], sizing options
- data grids [Windows Forms], row sizing
- data grids [Windows Forms], sizing options
ms.assetid: a5620a9c-0d06-41e3-8934-c25ddb16c9e6
ms.openlocfilehash: a236289939b9355e961ce1bfc9a7e0ff5349a95a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57717903"
---
# <a name="sizing-options-in-the-windows-forms-datagridview-control"></a>Windows 窗体 DataGridView 控件中的大小调整选项
<xref:System.Windows.Forms.DataGridView> 行、 列和标头可以更改由于许多不同的匹配项的大小。 下表显示了这些情况的发生。  
  
|匹配项|描述|  
|----------------|-----------------|  
|用户调整大小|用户可以通过拖动或双击行、 列或标头分隔符来进行大小调整。|  
|控件调整大小|在列填充模式列宽度控件宽度发生更改时更改;例如，当该控件停靠到其父窗体和用户调整窗体。|  
|单元格的值更改|在基于内容的自动调整大小模式下，大小更改以适应新的显示值。|  
|方法调用|以编程方式基于内容的大小调整，能让你在方法调用时根据单元格值的随机的大小调整。|  
|属性设置|此外可以设置特定的高度和宽度值。|  
  
 默认情况下，用户调整大小启用、 禁用自动调整大小，则和单元格的宽度大于其列的值将被剪裁。  
  
 下表显示了可用来调整默认行为，或若要使用特定的大小调整选项来实现特定效果的多个方案。  
  
|方案|实现|  
|--------------|--------------------|  
|使用列填充模式中的用于显示同样的大小调整相对较小且不显示水平滚动条占用该控件的整个宽度的列数中的数据。|将 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>。|  
|使用列填充模式中的使用显示不同大小的值。|将 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>。 通过将列设置初始化相对列宽<xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>属性或通过调用控件<xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>用数据填充该控件之后的方法。|  
|列填充模式中使用的不同重要性的值。|将 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>。 设置大型<xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>对于必须始终显示某些数据或将调整大小选项之外的其他列填充模式的特定列的值。|  
|使用列填充模式来避免显示控件背景。|设置<xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>到最后一列的属性<xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.Fill>和其他调整大小选项用于其他列。 如果其他列使用过多的可用空间，请设置<xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>最后一列的属性。|  
|显示固定宽度的列，例如图标或 ID 列。|设置<xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>到<xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.None>并<xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A>到<xref:System.Windows.Forms.DataGridViewTriState.False>列。 通过设置初始化其宽度<xref:System.Windows.Forms.DataGridViewColumn.Width%2A>属性或通过调用控件<xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A>用数据填充该控件之后的方法。|  
|单元格内容更改以避免剪裁和以优化空间的使用时，会自动调整大小。|自动调整大小属性设置为一个值，表示基于内容调整大小模式。 若要使用的大量数据时，请避免对性能产生负面影响，请使用计算显示的行的大小调整模式。|  
|调整大小以容纳中显示的行，以避免性能下降时处理多行的值。|使用自动或以编程方式调整大小的相应调整大小模式的枚举值。 若要调整大小以容纳新显示的行中的值，滚动时，调用调整大小的方法<xref:System.Windows.Forms.DataGridView.Scroll>事件处理程序。 若要自定义用户双击调整大小，以便仅显示的行中的值确定新的大小调整大小的方法中调用<xref:System.Windows.Forms.DataGridView.RowDividerDoubleClick>或<xref:System.Windows.Forms.DataGridView.ColumnDividerDoubleClick>事件处理程序。|  
|调整大小以适应单元格内容仅在特定时间以避免性能损失，或启用用户调整大小。|在事件处理程序中调用基于内容调整大小方法。 例如，使用<xref:System.Windows.Forms.DataGridView.DataBindingComplete>事件后绑定，初始化大小和处理<xref:System.Windows.Forms.DataGridView.CellValidated>或<xref:System.Windows.Forms.DataGridView.CellValueChanged>要调整大小以补偿用户编辑或更改事件中绑定的数据源。|  
|调整行高，以多行的单元格内容。|确保列宽适用于显示的文本段落，并使用自动或以编程方式基于内容的行大小调整的高度。 此外请确保使用显示具有多行内容的单元格<xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>单元格的样式值<xref:System.Windows.Forms.DataGridViewTriState.True>。<br /><br /> 通常情况下，将使用自动列大小调整模式来维护列宽度，或将其设置为特定宽度之前调整行高。|  
  
## <a name="resizing-with-the-mouse"></a>使用鼠标调整大小  
 默认情况下，用户可以调整行、 列和不使用基于单元格的值自动调整大小模式的标头大小。 若要防止用户与其他模式，如列填充模式中，调整大小将设置一个或多个以下<xref:System.Windows.Forms.DataGridView>属性：  
  
-   <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
 此外可以通过设置调整单个行或列的大小来防止用户其<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>属性。 默认情况下<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>属性值根据<xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A>列的属性值和<xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A>属性值的行。 如果显式设置<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>到<xref:System.Windows.Forms.DataGridViewTriState.True>或<xref:System.Windows.Forms.DataGridViewTriState.False>，但是，控件的值是该行或列的指定的值重写。 设置<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>到<xref:System.Windows.Forms.DataGridViewTriState.NotSet>还原继承。  
  
 因为<xref:System.Windows.Forms.DataGridViewTriState.NotSet>恢复值继承<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>属性将永远不会返回<xref:System.Windows.Forms.DataGridViewTriState.NotSet>值，除非行或列尚未添加到<xref:System.Windows.Forms.DataGridView>控件。 如果您需要确定是否<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>的行或列的属性值继承，请查看其<xref:System.Windows.Forms.DataGridViewElement.State%2A>属性。 如果<xref:System.Windows.Forms.DataGridViewElement.State%2A>值包括<xref:System.Windows.Forms.DataGridViewElementStates.ResizableSet>标志，<xref:System.Windows.Forms.DataGridViewBand.Resizable%2A>不继承属性值。  
  
## <a name="automatic-sizing"></a>自动调整大小  
 有两种类型中的自动调整大小的<xref:System.Windows.Forms.DataGridView>控件： 列填充模式和基于内容的自动调整大小。  
  
 列填充模式中的控件来填充控件的显示区域的宽度将导致可见的列。 有关此模式的详细信息，请参阅[Windows 窗体 DataGridView 控件中的列填充模式](column-fill-mode-in-the-windows-forms-datagridview-control.md)。  
  
 此外可以配置行、 列和标头，以便自动调整其大小以适应其单元格内容。 在这种情况下，单元格内容更改时，会发生大小调整。  
  
> [!NOTE]
>  如果保留单元格的值中使用的虚拟模式的自定义数据缓存，当用户编辑单元格的值，但不会发生更改的已缓存之外的值时时发生自动调整大小<xref:System.Windows.Forms.DataGridView.CellValuePushed>事件处理程序。 在这种情况下，调用<xref:System.Windows.Forms.DataGridView.UpdateCellValue%2A>方法，以强制要更新的单元格显示并应用当前的自动调整大小模式的控件。  
  
 如果仅对一个维度启用了基于内容的自动调整大小-的就是行而非针对列，或列但没有行 — 和<xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>也是其他维度发生更改时，也会发生已启用，大小调整。 例如，如果行而非针对列配置为自动调整大小和<xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>是启用，用户可以拖动列分隔符更改列的宽度和，以便单元格内容仍完全显示，将自动调整行高。  
  
 如果配置行和基于内容的自动调整大小的列和<xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>已启用，<xref:System.Windows.Forms.DataGridView>控件将调整大小，只要单元格内容发生更改，并且将使用理想的单元格高度为宽度比率时计算新的大小。  
  
 若要配置标头和行和不重写控件值的列的大小调整模式，设置一个或多个以下<xref:System.Windows.Forms.DataGridView>属性：  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A>  
  
 若要重写的单个列的控件的列大小调整模式，请设置其<xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>属性的值以外的其他<xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.NotSet>。 列的大小调整模式实际上由其<xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A>属性。 此属性的值基于列的<xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>属性值，除非该值<xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.NotSet>，在这种情况下该控件的<xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A>继承值。  
  
 使用基于内容的自动调整大小谨慎处理大量数据时。 若要避免性能损失，使用计算仅根据所显示的行，而不是分析中控件的每一行的大小自动调整大小模式。 获得最佳性能，加载使用以编程方式重设大小改为，以便您可以调整大小在特定时间，如紧跟新数据。  
  
 基于内容的自动调整大小模式的行、 列或您已隐藏通过设置行或列的标头不会影响<xref:System.Windows.Forms.DataGridViewBand.Visible%2A>属性或控件<xref:System.Windows.Forms.DataGridView.RowHeadersVisible%2A>或<xref:System.Windows.Forms.DataGridView.ColumnHeadersVisible%2A>属性设置为`false`。 例如，如果某列被隐藏后它会自动调整大小以适应大型单元格值，隐藏的列不会更改其大小如果删除包含大型单元格的值的行。 自动调整大小不会发生时的可见性发生更改，因此更改列<xref:System.Windows.Forms.DataGridViewColumn.Visible%2A>属性改回`true`不会强制其重新计算其大小以适应当前内容。  
  
 以编程方式基于内容调整大小会影响的行、 列和标头而不考虑它们的可见性。  
  
## <a name="programmatic-resizing"></a>以编程方式调整大小  
 禁用自动调整大小后，可以以编程方式设置的确切宽度或高度的行、 列或标头通过以下属性：  
  
-   <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=nameWithType>  
  
-   <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>  
  
 以编程方式还可以调整大小的行、 列和标头以适应其内容，使用以下方法：  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A>  
  
-   <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A>  
  
 这些方法将调整行、 列或一次标头而不是将它们配置为连续重设大小的大小。 新的大小自动计算要显示不经剪辑的所有单元格内容。 当您以编程方式调整列大小具有<xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A>的属性值<xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.Fill>，但是，使用计算的基于内容的宽度来按比例调整列<xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>属性值和的实际列宽度以便所有列都填充可用显示区域的控件然后根据这些新的比例计算。  
  
 以编程方式调整大小将有助于避免与连续重设大小的性能损失。 最好还为用户可调整大小的行、 列和标头，以及列填充模式中提供初始大小。  
  
 通常会在特定时间调用以编程方式调整大小的方法。 例如，可能会以编程方式加载数据之后, 调整所有列或后已修改特定单元格的值可能以编程方式调整都大小的特定行。  
  
## <a name="customizing-content-based-sizing-behavior"></a>自定义基于内容调整大小行为  
 使用派生时，你可以自定义大小调整行为<xref:System.Windows.Forms.DataGridView>单元格、 行和列类型通过重写<xref:System.Windows.Forms.DataGridViewCell.GetPreferredSize%2A?displayProperty=nameWithType>， <xref:System.Windows.Forms.DataGridViewRow.GetPreferredHeight%2A?displayProperty=nameWithType>，或<xref:System.Windows.Forms.DataGridViewColumn.GetPreferredWidth%2A?displayProperty=nameWithType>方法或通过调用受保护的调整大小的方法重载中派生<xref:System.Windows.Forms.DataGridView>控件。 受保护的调整大小方法重载用于处理在对，以实现理想的单元格高度为宽度的比例，避免过于宽或更高的单元格。 例如，如果您调用`AutoResizeRows(DataGridViewAutoSizeRowsMode,Boolean)`的重载<xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A>方法并传入的值`false`为<xref:System.Boolean>参数，重载将计算的理想高度和宽度的单元格的行中，但它将调整行高仅。 然后，必须调用<xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A>要调整列宽度为计算得到的理想方法。  
  
## <a name="content-based-sizing-options"></a>基于内容调整大小选项  
 使用的大小调整属性和方法的枚举具有相似的基于内容调整大小的值。 使用这些值，可以限制哪些单元格用于计算的首选的大小。 对于所有大小调整枚举，其名称显示的单元格引用的值限制在计算中显示的行的单元格。 不包括行是有助于避免对性能产生负面影响时使用了大量的行。 此外可以限制为在标头或非标头单元格的单元值的计算。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AllowUserToResizeRows%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeightSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidthSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.Resizable%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeRowsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersWidth%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersHeight%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewRow.Height%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumn%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumnHeadersHeight%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRow%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRows%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoResizeRowHeadersWidth%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewAutoSizeRowMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeRowsMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>
- <xref:System.Windows.Forms.DataGridViewColumnHeadersHeightSizeMode>
- <xref:System.Windows.Forms.DataGridViewRowHeadersWidthSizeMode>
- [调整 Windows 窗体 DataGridView 控件中列和行的大小](resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的列填充模式](column-fill-mode-in-the-windows-forms-datagridview-control.md)
- [如何：设置 Windows 窗体 DataGridView 控件的大小调整模式](how-to-set-the-sizing-modes-of-the-windows-forms-datagridview-control.md)
