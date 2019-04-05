---
title: 如何：设置元素的高度属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- height properties [WPF]
- Panel control [WPF], height properties of elements
ms.assetid: 5ab9e781-dbb8-469a-a3c8-cf38ce312647
ms.openlocfilehash: 608f74afd95ce03b3ecf71819c2181a9728b25af
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356282"
---
# <a name="how-to-set-the-height-properties-of-an-element"></a>如何：设置元素的高度属性
## <a name="example"></a>示例  
 此示例中直观地显示之间的四个高度相关的属性中的呈现行为差异[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]。  
  
 <xref:System.Windows.FrameworkElement>类公开描述的元素的高度特征的四个属性。 这四个属性可能会发生冲突，并且当他们这样做，将优先的值确定，如下所示：<xref:System.Windows.FrameworkElement.MinHeight%2A>值将优先于<xref:System.Windows.FrameworkElement.MaxHeight%2A>值，后者又优先于<xref:System.Windows.FrameworkElement.Height%2A>值。 第四个属性， <xref:System.Windows.FrameworkElement.ActualHeight%2A>，是只读的并将报告由与布局过程的交互的实际高度。  
  
 以下[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]示例绘制<xref:System.Windows.Shapes.Rectangle>元素 (`rect1`) 的子级作为<xref:System.Windows.Controls.Canvas>。 可以更改的高度属性<xref:System.Windows.Shapes.Rectangle>通过使用一系列<xref:System.Windows.Controls.ListBox>表示的属性值的元素<xref:System.Windows.FrameworkElement.MinHeight%2A>， <xref:System.Windows.FrameworkElement.MaxHeight%2A>，和<xref:System.Windows.FrameworkElement.Height%2A>。 以这种方式，以可视化方式显示每个属性的优先级。  
  
 [!code-xaml[HeightMinHeightMaxHeight#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#1)]  
[!code-xaml[HeightMinHeightMaxHeight#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml#2)]  
  
 下面的代码隐藏示例处理事件的<xref:System.Windows.Controls.Primitives.Selector.SelectionChanged>事件引发。 每个处理程序接受从输入<xref:System.Windows.Controls.ListBox>，将值作为分析<xref:System.Double>，并将值应用于指定高度相关的属性。 高度值也转换为字符串和写入到各种<xref:System.Windows.Controls.TextBlock>元素 （这些元素的定义不在所选的 XAML 所示）。  
  
 [!code-csharp[HeightMinHeightMaxHeight#3](~/samples/snippets/csharp/VS_Snippets_Wpf/HeightMinHeightMaxHeight/CSharp/Window1.xaml.cs#3)]
 [!code-vb[HeightMinHeightMaxHeight#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HeightMinHeightMaxHeight/VisualBasic/Window1.xaml.vb#3)]  
  
 有关完整示例，请参阅[高度属性示例](https://go.microsoft.com/fwlink/?LinkID=159993)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.Controls.ListBox>
- <xref:System.Windows.FrameworkElement.ActualHeight%2A>
- <xref:System.Windows.FrameworkElement.MaxHeight%2A>
- <xref:System.Windows.FrameworkElement.MinHeight%2A>
- <xref:System.Windows.FrameworkElement.Height%2A>
- [设置元素的宽度属性](how-to-set-the-width-properties-of-an-element.md)
- [面板概述](panels-overview.md)
- [高度属性示例](https://go.microsoft.com/fwlink/?LinkID=159993)
