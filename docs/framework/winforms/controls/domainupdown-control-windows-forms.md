---
title: DomainUpDown 控件（Windows 窗体）
ms.date: 03/30/2017
helpviewer_keywords:
- DomainUpDown control [Windows Forms]
- spin button control [Windows Forms], up-down controls
- up-down controls
- spin button control
- up-down controls [Windows Forms], spin button controls
ms.assetid: fb7cf017-e931-4a95-9d21-8caee4ee122a
ms.openlocfilehash: 83d674e3fb7ff7e715b75c635b891cd4e9703a21
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704518"
---
# <a name="domainupdown-control-windows-forms"></a>DomainUpDown 控件（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.DomainUpDown>如下所示的文本框中组合和一对按钮的控件用于列表中向上或向下移动。 该控件显示并从选项列表中设置一个文本字符串。 用户可以选择字符串，通过单击向上和向下按钮以浏览列表中，通过按向上和向下箭头键，或通过键入与匹配列表中的项的字符串。 此控件的可能用途之一是从名称按字母顺序排序列表中选择项。 (若要对列表进行排序，设置<xref:System.Windows.Forms.DomainUpDown.Sorted%2A>属性设置为`true`。)此控件的功能是非常类似于列表框或组合框中，但其占用空间很少。  
  
 控件的主要属性包括<xref:System.Windows.Forms.DomainUpDown.Items%2A>， <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A>，和<xref:System.Windows.Forms.DomainUpDown.Wrap%2A>。 <xref:System.Windows.Forms.DomainUpDown.Items%2A>属性包含的控件中显示其文本值的对象的列表。 如果<xref:System.Windows.Forms.UpDownBase.ReadOnly%2A>设置为`false`，该控件自动完成用户类型，并为列表中的值匹配的文本。 如果<xref:System.Windows.Forms.DomainUpDown.Wrap%2A>设置为`true`，滚过最后一项将转到第一个项列表中，反之亦然。 控件的主要方法是<xref:System.Windows.Forms.DomainUpDown.UpButton%2A>和<xref:System.Windows.Forms.DomainUpDown.DownButton%2A>。  
  
 此控件只显示文本字符串。 如果你想显示的数字值的控件，使用<xref:System.Windows.Forms.NumericUpDown>控件。 有关详细信息，请参阅[NumericUpDown 控件](numericupdown-control-windows-forms.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [DomainUpDown 控件概述](domainupdown-control-overview-windows-forms.md)  
 引入了的一般概念<xref:System.Windows.Forms.DomainUpDown>控件，它允许用户通过浏览和选择从文本字符串的列表。  
  
 [如何：以编程方式将项添加到 Windows 窗体 DomainUpDown 控件](how-to-add-items-to-windows-forms-domainupdown-controls-programmatically.md)  
 介绍如何指定文本字符串<xref:System.Windows.Forms.DomainUpDown>控件应显示。  
  
 [如何：从 Windows 窗体 DomainUpDown 控件移除项](how-to-remove-items-from-windows-forms-domainupdown-controls.md)  
 描述如何删除项从<xref:System.Windows.Forms.DomainUpDown>在代码中的控件。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.DomainUpDown>  
 对此类进行描述，并提供指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.NumericUpDown>  
 对此类进行描述并提供指向其所有成员...  
  
## <a name="related-sections"></a>相关章节  
 [可在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)  
 提供 Windows 窗体控件的完整列表，附带其使用情况相关信息的链接。
