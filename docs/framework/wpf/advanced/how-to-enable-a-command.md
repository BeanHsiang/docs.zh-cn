---
title: 如何：启用命令
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CommandBindings [WPF]
- commanding [WPF]
ms.assetid: d8016266-58d9-48f7-8298-a86b7ed49fbd
ms.openlocfilehash: a24a7a31154de58051677ba41496fcf4da3f2568
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57355059"
---
# <a name="how-to-enable-a-command"></a>如何：启用命令
下面的示例演示如何使用命令在[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]。  该示例演示如何将相关联<xref:System.Windows.Input.RoutedCommand>到<xref:System.Windows.Controls.Button>，创建<xref:System.Windows.Input.CommandBinding>，并创建事件处理程序实现<xref:System.Windows.Input.RoutedCommand>。  有关命令的详细信息，请参阅[命令概述](commanding-overview.md)。  
  
## <a name="example"></a>示例  
 代码的第一个部分创建[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]，其中包括<xref:System.Windows.Controls.Button>和一个<xref:System.Windows.Controls.StackPanel>，并创建<xref:System.Windows.Input.CommandBinding>，将使用的命令处理程序相关联<xref:System.Windows.Input.RoutedCommand>。  
  
 <xref:System.Windows.Input.ICommandSource.Command%2A>的属性<xref:System.Windows.Controls.Button>与关联<xref:System.Windows.Input.ApplicationCommands.Close%2A>命令。  
  
 <xref:System.Windows.Input.CommandBinding>添加到<xref:System.Windows.Input.CommandBindingCollection>根的<xref:System.Windows.Window>。 <xref:System.Windows.Input.CommandBinding.Executed>并<xref:System.Windows.Input.CommandBinding.CanExecute>事件处理程序将附加到此绑定并使用相关联<xref:System.Windows.Input.ApplicationCommands.Close%2A>命令。  
  
 无需<xref:System.Windows.Input.CommandBinding>没有命令逻辑，只有一种机制来调用命令。  当<xref:System.Windows.Controls.Button>单击时， <xref:System.Windows.Input.CommandManager.PreviewExecuted> <xref:System.Windows.RoutedEvent>跟在命令目标上引发<xref:System.Windows.Input.CommandManager.Executed> <xref:System.Windows.RoutedEvent>。  这些事件会遍历元素树，以查找<xref:System.Windows.Input.CommandBinding>针对该特定命令。  值得注意的是，因为<xref:System.Windows.RoutedEvent>隧道和冒泡元素树，必须格外小心 where<xref:System.Windows.Input.CommandBinding>放。   如果<xref:System.Windows.Input.CommandBinding>上的命令目标或不在的路由的另一个节点同级<xref:System.Windows.RoutedEvent>，则<xref:System.Windows.Input.CommandBinding>也不能访问。  
  
 [!code-xaml[EnableCloseCommand#CloseCommandBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml#closecommandbinding)]  
  
 [!code-csharp[EnableCloseCommand#CloseCommandBindingCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandbindingcodebehind)]
 [!code-vb[EnableCloseCommand#CloseCommandBindingCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandbindingcodebehind)]  
  
 代码实现的下一节<xref:System.Windows.Input.CommandManager.Executed>和<xref:System.Windows.Input.CommandBinding.CanExecute>事件处理程序。  
  
 <xref:System.Windows.Input.CommandManager.Executed>处理程序调用一个方法以关闭打开的文件。  <xref:System.Windows.Input.CommandBinding.CanExecute>处理程序调用的方法来确定文件是否处于打开状态。  如果文件处于打开状态，<xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A>设置为`true`; 否则为设置为`false`。  
  
 [!code-csharp[EnableCloseCommand#CloseCommandHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandhandler)]
 [!code-vb[EnableCloseCommand#CloseCommandHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandhandler)]  
  
## <a name="see-also"></a>请参阅
- [命令概述](commanding-overview.md)
