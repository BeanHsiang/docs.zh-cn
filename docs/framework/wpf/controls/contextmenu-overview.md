---
title: ContextMenu 概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], ContextMenu
- ContextMenu controls [WPF], about ContextMenu controls
ms.assetid: 16909c42-799a-4561-91e0-7d69dcfeea91
ms.openlocfilehash: 4d3677021e38c10d38c0e5ed5e5de1824397db50
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57357360"
---
# <a name="contextmenu-overview"></a>ContextMenu 概述
<xref:System.Windows.Controls.ContextMenu>类表示使用特定于上下文的公开功能的元素<xref:System.Windows.Controls.Menu>。 通常情况下，用户公开<xref:System.Windows.Controls.ContextMenu>在[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]通过右键单击鼠标按钮。 本主题介绍<xref:System.Windows.Controls.ContextMenu>元素，并提供有关如何使用中的示例[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]和代码。  
  
  
  
<a name="contextmenu_control"></a>   
## <a name="contextmenu-control"></a>ContextMenu 控件  
 一个<xref:System.Windows.Controls.ContextMenu>附加到特定控件。 <xref:System.Windows.Controls.ContextMenu>元素使您能够为用户提供的项的指定命令或关联的选项与特定控件，例如，列表<xref:System.Windows.Controls.Button>。 用户通过右键单击控件来显示菜单。 通常情况下，单击<xref:System.Windows.Controls.MenuItem>打开子菜单或导致应用程序执行某个命令。  
  
<a name="creating_contextmenus"></a>   
## <a name="creating-contextmenus"></a>创建 ContextMenus  
 以下示例演示如何创建<xref:System.Windows.Controls.ContextMenu>具有子菜单。 <xref:System.Windows.Controls.ContextMenu>控件附加到按钮控件。  
  
 [!code-xaml[ContextMenu#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml#1)]  
  
 [!code-csharp[ContextMenu#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ContextMenu#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ContextMenu/VisualBasic/Pane1.xaml.vb#2)]  
  
<a name="applying_styles_to_contextmenu"></a>   
## <a name="applying-styles-to-a-contextmenu"></a>将样式应用于 ContextMenu  
 通过使用控件<xref:System.Windows.Style>，可以显著改变外观和行为<xref:System.Windows.Controls.ContextMenu>而无需编写自定义控件。 除了设置可视化属性以外，还可以将样式应用于控件的各个部分。 例如，可以使用属性，来更改控件的部件的行为或可添加其他部分，或更改其布局<xref:System.Windows.Controls.ContextMenu>。 下面的示例演示几种方法添加到样式<xref:System.Windows.Controls.ContextMenu>控件。  
  
 第一个示例定义一个名为 `SimpleSysResources` 的样式，它演示如何在样式中使用当前的系统设置。 该示例将分配<xref:System.Windows.SystemColors.MenuHighlightBrushKey%2A>作为<xref:System.Windows.Controls.Control.Background%2A>颜色和<xref:System.Windows.SystemColors.MenuTextBrushKey%2A>作为<xref:System.Windows.Controls.Control.Foreground%2A>的颜色<xref:System.Windows.Controls.ContextMenu>。  
  
```xaml  
<Style x:Key="SimpleSysResources" TargetType="{x:Type MenuItem}">  
  <Setter Property = "Background" Value=   
    "{DynamicResource {x:Static SystemColors.MenuHighlightBrushKey}}"/>  
  <Setter Property = "Foreground" Value=   
    "{DynamicResource {x:Static SystemColors.MenuTextBrushKey}}"/>  
</Style>  
```  
  
 下面的示例使用<xref:System.Windows.Trigger>要更改的外观元素<xref:System.Windows.Controls.Menu>响应，则将引发的事件<xref:System.Windows.Controls.ContextMenu>。 当用户将鼠标移到菜单的外观<xref:System.Windows.Controls.ContextMenu>项更改。  
  
```xaml  
<Style x:Key="Triggers" TargetType="{x:Type MenuItem}">  
  <Style.Triggers>  
    <Trigger Property="MenuItem.IsMouseOver" Value="true">  
      <Setter Property = "FontSize" Value="16"/>  
      <Setter Property = "FontStyle" Value="Italic"/>  
      <Setter Property = "Foreground" Value="Red"/>  
    </Trigger>  
  </Style.Triggers>  
</Style>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.ContextMenu>
- <xref:System.Windows.Style>
- <xref:System.Windows.Controls.Menu>
- <xref:System.Windows.Controls.MenuItem>
- [ContextMenu](contextmenu.md)
- [ContextMenu 样式和模板](contextmenu-styles-and-templates.md)
- [WPF 控件库示例](https://go.microsoft.com/fwlink/?LinkID=160053)
