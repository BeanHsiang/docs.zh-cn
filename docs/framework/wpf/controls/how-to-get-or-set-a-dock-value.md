---
title: 如何：获取或设置 Dock 值
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dock values [WPF], setting
- Dock values [WPF], getting
ms.assetid: fcf4ab8a-c7cd-4835-8d04-de1c999ab4a8
ms.openlocfilehash: 7825377146532a6660e1838fa25631b788afe035
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374514"
---
# <a name="how-to-get-or-set-a-dock-value"></a>如何：获取或设置 Dock 值
下面的示例演示如何分配<xref:System.Windows.Controls.Dock>对象值。 该示例使用<xref:System.Windows.Controls.DockPanel.GetDock%2A>并<xref:System.Windows.Controls.DockPanel.SetDock%2A>方法的<xref:System.Windows.Controls.DockPanel>。  
  
## <a name="example"></a>示例  
 该示例创建的实例<xref:System.Windows.Controls.TextBlock>元素中， `txt1`，并将分配<xref:System.Windows.Controls.Dock>的值`Top`通过<xref:System.Windows.Controls.DockPanel.SetDock%2A>方法<xref:System.Windows.Controls.DockPanel>。 然后，将的值<xref:System.Windows.Controls.Dock>属性设置为<xref:System.Windows.Controls.TextBlock.Text%2A>的<xref:System.Windows.Controls.TextBlock>元素中的使用<xref:System.Windows.Controls.DockPanel.GetDock%2A>方法。 最后，该示例将添加<xref:System.Windows.Controls.TextBlock>父元素<xref:System.Windows.Controls.DockPanel>， `dp1`。  
  
 [!code-csharp[DockPanelSetDock#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DockPanelSetDock/CSharp/DockPanel_SetDock.cs#1)]
 [!code-vb[DockPanelSetDock#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelSetDock/VisualBasic/DockPanel_SetDock.vb#1)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.DockPanel>
- <xref:System.Windows.Controls.DockPanel.GetDock%2A>
- <xref:System.Windows.Controls.DockPanel.SetDock%2A>
- [面板概述](panels-overview.md)
