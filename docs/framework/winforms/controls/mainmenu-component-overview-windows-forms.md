---
title: MainMenu 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- MenuItem
- MainMenu
helpviewer_keywords:
- MainMenu control [Windows Forms], about MainMenu control
- menus
ms.assetid: b41cc5a3-cc59-4996-aa3c-8dd9c17d3c90
ms.openlocfilehash: 6c2c33c8c03751e87d71e65523b82d92b18f31c4
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709861"
---
# <a name="mainmenu-component-overview-windows-forms"></a>MainMenu 组件概述（Windows 窗体）
> [!IMPORTANT]
>  尽管<xref:System.Windows.Forms.MenuStrip>和<xref:System.Windows.Forms.ContextMenuStrip>替换并将功能添加到<xref:System.Windows.Forms.MainMenu>并<xref:System.Windows.Forms.ContextMenu>的早期版本中，控件<xref:System.Windows.Forms.MainMenu>和<xref:System.Windows.Forms.ContextMenu>也可选择将保留向后兼容性和将来使用。  
  
 Windows 窗体<xref:System.Windows.Forms.MainMenu>组件在运行时显示一个菜单。 主菜单和各个项的所有子菜单是<xref:System.Windows.Forms.MenuItem>对象。  
  
## <a name="key-properties"></a>键属性  
 菜单项可以指定为默认项的设置<xref:System.Windows.Forms.MenuItem.DefaultItem%2A>属性设置为`true`。 单击菜单时，默认项以粗体文本显示。 菜单项<xref:System.Windows.Forms.MenuItem.Checked%2A>属性是`true`或`false`，并指示是否选定菜单项。 菜单项<xref:System.Windows.Forms.MenuItem.RadioCheck%2A>属性自定义的选定项的外观： 如果<xref:System.Windows.Forms.MenuItem.RadioCheck%2A>设置为`true`，单选按钮旁边的项; 如果<xref:System.Windows.Forms.MenuItem.RadioCheck%2A>设置为`false`，项的旁边显示复选标记。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.MainMenu>
- <xref:System.Windows.Forms.Menu>
- <xref:System.Windows.Forms.MenuItem>
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ContextMenuStrip>
- [MenuStrip 控件概述](menustrip-control-overview-windows-forms.md)
