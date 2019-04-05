---
title: 如何：对 FrameworkElement 的大小进行动画处理
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], FrameworkElement size
- FrameworkElement [WPF], animating size of
ms.assetid: d4cd5a13-c20d-4a6f-a2ba-14f2c9ce4cef
ms.openlocfilehash: d1995deec5ab2c9bf405911af43b4d242d599119
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360987"
---
# <a name="how-to-animate-the-size-of-a-frameworkelement"></a>如何：对 FrameworkElement 的大小进行动画处理
要进行动画处理的大小<xref:System.Windows.FrameworkElement>，也可以动态显示其<xref:System.Windows.FrameworkElement.Width%2A>并<xref:System.Windows.FrameworkElement.Height%2A>属性或使用经过动画处理的<xref:System.Windows.Media.ScaleTransform>。  
  
 在下面的示例之间进行动画处理使用这两种方法的两个按钮的大小。 通过对进行动画处理调整一个按钮的大小及其<xref:System.Windows.FrameworkElement.Width%2A>由进行动画处理调整大小属性，另一个<xref:System.Windows.Media.ScaleTransform>应用于其<xref:System.Windows.UIElement.RenderTransform%2A>属性。 每个按钮包含一些文本。 最初的文本将出现在这两个按钮中相同，但这些按钮会调整大小时，第二个按钮中的文本会显得失真。  
  
## <a name="example"></a>示例  
 [!code-xaml[transformanimations_snip#1](~/samples/snippets/xaml/VS_Snippets_Wpf/transformanimations_snip/XAML/AnimatingSizeExample.xaml#1)]  
  
 在转换元素时，转换整个元素及其内容。 直接更改的大小的元素，如下所示的第一个按钮，这种情况时除非其大小和位置取决于其父元素的大小，否则无法调整大小的元素的内容。  
  
 通过将应用到动画的转换对元素的大小进行动画处理其<xref:System.Windows.UIElement.RenderTransform%2A>属性提供了更好的性能不是进行动画处理其<xref:System.Windows.FrameworkElement.Width%2A>并<xref:System.Windows.FrameworkElement.Height%2A>直接，因为<xref:System.Windows.UIElement.RenderTransform%2A>属性不会触发布局过程。  
  
 有关对属性进行动画处理的详细信息，请参阅[动画概述](../graphics-multimedia/animation-overview.md)。 有关转换的详细信息，请参阅[转换概述](../graphics-multimedia/transforms-overview.md)。
