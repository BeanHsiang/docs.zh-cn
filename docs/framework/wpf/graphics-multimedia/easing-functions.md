---
title: 缓动函数
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applying mathematical formulas to animations [WPF]
- applying easing functions to animations [WPF]
- mathematical formulas [WPF], applying to animations
- animations [WPF], realistic movement
- easing functions [WPF]
- customizing easing functions [WPF]
- easing functions [WPF], definition
- easing functions [WPF], customizing
- animations [WPF], applying
ms.assetid: 075b9c2b-82c4-43fa-b3cd-de0b6236eb38
ms.openlocfilehash: 456308e37bddc1df86b49085139a3810c4959a58
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354500"
---
# <a name="easing-functions"></a>缓动函数
缓动函数允许将自定义的数学公式应用到动画。 例如，用户可能希望某个对象逼真地弹跳或表现出像在弹簧上一样。 可使用关键帧甚至 From/To/By 动画来近似地实现这些效果，但它将需要大量工作，并且动画不如使用数学公式准确。  
  
 除了通过继承创建自定义的缓动函数<xref:System.Windows.Media.Animation.EasingFunctionBase>，可以使用由运行时提供的多个缓动函数之一创建常见效果。  
  
-   <xref:System.Windows.Media.Animation.BackEase>：略微收回动画的动作，然后再开始进行动画处理指示的路径中。  
  
-   <xref:System.Windows.Media.Animation.BounceEase>：创建弹跳效果。  
  
-   <xref:System.Windows.Media.Animation.CircleEase>：创建加速和/或减速使用循环函数的动画。  
  
-   <xref:System.Windows.Media.Animation.CubicEase>：创建加速和/或减速使用的公式的动画*f*(*t*) = *t*<sup>3</sup>。  
  
-   <xref:System.Windows.Media.Animation.ElasticEase>：创建类似于弹簧来回直到静止的动画。  
  
-   <xref:System.Windows.Media.Animation.ExponentialEase>：创建加速和/或减速使用指数公式的动画。  
  
-   <xref:System.Windows.Media.Animation.PowerEase>：创建加速和/或减速使用的公式的动画*f*(*t*) = *t*<sup>p</sup>其中 p 等于<xref:System.Windows.Media.Animation.PowerEase.Power%2A>属性。  
  
-   <xref:System.Windows.Media.Animation.QuadraticEase>：创建加速和/或减速使用的公式的动画*f*(*t*) = *t*<sup>2</sup>。  
  
-   <xref:System.Windows.Media.Animation.QuarticEase>：创建加速和/或减速使用的公式的动画*f*(*t*) = *t*<sup>4</sup>。  
  
-   <xref:System.Windows.Media.Animation.QuinticEase>：创建加速和/或减速使用的公式的动画*f*(*t*) = *t*<sup>5</sup>。  
  
-   <xref:System.Windows.Media.Animation.SineEase>：创建加速和/或减速使用正弦公式的动画。  
  
 若要应用到动画的缓动函数，使用`EasingFunction`动画属性指定要应用到动画的缓动函数。 下面的示例应用<xref:System.Windows.Media.Animation.BounceEase>缓动函数到<xref:System.Windows.Media.Animation.DoubleAnimation>创建弹跳效果。  
  
 [!code-xaml[BounceEase_snippet#BounceEase](~/samples/snippets/csharp/VS_Snippets_Wpf/bounceease_snippet/CS/window1.xaml#bounceease)]  
  
 在上一示例中，缓动函数应用于 From/To/By 动画。 还可以将这些缓动函数应用到关键帧动画。 以下示例显示如何将关键帧与其相关联的缓动函数结合使用，以创建一个协定上升、减速、向下展开（如同下落），然后弹跳至停止的矩形的动画。  
  
 [!code-xaml[EasingFunctionDoubleKeyFrame_snippet#EasingFunctionDoubleKeyFrame](~/samples/snippets/csharp/VS_Snippets_Wpf/easingfunctiondoublekeyframe_snippet/CS/window1.xaml#easingfunctiondoublekeyframe)]  
  
 可以使用<xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>属性更改缓动函数的行为方式，即更改动画的内插。 有三个可能的值可以为<xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>:  
  
-   <xref:System.Windows.Media.Animation.EasingMode.EaseIn>：内插遵循与缓动函数相关联的数学公式。  
  
-   <xref:System.Windows.Media.Animation.EasingMode.EaseOut>：内插遵循 100%内插值减去输出与缓动函数相关联的公式。  
  
-   <xref:System.Windows.Media.Animation.EasingMode.EaseInOut>：使用内插<xref:System.Windows.Media.Animation.EasingMode.EaseIn>动画的第一个另一半和<xref:System.Windows.Media.Animation.EasingMode.EaseOut>虚拟机。  
  
 下图演示了不同的值<xref:System.Windows.Media.Animation.EasingFunctionBase.EasingMode%2A>其中*f*(*x*) 表示动画进度和*t*表示时间。  
  
 <xref:System.Windows.Media.Animation.BackEase>  
  
 ![BackEase EasingMode 图。](./media/backease-graph.png "BackEase_Graph")  
  
 <xref:System.Windows.Media.Animation.BounceEase>  
  
 ![BounceEase EasingMode 图。](./media/bounceease-graph.png "BounceEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CircleEase>  
  
 ![CircleEase EasingMode图。](./media/circleease-graph.png "CircleEase_Graph")  
  
 <xref:System.Windows.Media.Animation.CubicEase>  
  
 ![CubicEase EasingMode 图。](./media/cubicease-graph.png "CubicEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ElasticEase>  
  
 ![带不同缓动模式图的 ElasticEase。](./media/elasticease-graph.png "ElasticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.ExponentialEase>  
  
 ![不同缓动模式的 ExponentialEase 图。](./media/exponentialease-graph.png "ExponentialEase_Graph")  
  
 <xref:System.Windows.Media.Animation.PowerEase>  
  
 ![带不同缓动模式图的 QuarticEase。](./media/quarticease-graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuadraticEase>  
  
 ![带不同缓动模式图的 QuadraticEase](./media/quadraticease-graph.png "QuadraticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuarticEase>  
  
 ![带不同缓动模式图的 QuarticEase。](./media/quarticease-graph.png "QuarticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.QuinticEase>  
  
 ![带不同缓动模式图的 QuinticEase。](./media/quinticease-graph.png "QuinticEase_Graph")  
  
 <xref:System.Windows.Media.Animation.SineEase>  
  
 ![不同 EasingMode 值的 SineEase](./media/sineease-graph.png "SineEase_Graph")  
  
> [!NOTE]
>  可以使用<xref:System.Windows.Media.Animation.PowerEase>来创建相同的行为<xref:System.Windows.Media.Animation.CubicEase>， <xref:System.Windows.Media.Animation.QuadraticEase>， <xref:System.Windows.Media.Animation.QuarticEase>，并<xref:System.Windows.Media.Animation.QuinticEase>使用<xref:System.Windows.Media.Animation.PowerEase.Power%2A>属性。 例如，如果你想要使用<xref:System.Windows.Media.Animation.PowerEase>将替换为<xref:System.Windows.Media.Animation.CubicEase>，指定<xref:System.Windows.Media.Animation.PowerEase.Power%2A>值为 3。  
  
 除了使用运行时中附带的缓动函数，可以创建自己的自定义缓动函数，通过继承<xref:System.Windows.Media.Animation.EasingFunctionBase>。 以下示例演示如何创建简单的自定义缓动函数。 可以添加您自己的数学逻辑通过重写的缓动函数的行为方式<xref:System.Windows.Media.Animation.EasingFunctionBase.EaseInCore%2A>方法。   
  
 [!code-csharp[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/customlog10easingfunction.cs#customeasingfunction)]
 [!code-vb[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/visualbasic/VS_Snippets_Wpf/customeasingfunction/visualbasic/customlog10easingfunction.vb#customeasingfunction)]
 [!code-xaml[CustomEasingFunction#CustomEasingFunction](~/samples/snippets/csharp/VS_Snippets_Wpf/customeasingfunction/csharp/window1.xaml#customeasingfunction)]
