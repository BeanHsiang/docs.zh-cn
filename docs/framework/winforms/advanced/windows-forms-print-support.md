---
title: Windows 窗体打印支持
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, printing
- printing [Windows Forms]
- forms [Windows Forms], printing (using designer)
- printing [Windows Forms], Windows Forms, support
- printing [Windows Forms], print support
ms.assetid: a4a2960c-eb70-48e2-b641-cfb222704e46
ms.openlocfilehash: 8e008f2cb4b2f32cdba676e68d9fd790530e2b06
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708127"
---
# <a name="windows-forms-print-support"></a>Windows 窗体打印支持
使用的主要包含在 Windows 窗体中的打印[PrintDocument 组件](../controls/printdocument-component-windows-forms.md)组件，使用户能够打印，并[PrintPreviewDialog 控件](../controls/printpreviewdialog-control-windows-forms.md)控件， [PrintDialog组件](../controls/printdialog-component-windows-forms.md)并[PageSetupDialog 组件](../controls/pagesetupdialog-component-windows-forms.md)要向用户习惯于 Windows 操作系统提供熟悉的图形界面的组件。  
  
 通常情况下，创建的新实例<xref:System.Drawing.Printing.PrintDocument>组件，将设置描述打印使用内容的属性<xref:System.Drawing.Printing.PrinterSettings>并<xref:System.Drawing.Printing.PageSettings>类，并调用<xref:System.Drawing.Printing.PrintDocument.Print%2A>方法来实际打印文档。  
  
 从基于 Windows 的应用程序，打印期间<xref:System.Drawing.Printing.PrintDocument>组件会警告用户正在进行打印的这一事实，并允许打印作业要取消显示中止打印对话框。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：创建标准 Windows 窗体打印作业](how-to-create-standard-windows-forms-print-jobs.md)  
 说明如何使用<xref:System.Drawing.Printing.PrintDocument>组件从 Windows 窗体中打印。  
  
 [如何：在运行时捕获用户输入从 PrintDialog](how-to-capture-user-input-from-a-printdialog-at-run-time.md)  
 说明如何修改所选的打印选项，以编程方式使用<xref:System.Windows.Forms.PrintDialog>组件。  
  
 [如何：选择连接到在 Windows 窗体中的用户的计算机的打印机](how-to-choose-the-printers-attached-to-user-computer-in-windows-forms.md)  
 介绍更改打印机来打印到使用<xref:System.Windows.Forms.PrintDialog>在运行时组件。  
  
 [如何：在 Windows 窗体中打印图形](how-to-print-graphics-in-windows-forms.md)  
 介绍向打印机发送图形。  
  
 [如何：打印 Windows 窗体中的多页文本文件](how-to-print-a-multi-page-text-file-in-windows-forms.md)  
 描述向打印机发送文本。  
  
 [如何：完整的 Windows 窗体打印作业](how-to-complete-windows-forms-print-jobs.md)  
 介绍如何向完成的打印作业的用户发出警报。  
  
 [如何：打印 Windows 窗体](how-to-print-a-windows-form.md)  
 演示如何打印一份当前窗体。  
  
 [如何：使用打印预览的 Windows 窗体中打印](how-to-print-in-windows-forms-using-print-preview.md)  
 演示如何使用<xref:System.Windows.Forms.PrintPreviewDialog>用于打印文档。  
  
## <a name="related-sections"></a>相关章节  
 [PrintDocument 组件](../controls/printdocument-component-windows-forms.md)  
 说明使用方式的<xref:System.Drawing.Printing.PrintDocument>组件。  
  
 [PrintDialog 组件](../controls/printdialog-component-windows-forms.md)  
 说明使用方式的<xref:System.Windows.Forms.PrintDialog>组件。  
  
 [PrintPreviewDialog 控件](../controls/printpreviewdialog-control-windows-forms.md)  
 说明使用方式的<xref:System.Windows.Forms.PrintPreviewDialog>控件。  
  
 [PageSetupDialog 组件](../controls/pagesetupdialog-component-windows-forms.md)  
 说明使用方式的<xref:System.Windows.Forms.PageSetupDialog>组件。  
  
 <xref:System.Drawing.Printing>  
 描述中的类<xref:System.Drawing.Printing>命名空间。
