---
title: PageSetupDialog 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- PageSetupDialog
helpviewer_keywords:
- Page Setup dialog box [Windows Forms], displaying
- PageSetupDialog component
ms.assetid: 791caacb-a5ca-4fca-bad9-1a5721ad697c
ms.openlocfilehash: 702e9a40652e00cc2f93dd52af29a61a50c90ae0
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715797"
---
# <a name="pagesetupdialog-component-overview-windows-forms"></a>PageSetupDialog 组件概述（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.PageSetupDialog>组件是一个预配置的对话框，用于在基于 Windows 的应用程序中设置用于打印的页详细信息。 用于在基于 Windows 的应用程序中作为一个简单的解决方案为用户设置首选项而不是配置您自己的对话框。 可以使用户能够设置边框和边距调整、 页眉和页脚和纵向或横向布局。 利用标准的 Windows 对话框，你可以创建其基本功能可立即为用户所熟悉的应用程序。  
  
## <a name="key-properties-and-methods"></a>键属性和方法  
 使用<xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>方法，以便在运行时显示对话框。 此组件具有可以设置与单个页面的属性 (<xref:System.Drawing.Printing.PrintDocument>类) 或任何文档 (<xref:System.Drawing.Printing.PageSettings>类)。 此外，<xref:System.Windows.Forms.PageSetupDialog>组件可用于确定特定的打印机设置，它们将存储在<xref:System.Drawing.Printing.PrinterSettings>类。  
  
 添加到窗体时<xref:System.Windows.Forms.PageSetupDialog>组件在 Windows 窗体设计器底部的任务栏中显示。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.PageSetupDialog>
- [PageSetupDialog 组件](pagesetupdialog-component-windows-forms.md)
