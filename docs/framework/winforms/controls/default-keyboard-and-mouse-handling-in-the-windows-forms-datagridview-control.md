---
title: 默认键盘和鼠标处理 Windows 窗体 DataGridView 控件中
ms.date: 02/13/2018
helpviewer_keywords:
- data grids [Windows Forms], mouse handling
- DataGridView control [Windows Forms], navigation keys
- keyboards [Windows Forms], default handling in DataGridView control
- DataGridView control [Windows Forms], keyboard handling
- mouse [Windows Forms], default handling in DataGridView control
- DataGridView control [Windows Forms], mouse handling
- navigation keys [Windows Forms], DataGridView control
ms.assetid: 4519b928-bfc8-4e8b-bb9c-b1e76a0ca552
ms.openlocfilehash: 56585bf91a559844f15aede4519706674357a924
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708309"
---
# <a name="default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control"></a>默认键盘和鼠标处理 Windows 窗体 DataGridView 控件中

下表描述了用户如何与交互<xref:System.Windows.Forms.DataGridView>控制通过键盘和鼠标。  
  
> [!NOTE]
>  若要自定义键盘行为，可以处理标准键盘事件，如<xref:System.Windows.Forms.Control.KeyDown>。 但是，在编辑模式下，寄宿编辑控件接收键盘输入和键盘事件将不会对<xref:System.Windows.Forms.DataGridView>控件。 若要处理编辑控件事件，请将您的处理程序附加到编辑控件中<xref:System.Windows.Forms.DataGridView.EditingControlShowing>事件处理程序。 或者，你可以自定义中的键盘行为<xref:System.Windows.Forms.DataGridView>通过重写子类<xref:System.Windows.Forms.DataGridView.ProcessDialogKey%2A>和<xref:System.Windows.Forms.DataGridView.ProcessDataGridViewKey%2A>方法。  
  
## <a name="default-keyboard-handling"></a>默认键盘处理  
  
### <a name="basic-navigation-and-entry-keys"></a>基本的导航和项键  
  
|键或键组合|描述|  
|----------------------------|-----------------|  
|向下键|将焦点移到当前单元格的正下方的单元格。 如果焦点位于最后一行中，没有任何影响。|  
|向左键|将焦点移到上一个单元格的行中。 如果焦点位于行中的第一个单元，没有任何影响。|  
|向右键|将焦点移到下一个单元格的行中。 如果焦点位于行中的最后一个单元格，没有任何影响。|  
|向上键|将焦点移到当前单元格的正上方的单元格。 如果焦点位于第一行中，没有任何影响。|  
|Home|将焦点移到当前行中的第一个单元。|  
|End|将焦点移到当前行中的最后一个单元。|  
|Page Down|将控件向下滚动完全显示的行数。 将焦点移动到完全显示的最后一行，而无需更改的列。|  
|Page Up|控件向上滚动完全显示的行数。 将焦点移到而无需更改列显示的第一行。|  
|Tab|如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`false`，会将焦点移到下一个单元格的当前行。 如果焦点已在行的最后一个单元中，将焦点移到下一行中的第一个单元。 如果焦点在控件中的最后一个单元中，将焦点移到下一个控件的父容器的 tab 键顺序。<br /><br /> 如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`true`，会将焦点移到下一个控件的父容器的 tab 键顺序。|  
|Shift+Tab|如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`false`，会将焦点移到上一个单元格的当前行中。 如果焦点已在行的第一个单元中，将焦点移到上一行中的最后一个单元。 如果焦点在控件中的第一个单元中，将焦点移到上一个控件的父容器的 tab 键顺序。<br /><br /> 如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`true`，会将焦点移到上一个控件的父容器的 tab 键顺序。|  
|Ctrl+Tab|如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`false`，会将焦点移到下一个控件的父容器的 tab 键顺序。<br /><br /> 如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`true`，会将焦点移到下一个单元格的当前行。 如果焦点已在行的最后一个单元中，将焦点移到下一行中的第一个单元。 如果焦点在控件中的最后一个单元中，将焦点移到下一个控件的父容器的 tab 键顺序。|  
|Ctrl+Shift+Tab|如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`false`，会将焦点移到上一个控件的父容器的 tab 键顺序。<br /><br /> 如果<xref:System.Windows.Forms.DataGridView.StandardTab%2A>属性值是`true`，会将焦点移到上一个单元格的当前行中。 如果焦点已在行的第一个单元中，将焦点移到上一行中的最后一个单元。 如果焦点在控件中的第一个单元中，将焦点移到上一个控件的父容器的 tab 键顺序。|  
|CTRL + 箭头|将焦点移到的最远的单元格的箭头的方向。|  
|CTRL + HOME|将焦点移到控件中的第一个单元。|  
|CTRL + END|将焦点移到控件中的最后一个单元。|  
|CTRL + PAGE 减少/增加|PAGE down 键或 PAGE UP 相同。|  
|F2|将当前单元格放入单元格编辑模式下，如果<xref:System.Windows.Forms.DataGridView.EditMode%2A>属性值是<xref:System.Windows.Forms.DataGridViewEditMode.EditOnF2>或<xref:System.Windows.Forms.DataGridViewEditMode.EditOnKeystrokeOrF2>。|
|F3|如果对当前列进行排序<xref:System.Windows.Forms.DataGridViewColumn.SortMode%2A?displayProperty=nameWithType>属性值是<xref:System.Windows.Forms.DataGridViewColumnSortMode.Automatic>。 它等同于单击当前列标题。 自.NET Framework 4.7.2 之后可用。 若要启用此功能，应用程序必须面向.NET Framework 4.7.2 或更高版本或明确选择使用 AppContext 开关的辅助功能改进。|  
|F4|如果当前单元格<xref:System.Windows.Forms.DataGridViewComboBoxCell>，使单元格进入编辑模式，并显示下拉列表。|  
|ALT + 向上/向下键|如果当前单元格<xref:System.Windows.Forms.DataGridViewComboBoxCell>，使单元格进入编辑模式，并显示下拉列表。|  
|空格键|如果当前单元格<xref:System.Windows.Forms.DataGridViewButtonCell>， <xref:System.Windows.Forms.DataGridViewLinkCell>，或<xref:System.Windows.Forms.DataGridViewCheckBoxCell>，将引发<xref:System.Windows.Forms.DataGridView.CellClick>和<xref:System.Windows.Forms.DataGridView.CellContentClick>事件。 如果当前单元格<xref:System.Windows.Forms.DataGridViewButtonCell>，还会按下按钮。 如果当前单元格<xref:System.Windows.Forms.DataGridViewCheckBoxCell>，也会更改的复选状态。|  
|Enter|提交到当前单元格和行的任何更改并将焦点移到当前单元格的正下方的单元格。 如果焦点位于最后一行中，而无需移动焦点提交任何更改。|  
|ESC|如果控件处于编辑模式下，取消编辑。 如果控件不处于编辑模式中，将恢复如果该控件绑定到支持编辑数据源已对当前行进行任何更改或已与行级提交作用域中实现虚拟模式。|  
|退格符|编辑单元格时，请删除在插入点之前的字符。|  
|DELETE|编辑单元格时，请在插入点后删除的字符。|  
|Ctrl+Enter|而无需将焦点移动到当前单元格提交任何更改。 此外提交对当前行，如果该控件绑定到数据源支持的编辑或虚拟模式的任何更改已实现使用行级提交作用域。|  
|Ctrl+0|进入<xref:System.DBNull.Value?displayProperty=nameWithType>值到当前单元格，如果可以编辑该单元格。 默认情况下的显示值为<xref:System.DBNull>单元格的值为值<xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A>属性的<xref:System.Windows.Forms.DataGridViewCellStyle>作用于当前单元格。|  
  
### <a name="selection-keys"></a>选择键

 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>属性设置为`false`并<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>属性设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.CellSelect>，通过使用导航键来更改当前单元格选定内容更改到新的单元格。 SHIFT、 CTRL 和 ALT 键不会影响此行为。  
  
 如果<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect>或<xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>，会发生相同的行为，但带有以下添加内容。  
  
|键或键组合|描述|  
|----------------------------|-----------------|  
|SHIFT + 空格键|将选择整行或列 （与单击行或列标题相同）。|  
|导航键 （箭头键，页面向上主页，结束）|如果选择整行或列，则更改为新行或列的当前单元格将所选内容移动到完整的新行或列 （具体取决于选择模式中）。|  
  
 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>设置为`false`并<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect>或<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>，通过使用键盘更改到新行或列的当前单元格将选项移到完整的新行或列。 SHIFT、 CTRL 和 ALT 键不会影响此行为。  
  
 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>设置为`true`、 导航行为不会更改，但按下 shift 键 （包括 CTRL + SHIFT） 时使用键盘导航将修改多单元格的选择。 导航开始之前，该控件将当前单元格标记为定位单元格。 导航在按住 SHIFT 的同时，所选内容将包括当前单元格的定位单元格之间的所有单元格。 如果已选择它们，但如果的键盘导航暂时将其置于当前单元格的定位单元格之间则会取消选定，则在控件中的其他单元格将保持选中状态。  
  
 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>设置为`true`并<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect>或<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>，当前单元格的定位单元格的行为是相同的但仅完整行或列被选中或取消选择。  
  
## <a name="default-mouse-handling"></a>默认的鼠标处理
  
### <a name="basic-mouse-handling"></a>基本的鼠标处理
  
> [!NOTE]
>  单击鼠标左键的单元格始终将更改当前单元格。 单击鼠标右键按钮包含的单元格将打开快捷菜单，其中一个可用时。  
  
|鼠标操作|描述|  
|------------------|-----------------|  
|向下鼠标左键|可单击的单元格的当前单元格，并引发<xref:System.Windows.Forms.DataGridView.CellMouseDown?displayProperty=nameWithType>事件。|  
|释放鼠标左键|引发 <xref:System.Windows.Forms.DataGridView.CellMouseUp?displayProperty=nameWithType> 事件|  
|单击鼠标左键|将引发<xref:System.Windows.Forms.DataGridView.CellClick?displayProperty=nameWithType>和<xref:System.Windows.Forms.DataGridView.CellMouseClick?displayProperty=nameWithType>事件|  
|向下鼠标左键并拖动列标题单元格上|如果<xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=nameWithType>属性是`true`，移动所列，以便它可以放入新的位置。|  
  
### <a name="mouse-selection"></a>鼠标选择

 没有选择行为是与鼠标中键或鼠标滚轮相关联。  
  
 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>属性设置为`false`并<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>属性设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.CellSelect>，出现以下行为。  
  
|鼠标操作|描述|  
|------------------|-----------------|  
|单击鼠标左键|如果用户单击一个单元格，请选择仅当前单元格。 如果用户单击行或列标题没有选择行为。|  
|单击鼠标右键按钮|如果有的话，则显示快捷菜单。|  
  
 相同的行为发生时<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect>或<xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>，区别在于，具体取决于选择模式下，单击行或列标题将选择整行或列并设置当前单元格行或列中的第一个单元格。  
  
 如果<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect>或<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>，单击行或列中的任何单元格将选择整行或列。  
  
 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>设置为`true`，在按住 CTRL 或 SHIFT 的同时单击某个单元格将修改多单元格的选择。  
  
 时按住 CTRL 的同时单击的单元格，单元格将更改其选择状态，而所有其他单元格将保留其当前选择状态。  
  
 在按住 SHIFT 的同时单击一个单元格或一系列单元格，所选内容将包括当前单元格和定位单元格位于第一次单击之前的当前单元格的位置之间的所有单元格。 单击并拖动指针跨多个单元格的定位单元格时，单击拖动操作开始处的单元格。 随后按下 shift 键的同时单击更改当前单元格，但不是定位单元格。 如果已选择它们，但如果鼠标导航暂时将其置于当前单元格的定位单元格之间则会取消选定，则在控件中的其他单元格将保持选中状态。  
  
 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>设置为`true`并<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect>或<xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect>，在按住 SHIFT 的同时单击行或列标题 （具体取决于所选内容模式下） 将修改现有选择整行或列，如果此类所选内容存在。 否则为它将清除所选内容并开始新的完整行或列的选择。 在按住 CTRL 的同时单击行或列标题，但是，将添加或删除被单击的行或列从当前所选内容而无需以其他方式修改当前所选内容。  
  
 如果<xref:System.Windows.Forms.DataGridView.MultiSelect%2A>设置为`true`并<xref:System.Windows.Forms.DataGridView.SelectionMode%2A>设置为<xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect>或<xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect>、 按 SHIFT 或 CTRL 键同时单击某个单元格同样的行为除外，只能使用完整的行和列会受到影响。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.DataGridView>
- [DataGridView 控件](datagridview-control-windows-forms.md)
