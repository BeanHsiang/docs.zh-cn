---
title: ErrorProvider 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- ErrorProvider
helpviewer_keywords:
- errors [Windows Forms], displaying to users
- error messages [Windows Forms], displaying
- ErrorProvider component [Windows Forms], about ErrorProvider component
ms.assetid: ced189f2-b5c8-46a7-a6f1-37f5af95dc99
ms.openlocfilehash: 61a8d4baba35a7a8a8ae221b054029eb59107d0e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716252"
---
# <a name="errorprovider-component-overview-windows-forms"></a>ErrorProvider 组件概述（Windows 窗体）
Windows 窗体[ErrorProvider](errorprovider-component-windows-forms.md)组件用来验证窗体或控件的用户输入。 它通常使用与验证窗体上的用户输入或显示在数据集中的错误。 错误提供程序是更好的选择与在消息框中，显示一条错误消息，因为一旦关闭消息框，则错误消息不再可见。 <xref:System.Windows.Forms.ErrorProvider>组件均显示一个错误图标 (![ErrorProvider 图标](./media/vberrorprovidericon.gif "vbErrorProviderIcon")) 相关的控件，例如文本框; 当用户鼠标指针悬停旁边错误图标工具提示出现，显示错误消息字符串。  
  
## <a name="key-properties"></a>键属性  
 <xref:System.Windows.Forms.ErrorProvider>组件的主要属性有<xref:System.Windows.Forms.ErrorProvider.DataSource%2A>， <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A>，和<xref:System.Windows.Forms.ErrorProvider.Icon%2A>。 使用时<xref:System.Windows.Forms.ErrorProvider>组件与数据绑定控件<xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A>属性必须设置为适当的容器 （通常是 Windows 窗体） 中要在窗体上显示一个错误图标的组件的顺序。 在设计器中，添加组件时<xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A>属性设置为包含窗体; 如果在代码中添加控件，则必须将其自己。  
  
 <xref:System.Windows.Forms.ErrorProvider.Icon%2A>属性可以设置为自定义错误图标而不是默认值。 当<xref:System.Windows.Forms.ErrorProvider.DataSource%2A>属性设置，<xref:System.Windows.Forms.ErrorProvider>组件可以显示的数据集的错误消息。 关键方法<xref:System.Windows.Forms.ErrorProvider>组件是<xref:System.Windows.Forms.ErrorProvider.SetError%2A>方法，用于指定错误消息字符串以及应显示错误图标的位置。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.ErrorProvider>组件没有可访问性客户端提供的内置支持。 若要使你的应用程序时使用此组件可访问，必须提供其他可访问的反馈机制。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ErrorProvider>
- [如何：在一个数据集中使用 Windows 窗体 ErrorProvider 组件查看错误](view-errors-within-a-dataset-with-wf-errorprovider-component.md)
- [如何：对于表格验证使用 Windows 窗体 ErrorProvider 组件显示错误图标](display-error-icons-for-form-validation-with-wf-errorprovider.md)
