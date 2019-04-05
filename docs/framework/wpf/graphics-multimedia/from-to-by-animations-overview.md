---
title: 从-到-By 动画概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], From/to/by
- From/to/by animation
ms.assetid: 516fce0a-e7f8-49b8-b018-53b3d409a8a3
ms.openlocfilehash: 40a37542d6151d05910bc033657d85c6a9f5483b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57362755"
---
# <a name="fromtoby-animations-overview"></a>From/To/By 动画概述
本主题介绍如何使用 From/To/By 动画对依赖属性进行动画处理。 From/To/By 动画创建两个值之间的转换。  
  
<a name="prereq"></a>   
## <a name="prerequisites"></a>系统必备  
 若要了解本主题，您应熟悉[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画功能。 有关动画功能的简介，请参阅[动画概述](animation-overview.md)。  
  
<a name="whatisanimation"></a>   
## <a name="what-is-a-fromtoby-animation"></a>什么是 From/To/By 动画？  
 From/To/By 动画是一种<xref:System.Windows.Media.Animation.AnimationTimeline>创建起始值和终止值之间的转换。 完成转换所需的时间量由<xref:System.Windows.Media.Animation.Timeline.Duration%2A>对动画。  
  
 可以应用 From/To/By 动画对属性使用<xref:System.Windows.Media.Animation.Storyboard>标记和代码，或通过使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>中代码的方法。 您还可以使用 From/To/By 动画创建<xref:System.Windows.Media.Animation.AnimationClock>并将其应用到一个或多个属性。 有关应用动画的不同方法的详细信息，请参阅[属性动画技术概述](property-animation-techniques-overview.md)。  
  
 From/To/By 动画的目标值不能超过两个。 如果需要具有两个以上目标值的动画，请使用关键帧。 关键帧动画进行了介绍[关键帧动画概述](key-frame-animations-overview.md)。  
  
<a name="animation_types"></a>   
## <a name="fromtoby-animation-types"></a>From/To/By 动画类型  
 由于动画会生成属性值，因此不同的属性类型具有不同的动画类型。 若要对采用的属性进行动画处理<xref:System.Double>，如<xref:System.Windows.FrameworkElement.Width%2A>属性的元素，使用生成的动画，<xref:System.Double>值。 若要对采用的属性进行动画处理<xref:System.Windows.Point>，使用生成的动画，<xref:System.Windows.Point>值，等等。  
  
 From/To/By 动画类属于<xref:System.Windows.Media.Animation>命名空间，并使用以下命名约定：  
  
 *\<Type>* `Animation`  
  
 其中 *\<Type>* 为该类进行动画处理的值的类型。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供以下 From/To/By 动画类。  
  
|属性类型|对应的 From/To/By 动画类|  
|-------------------|------------------------------------------------|  
|<xref:System.Byte>|<xref:System.Windows.Media.Animation.ByteAnimation>|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|  
|<xref:System.Decimal>|<xref:System.Windows.Media.Animation.DecimalAnimation>|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|  
|<xref:System.Int16>|<xref:System.Windows.Media.Animation.Int16Animation>|  
|<xref:System.Int32>|<xref:System.Windows.Media.Animation.Int32Animation>|  
|<xref:System.Int64>|<xref:System.Windows.Media.Animation.Int64Animation>|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|  
|<xref:System.Windows.Media.Media3D.Quaternion>|<xref:System.Windows.Media.Animation.QuaternionAnimation>|  
|<xref:System.Windows.Rect>|<xref:System.Windows.Media.Animation.RectAnimation>|  
|<xref:System.Windows.Media.Media3D.Rotation3D>|<xref:System.Windows.Media.Animation.Rotation3DAnimation>|  
|<xref:System.Single>|<xref:System.Windows.Media.Animation.SingleAnimation>|  
|<xref:System.Windows.Size>|<xref:System.Windows.Media.Animation.SizeAnimation>|  
|<xref:System.Windows.Thickness>|<xref:System.Windows.Media.Animation.ThicknessAnimation>|  
|<xref:System.Windows.Media.Media3D.Vector3D>|<xref:System.Windows.Media.Animation.Vector3DAnimation>|  
|<xref:System.Windows.Vector>|<xref:System.Windows.Media.Animation.VectorAnimation>|  
  
<a name="anim_values"></a>   
## <a name="target-values"></a>目标值  
 From/To/By 动画创建两个目标值之间的转换。 通常指定起始值 (通过设置<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性) 和终止值 (通过设置<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性)。 但是，还可以仅指定起始值、目标值或偏移值。 在这些类中，动画从要进行动画处理的属性中获取缺少的目标值。 以下列表描述了指定动画目标值的各种方法。  
  
-   **起始值**  
  
     使用<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性时想要显式指定动画的起始值。 可以使用<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性本身，或使用<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>或<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性。 如果仅指定<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性中，动画从该值过渡到基值属性的基值。  
  
-   **终止值**  
  
     若要指定动画的结束值，使用其<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性。 如果使用<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>本身的属性，从要进行动画处理的属性或将应用到相同属性的另一个动画的输出动画获取其起始值。 可以使用<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性和<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性来显式指定开始和结束值的动画。  
  
-   **偏移值**  
  
     <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性可以指定偏移，而不是显式的起始或动画的结束值。 <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>动画属性指定由多少动画更改其持续时间内的值。 可以使用<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>独自或与属性<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性。 如果仅指定<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性，则动画将偏移量的值添加到属性的基值或另一个动画的输出。  
  
<a name="examples"></a>   
## <a name="using-fromtoby-values"></a>使用 From/To/By 值  
 以下部分介绍如何使用<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>， <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>，和<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性单独或一起。  
  
 本节中的示例的每次使用<xref:System.Windows.Media.Animation.DoubleAnimation>，这是一种 From/To/By 动画进行动画处理<xref:System.Windows.FrameworkElement.Width%2A>属性的<xref:System.Windows.Shapes.Rectangle>，它是 10 个设备无关的像素高和 100 设备无关的像素宽。  
  
 尽管每个示例使用<xref:System.Windows.Media.Animation.DoubleAnimation>、 From、 To 和 By 属性的所有 From/To/By 动画的行为相同。 尽管每个示例使用<xref:System.Windows.Media.Animation.Storyboard>，可以以其他方式使用 From/To/By 动画。 有关详细信息，请参阅[属性动画技术概述](property-animation-techniques-overview.md)。  
  
### <a name="fromto"></a>从/到  
 当您将设置<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>并<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>值一起，动画从指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性，为指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性。  
  
 下面的示例设置<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>的属性<xref:System.Windows.Media.Animation.DoubleAnimation>为 50 和其<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性设置为 300。 因此，<xref:System.Windows.FrameworkElement.Width%2A>的<xref:System.Windows.Shapes.Rectangle>从 50 到 300 的动画。  
  
 [!code-csharp[basicvalues_snip#FromToAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromtoanimationinline)]
 [!code-vb[basicvalues_snip#FromToAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromtoanimationinline)]  
  
### <a name="to"></a>到  
 如果只设置<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性，则动画从属性的基值，或从之前应用到相同的属性，为指定的值的组合动画的输出继续<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性。  
  
 ("组合动画"是指<xref:System.Windows.Media.Animation.ClockState.Active>或<xref:System.Windows.Media.Animation.ClockState.Filling>之前应用于通过使用应用当前动画时所做的更改的相同属性的动画<xref:System.Windows.Media.Animation.HandoffBehavior.Compose>的切换行为。)  
  
 下面的示例只是设置<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性的<xref:System.Windows.Media.Animation.DoubleAnimation>为 300。 不指定了任何起始值，因为<xref:System.Windows.Media.Animation.DoubleAnimation>使用的基值 (100)<xref:System.Windows.FrameworkElement.Width%2A>属性作为其起始值。 <xref:System.Windows.FrameworkElement.Width%2A>的<xref:System.Windows.Shapes.Rectangle>从 100 到动画的目标值 300 的动画。  
  
 [!code-csharp[basicvalues_snip#ToAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#toanimationinline)]
 [!code-vb[basicvalues_snip#ToAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#toanimationinline)]  
  
### <a name="by"></a>间距  
 如果只设置<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>动画属性，则动画继续从进行动画处理，该属性的基值或组合动画值和由指定的值的总和的输出<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性。  
  
 下面的示例只是设置<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性的<xref:System.Windows.Media.Animation.DoubleAnimation>为 300。 由于该示例未指定起始值，<xref:System.Windows.Media.Animation.DoubleAnimation>使用的基础价值<xref:System.Windows.FrameworkElement.Width%2A>属性，100，作为其起始值。 结束值确定添加<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>动画，300，为其起始值 100 的值：400. 因此，<xref:System.Windows.FrameworkElement.Width%2A>的<xref:System.Windows.Shapes.Rectangle>从 100 到 400 的动画。  
  
 [!code-csharp[basicvalues_snip#ByAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#byanimationinline)]
 [!code-vb[basicvalues_snip#ByAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#byanimationinline)]  
  
### <a name="fromby"></a>From/By  
 当您将设置<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>和<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>动画的属性，动画从指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性，为之和指定值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>和<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性。  
  
 下面的示例设置<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>的属性<xref:System.Windows.Media.Animation.DoubleAnimation>为 50 和其<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性设置为 300。 结束值确定添加<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>动画，其起始值 50 到 300 的值：350. 因此，<xref:System.Windows.FrameworkElement.Width%2A>的<xref:System.Windows.Shapes.Rectangle>从 50 到 350 的动画。  
  
 [!code-csharp[basicvalues_snip#FromByAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#frombyanimationinline)]
 [!code-vb[basicvalues_snip#FromByAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#frombyanimationinline)]  
  
### <a name="from"></a>From  
 您只需指定<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>值的动画，动画从指定的值<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性，为要进行动画处理的属性的基值或组合动画的输出。  
  
 下面的示例只是设置<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性的<xref:System.Windows.Media.Animation.DoubleAnimation>为 50。 指定不终止值，因为<xref:System.Windows.Media.Animation.DoubleAnimation>使用的基础价值<xref:System.Windows.FrameworkElement.Width%2A>属性，100，作为其终止值。 <xref:System.Windows.FrameworkElement.Width%2A>的<xref:System.Windows.Shapes.Rectangle>从 50 到的基值的动画<xref:System.Windows.FrameworkElement.Width%2A>属性，100。  
  
 [!code-csharp[basicvalues_snip#FromAnimationInline](~/samples/snippets/csharp/VS_Snippets_Wpf/basicvalues_snip/CSharp/AnimationTargetValuesExample.cs#fromanimationinline)]
 [!code-vb[basicvalues_snip#FromAnimationInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/basicvalues_snip/VisualBasic/AnimationTargetValuesExample.vb#fromanimationinline)]  
  
### <a name="toby"></a>To/By  
 如果同时设置<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>并<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>的动画，属性<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>属性将被忽略。  
  
<a name="otheranimationtypes"></a>   
## <a name="other-animation-types"></a>其他动画类型  
 From/To/By 动画不是唯一的动画类型的[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]提供： 它还提供了关键帧动画和路径动画。  
  
-   关键帧动画沿使用关键帧描述的任意数量的目标值进行动画处理。 有关详细信息，请参阅[关键帧动画概述](key-frame-animations-overview.md)。  
  
-   路径动画会生成输出值<xref:System.Windows.Media.PathGeometry>。 有关详细信息，请参阅[路径动画概述](path-animations-overview.md)。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还支持创建自己的自定义动画类型。 有关详细信息，请参阅[自定义动画概述](custom-animations-overview.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Animation.Timeline>
- <xref:System.Windows.Media.Animation.Storyboard>
- [动画概述](animation-overview.md)
- [演示图板概述](storyboards-overview.md)
- [关键帧动画概述](key-frame-animations-overview.md)
- [路径动画概述](path-animations-overview.md)
- [自定义动画概述](custom-animations-overview.md)
- [From、To 和 By 动画目标值示例](https://go.microsoft.com/fwlink/?LinkID=159988)
