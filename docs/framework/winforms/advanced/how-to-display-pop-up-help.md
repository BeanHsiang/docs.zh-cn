---
title: 如何：显示弹出帮助
ms.date: 03/30/2017
helpviewer_keywords:
- pop-up Help
- Help [Windows Forms], pop-up Help
- Windows Forms, displaying Help
- forms [Windows Forms], displaying Help
- modal dialog boxes [Windows Forms], pop-up Help
- F1 Help [Windows Forms], in dialog boxes
- HelpProvider component [Windows Forms]
- Help [Windows Forms], adding to dialog boxes
ms.assetid: 218aa81e-e87e-4d67-af05-11627bbdce3b
ms.openlocfilehash: 875ed49e3a7dbe7205abb47ee1f2012d82826416
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711468"
---
# <a name="how-to-display-pop-up-help"></a>如何：显示弹出帮助
若要在 Windows 窗体上显示帮助的一种方法是通过**帮助**按钮，位于标题栏，可通过访问右侧<xref:System.Windows.Forms.Form.HelpButton%2A>属性。 此类型的“帮助”显示非常适用于对话框。 使用 <xref:System.Windows.Forms.Form.ShowDialog%2A> 方法适度显示的对话框在获取外部帮助系统时会遇到问题，因为必须先关闭模型对话框后才能切换到另一个窗口。 此外，使用**帮助**按钮，则需要无**最小化**按钮或**最大化**按钮的标题栏中所示。 这是一个标准对话框约定，而窗体通常具有**最小化**并**最大化**按钮。  
  
 请注意，你还可以使用 <xref:System.Windows.Forms.HelpProvider> 组件将控件链接到帮助系统中的文件，即使你已实现了弹出帮助。 有关详细信息，请参阅[Windows 应用程序中提供帮助](how-to-provide-help-in-a-windows-application.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-display-pop-up-help"></a>显示弹出帮助  
  
1.  拖动[HelpProvider](../controls/helpprovider-component-windows-forms.md)组件从工具箱拖到窗体。  
  
     它将显示在 Windows 窗体设计器底部的任务栏中。  
  
2.  在“属性”窗口，将 <xref:System.Windows.Forms.Form.HelpButton%2A> 属性设置为 `true`。 这将在窗体的标题栏右侧显示带问号的按钮。  
  
3.  为了显示 <xref:System.Windows.Forms.Form.HelpButton%2A>，必须将窗体的 <xref:System.Windows.Forms.Form.MinimizeBox%2A> 和 <xref:System.Windows.Forms.Form.MaximizeBox%2A> 属性设置为 `false`，将 <xref:System.Windows.Forms.Form.ControlBox%2A> 属性设置为 `true` 以及将 <xref:System.Windows.Forms.Form.FormBorderStyle%2A> 属性设置为下列值之一：<xref:System.Windows.Forms.FormBorderStyle.FixedSingle>、<xref:System.Windows.Forms.FormBorderStyle.Fixed3D>、<xref:System.Windows.Forms.FormBorderStyle.FixedDialog> 或 <xref:System.Windows.Forms.FormBorderStyle.Sizable>。  
  
4.  选择想在你的窗体上显示帮助的控件，然后在“属性”窗口设置“帮助”字符串。 这是将类似于窗口中显示的文本的字符串[工具提示](../controls/tooltip-component-windows-forms.md)。  
  
5.  按 F5 。  
  
6.  按**帮助**按钮的标题栏上，单击设置帮助字符串的控件。  
  
## <a name="see-also"></a>请参阅
- [使用工具提示的控件帮助](control-help-using-tooltips.md)
- [在 Windows 窗体中集成用户帮助](integrating-user-help-in-windows-forms.md)
- [Windows 窗体](../index.md)
