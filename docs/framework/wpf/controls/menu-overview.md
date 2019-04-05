---
title: 菜单概述
ms.date: 03/30/2017
helpviewer_keywords:
- Menu control [WPF]
- controls [WPF], Menu
ms.assetid: 67df6de5-db96-4c71-b752-af90729a6537
ms.openlocfilehash: d5f53603ea22b2ae12a9846ba6bdce525790ce15
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360936"
---
# <a name="menu-overview"></a>菜单概述
<xref:System.Windows.Controls.Menu>类可用于组织与命令和事件处理程序的层次结构顺序关联的元素。 每个<xref:System.Windows.Controls.Menu>元素包含一系列<xref:System.Windows.Controls.MenuItem>元素。  
  
  
<a name="menu_control"></a>   
## <a name="menu-control"></a>Menu 控件  
 <xref:System.Windows.Controls.Menu>控件显示的项的指定命令或应用程序的选项列表。 通常情况下，单击<xref:System.Windows.Controls.MenuItem>打开子菜单或导致应用程序执行某个命令。  
  
<a name="creating_menus"></a>   
## <a name="creating-menus"></a>创建菜单  
 下面的示例创建<xref:System.Windows.Controls.Menu>操作中的文本<xref:System.Windows.Controls.TextBox>。 <xref:System.Windows.Controls.Menu>包含<xref:System.Windows.Controls.MenuItem>对象使用<xref:System.Windows.Controls.MenuItem.Command%2A>， <xref:System.Windows.Controls.MenuItem.IsCheckable%2A>，并<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A>属性和<xref:System.Windows.Controls.MenuItem.Checked>， <xref:System.Windows.Controls.MenuItem.Unchecked>，和<xref:System.Windows.Controls.MenuItem.Click>事件。  
  
 [!code-xaml[MenuItemCommandsAndEvents#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandsAndEvents/CSharp/Window1.xaml#1)]  
  
 [!code-csharp[MenuItemCommandsAndEvents#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandsAndEvents/CSharp/Window1.xaml.cs#2)]
 [!code-vb[MenuItemCommandsAndEvents#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandsAndEvents/VisualBasic/Window1.xaml.vb#2)]  
  
<a name="menus_with_shortcutkeys"></a>   
## <a name="menuitems-with-keyboard-shortcuts"></a>使用键盘快捷方式的菜单项  
 键盘快捷方式可通过键盘来调用输入的字符组合<xref:System.Windows.Controls.Menu>命令。 例如，“复制”的快捷方式是 CTRL+C。 有两个属性将与键盘快捷方式和菜单项 —<xref:System.Windows.Controls.MenuItem.InputGestureText%2A>或<xref:System.Windows.Controls.MenuItem.Command%2A>。  
  
<a name="menus_inputgesturetext"></a>   
### <a name="inputgesturetext"></a>InputGestureText  
 下面的示例演示如何使用<xref:System.Windows.Controls.MenuItem.InputGestureText%2A>要分配到的键盘快捷方式文本属性<xref:System.Windows.Controls.MenuItem>控件。 这仅将键盘快捷方式放置在菜单项中。  它不会将与命令关联<xref:System.Windows.Controls.MenuItem>。 应用程序必须处理用户的输入才能执行操作。  
  
 [!code-xaml[MenuEvent#6](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuEvent/CSharp/Pane1.xaml#6)]  
  
<a name="menus_commands"></a>   
### <a name="command"></a>命令  
 下面的示例演示如何使用<xref:System.Windows.Controls.MenuItem.Command%2A>要关联属性**开放**并**保存**命令<xref:System.Windows.Controls.MenuItem>控件。 命令属性不仅将命令与<xref:System.Windows.Controls.MenuItem>，但它还会提供输入的手势文本以用作快捷方式。  
  
 [!code-xaml[MenuEvent#8](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuEvent/CSharp/Pane1.xaml#8)]  
  
 <xref:System.Windows.Controls.MenuItem>类还具有<xref:System.Windows.Controls.MenuItem.CommandTarget%2A>属性，用于指定发生命令的元素。 如果<xref:System.Windows.Controls.MenuItem.CommandTarget%2A>未设置，具有键盘焦点的元素接收命令。 有关命令的详细信息，请参阅[命令概述](../advanced/commanding-overview.md)。  
  
<a name="menu_styling"></a>   
## <a name="menu-styling"></a>菜单样式设置  
 使用控件样式设置，你可以显著改变外观和行为<xref:System.Windows.Controls.Menu>而无需编写自定义控件的控件。 除了设置视觉属性，还可以应用<xref:System.Windows.Style>到控件的各个部分，更改通过属性，控件的部件的行为或添加其他部分，或更改控件的布局。 下面的示例演示几种方法添加<xref:System.Windows.Style>到<xref:System.Windows.Controls.Menu>控件。  
  
 第一个代码示例定义了<xref:System.Windows.Style>调用`Simple`，演示如何在样式中使用当前系统设置。 代码将 `MenuHighlightBrush` 的颜色分配为菜单的背景色，将 `MenuTextBrush` 分配为菜单的前景色。 请注意，使用资源键分配画笔。  
  
 [!code-xaml[MenuStylesSnippet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuStylesSnippet/CS/app.xaml#1)]  
  
 下面的示例使用<xref:System.Windows.Trigger>元素，您可以更改的外观<xref:System.Windows.Controls.MenuItem>发生的事件响应<xref:System.Windows.Controls.Menu>。 当将鼠标移到<xref:System.Windows.Controls.Menu>的前景色和字体特征的菜单项的更改。  
  
 [!code-xaml[MenuStylesSnippet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuStylesSnippet/CS/app.xaml#2)]  
  
## <a name="see-also"></a>请参阅
- [WPF 控件库示例](https://go.microsoft.com/fwlink/?LinkID=160053)
