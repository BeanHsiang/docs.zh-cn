---
title: 如何：将 ListBox 绑定到数据
ms.date: 03/30/2017
helpviewer_keywords:
- ListBox controls [WPF], binding data to
- data binding [WPF], ListBox control
- binding data [WPF], to ListBox control
ms.assetid: de93a907-709a-44a7-84bf-578b846a3d8b
ms.openlocfilehash: 2cbcb0fb859605c33e2d92559b4a47aa1725472c
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372876"
---
# <a name="how-to-bind-a-listbox-to-data"></a>如何：将 ListBox 绑定到数据
应用程序开发人员可以创建<xref:System.Windows.Controls.ListBox>而无需指定的每个内容控件<xref:System.Windows.Controls.ListBoxItem>单独。 数据绑定可用于将数据绑定到的各个项。  
  
 下面的示例演示如何创建<xref:System.Windows.Controls.ListBox>填充<xref:System.Windows.Controls.ListBoxItem>通过数据绑定到的数据源的元素*颜色*。 在这种情况下不需要使用<xref:System.Windows.Controls.ListBoxItem>标记，以指定每个项的内容。  
  
## <a name="example"></a>示例  
 [!code-xaml[ListBoxEvent#7](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#7)]  
[!code-xaml[ListBoxEvent#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#3)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.ListBox>
- <xref:System.Windows.Controls.ListBoxItem>
- [控件](../advanced/optimizing-performance-controls.md)
