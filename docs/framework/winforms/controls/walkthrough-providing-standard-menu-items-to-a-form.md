---
title: 演练：向窗体提供标准菜单项
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- menu items [Windows Forms], standard
- toolbars [Windows Forms], walkthroughs
- StatusStrip control [Windows Forms]
- ToolStrip control [Windows Forms]
ms.assetid: dac37d98-589e-4d6d-9673-6437e8943122
ms.openlocfilehash: 846660fda37797e9d53d8f1d5a8a4f812d33e8df
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711754"
---
# <a name="walkthrough-providing-standard-menu-items-to-a-form"></a>演练：向窗体提供标准菜单项
可使用 <xref:System.Windows.Forms.MenuStrip> 控件向窗体提供标准菜单。  
  
 本演练演示如何使用<xref:System.Windows.Forms.MenuStrip>控件创建标准菜单。 在窗体还时用户选择菜单项的响应。 在本演练阐释了以下任务：  
  
-   创建一个 Windows 窗体项目。  
  
-   创建标准菜单。  
  
-   创建<xref:System.Windows.Forms.StatusStrip>控件。  
  
-   处理菜单项的选择。  
  
 完成，你将拥有带有标准菜单显示菜单项选择中的窗体<xref:System.Windows.Forms.StatusStrip>控件。  
  
 要将本主题中的代码作为单个列表进行复制，请参阅[如何：向窗体提供标准菜单项](how-to-provide-standard-menu-items-to-a-form.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，你将需要：  
  
-   若要能够创建和安装 Visual Studio 的计算机上运行 Windows 窗体应用程序项目的足够权限。  
  
## <a name="creating-the-project"></a>创建项目  
 第一步是创建项目并设置窗体。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
1.  创建一个名为 Windows 应用程序项目**StandardMenuForm** (**文件** > **新建** > **项目** >  **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**)。  
  
2.  在 Windows 窗体设计器中，选择窗体。  
  
## <a name="creating-a-standard-menu"></a>创建标准菜单  
 Windows 窗体设计器可以自动填充<xref:System.Windows.Forms.MenuStrip>带有标准菜单项控件。  
  
#### <a name="to-create-a-standard-menu"></a>创建标准菜单  
  
1.  从**工具箱**，拖动<xref:System.Windows.Forms.MenuStrip>控件拖到窗体上的。  
  
2.  单击<xref:System.Windows.Forms.MenuStrip>控件的智能标记标志符号 (![智能标记标志符号](./media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph"))，然后选择**插入标准项**。  
  
     <xref:System.Windows.Forms.MenuStrip>使用标准菜单项填充控件。  
  
3.  单击**文件**菜单项以查看其默认菜单项和对应的图标。  
  
## <a name="creating-a-statusstrip-control"></a>创建 StatusStrip 控件  
 使用<xref:System.Windows.Forms.StatusStrip>控件来显示 Windows 窗体应用程序的状态。 在本示例中，用户选择菜单项显示在<xref:System.Windows.Forms.StatusStrip>控件。  
  
#### <a name="to-create-a-statusstrip-control"></a>若要创建 StatusStrip 控件  
  
1.  从**工具箱**，拖动<xref:System.Windows.Forms.StatusStrip>控件拖到窗体上的。  
  
     <xref:System.Windows.Forms.StatusStrip>控件自动将停靠到窗体的底部。  
  
2.  单击<xref:System.Windows.Forms.StatusStrip>控件的下拉按钮并选择**statuslabel 设置**以添加<xref:System.Windows.Forms.ToolStripStatusLabel>控制对<xref:System.Windows.Forms.StatusStrip>控件。  
  
## <a name="handling-item-selection"></a>处理项选择  
 处理<xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked>事件，当用户选择菜单项时进行响应。  
  
#### <a name="to-handle-item-selection"></a>若要处理的项选择  
  
1.  单击**文件**菜单项，在创建创建标准菜单部分。  
  
2.  在“属性”窗口中，单击“事件”。  
  
3.  双击<xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked>事件。  
  
     Windows 窗体设计器生成的事件处理程序<xref:System.Windows.Forms.ToolStripDropDownItem.DropDownItemClicked>事件。  
  
4.  以下代码插入到的事件处理程序。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#3)]  
  
5.  插入`UpdateStatus`到窗体的实用程序方法定义。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StandardMenu#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StandardMenu#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StandardMenu/VB/Form1.vb#2)]  
  
## <a name="checkpoint"></a>检查点  
  
#### <a name="to-test-your-form"></a>若要测试你的窗体  
  
1.  按 F5 编译并运行你的窗体。  
  
2.  单击**文件**要打开的菜单的菜单项。  
  
3.  上**文件**菜单中，单击某一项以将其选中。  
  
     <xref:System.Windows.Forms.StatusStrip>控件显示所选的项。  
  
## <a name="next-steps"></a>后续步骤  
 在本演练中，已创建带有标准菜单窗体。 可以使用<xref:System.Windows.Forms.ToolStrip>实现多种其他用途的控件的系列：  
  
-   创建与控件的快捷菜单<xref:System.Windows.Forms.ContextMenuStrip>。 有关详细信息，请参阅[ContextMenu 组件概述](contextmenu-component-overview-windows-forms.md)。  
  
-   创建多文档界面 (MDI) 窗体通过停靠<xref:System.Windows.Forms.ToolStrip>控件。 有关详细信息，请参见[演练：创建具有菜单合并功能和 ToolStrip 控件的 MDI 窗体](walkthrough-creating-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)。  
  
-   提供你<xref:System.Windows.Forms.ToolStrip>控件专业的外观。 有关详细信息，请参阅[如何：设置 ToolStrip 呈现程序](how-to-set-the-toolstrip-renderer-for-an-application.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [MenuStrip 控件](menustrip-control-windows-forms.md)
