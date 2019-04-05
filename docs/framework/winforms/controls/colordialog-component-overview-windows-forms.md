---
title: ColorDialog 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- ColorDialog
helpviewer_keywords:
- color dialog box [Windows Forms], about color dialog box
- ColorDialog component [Windows Forms], about ColorDialog
ms.assetid: 6dbdd8f0-f697-4728-bb09-7ea156f6d800
ms.openlocfilehash: 7dd48c8df0a36262962df596e8efadf4de1c2cd3
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713327"
---
# <a name="colordialog-component-overview-windows-forms"></a>ColorDialog 组件概述（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.ColorDialog>组件是一个预配置的对话框，允许用户从调色板选择颜色以及将自定义颜色添加到该调色板。 此对话框与在其他基于 Windows 的应用程序中看到的用于选择颜色的对话框相同。 在基于 Windows 的应用程序中，使用它作为一种替代配置自己对话框的简单解决方案。  
  
 中返回在对话框中选择的颜色<xref:System.Windows.Forms.ColorDialog.Color%2A>属性。 如果<xref:System.Windows.Forms.ColorDialog.AllowFullOpen%2A>属性设置为`false`、"自定义颜色"按钮处于禁用状态，并且用户仅限于调色板中的预定义颜色。 如果<xref:System.Windows.Forms.ColorDialog.SolidColorOnly%2A>属性设置为`true`，用户不能选择抖色的颜色。 若要显示对话框中，必须调用其<xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>方法。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ColorDialog>
- [ColorDialog 组件](colordialog-component-windows-forms.md)
- [对话框控件和组件](dialog-box-controls-and-components-windows-forms.md)
- [如何：更改 Windows 窗体 ColorDialog 组件的外观](how-to-change-the-appearance-of-the-windows-forms-colordialog-component.md)
