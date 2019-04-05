---
title: 如何：在使用演示图板对属性进行动画处理后设置该属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], changing property values after
ms.assetid: 79466556-4dbf-40bd-9c1e-a77613b07077
ms.openlocfilehash: 1f66c79f18fd02327c0c1f4f20787e566437f20f
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57359423"
---
# <a name="how-to-set-a-property-after-animating-it-with-a-storyboard"></a>如何：在使用演示图板对属性进行动画处理后设置该属性
在某些情况下，它可能显示后进行动画处理，无法更改属性的值。  
  
## <a name="example"></a>示例  
 在以下示例中，<xref:System.Windows.Media.Animation.Storyboard>使用的颜色进行动画处理<xref:System.Windows.Media.SolidColorBrush>。 单击此按钮时，会触发情节提要。 <xref:System.Windows.Media.Animation.Timeline.Completed> ，以便通知程序处理事件时<xref:System.Windows.Media.Animation.ColorAnimation>完成。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton1Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton1declaration)]  
  
## <a name="example"></a>示例  
 之后<xref:System.Windows.Media.Animation.ColorAnimation>完成后，该程序尝试更改画笔的颜色为蓝色。  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton1Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton1handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton1Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton1handler)]  
  
 前面的代码似乎不执行任何操作： 画笔仍然保持为黄色，即的值提供的<xref:System.Windows.Media.Animation.ColorAnimation>，经过动画处理的画笔。 基础属性值 （基本值） 实际更改为蓝色。 但是，有效，或当前的值仍保持为黄色因为<xref:System.Windows.Media.Animation.ColorAnimation>仍然在重写的基础价值。 如果你想要再次变得有效的值的基础值，必须使动画不再影响该属性。 有三种方法使用演示图板动画执行此操作：  
  
-   设置动画的<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>属性 <xref:System.Windows.Media.Animation.FillBehavior.Stop>  
  
-   删除整个情节提要。  
  
-   删除中的各个属性的动画。  
  
## <a name="set-the-animations-fillbehavior-property-to-stop"></a>将动画的 FillBehavior 属性设置为 Stop  
 通过设置<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>到<xref:System.Windows.Media.Animation.FillBehavior.Stop>，告诉动画停止到达其有效期末尾后影响其目标属性。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton2Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton2declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton2Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton2handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton2Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton2handler)]  
  
## <a name="remove-the-entire-storyboard"></a>删除整个情节提要  
 通过使用<xref:System.Windows.Media.Animation.RemoveStoryboard>触发器或<xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=nameWithType>方法，您告诉情节提要动画停止影响其目标属性。 此方法和设置之间的区别<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>属性是可以删除情节提要在任何时间，而<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>属性动画到达其活动周期的结尾时才有意义。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton3Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton3declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton3Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton3handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton3Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton3handler)]  
  
## <a name="remove-an-animation-from-an-individual-property"></a>从的单个属性中删除动画  
 若要停止的动画影响属性的另一种方法是使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29>对象进行动画处理的方法。 指定要进行动画处理的第一个参数的属性和`null`为第二个。  
  
 [!code-xaml[timingbehaviors_snip#GraphicsMMButton4Declaration](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml#graphicsmmbutton4declaration)]  
  
 [!code-csharp[timingbehaviors_snip#GraphicsMMButton4Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AnimateThenSetPropertyExample.xaml.cs#graphicsmmbutton4handler)]
 [!code-vb[timingbehaviors_snip#GraphicsMMButton4Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_snip/visualbasic/animatethensetpropertyexample.xaml.vb#graphicsmmbutton4handler)]  
  
 此方法也适用于非演示图板动画。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>
- <xref:System.Windows.Media.Animation.Storyboard.Remove%2A?displayProperty=nameWithType>
- <xref:System.Windows.Media.Animation.RemoveStoryboard>
- [动画概述](animation-overview.md)
- [属性动画技术概述](property-animation-techniques-overview.md)
