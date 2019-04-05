---
title: Windows 窗体 DataGrid 控件的键盘快捷键
ms.date: 03/30/2017
helpviewer_keywords:
- keyboard shortcuts [Windows Forms], DataGrid control
- DataGrid control [Windows Forms], navigation keys
ms.assetid: a01780f9-20d5-4f5f-808f-c790c9a007a5
ms.openlocfilehash: c04340cf2d2c8e318ea7348c978ef943563c24da
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711767"
---
# <a name="keyboard-shortcuts-for-the-windows-forms-datagrid-control"></a>Windows 窗体 DataGrid 控件的键盘快捷键
> [!NOTE]
>  
  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。 有关详细信息，请参阅 [Windows 窗体 DataGridView 控件与 DataGrid 控件之间的区别](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 下表列出了可用于在 Windows 窗体中导航的键盘快捷键<xref:System.Windows.Forms.DataGrid>控件：  
  
|操作|快捷键|  
|------------|--------------|  
|完成一个单元格输入并向下移动到下一个单元格。<br /><br /> 如果焦点在子表链接，则导航到该表。|Enter|  
|如果在单元格编辑模式下则取消单元格编辑。<br /><br /> 如果处于字幕选择模式，则取消编辑的行。|ESC|  
|编辑单元格时，请删除在插入点之前的字符。|退格符|  
|编辑单元格时，请删除后插入点的字符。|DELETE|  
|移动到当前行中的第一个单元。|Home|  
|移动到最后一个单元格的当前行中。|End|  
|突出显示的当前单元格中的字符并将光标移至行尾。 双击单元格的行为相同。|F2|  
|如果焦点位于单元格上，转到下一个单元格的行中。<br /><br /> 如果焦点位于行中的最后一个单元，将移动到行的第一个子表链接，然后展开它。<br /><br /> 如果焦点位于一个子链接，将移动到下一个子链接。<br /><br /> 如果焦点位于最后一个子链接，转到下一行的第一个单元。|Tab|  
|如果焦点位于单元格上，转到上一个单元格的行中。<br /><br /> 如果焦点位于行中的第一个单元，将移到上一行的最后一个展开的子表链接或移动到最后一个单元格的前一行。<br /><br /> 如果焦点位于一个子链接，将移动到上一个子链接。<br /><br /> 如果焦点位于第一个子链接，将移到最后一个单元格的前一行。|Shift+Tab|  
|将移动到下一个控件的 tab 键顺序。|Ctrl+Tab|  
|将移动到上一个控件的 tab 键顺序。|Ctrl+Shift+Tab|  
|如果在子表移到父表。 单击后退按钮相同的行为。|Alt+向左键|  
|展开子表提供了链接。 ALT + 向下箭头展开所有链接，而不仅仅是所选的链接。|ALT + 向下键或 CTRL + 加号|  
|折叠子表提供了链接。 ALT + 向上箭头折叠所有链接，而不仅仅是所选链接。|ALT + 向上键或 CTRL + 减号|  
|将移到箭头方向中的最远非空单元格。|CTRL + 箭头|  
|扩展选择一行 （不包括子表提供了链接） 的箭头的方向。|SHIFT + 向上/向下键|  
|扩展到最远非空行的 （不包括子表提供了链接） 的箭头方向选择。|CTRL + SHIFT + 向上/向下键|  
|将移动到左上角单元格。|CTRL + HOME|  
|移动到右下角单元格。|CTRL + END|  
|扩展将选择最上面一行的内容。|CTRL + SHIFT + HOME|  
|扩展到底部行选择。|CTRL + SHIFT + END|  
|选择当前行 （不包括子表提供了链接）。|SHIFT + 空格键|  
|选择整个网格 （不包括子表提供了链接）。|Ctrl+A|  
|显示子表中的父行。|Ctrl+Page Down|  
|隐藏子表中的父行。|Ctrl+Page Up|  
|向下扩展选择一个屏幕 （不包括子表提供了链接）。|Shift+Page Down|  
|向上扩展选择一个屏幕 （不包括子表提供了链接）。|Shift+Page Up|  
|调用<xref:System.Windows.Forms.DataGrid.EndEdit%2A>当前行的方法。|Ctrl+Enter|  
|输入<xref:System.DBNull.Value?displayProperty=nameWithType>在编辑模式下的单元格中的值。|Ctrl+0|  
  
## <a name="see-also"></a>请参阅
- [DataGrid 控件概述](datagrid-control-overview-windows-forms.md)
- [DataGrid 控件](datagrid-control-windows-forms.md)
