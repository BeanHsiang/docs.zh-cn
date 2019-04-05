---
title: 如何：使用触发器为 ListView 中的选定项设置样式
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], styling
ms.assetid: 1e2bdce0-afe8-4507-9b18-f33de43de25a
ms.openlocfilehash: 8c2d4adb2471c0f1891288573ce6b6460b20151d
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367916"
---
# <a name="how-to-use-triggers-to-style-selected-items-in-a-listview"></a>如何：使用触发器为 ListView 中的选定项设置样式
此示例演示如何定义<xref:System.Windows.Style.Triggers%2A>有关<xref:System.Windows.Controls.ListViewItem>控件，以便时的属性值<xref:System.Windows.Controls.ListViewItem>更改，<xref:System.Windows.Style>的<xref:System.Windows.Controls.ListViewItem>响应中的更改。  
  
## <a name="example"></a>示例  
 如果你想<xref:System.Windows.Style>的<xref:System.Windows.Controls.ListViewItem>若要更改以响应属性更改，请定义<xref:System.Windows.Style.Triggers%2A>为<xref:System.Windows.Style>更改。  
  
 下面的示例定义<xref:System.Windows.Trigger>，用于设置<xref:System.Windows.Controls.Control.Foreground%2A>属性设置为<xref:System.Windows.Media.Brushes.Blue%2A>，并更改<xref:System.Windows.FrameworkElement.Cursor%2A>以显示<xref:System.Windows.Input.CursorType.Hand>时<xref:System.Windows.UIElement.IsMouseOver%2A>属性更改为`true`。  
  
 [!code-xaml[ListViewChkBox#ListViewItemTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersstart)]  
[!code-xaml[ListViewChkBox#Trigger](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#trigger)]  
[!code-xaml[ListViewChkBox#ListViewItemTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersend)]  
  
 下面的示例定义<xref:System.Windows.MultiTrigger>，用于设置<xref:System.Windows.Controls.Control.Foreground%2A>的属性<xref:System.Windows.Controls.ListViewItem>到<xref:System.Windows.Media.Brushes.Yellow%2A>时<xref:System.Windows.Controls.ListViewItem>是选定的项且具有键盘焦点。  
  
 [!code-xaml[ListViewChkBox#ListViewItemTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersstart)]  
[!code-xaml[ListViewChkBox#MultiTrigger](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#multitrigger)]  
[!code-xaml[ListViewChkBox#ListViewItemTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewChkBox/CS/window1.xaml#listviewitemtriggersend)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.Control>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [帮助主题](listview-how-to-topics.md)
- [ListView 概述](listview-overview.md)
- [GridView 概述](gridview-overview.md)
