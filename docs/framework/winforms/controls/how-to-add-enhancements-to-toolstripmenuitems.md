---
title: 如何：向 Toolstripmenuitem 添加增强功能
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- commands [Windows Forms], grouping on menus
- check marks [Windows Forms], adding to menus
- ToolStripMenuItems [Windows Forms], displaying access keys
- menus [Windows Forms], grouping commands
- menu items [Windows Forms], displaying shortcut keys
- ToolStripMenuItems
- separators [Windows Forms], displaying on menus
- menu items [Windows Forms], showing separators
- menu items [Windows Forms], adding check marks
- ToolStripMenuItems [Windows Forms], adding check marks
- menu items [Windows Forms], adding images
- ToolStripSeparators [Windows Forms], displaying on MenuStrips
- menu items [Windows Forms], displaying access keys
- ToolStripMenuItems [Windows Forms], displaying shortcut keys
- ToolStripMenuItems [Windows Forms], adding images
- keyboard shortcuts [Windows Forms], displaying on menus
- images [Windows Forms], adding to menus
- ToolStripMenuItems [Windows Forms], showing separator bars
ms.assetid: aa5f19bb-b545-4378-bfa6-36ba592f0d7c
ms.openlocfilehash: 68a926eba184d12d58e537d8db0a5baefb0fbe95
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57719320"
---
# <a name="how-to-add-enhancements-to-toolstripmenuitems"></a>如何：向 Toolstripmenuitem 添加增强功能
你可以增强的可用性<xref:System.Windows.Forms.MenuStrip>和<xref:System.Windows.Forms.ContextMenuStrip>中通过以下方式控件：  
  
-   添加复选标记来指定是否打开或关闭，打开某项功能，如是否沿字处理应用程序的边距显示标尺，或以指示列表中的文件的文件上未显示，例如**窗口**菜单。  
  
-   添加直观地表示菜单命令的图像。  
  
-   显示键盘快捷方式，以提供用于执行命令的键盘代替鼠标。 例如，按 CTRL + C 执行**复制**命令。  
  
-   显示访问密钥的菜单导航提供鼠标键盘替代方法。 例如，按 ALT + F 将选择**文件**菜单。  
  
-   显示分隔条以组相关的命令，并使菜单更具可读性。  
  
### <a name="to-display-a-check-mark-on-a-menu-command"></a>若要显示一个复选标记上的菜单命令  
  
-   设置其<xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A>属性设置为`true`。  
  
     它还会设置<xref:System.Windows.Forms.ToolStripMenuItem.CheckState%2A>属性设置为`true`。 仅当你想要显示为默认情况下，无论是否选中为选中的菜单命令，请使用此过程。  
  
### <a name="to-display-a-check-mark-that-changes-state-with-each-click"></a>若要显示与每次单击状态更改的选中标记  
  
-   设置菜单命令<xref:System.Windows.Forms.ToolStripMenuItem.CheckOnClick%2A>属性设置为`true`。  
  
### <a name="to-add-an-image-to-a-menu-command"></a>若要将图像添加到菜单命令  
  
-   设置菜单命令的<xref:System.Windows.Forms.ToolStripItem.Image%2A>属性设置为映像的名称。 如果<xref:System.Windows.Forms.ToolStripItemDisplayStyle>此菜单命令属性设置为<xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text>或<xref:System.Windows.Forms.ToolStripItemDisplayStyle.None>，不能显示该图像。  
  
> [!NOTE]
>  图像边距还可以显示一个复选标记是否您选择。 此外，可以设置<xref:System.Windows.Forms.ToolStripMenuItem.Checked%2A>属性的映像`true`，和与阴影边框，该图像将显示在运行时。  
  
### <a name="to-display-a-shortcut-key-for-a-menu-command"></a>若要显示的菜单命令快捷键  
  
-   设置菜单命令<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A>属性设置为所需的键盘组合，例如 CTRL + O 则表示**开放**菜单命令，并设置<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>属性设置为`true`。  
  
### <a name="to-display-custom-shortcut-keys-for-a-menu-command"></a>若要显示的菜单命令的自定义快捷键  
  
-   设置菜单命令<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeyDisplayString%2A>属性设置为所需的键盘组合，例如 CTRL + SHIFT + O 而不是 SHIFT + CTRL + O 和集<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>属性设置为`true`。  
  
### <a name="to-display-an-access-key-for-a-menu-command"></a>若要显示的菜单命令的访问密钥  
  
-   当您将设置<xref:System.Windows.Forms.ToolStripItem.Text%2A>菜单命令属性中输入与号 (&) 想要访问密钥作为带有下划线的字母前。 例如，如果键入`&Open`作为<xref:System.Windows.Forms.ToolStripItem.Text%2A>菜单项的属性将导致显示为菜单命令<u>O</u>笔。
  
     若要导航到此菜单命令，请按 alt 键，将焦点设置到<xref:System.Windows.Forms.MenuStrip>，按菜单名称的访问密钥。 当菜单打开并显示带访问键的项时，只需按下访问键来选择菜单命令。  
  
> [!NOTE]
>  避免定义重复的访问密钥，如两次在同一个菜单系统中定义 ALT + F。 不能保证重复的访问键的选择顺序。  
  
### <a name="to-display-a-separator-bar-between-menu-commands"></a>若要显示的菜单命令之间的分隔条  
  
-   定义后你<xref:System.Windows.Forms.MenuStrip>和它将包含的项使用<xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A>或<xref:System.Windows.Forms.ToolStripItemCollection.Add%2A>方法添加的菜单命令和<xref:System.Windows.Forms.ToolStripSeparator>控件添加到<xref:System.Windows.Forms.MenuStrip>中所需的顺序。  
  
    ```vb  
    ' This code adds a top-level File menu to the MenuStrip.  
    Me.menuStrip1.Items.Add(New ToolStripMenuItem() _  
    {Me.fileToolStripMenuItem})  
  
    ' This code adds the New and Open menu commands, a separator bar,   
    ' and the Save and Exit menu commands to the top-level File menu,   
    ' in that order.  
    Me.fileToolStripMenuItem.DropDownItems.AddRange(New _  
    ToolStripMenuItem() {Me.newToolStripMenuItem, _  
    Me.openToolStripMenuItem, Me.toolStripSeparator1, _  
    Me.saveToolStripMenuItem, Me.exitToolStripMenuItem})  
    ```  
  
    ```csharp  
    // This code adds a top-level File menu to the MenuStrip.  
    this.menuStrip1.Items.Add(new ToolStripItem[]_  
    {this.fileToolStripMenuItem});  
  
    // This code adds the New and Open menu commands, a separator bar,   
    // and the Save and Exit menu commands to the top-level File menu,   
    // in that order.  
    this.fileToolStripMenuItem.DropDownItems.AddRange(new _  
    ToolStripItem[] {  
    this.newToolStripMenuItem,  
    this.openToolStripMenuItem,  
    this.toolStripSeparator1,  
    this.saveToolStripMenuItem,  
    this.exitToolStripMenuItem});  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [MenuStrip 控件概述](menustrip-control-overview-windows-forms.md)
