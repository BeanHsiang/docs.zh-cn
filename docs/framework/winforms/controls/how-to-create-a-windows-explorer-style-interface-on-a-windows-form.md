---
title: 如何：在 Windows 窗体上创建一个 Windows 资源管理器样式界面
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Explorer [Windows Forms], creating with Windows Forms
- SplitContainer control [Windows Forms], Explorer-style interface
- forms [Windows Forms], Windows Explorer type
ms.assetid: 9a3d5f4f-5dda-4350-9ad5-57ce5976dc47
ms.openlocfilehash: 444d85265822b5dd4b3a5fd5f4329ec6cc1427f5
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705007"
---
# <a name="how-to-create-a-windows-explorerstyle-interface-on-a-windows-form"></a>如何：在 Windows 窗体上创建一个 Windows 资源管理器样式界面
Windows 资源管理器是由于其比较熟悉的应用程序的一个常见用户界面选择。  
  
 从根本上来说，Windows 资源管理器是<xref:System.Windows.Forms.TreeView>控件和一个<xref:System.Windows.Forms.ListView>上单独的面板的控件。 通过拆分器，面板进行可调整大小。 此类控件排列是用于显示和浏览信息非常有效。  
  
 以下步骤说明如何在 Windows 资源管理器类似的窗体中排列控件。 它们不显示如何添加 Windows 资源管理器应用程序的文件浏览功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-create-a-windows-explorer-style-windows-form"></a>若要创建 Windows 资源管理器样式 Windows 窗体  
  
1.  创建新的 Windows 应用程序项目 (**文件** > **新建** > **项目** > **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**)。  
  
2.  从**工具箱**:  
  
    1.  拖动<xref:System.Windows.Forms.SplitContainer>控件拖到窗体上的。  
  
    2.  拖动<xref:System.Windows.Forms.TreeView>控制**SplitterPanel1** (的面板<xref:System.Windows.Forms.SplitContainer>控制标记**Panel1**)。  
  
    3.  拖动<xref:System.Windows.Forms.ListView>控制**SplitterPanel2** (的面板<xref:System.Windows.Forms.SplitContainer>控制标记**Panel2**)。  
  
3.  通过按 CTRL 键并依次单击选择所有三个控件。 当选择<xref:System.Windows.Forms.SplitContainer>控件中，单击拆分条中，而不是面板。  
  
    > [!NOTE]
    >  不要使用**全**命令**编辑**菜单。 如果这样做下, 一步中所需的属性不会出现在**属性**窗口。  
  
4.  在“属性”  窗口中，将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle.Fill>。  
  
5.  按 F5 运行该应用程序。  
  
     窗体显示类似于在 Windows 资源管理器的两部分组成用户界面。  
  
    > [!NOTE]
    >  当拖动拆分器时，面板调整自身大小。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.SplitContainer>
- [如何：用 Windows 窗体创建多窗格用户界面](how-to-create-a-multipane-user-interface-with-windows-forms.md)
- [如何：定义大小调整和拆分窗口中定位行为](how-to-define-resize-and-positioning-behavior-in-a-split-window.md)
- [如何：水平拆分窗口](how-to-split-a-window-horizontally.md)
- [SplitContainer 控件](splitcontainer-control-windows-forms.md)
