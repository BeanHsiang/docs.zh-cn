---
title: OpenFileDialog 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- OpenFileDialog
helpviewer_keywords:
- OpenFileDialog component [Windows Forms], about OpenFileDialog
- Open File dialog box [Windows Forms], displaying in Windows Forms
ms.assetid: cd717300-46b6-4f82-8207-b218fa7fa407
ms.openlocfilehash: ad2fea74f0f3110ab2868064c588a7611d4261e3
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57702901"
---
# <a name="openfiledialog-component-overview-windows-forms"></a>OpenFileDialog 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.OpenFileDialog> 组件是一个预配置的对话框。 它是相同**打开的文件**公开的 Windows 操作系统的对话框。 它继承自 <xref:System.Windows.Forms.CommonDialog> 类。  
  
## <a name="using-this-component"></a>使用此组件  
 将在基于 Windows 的应用程序中的此组件作为一个简单的解决方案的文件选择而不用配置你自己的对话框。 利用标准的 Windows 对话框，你可以创建其基本功能可立即为用户所熟悉的应用程序。 但是，应注意，当使用<xref:System.Windows.Forms.OpenFileDialog>组件，您必须编写您自己的文件打开逻辑。  
  
 使用<xref:System.Windows.Forms.CommonDialog.ShowDialog%2A>方法，以便在运行时显示对话框。 可以让用户选择多个文件与要打开<xref:System.Windows.Forms.OpenFileDialog.Multiselect%2A>属性。 此外，还可以使用<xref:System.Windows.Forms.OpenFileDialog.ShowReadOnly%2A>属性来确定是否在对话框中显示只读复选框。 <xref:System.Windows.Forms.OpenFileDialog.ReadOnlyChecked%2A>属性指示是否选定只读复选框。 最后，<xref:System.Windows.Forms.FileDialog.Filter%2A>属性设置的当前文件名筛选器字符串，它确定在对话框中的"文件类型"框中显示的选项。  
  
 添加到窗体时<xref:System.Windows.Forms.OpenFileDialog>组件在 Windows 窗体设计器底部的任务栏中显示。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.OpenFileDialog>
- [OpenFileDialog 组件](openfiledialog-component-windows-forms.md)
