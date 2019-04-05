---
title: 如何：将命令挂钩到支持命令的控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Control class [WPF], attaching a RoutedCommand
- classes [WPF], Control [WPF], attaching a RoutedCommand
- RoutedCommand class [WPF], attaching to a Control
- classes [WPF], RoutedCommand [WPF], attaching to a Control
ms.assetid: 8d8592ae-0c91-469e-a1cd-d179c4544548
ms.openlocfilehash: 2bb3e00cad1a629a405fa75ef32a289c4006f324
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364432"
---
# <a name="how-to-hook-up-a-command-to-a-control-with-command-support"></a>如何：将命令挂钩到支持命令的控件
以下示例显示如何将 <xref:System.Windows.Input.RoutedCommand> 挂钩到含对该命令的内置支持的 <xref:System.Windows.Controls.Control>。  有关将命令挂钩到多个源的完整示例，请参阅[创建自定义 RoutedCommand 示例](https://github.com/Microsoft/WPF-Samples/tree/master/Input%20and%20Commands/CustomRoutedCommand)示例。  
  
## <a name="example"></a>示例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了应用程序程序员经常遇到的常见命令库。  构成命令库的类为：<xref:System.Windows.Input.ApplicationCommands>、<xref:System.Windows.Input.ComponentCommands>、<xref:System.Windows.Input.NavigationCommands>、<xref:System.Windows.Input.MediaCommands> 和 <xref:System.Windows.Documents.EditingCommands>。  
  
 构成这些类的静态 <xref:System.Windows.Input.RoutedCommand> 对象不提供命令逻辑。  命令的逻辑通过 <xref:System.Windows.Input.CommandBinding> 与命令相关联。  某些控件的部分命令具有内置的 CommandBindings。  这种机制可使命令的语义保持不变，而实际实现可以更改。  例如，<xref:System.Windows.Controls.TextBox> 对 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令的处理方式与专门支持图像的控件对其的处理方式不同，后者的基本思路是通过粘贴让内容保持不变。  命令无法提供命令逻辑，但是控件或应用程序必须提供命令逻辑。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的许多控件都为命令库中的某些命令提供内置支持。  例如，<xref:System.Windows.Controls.TextBox> 支持许多应用程序编辑命令，例如 <xref:System.Windows.Input.ApplicationCommands.Paste%2A>、<xref:System.Windows.Input.ApplicationCommands.Copy%2A>、<xref:System.Windows.Input.ApplicationCommands.Cut%2A>、<xref:System.Windows.Input.ApplicationCommands.Redo%2A> 和 <xref:System.Windows.Input.ApplicationCommands.Undo%2A>。  应用程序开发人员不必执行任何特殊操作即可使命令适用于这些控件。  如果命令执行时，<xref:System.Windows.Controls.TextBox> 是命令目标，它将使用内置于控件中的 <xref:System.Windows.Input.CommandBinding> 处理该命令。  
  
 以下说明如何将 <xref:System.Windows.Controls.MenuItem> 用作 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令的命令源，其中 <xref:System.Windows.Controls.TextBox> 是命令的目标。  定义 <xref:System.Windows.Controls.TextBox> 如何执行粘贴的所有逻辑都已内置到 <xref:System.Windows.Controls.TextBox> 控件中。  
  
 已创建 <xref:System.Windows.Controls.MenuItem>，并将其 <xref:System.Windows.Controls.MenuItem.Command%2A> 属性设置为 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令。  <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> 未显式设置为 <xref:System.Windows.Controls.TextBox> 对象。  未设置 <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> 时，该命令的目标是具有键盘焦点的元素。  如果具有键盘焦点的元素不支持 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令，或当前无法执行粘贴命令（例如，剪贴板为空），则 <xref:System.Windows.Controls.MenuItem> 为灰显。  
  
 [!code-xaml[MenuItemCommandTask_XAML#MenuItemCommanding](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask_XAML/CS/Window1.xaml#menuitemcommanding)]  
  
 [!code-csharp[MenuItemCommandTask#MenuItemCommandingCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask/CSharp/Window1.xaml.cs#menuitemcommandingcodebehind)]
 [!code-vb[MenuItemCommandTask#MenuItemCommandingCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandTask/VisualBasic/Window1.xaml.vb#menuitemcommandingcodebehind)]  
  
## <a name="see-also"></a>请参阅
- [命令概述](commanding-overview.md)
- [将命令挂钩到不支持命令的控件](how-to-hook-up-a-command-to-a-control-with-no-command-support.md)
