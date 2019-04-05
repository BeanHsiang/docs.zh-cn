---
title: 如何：Move ToolStripMenuItems
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStripMenuItems [Windows Forms], moving
- menus [Windows Forms], arranging items
- ToolStripMenuItems [Windows Forms], dragging and dropping
- menu items [Windows Forms], moving
- menu items [Windows Forms], cutting and pasting
- menu items [Windows Forms], dragging and dropping
- MenuStrip control [Windows Forms], arranging items
- ToolStripMenuItems [Windows Forms], cutting and pasting
ms.assetid: cab9e03e-4edd-4c25-b3e3-bd1edc602bd9
ms.openlocfilehash: 50b5fd16780147ad7592035a901d993495dcb878
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708946"
---
# <a name="how-to-move-toolstripmenuitems"></a>如何：Move ToolStripMenuItems
在设计时，您可以将移动整个顶级菜单及其菜单项到其他位置<xref:System.Windows.Forms.MenuStrip>。 您还可以顶级菜单之间移动单个菜单项或更改菜单中的菜单项的位置。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-move-a-top-level-menu-and-its-menu-items-to-another-top-level-location"></a>若要将顶级菜单和菜单项移动到另一个顶级位置  
  
1.  单击并按住鼠标左键在你想要移动的菜单上。  
  
2.  将插入点拖到预期的新位置之前的顶级菜单并释放鼠标按钮。  
  
     所选的菜单将插入点右移。  
  
### <a name="to-move-a-top-level-menu-and-its-menu-items-to-a-drop-down-location"></a>若要将顶级菜单及其菜单项移动到下拉列表位置  
  
1.  左键单击想要移动并按 CTRL + X，或右键单击该菜单并选择**剪切**从快捷菜单。  
  
2.  在目标顶级菜单中，左键单击预期新位置上方的菜单项，按 CTRL + V，或右键单击预期新位置上方的菜单项并选择**粘贴**从快捷菜单。  
  
     你将剪切的菜单将插入到所选的菜单项之后。  
  
### <a name="to-move-a-menu-item-within-a-menu-using-the-items-collection-editor"></a>若要移动菜单使用项集合编辑器中的菜单项  
  
1.  右键单击包含你想要移动的菜单项的菜单。  
  
2.  从快捷菜单中，选择**编辑 Dropdownitem**。  
  
3.  在中**项集合编辑器**，左键单击想要移动的菜单项。  
  
4.  单击向上和向下箭头键移动菜单内的菜单项。  
  
5.  单击 **“确定”**。  
  
### <a name="to-move-a-menu-item-within-a-menu-using-the-keyboard"></a>若要移动菜单项在菜单中使用键盘  
  
1.  按住 ALT 键。  
  
2.  单击并按住鼠标左键你想要移动的菜单项。  
  
3.  将菜单项拖动到新位置并释放鼠标按钮。  
  
### <a name="to-move-a-menu-item-to-another-menu"></a>若要移动到另一个菜单的菜单项  
  
1.  左键单击想要移动并按 CTRL + X，或右键单击菜单项和选择的菜单项**剪切**从快捷菜单。  
  
2.  左键单击将包含您剪切菜单项的菜单。  
  
3.  左键单击预期新位置之前的菜单项并按 CTRL + V，或右键单击预期新位置并选择之前的菜单项**粘贴**从快捷菜单。  
  
     您剪切菜单项将插入所选的菜单项之后。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip 控件概述](menustrip-control-overview-windows-forms.md)
