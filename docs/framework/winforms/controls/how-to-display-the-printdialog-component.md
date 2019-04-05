---
title: 如何显示 PrintDialog 组件
ms.date: 03/30/2017
helpviewer_keywords:
- Print dialog box [Windows Forms], displaying
- PrintDialog component [Windows Forms], displaying
- printing [Windows Forms], displaying print dialog box
ms.assetid: 745a8db7-0526-4b21-b09d-18e13ed32014
ms.openlocfilehash: 198ae75d407bd1837033a1cc186d84ff972fdc2f
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55285150"
---
# <a name="how-to-display-the-printdialog-component"></a>如何显示 PrintDialog 组件

<xref:System.Windows.Forms.PrintDialog>组件是许多用户都非常熟悉的标准 Windows 打印对话框。 由于你的用户将立即熟悉它，则将会有所帮助供你使用<xref:System.Windows.Forms.PrintDialog>组件。

## <a name="to-display-the-printdialog-component"></a>显示 PrintDialog 组件

- 调用<xref:System.Windows.Forms.Form.ShowDialog%2A>从你的应用程序的代码中的方法。

     显示出该组件后，用户可以与之进行交互，设置打印作业的属性。 这些都保存在<xref:System.Drawing.Printing.PrinterSettings>类 (和<xref:System.Drawing.Printing.PageSettings>类，如果用户访问[PageSetupDialog 组件](pagesetupdialog-component-windows-forms.md)通过<xref:System.Windows.Forms.PrintDialog>组件) 与该打印作业相关联。 然后可以调用它们所设置的属性以确定打印作业的细节。

## <a name="see-also"></a>请参阅

- [如何：创建标准 Windows 窗体打印作业](../advanced/how-to-create-standard-windows-forms-print-jobs.md)
- [如何：在运行时捕获用户输入从 PrintDialog](../advanced/how-to-capture-user-input-from-a-printdialog-at-run-time.md)
- [PrintPreviewDialog 控件](printpreviewdialog-control-windows-forms.md)
- [PrintDialog 组件](printdialog-component-windows-forms.md)
- [Windows 窗体打印支持](../advanced/windows-forms-print-support.md)
- [Windows 窗体控件](index.md)