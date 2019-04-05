---
title: 如何：用 Windows 窗体使用设计器创建多窗格用户界面
ms.date: 03/30/2017
helpviewer_keywords:
- user interface [Windows Forms], multipane
- SplitContainer control [Windows Forms], using the designer
- multipane user interface
ms.assetid: c3f9294d-a26c-4198-9242-f237f55f7573
ms.openlocfilehash: 1ad446fde4ccfc9ad9c48e619321deed044f1014
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713769"
---
# <a name="how-to-create-a-multipane-user-interface-with-windows-forms-using-the-designer"></a>如何：用 Windows 窗体使用设计器创建多窗格用户界面
在下面的过程中，将创建类似于在 Microsoft Outlook 中使用与多窗格用户界面**文件夹**列表中，**消息**窗格中，和一个**预览**窗格。 这种排列方式被实现主要通过处理该窗体控件停靠。  
  
 停靠控件时，您可以确定控件固定的父容器的边缘。 因此，如果您设置<xref:System.Windows.Forms.SplitContainer.Dock%2A>属性设置为<xref:System.Windows.Forms.DockStyle.Right>，将在该控件的右边缘停靠到其父控件的右边缘。 此外，该控件的停靠的边缘调整大小以匹配的它的容器控件。 详细了解如何<xref:System.Windows.Forms.SplitContainer.Dock%2A>属性的工作原理，请参阅[如何：在 Windows 窗体上停靠控件](how-to-dock-controls-on-windows-forms.md)。  
  
 此过程重点介绍排列<xref:System.Windows.Forms.SplitContainer>和其他控件在窗体上，而不上添加功能以使应用程序模仿 Microsoft Outlook。  
  
 若要创建此用户界面，您将中的所有控件<xref:System.Windows.Forms.SplitContainer>控件，它包含<xref:System.Windows.Forms.TreeView>左侧面板中的控件。 右侧面板中的<xref:System.Windows.Forms.SplitContainer>控件包含第二个<xref:System.Windows.Forms.SplitContainer>控件替换<xref:System.Windows.Forms.ListView>控制上述<xref:System.Windows.Forms.RichTextBox>控件。 这些<xref:System.Windows.Forms.SplitContainer>控件启用独立调整大小的窗体上的其他控件。 您可以改写此过程，以制作出的您自己的自定义用户界面中的技术。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-create-an-outlook-style-user-interface-at-design-time"></a>若要在设计时创建的 Outlook 样式用户界面  
  
1.  创建新的 Windows 应用程序项目 (**文件** > **新建** > **项目** > **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**)。  
  
2.  拖动<xref:System.Windows.Forms.SplitContainer>控件从**工具箱**到窗体。 在“属性”  窗口中，将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle.Fill>。  
  
3.  拖动<xref:System.Windows.Forms.TreeView>控件从**工具箱**的左侧面板到<xref:System.Windows.Forms.SplitContainer>控件。 在中**属性**窗口中，将<xref:System.Windows.Forms.SplitContainer.Dock%2A>属性设置为<xref:System.Windows.Forms.DockStyle.Left>通过单击左侧面板中单击向下箭头时显示的值编辑器中。  
  
4.  将另一个<xref:System.Windows.Forms.SplitContainer>控件从**工具箱**; 将其放在右侧面板中的<xref:System.Windows.Forms.SplitContainer>向窗体添加的控件。 在中**属性**窗口中，将<xref:System.Windows.Forms.SplitContainer.Dock%2A>属性设置为<xref:System.Windows.Forms.DockStyle.Fill>并<xref:System.Windows.Forms.SplitContainer.Orientation%2A>属性设置为<xref:System.Windows.Forms.Orientation.Horizontal>。  
  
5.  拖动<xref:System.Windows.Forms.ListView>控件从**工具箱**到第二个的上部面板<xref:System.Windows.Forms.SplitContainer>向窗体添加的控件。 将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 控件的 <xref:System.Windows.Forms.ListView> 属性设置为 <xref:System.Windows.Forms.DockStyle.Fill>。  
  
6.  拖动<xref:System.Windows.Forms.RichTextBox>控件从**工具箱**到较低的第二个面板<xref:System.Windows.Forms.SplitContainer>控件。 将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 控件的 <xref:System.Windows.Forms.RichTextBox> 属性设置为 <xref:System.Windows.Forms.DockStyle.Fill>。  
  
     此时，如果按 F5 运行该应用程序时，窗体将显示类似于 Microsoft Outlook 的三部分组成的用户界面。  
  
    > [!NOTE]
    >  将鼠标指针放于任何在拆分器<xref:System.Windows.Forms.SplitContainer>控件，可以调整大小的内部尺寸。  
  
     此时应用程序开发中了精心设计复杂的用户界面。 下一步是继续进行编程的应用程序本身，可能是通过连接<xref:System.Windows.Forms.TreeView>控件和<xref:System.Windows.Forms.ListView>到某种类型的数据源的控件。 有关连接到数据控件的详细信息，请参阅[数据绑定和 Windows 窗体](../data-binding-and-windows-forms.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.SplitContainer>
- [SplitContainer 控件](splitcontainer-control-windows-forms.md)
