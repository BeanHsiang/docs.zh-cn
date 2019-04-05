---
title: 如何：与使用设计器在 Windows 窗体面板控件的组控件
ms.date: 03/30/2017
helpviewer_keywords:
- Panel control [Windows Forms], grouping controls
- controls [Windows Forms], grouping
- Windows Forms controls, grouping
ms.assetid: 7e1cd708-fdb1-49d8-9ca2-5640b276bf2e
ms.openlocfilehash: f1aa3b54eb842bb92e4ae2cbb562a11464acac63
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57717437"
---
# <a name="how-to-group-controls-with-the-windows-forms-panel-control-using-the-designer"></a>如何：与使用设计器在 Windows 窗体面板控件的组控件
Windows 窗体<xref:System.Windows.Forms.Panel>控件用于分组其他控件。 有三个原因与组控件。 一个是 visual 对于清除用户界面; 相关窗体元素的分组另一种是以编程方式分组的单选按钮，例如;最后一个是用于在设计时作为一个单元移动控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-create-a-group-of-controls"></a>若要创建的一组控件  
  
1.  拖动<xref:System.Windows.Forms.Panel>控件从**Windows 窗体**拖到窗体工具箱选项卡中的。  
  
2.  将其他控件添加到每个面板内绘制的面板。  
  
     如果你想要将括在面板中的现有控件，可以选择所有控件，将它们剪切到剪贴板，再都选择<xref:System.Windows.Forms.Panel>控件，然后再将其粘贴到面板。 您还可以将它们拖到面板。  
  
3.  （可选）如果你想要将边框添加到面板，设置其<xref:System.Windows.Forms.BorderStyle>属性。 有三种选择： <xref:System.Windows.Forms.BorderStyle.Fixed3D>， <xref:System.Windows.Forms.BorderStyle.FixedSingle>，和<xref:System.Windows.Forms.BorderStyle.None>。  
  
## <a name="see-also"></a>请参阅
- [Panel 控件](panel-control-windows-forms.md)
- [Panel 控件概述](panel-control-overview-windows-forms.md)
- [如何：设置面板的背景](how-to-set-the-background-of-a-windows-forms-panel.md)
