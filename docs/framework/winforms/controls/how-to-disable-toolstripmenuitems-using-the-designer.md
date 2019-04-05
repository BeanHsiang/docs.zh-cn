---
title: 如何：使用设计器禁用 Toolstripmenuitem
ms.date: 03/30/2017
helpviewer_keywords:
- ToolStripMenuItems [Windows Forms], disabling in designer
- MenuStrip control [Windows Forms], disabling menu items in designer
- menu items [Windows Forms], disabling
- menus [Windows Forms], disabling items
ms.assetid: 985e311e-7d67-4205-b5a3-d045b68a4a03
ms.openlocfilehash: a185fe4421b5b5d7846c7d8cacbfc1cae5f805eb
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704423"
---
# <a name="how-to-disable-toolstripmenuitems-using-the-designer"></a>如何：使用设计器禁用 Toolstripmenuitem
您可以限制或扩大用户可通过启用和禁用对用户活动的响应中的菜单项的命令。 菜单项时创建，但这可以通过调整默认情况下启用<xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A>属性。 在设计时使用此属性可**属性**窗口或以编程方式在代码中设置。 有关详细信息，请参阅[如何：禁用 ToolStripMenuItems](how-to-disable-toolstripmenuitems.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-disable-a-menu-item-at-design-time"></a>若要在设计时禁用菜单项  
  
1.  使用窗体上选择的菜单项，设置<xref:System.Windows.Forms.ToolStripMenuItem.Enabled%2A>属性设置为`false`。  
  
    > [!TIP]
    >  禁用菜单中的第一个或顶级菜单项将禁用菜单内包含的所有菜单项。 同样，禁用具有子菜单项的菜单项将禁用的子菜单项。 如果给定的菜单上的所有命令都都对用户不可用，它视为良好编程习惯，同时隐藏和禁用整个菜单中，这提供了一个清晰的用户界面。 应同时隐藏和禁用菜单上，因为仅隐藏不会阻止到通过快捷键菜单命令的访问权限。 设置<xref:System.Windows.Forms.ToolStripItem.Visible%2A>属性的顶级菜单项`false`若要隐藏整个菜单。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [如何：隐藏 Toolstripmenuitem](how-to-hide-toolstripmenuitems.md)
- [MenuStrip 控件概述](menustrip-control-overview-windows-forms.md)
