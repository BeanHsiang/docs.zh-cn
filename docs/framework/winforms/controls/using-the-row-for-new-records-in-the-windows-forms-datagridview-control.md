---
title: 在 Windows 窗体 DataGridView 控件中使用新记录行
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], adding rows for new records
- rows [Windows Forms], new records
- DataGridView control [Windows Forms], data entry
ms.assetid: 6110f1ea-9794-442c-a98a-f104a1feeaf4
ms.openlocfilehash: 041738ba375022be7c80526f25e5761314dffbf1
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703915"
---
# <a name="using-the-row-for-new-records-in-the-windows-forms-datagridview-control"></a>在 Windows 窗体 DataGridView 控件中使用新记录行
当你使用<xref:System.Windows.Forms.DataGridView>用于编辑应用程序中的数据，通常要使用户能够将新的数据行添加到数据存储。 <xref:System.Windows.Forms.DataGridView>控件通过其中总是最后一行以显示新记录，提供行来支持此功能。 它是使用其行标题中的星号 （*） 符号进行标记。 以下各节讨论一些应考虑启用程序与用于新记录的行时的情况。  
  
## <a name="displaying-the-row-for-new-records"></a>为新记录中显示行  
 使用<xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A>属性以指示是否显示新记录所对应的行。 此属性的默认值为 `true`。  
  
 有关数据绑定的情况下，将显示新记录所对应的行如果<xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A>控件的属性和<xref:System.ComponentModel.IBindingList.AllowNew%2A?displayProperty=nameWithType>数据源的属性都是`true`。 如果有任一项`false`则不会显示一行。  
  
## <a name="populating-the-row-for-new-records-with-default-data"></a>为新记录使用默认数据填充行  
 当用户选择用于新记录的行作为当前行<xref:System.Windows.Forms.DataGridView>控件将引发<xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded>事件。  
  
 此事件提供了新的访问权限<xref:System.Windows.Forms.DataGridViewRow>并使您能够填充具有默认数据的新行。 有关详细信息，请参阅[如何：指定 Windows 窗体 DataGridView 控件中的新行的默认值](specify-default-values-for-new-rows-in-the-datagrid.md)  
  
## <a name="the-rows-collection"></a>行集合  
 用于新记录的行包含在<xref:System.Windows.Forms.DataGridView>控件的<xref:System.Windows.Forms.DataGridView.Rows%2A>集合但其行为以不同的方式在两个方面：  
  
-   用于新记录的行不能删除从<xref:System.Windows.Forms.DataGridView.Rows%2A>集合以编程方式。 <xref:System.InvalidOperationException>如果尝试执行此操作，将引发。 用户也不能删除用于新记录的行。 <xref:System.Windows.Forms.DataGridViewRowCollection.Clear%2A?displayProperty=nameWithType>方法不会删除从此行<xref:System.Windows.Forms.DataGridView.Rows%2A>集合。  
  
-   用于新记录的行后，可以不添加任何行。 <xref:System.InvalidOperationException>如果尝试执行此操作会引发。 因此，为新记录行始终是中的最后一行<xref:System.Windows.Forms.DataGridView>控件。 上的方法<xref:System.Windows.Forms.DataGridViewRowCollection>中添加行 —<xref:System.Windows.Forms.DataGridViewRowCollection.Add%2A>， <xref:System.Windows.Forms.DataGridViewRowCollection.AddCopy%2A>，和<xref:System.Windows.Forms.DataGridViewRowCollection.AddCopies%2A>— 存在用于新记录的行时在内部调用插入方法。  
  
## <a name="visual-customization-of-the-row-for-new-records"></a>Visual 自定义项的行的新记录  
 创建新记录所对应的行时，它基于指定的行<xref:System.Windows.Forms.DataGridView.RowTemplate%2A>属性。 未指定此行的任何单元格样式继承从其他属性。 有关单元格的样式继承的详细信息，请参阅[Windows 窗体 DataGridView 控件中的单元格样式](cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
 为新的记录检索从每个单元格的单元格的行中所显示的初始值<xref:System.Windows.Forms.DataGridViewCell.DefaultNewRowValue%2A>属性。 有关类型的单元格<xref:System.Windows.Forms.DataGridViewImageCell>，此属性返回占位符图像。 否则，此属性返回`null`。 您可以重写此属性以返回自定义值。 但是，可以通过替换这些初始值<xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded>当焦点进入新记录的行时，事件处理程序。  
  
 这是一个箭头，或者是一个星号，用于此行的标头的标准图标不被公开。 如果你想要自定义图标，将需要创建一个自定义<xref:System.Windows.Forms.DataGridViewRowHeaderCell>类。  
  
 使用标准图标<xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>属性的<xref:System.Windows.Forms.DataGridViewCellStyle>行标头单元格被使用。 如果没有足够的空间来显示它们完全不会呈现标准图标。  
  
 如果行标头单元格的字符串设置，并且没有足够的空间用于文本和图标，先删除该图标。  
  
## <a name="sorting"></a>排序  
 在未绑定模式下，将总是被新记录添加到末尾<xref:System.Windows.Forms.DataGridView>即使用户已排序的内容<xref:System.Windows.Forms.DataGridView>。 用户将需要再次应用排序，以便对行进行排序到正确的位置;此行为是类似于<xref:System.Windows.Forms.ListView>控件。  
  
 在数据绑定和虚拟模式下，插入行为应用排序时将依赖于数据模型的实现。 有关[!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]，该行立即排列到正确的位置。  
  
## <a name="other-notes-on-the-row-for-new-records"></a>用于新记录的行上的其他说明  
 不能设置<xref:System.Windows.Forms.DataGridViewRow.Visible%2A>属性到此行`false`。 <xref:System.InvalidOperationException>如果尝试执行此操作会引发。  
  
 未选定状态始终创建新记录所对应的行。  
  
## <a name="virtual-mode"></a>虚拟模式  
 如果要实现虚拟模式下，将需要跟踪新记录行需要在数据模型，何时回滚添加行时。 此功能的具体实现取决于实现数据模型和及其事务语义，例如，提交作用域是否在单元格或行级别。 有关详细信息，请参阅[Windows 窗体 DataGridView 控件中的虚拟模式](virtual-mode-in-the-windows-forms-datagridview-control.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.DefaultValuesNeeded?displayProperty=nameWithType>
- [Windows 窗体 DataGridView 控件中的数据输入](data-entry-in-the-windows-forms-datagridview-control.md)
- [如何：指定 Windows 窗体 DataGridView 控件中的新行的默认值](specify-default-values-for-new-rows-in-the-datagrid.md)
