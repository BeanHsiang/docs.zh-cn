---
title: 如何：使用 GridSplitter 调整列的大小
ms.date: 03/30/2017
helpviewer_keywords:
- grid columns [WPF], resizing
- GridSplitter control [WPF], resizing grid columns
- resizing grid columns [WPF]
ms.assetid: 47b20fe6-7adc-4aa6-9693-b4e184eef74b
ms.openlocfilehash: 93106ee25d98a056dfa5ba1a064c9803bebb072e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374123"
---
# <a name="how-to-resize-columns-with-a-gridsplitter"></a>如何：使用 GridSplitter 调整列的大小
此示例演示如何创建垂直<xref:System.Windows.Controls.GridSplitter>若要重新分发中的两个列之间的间距<xref:System.Windows.Controls.Grid>而无需更改的维度<xref:System.Windows.Controls.Grid>。  
  
## <a name="example"></a>示例  
 **如何创建覆盖列边缘的 GridSplitter**  
  
 若要指定<xref:System.Windows.Controls.GridSplitter>中的相邻列的大小进行调整<xref:System.Windows.Controls.Grid>，将<xref:System.Windows.Controls.Grid.Column%2A>附加属性设置为要重设大小的列之一。 如果你<xref:System.Windows.Controls.Grid>具有多个行，设置<xref:System.Windows.Controls.Grid.RowSpan%2A>附加属性设置为行数。 然后设置<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>属性设置为<xref:System.Windows.HorizontalAlignment.Left>或<xref:System.Windows.HorizontalAlignment.Right>（设置的对齐方式取决于你想要调整大小的两个列）。 最后，设置<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>属性设置为<xref:System.Windows.VerticalAlignment.Stretch>。  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterColumnOverlay](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplittercolumnoverlay)]  
  
 一个<xref:System.Windows.Controls.GridSplitter>不具有其各自的列中的其他控件可能会被遮盖<xref:System.Windows.Controls.Grid>。 有关如何避免此问题的详细信息，请参阅[确保 GridSplitter 可见](how-to-make-sure-that-a-gridsplitter-is-visible.md)。  
  
 **如何创建占据一列的 GridSplitter**  
  
 若要指定<xref:System.Windows.Controls.GridSplitter>占据一列中的<xref:System.Windows.Controls.Grid>，将<xref:System.Windows.Controls.Grid.Column%2A>附加属性设置为要重设大小的列之一。 如果您的网格包含多个行，请设置<xref:System.Windows.Controls.Grid.RowSpan%2A>附加属性设置为行数。 然后设置<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>到<xref:System.Windows.HorizontalAlignment.Center>，请设置<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>属性设置为<xref:System.Windows.VerticalAlignment.Stretch>，并设置<xref:System.Windows.Controls.ColumnDefinition.Width%2A>包含的列的<xref:System.Windows.Controls.GridSplitter>到<xref:System.Windows.GridLength.Auto%2A>。  
  
 下面的示例演示如何定义垂直<xref:System.Windows.Controls.GridSplitter>的占据一列和调整任意一侧列的大小。  
  
 [!code-xaml[GridSplitterRowColumn#GridSplitterEntireColumnPart1](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart1)]  
[!code-xaml[GridSplitterRowColumn#GridSplitterEntireColumnPart2](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterRowColumn/CS/Window1.xaml#gridsplitterentirecolumnpart2)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.GridSplitter>
- [帮助主题](gridsplitter-how-to-topics.md)
