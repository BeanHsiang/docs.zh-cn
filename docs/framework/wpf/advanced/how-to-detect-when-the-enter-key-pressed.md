---
title: 如何：检测何时按下 Enter 键
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Enter key [WPF], detecting
- keys [WPF], Enter
ms.assetid: a66f39d2-ef4a-43a5-b454-a4ea0fe88655
ms.openlocfilehash: 1796127d33087a3fd4504d03f175f8afe5323630
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57351855"
---
# <a name="how-to-detect-when-the-enter-key-pressed"></a>如何：检测何时按下 Enter 键
此示例演示如何检测何时<xref:System.Windows.Input.Key.Enter>键盘上按下键。  
  
 此示例中包含的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]文件和代码隐藏文件。  
  
## <a name="example"></a>示例  
 当用户按<xref:System.Windows.Input.Key.Enter>中的键<xref:System.Windows.Controls.TextBox>，在文本框中输入将出现在另一个区域的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]。  
  
 以下[!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)]创建用户界面，其中包括<xref:System.Windows.Controls.StackPanel>即<xref:System.Windows.Controls.TextBlock>，和一个<xref:System.Windows.Controls.TextBox>。  
  
 [!code-xaml[keydown#KeyDownUI](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml#keydownui)]  
  
 下面的代码隐藏创建<xref:System.Windows.UIElement.KeyDown>事件处理程序。  如果按下的键是<xref:System.Windows.Input.Key.Enter>键，显示一条消息是在<xref:System.Windows.Controls.TextBlock>。  
  
 [!code-csharp[keydown#KeyDownSample](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml.cs#keydownsample)]
 [!code-vb[keydown#KeyDownSample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/KeyDown/VisualBasic/Window1.xaml.vb#keydownsample)]  
  
## <a name="see-also"></a>请参阅
- [输入概述](input-overview.md)
- [路由事件概述](routed-events-overview.md)
