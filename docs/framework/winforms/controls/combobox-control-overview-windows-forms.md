---
title: ComboBox 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- ComboBox
helpviewer_keywords:
- drop-down lists [Windows Forms], Windows Forms
- ComboBox control [Windows Forms], about ComboBox control
- drop-down lists [Windows Forms], ComboBox control
- combo boxes [Windows Forms], about combo boxes
ms.assetid: a58b393f-a614-45d1-8961-857a024b5acd
ms.openlocfilehash: b20c3a5009367d807f548d93b7c1dfb50e5a7d8a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724003"
---
# <a name="combobox-control-overview-windows-forms"></a>ComboBox 控件概述（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.ComboBox>控件用于显示下拉组合框中的数据。 默认情况下，<xref:System.Windows.Forms.ComboBox>控件将显示在两个部分： 上半部分是允许用户键入列表项的文本框。 第二部分是显示的用户可以从中选择一个项列表的列表框。 有关其他样式组合框的详细信息，请参阅[何时使用 Windows 窗体 ComboBox Instead of ListBox](when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)。  
  
 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>属性返回对应的整数值到所选的列表项。 你可以以编程方式更改选定的项，通过更改<xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>代码中的值; 在组合框的文本框部分中将显示在列表中的相应项。 如果未不选择任何项，<xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>值为-1。 如果选择列表中的第一项，则<xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>值为 0。 <xref:System.Windows.Forms.ComboBox.SelectedItem%2A>属性是类似于<xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>，但返回项本身，而通常一个字符串值。 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A>属性反映了在列表中，项的数目和的值<xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A>属性始终为一个超过最大可能<xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>值，因为<xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>是从零开始。  
  
 若要添加或删除中的项<xref:System.Windows.Forms.ComboBox>控制，请使用<xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A>， <xref:System.Windows.Forms.ComboBox.ObjectCollection.Insert%2A>，<xref:System.Windows.Forms.ComboBox.ObjectCollection.Clear%2A>或<xref:System.Windows.Forms.ComboBox.ObjectCollection.Remove%2A>方法。 或者，您可以向列表添加项使用<xref:System.Windows.Forms.ComboBox.Items%2A>在设计器中的属性。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ComboBox>
- [ListBox 控件概述](listbox-control-overview-windows-forms.md)
- [何时使用 Windows 窗体 ComboBox 而非 ListBox](when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)
- [如何：添加和删除项从 Windows 窗体 ComboBox、 ListBox 或 CheckedListBox 控件](add-and-remove-items-from-a-wf-combobox.md)
- [如何：排序的内容的 Windows 窗体 ComboBox、 ListBox 或 CheckedListBox 控件](sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)
- [如何：访问特定于 Windows 中的项窗体 ComboBox、 ListBox 或 CheckedListBox 控件](access-specific-items-in-a-wf-combobox-listbox-or-checkedlistbox.md)
- [如何：将 Windows 窗体 ComboBox 或 ListBox 控件绑定到数据](how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)
- [用于列出选项的 Windows 窗体控件](windows-forms-controls-used-to-list-options.md)
- [如何：为 Windows 窗体 ComboBox、 ListBox 或 CheckedListBox 控件创建查找表](create-a-lookup-table-for-a-wf-combobox-listbox.md)
