---
title: 如何：使 UIElement 呈现为透明或半透明
ms.date: 03/30/2017
helpviewer_keywords:
- UIElements [WPF], transparency
- opacity [WPF], of UIElements
- transparency of UIElements [WPF]
- UIElements [WPF], opacity
ms.assetid: a49fc8d6-7b32-4f28-9122-39b632a19b4b
ms.openlocfilehash: 1de9a7e11fee241ecb71242e9808e77b7e5e63b0
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57370522"
---
# <a name="how-to-make-a-uielement-transparent-or-semi-transparent"></a>如何：使 UIElement 呈现为透明或半透明
此示例演示如何使<xref:System.Windows.UIElement>透明或半透明。 若要使元素透明或半透明，设置其<xref:System.Windows.UIElement.Opacity%2A>属性。 值为`0.0`使元素完全透明，而值`1.0`使元素完全不透明。 值为`0.5`使元素 50%，依此类推。 元素的<xref:System.Windows.UIElement.Opacity%2A>设置为`1.0`默认情况下。  
  
## <a name="example"></a>示例  
 下面的示例设置<xref:System.Windows.UIElement.Opacity%2A>某个按钮`0.25`，使它和其内容 （在此情况下，该按钮的文本） 25%不透明。  
  
 [!code-xaml[brushsamples_snip#2](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#2)]  
  
 [!code-csharp[brushsamples_procedural_snip#2](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#2)]  
  
 如果元素的内容有其自己<xref:System.Windows.UIElement.Opacity%2A>设置，这些值相乘的包含元素<xref:System.Windows.UIElement.Opacity%2A>。  
  
 下面的示例设置按钮的<xref:System.Windows.UIElement.Opacity%2A>到`0.25`，并<xref:System.Windows.UIElement.Opacity%2A>的<xref:System.Windows.Controls.Image>控件中的按钮，包含与`0.5`。 因此，图像将显示为 12.5%不透明：0.25 * 0.5 = 0.125.  
  
 [!code-xaml[brushsamples_snip#3](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#3)]  
  
 [!code-csharp[brushsamples_procedural_snip#3](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#3)]  
  
 另一种方法来控制元素的不透明度是设置的不透明度<xref:System.Windows.Media.Brush>绘制元素。 这种方法使您可以选择性地更改的一个元素部分的不透明度，并通过将元素的提供性能优势<xref:System.Windows.UIElement.Opacity%2A>属性。 下面的示例设置<xref:System.Windows.Media.Brush.Opacity%2A>的<xref:System.Windows.Media.SolidColorBrush>用于绘制按钮的<xref:System.Windows.Controls.Control.Background%2A>设置为`0.25`。 因此，画笔的背景为 25%不透明的但其内容 （该按钮的文本） 仍保留 100%不透明。  
  
 [!code-xaml[brushsamples_snip#4](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_snip/CS/OpacityExample.xaml#4)]  
  
 [!code-csharp[brushsamples_procedural_snip#4](~/samples/snippets/csharp/VS_Snippets_Wpf/brushsamples_procedural_snip/CSharp/OpacityExample.cs#4)]  
  
 您也可以控制单个颜色画笔的不透明度。 有关颜色和画笔的详细信息，请参阅[使用纯色和渐变概述进行绘制](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)。 有关演示如何对元素的不透明度进行动画处理的示例，请参阅[对元素或画笔的不透明度进行动画处理](../graphics-multimedia/how-to-animate-the-opacity-of-an-element-or-brush.md)。
