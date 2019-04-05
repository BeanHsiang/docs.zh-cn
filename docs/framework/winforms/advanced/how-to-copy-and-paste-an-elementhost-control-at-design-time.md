---
title: 如何：复制并粘贴 ElementHost 控件在设计时
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, content copying and pasting
- interoperability [WPF]
- ElementHost control [Windows Forms], copying and pasting at design time
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: e570375d-2a68-44ba-b4f7-c781af2d20e8
ms.openlocfilehash: 203a01ef82554bf4104f3000c0821cceeafac9f7
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710415"
---
# <a name="how-to-copy-and-paste-an-elementhost-control-at-design-time"></a>如何：复制并粘贴 ElementHost 控件在设计时
此过程演示如何将复制在 Windows 窗体上的 Windows Presentation Foundation (WPF) 控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-copy-and-paste-an-elementhost-control-at-design-time"></a>若要复制并粘贴 ElementHost 控件在设计时  
  
1.  添加新的 WPF<xref:System.Windows.Controls.UserControl>到 Windows 窗体项目。 使用控件类型的默认名称，`UserControl1.xaml`。 有关详细信息，请参见[演练：在设计时在 Windows 窗体上创建新的 WPF 内容](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  在中**属性**窗口中，设置的值<xref:System.Windows.FrameworkElement.Width%2A>并<xref:System.Windows.FrameworkElement.Height%2A>的属性`UserControl1`到`200`。  
  
3.  将 <xref:System.Windows.Controls.Control.Background%2A> 属性的值设置为 `Blue`。  
  
4.  生成项目。  
  
5.  在 Windows 窗体设计器中打开 `Form1`。  
  
6.  从**工具箱**，将拖动的一个实例`UserControl1`拖到窗体。  
  
     
  `UserControl1` 的实例托管在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
7.  选择`elementHost1` 后，按 CTRL + C 将它复制到剪贴板。  
  
8.  按 CTRL + V 粘贴复制的控件拖到窗体。  
  
     一个新<xref:System.Windows.Forms.Integration.ElementHost>名为控件`elementHost2`窗体上创建。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [迁移和互操作性](../../wpf/advanced/migration-and-interoperability.md)
- [使用 WPF 控件](using-wpf-controls.md)
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
