---
title: ToolBar 控件（Windows 窗体）
ms.date: 03/30/2017
helpviewer_keywords:
- toolbars [Windows Forms]
- ToolBar control [Windows Forms]
ms.assetid: 6b40e9ce-6a7a-4784-bfc9-7f1d36b7462e
ms.openlocfilehash: 3f0a1b6a7f83753ccae1a129528ed320a2613122
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723026"
---
# <a name="toolbar-control-windows-forms"></a>ToolBar 控件（Windows 窗体）
> [!NOTE]
>  
  <xref:System.Windows.Forms.ToolStrip> 控件取代了 `ToolBar` 控件并添加了功能；但是，可以选择保留 `ToolBar` 控件以实现向后兼容并供将来使用。  
  
 Windows 窗体 `ToolBar` 控件在窗体上用作可显示下拉菜单的行的控件条以及可激活命令的位图按钮。 因此，单击工具栏按钮相当于选择菜单命令。 按钮可配置为显示为并用作下压按钮、下拉菜单或分隔符。 通常，工具栏包含对应于应用程序菜单结构中的项的按钮和菜单，提供对应用程序最常用的函数和命令的快速访问。  
  
> [!NOTE]
>  `ToolBar` 控件的 <xref:System.Windows.Forms.ToolBarButton.DropDownMenu%2A> 属性将 <xref:System.Windows.Forms.ContextMenu> 类的实例作为引用。 在应用程序的工具栏上实现此类按钮时，请仔细考虑所传递的引用，因为此属性将接受从 <xref:System.Windows.Forms.Menu> 类继承的所有对象。  
  
## <a name="in-this-section"></a>本节内容  
 [ToolBar 控件概述](toolbar-control-overview-windows-forms.md)  
 介绍 `ToolBar` 控件的一般概念，此控件可用于设计用户可使用的自定义工具栏。  
  
 [如何：向 ToolBar 控件添加按钮](how-to-add-buttons-to-a-toolbar-control.md)  
 介绍如何向 `ToolBar` 控件添加按钮。  
  
 [如何：定义的工具栏按钮的图标](how-to-define-an-icon-for-a-toolbar-button.md)  
 介绍如何显示 `ToolBar` 控件按钮中的图标。  
  
 [如何：触发工具栏按钮的菜单事件](how-to-trigger-menu-events-for-toolbar-buttons.md)  
 指示如何编写代码以解释用户在 `ToolBar` 控件中单击的按钮。  
  
 另请参阅[如何：定义使用设计器的工具栏按钮的图标](how-to-define-an-icon-for-a-toolbar-button-using-the-designer.md)，[如何：将按钮添加到使用设计器的工具栏控件](how-to-add-buttons-to-a-toolbar-control-using-the-designer.md)。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.ToolBar> 类  
 提供类及其成员的相关引用信息。  
  
## <a name="related-sections"></a>相关章节  
 [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)  
 提供 Windows 窗体控件的完整列表，附带其使用情况相关信息的链接。  
  
 [ToolStrip 控件](toolstrip-control-windows-forms.md)  
 介绍可以承载 Windows 窗体应用程序中的菜单、控件和用户控件的工具栏。
