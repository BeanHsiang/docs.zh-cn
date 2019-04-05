---
title: 如何：使用关键帧针对对象进行动画处理
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], objects with key frames
- key frames [WPF], animating objects with
ms.assetid: b1f15ba9-cac7-4cea-8699-5c6b55c05c5e
ms.openlocfilehash: 1e0e464adf70aeeaecb522d328d3087ca66a530c
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368553"
---
# <a name="how-to-animate-an-object-by-using-key-frames"></a>如何：使用关键帧针对对象进行动画处理
此示例演示如何对一个对象，其在此示例中为进行动画处理<xref:System.Windows.Controls.Page.Background%2A>属性的<xref:System.Windows.Controls.Page>控件，使用关键帧。  
  
## <a name="example"></a>示例  
 下面的示例使用<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>类进行动画处理颜色更改为<xref:System.Windows.Controls.Page.Background%2A>属性的<xref:System.Windows.Controls.Page>控件。 示例动画按固定间隔更改为不同的背景画笔。 此动画使用<xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>类，以创建三个不同的关键帧。 动画使用关键帧按以下方式：  
  
1.  在第一秒结束时，进行动画处理的实例<xref:System.Windows.Media.LinearGradientBrush>类。 以便颜色黄色从过渡为红色的橙色到，该示例的此部分适用于的背景色线性渐变。  
  
2.  在下一步秒结束时，进行动画处理的实例<xref:System.Windows.Media.RadialGradientBrush>类。 此部分示例适用范围径向渐变的背景色，以便从白色到黑色蓝色颜色转换。  
  
3.  在第三个秒结束时，进行动画处理的实例<xref:System.Windows.Media.DrawingBrush>类。 该示例的此部分适用于在后台棋盘图案。  
  
4.  动画将重新开始并无限期地重复。  
  
> [!NOTE]
>  <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame> 是唯一的您可以使用关键帧类型<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>类。 关键帧等<xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>，它是在值中，创建突然变化，突然发生在此示例中的颜色更改。  
  
 [!code-xaml[keyframes_snip#ObjectAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/ObjectAnimationUsingKeyFramesExample.xaml#objectanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参阅[关键帧动画示例](https://go.microsoft.com/fwlink/?LinkID=160012)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>
- <xref:System.Windows.Controls.Page.Background%2A>
- <xref:System.Windows.Controls.Page>
- <xref:System.Windows.Media.Animation.DiscreteObjectKeyFrame>
- <xref:System.Windows.Media.LinearGradientBrush>
- <xref:System.Windows.Media.RadialGradientBrush>
- <xref:System.Windows.Media.DrawingBrush>
- [关键帧动画概述](key-frame-animations-overview.md)
- [关键帧操作说明主题](key-frame-animation-how-to-topics.md)
