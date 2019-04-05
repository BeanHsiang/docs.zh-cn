---
title: MenuStrip 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- MenuStrip
helpviewer_keywords:
- MenuStrip control [Windows Forms], about MenuStrip control
- menus [Windows Forms], creating
ms.assetid: f45516e5-bf01-4468-b851-d45f4c33c055
ms.openlocfilehash: 41688dce0e645b643d7a10a5cf330f1f3a5f9cc8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54653705"
---
# <a name="menustrip-control-overview-windows-forms"></a>MenuStrip 控件概述（Windows 窗体）
菜单通过持有一个共同的主题进行分组的命令公开给用户的功能。  
  
 <xref:System.Windows.Forms.MenuStrip>控制是此版本的 Visual Studio 和.NET Framework 中新增。 与该控件可以轻松创建诸如 Microsoft Office 中的菜单。  
  
 <xref:System.Windows.Forms.MenuStrip>控件支持多文档界面 (MDI) 和菜单合并功能、 工具提示和溢出。 可以通过添加访问密钥、 键盘快捷方式，复选标记、 图像和分隔条增强的可用性和菜单的可读性。  
  
 <xref:System.Windows.Forms.MenuStrip>控制取代并添加了功能<xref:System.Windows.Forms.MainMenu>控制; 但是，<xref:System.Windows.Forms.MainMenu>以备向后兼容性和将来使用保留控件，如果您选择。  
  
## <a name="ways-to-use-the-menustrip-control"></a>如何使用 MenuStrip 控件  
 使用<xref:System.Windows.Forms.MenuStrip>控制转移到：  
  
-   创建轻松地自定义，支持的常用的菜单高级用户界面和布局功能，例如文本和图像排序和对齐方式、 拖放操作、 MDI、 溢出和访问菜单命令的其他模式。  
  
-   支持的典型的外观和行为的操作系统。  
  
-   与处理事件的其他控件相同的方式处理始终对所有容器和包含的项的事件。  
  
 下表显示了一些特别重要的属性的<xref:System.Windows.Forms.MenuStrip>和关联的类。  
  
|属性|描述|  
|--------------|-----------------|  
|<xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A>|获取或设置<xref:System.Windows.Forms.ToolStripMenuItem>，用来显示 MDI 子窗体的列表。|  
|<xref:System.Windows.Forms.ToolStripItem.MergeAction%2A?displayProperty=nameWithType>|获取或设置如何与 MDI 应用程序中的父菜单合并子菜单。|  
|<xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A?displayProperty=nameWithType>|获取或设置在 MDI 应用程序中合并菜单中项的位置。|  
|<xref:System.Windows.Forms.Form.IsMdiContainer%2A?displayProperty=nameWithType>|获取或设置一个值，该值指示是否在窗体 MDI 子窗体的容器。|  
|<xref:System.Windows.Forms.MenuStrip.ShowItemToolTips%2A>|获取或设置一个值，该值指示是否显示工具提示<xref:System.Windows.Forms.MenuStrip>。|  
|<xref:System.Windows.Forms.MenuStrip.CanOverflow%2A>|获取或设置一个值，该值指示 <xref:System.Windows.Forms.MenuStrip> 是否支持溢出功能。|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShortcutKeys%2A>|获取或设置与关联的键盘快捷方式<xref:System.Windows.Forms.ToolStripMenuItem>。|  
|<xref:System.Windows.Forms.ToolStripMenuItem.ShowShortcutKeys%2A>|获取或设置与之关联的值，该值指示是否的快捷键<xref:System.Windows.Forms.ToolStripMenuItem>旁边显示<xref:System.Windows.Forms.ToolStripMenuItem>。|  
  
 下表显示了重要<xref:System.Windows.Forms.MenuStrip>伴生类。  
  
|类|描述|  
|-----------|-----------------|  
|<xref:System.Windows.Forms.ToolStripMenuItem>|表示在显示的可选选项<xref:System.Windows.Forms.MenuStrip>或<xref:System.Windows.Forms.ContextMenuStrip>。|  
|<xref:System.Windows.Forms.ContextMenuStrip>|表示快捷菜单。|  
|<xref:System.Windows.Forms.ToolStripDropDown>|表示允许用户从用户单击时显示的列表中选择单个项的控件<xref:System.Windows.Forms.ToolStripDropDownButton>或更高级别的菜单项。|  
|<xref:System.Windows.Forms.ToolStripDropDownItem>|提供基本功能，用于控件派生自<xref:System.Windows.Forms.ToolStripItem>显示下拉项在单击时。|  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ContextMenuStrip>
- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripDropDown>
