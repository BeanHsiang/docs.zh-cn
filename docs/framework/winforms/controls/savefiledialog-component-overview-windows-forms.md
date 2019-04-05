---
title: SaveFileDialog 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- SaveFileDialog
helpviewer_keywords:
- Save File dialog box [Windows Forms], displaying
- SaveFileDialog component [Windows Forms], about SaveFileDialog
ms.assetid: be7a625f-46fd-4d06-9985-b613dcbf9bd2
ms.openlocfilehash: 93bf0f63e18ee3a384aa062c80faa991b68a6abe
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57721497"
---
# <a name="savefiledialog-component-overview-windows-forms"></a>SaveFileDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.SaveFileDialog> 组件是一个预配置的对话框。 它是标准相同**保存文件**对话框中使用的 Windows。 它继承自 <xref:System.Windows.Forms.CommonDialog> 类。  
  
## <a name="working-with-the-savefiledialog-component"></a>使用 SaveFileDialog 组件  
 使用它作为一个简单的解决方案，使用户能够保存文件而不是配置你自己的对话框。 利用标准 Windows 对话框，您创建的应用程序的基本功能是立即为用户所熟悉。 但是，应注意，当使用<xref:System.Windows.Forms.SaveFileDialog>组件，您必须编写您自己保存文件的逻辑。  
  
 可以使用<xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>方法，以便在运行时显示的对话框。 您可以打开文件中读/写模式下使用<xref:System.Windows.Forms.SaveFileDialog.OpenFile%2A>方法。  
  
 添加到窗体时<xref:System.Windows.Forms.SaveFileDialog>组件在 Windows 窗体设计器底部的任务栏中显示。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.SaveFileDialog>
- [SaveFileDialog 组件](savefiledialog-component-windows-forms.md)
