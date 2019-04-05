---
title: 关键帧动画概述
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], key-frame
- key frames [WPF], about key-frame animations
- multiple animation target values [WPF]
ms.assetid: 10028f97-bb63-41fc-b8ad-663dac7ea203
ms.openlocfilehash: a4606b73835087a406d989960d7a6e24ad218769
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57362976"
---
# <a name="key-frame-animations-overview"></a>关键帧动画概述
本主题介绍关键帧动画。 通过关键帧动画，可以使用两个以上的目标值进行动画处理，并控制动画的内插方法。  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>系统必备  
 若要理解本概述，用户应熟悉 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 动画和时间线。 有关动画的简介，请参阅[动画概述](animation-overview.md)。 它还有助于熟悉 From/To/By 动画。 有关详细信息，请参阅“From/To/By 动画概述”。  
  
<a name="whatisakeyframeanimation"></a>   
## <a name="what-is-a-key-frame-animation"></a>什么是关键帧动画？  
 与 From/To/By 动画类似，关键帧动画对目标属性的值进行动画处理。 它通过创建其目标值之间的转换其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>。 但是，From/To/By 动画可以在两个值之间创建过渡，而单个关键帧动画可以在任意数量的目标值之间创建过渡。 不同于 From/To/By 动画，关键帧动画没有设置其目标值所需的 From、To 或 By 属性。 关键帧动画的目标值使用关键帧对象进行描述，因此称作“关键帧动画”。 若要指定动画的目标值，您可以创建关键帧对象并将其添加到动画的<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.KeyFrames%2A>集合。 动画运行时，将在指定的帧之间过渡。  
  
 某些关键帧方法除支持多个目标值外，甚至还支持多个内插方法。 动画的内插方法定义了从一个值过渡到下一个值的方式。 有三种内插类型：离散、线性和曲线。  
  
 若要使用关键帧动画进行动画处理，需要完成下列步骤。  
  
-   声明动画并指定其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>，就像 from/to/by 动画。  
  
-   对于每个目标值，请创建相应类型的一个关键帧，将其值设置并<xref:System.Windows.Media.Animation.KeyTime>，并将其添加到动画的<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.KeyFrames%2A>集合。  
  
-   以针对 From/To/By 动画的方式将该动画与属性相关联。 有关使用演示图板将动画应用到属性的详细信息，请参阅[演示图板概述](storyboards-overview.md)。  
  
 下面的示例使用<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>进行动画处理<xref:System.Windows.Shapes.Rectangle>到四个不同位置的元素。  
  
 [!code-xaml[keyframes_ovw_snippet#BasicKeyFrameExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyFramesIntroduction.xaml#basickeyframeexamplewholepage)]  
  
 喜欢 From/To/By 动画，关键帧动画可以通过使用应用于属性<xref:System.Windows.Media.Animation.Storyboard>标记和代码中或通过使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>中代码的方法。 您还可以使用关键帧动画创建<xref:System.Windows.Media.Animation.AnimationClock>并将其应用到一个或多个属性。 有关应用动画的不同方法的详细信息，请参阅[属性动画技术概述](property-animation-techniques-overview.md)。  
  
<a name="animation_types"></a>   
## <a name="key-frame-animation-types"></a>关键帧动画类型  
 由于动画会生成属性值，因此不同的属性类型具有不同的动画类型。 采用属性进行动画处理<xref:System.Double>(例如元素的<xref:System.Windows.FrameworkElement.Width%2A>属性)，可以使用生成的动画<xref:System.Double>值。 采用属性进行动画处理<xref:System.Windows.Point>，可以使用生成的动画<xref:System.Windows.Point>值，等等。  
  
 关键帧动画类属于<xref:System.Windows.Media.Animation>命名空间，并且遵守以下命名约定：  
  
 *\<Type>* `AnimationUsingKeyFrames`  
  
 其中 *\<Type>* 为该类进行动画处理的值的类型。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了以下关键帧动画类。  
  
|属性类型|对应的 From/To/By 动画类|支持的内插方法|  
|-------------------|------------------------------------------------|-------------------------------------|  
|<xref:System.Boolean>|<xref:System.Windows.Media.Animation.BooleanAnimationUsingKeyFrames>|离散|  
|<xref:System.Byte>|<xref:System.Windows.Media.Animation.ByteAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Decimal>|<xref:System.Windows.Media.Animation.DecimalAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Int16>|<xref:System.Windows.Media.Animation.Int16AnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Int32>|<xref:System.Windows.Media.Animation.Int32AnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Int64>|<xref:System.Windows.Media.Animation.Int64AnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingKeyFrames>|离散|  
|<xref:System.Object>|<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>|离散|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Media.Media3D.Quaternion>|<xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Rect>|<xref:System.Windows.Media.Animation.RectAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Media.Media3D.Rotation3D>|<xref:System.Windows.Media.Animation.Rotation3DAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Single>|<xref:System.Windows.Media.Animation.SingleAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.String>|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|离散|  
|<xref:System.Windows.Size>|<xref:System.Windows.Media.Animation.SizeAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Thickness>|<xref:System.Windows.Media.Animation.ThicknessAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Media.Media3D.Vector3D>|<xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames>|离散、线性、曲线|  
|<xref:System.Windows.Vector>|<xref:System.Windows.Media.Animation.VectorAnimationUsingKeyFrames>|离散、线性、曲线|  
  
<a name="animation_target_values"></a>   
## <a name="target-values-key-frames-and-key-times"></a>目标值（关键帧）和关键时间  
 就像在对不同属性类型进行动画处理时有不同类型的关键帧动画一样，关键帧对象的类型也各不相同：对于每种进行动画处理的值和所支持的内插方法，都有一个对象类型。 关键帧类型遵循以下命名约定：  
  
 *\<InterpolationMethod>\<Type>* `KeyFrame`  
  
 其中 *\<InterpolationMethod>* 是关键帧使用的内插方法，*\<Type>* 是类进行动画处理的值的类型。 支持所有三种内插方法的关键帧动画有三种关键帧类型可供使用。 例如，可以使用三种关键帧类型和<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>: <xref:System.Windows.Media.Animation.DiscreteDoubleKeyFrame>， <xref:System.Windows.Media.Animation.LinearDoubleKeyFrame>，和<xref:System.Windows.Media.Animation.SplineDoubleKeyFrame>。 （后面部分将对内插方法进行详细说明。）  
  
 关键帧的主要用途是指定<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>和一个<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>。 每个关键帧类型都可提供这两种属性。  
  
-   <xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>属性指定该关键帧的目标值。  
  
-   <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>属性指定当 (动画的内<xref:System.Windows.Media.Animation.Timeline.Duration%2A>) 关键帧的<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>为止。  
  
 关键帧动画开始后，循环访问其关键帧中定义的顺序按其<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>属性。  
  
-   如果 0 时刻没有关键帧，动画创建目标属性的当前值之间的转换和<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>的第一个关键帧; 否则，该动画的输出值将成为第一个关键帧的值。  
  
-   动画创建之间的转换<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>的第一个和第二个关键帧使用指定的第二个关键帧的内插方法。 第一个关键帧的过渡起始<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>时结束和第二个关键帧的<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>达到。  
  
-   动画将继续，这会创建每个后续关键帧和其前面的关键帧之间的过渡。  
  
-   最后的最大关键时间的关键帧，动画将转换为值是等于或小于动画的<xref:System.Windows.Media.Animation.Timeline.Duration%2A>。  
  
 如果该动画<xref:System.Windows.Media.Animation.Timeline.Duration%2A>是<xref:System.Windows.Duration.Automatic%2A>或其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>等于最后一个关键帧在动画结束的时间。 否则为如果动画<xref:System.Windows.Duration>大于关键时间的最后一个关键帧的关键帧值直到其到达末尾的动画保留其<xref:System.Windows.Duration>。 与所有动画关键帧动画使用其<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>属性来确定是否保留最终值到达其活动期结束时。 有关详细信息，请参阅[计时行为概述](timing-behaviors-overview.md)。  
  
 下面的示例使用<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>对象定义在前面的示例演示如何<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>和<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>属性的工作。  
  
-   第一个关键帧立即将动画的输出值设置为 0。  
  
-   第二个关键帧在 0 和 350 之间进行动画处理。 它在第一个关键帧结束后开始（开始时间 = 0 秒），播放 2 秒钟，结束时间 = 0:0:2。  
  
-   第三个关键帧在 350 和 50 之间进行动画处理。 它在第二个关键帧结束时开始（开始时间 = 2 秒），播放 5 秒钟，结束时间 = 0:0:7。  
  
-   第四个关键帧在 50 和 200 之间进行动画处理。 它在第三个关键帧结束时开始（开始时间 = 7 秒），播放 1 秒钟，结束时间 = 0:0:8。  
  
-   因为<xref:System.Windows.Media.Animation.Timeline.Duration%2A>动画属性设置为 10 秒，则该动画保留其最终值两秒钟，结束之前开始时间 = 0:0:10。  
  
 [!code-xaml[keyframes_ovw_snippet#BasicKeyFrameExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyFramesIntroduction.xaml#basickeyframeexamplewholepage)]  
  
<a name="interpolationmethods"></a>   
## <a name="interpolation-methods"></a>内插方法  
 前面部分提到了某些关键帧动画支持多种内插方法。 动画的内插对动画在其持续时间内在值之间进行过渡的方式进行了描述。 通过选择动画要使用哪种关键帧类型，可以定义该关键帧段的内插方法。 有三种不同类型的内插方法：线性、离散和曲线。  
  
### <a name="linear-interpolation"></a>线性内插  
 使用线性内插，动画将以段持续时间的固定速度进行播放。 例如，如果关键帧段从 0 过渡到 10，持续时间为 5 秒，则动画会在指定时间输出以下值：  
  
|时间|输出值|  
|----------|------------------|  
|0|0|  
|1|2|  
|2|4|  
|3|6|  
|4|8|  
|4.25|8.5|  
|4.5|9|  
|5|10|  
  
### <a name="discrete-interpolation"></a>离散内插  
 使用离散内插，动画函数将从一个值跳到下一个值，没有内插。 如果关键帧段从 0 过渡到 10，持续时间为 5 秒，则动画会在指定时间输出以下值：  
  
|时间|输出值|  
|----------|------------------|  
|0|0|  
|1|0|  
|2|0|  
|3|0|  
|4|0|  
|4.25|0|  
|4.5|0|  
|5|10|  
  
 注意动画在段持续时间恰好结束之前不会更改其输出值的方式。  
  
 曲线内插更为复杂。 相关内容将在下一节介绍。  
  
<a name="anim_spline"></a>   
### <a name="splined-interpolation"></a>曲线内插  
 曲线内插可用于达到更现实的计时效果。 由于动画通常用于模拟现实世界中出现的效果，因此开发人员可能需要精确地控制对象的加速和减速，并需要严格地对计时段进行操作。 通过自由绘制曲线关键帧，可以使用曲线内插进行动画处理。 利用其他关键帧，您可以指定<xref:System.Windows.Media.Animation.IKeyFrame.Value%2A>和<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>。 使用样条关键帧，您还指定<xref:System.Windows.Media.Animation.SplineDoubleKeyFrame.KeySpline%2A>。 下面的示例演示一个单个自由绘制曲线关键帧为<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>。 请注意<xref:System.Windows.Media.Animation.KeySpline>属性; 它就是自由绘制曲线关键帧不同于其他类型的关键帧。  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexample)]  
  
 一条三次方贝塞尔曲线由一个起点、一个终点和两个控制点定义。 <xref:System.Windows.Media.Animation.KeySpline>自由绘制曲线关键帧的属性定义从 (0，0) 延伸到 (1，1) 的贝塞尔曲线的两个控制点。 第一个控制点控制贝塞尔曲线前半部分的曲线因子，第二个控制点控制贝塞尔线段后半部分的曲线因子。 生成的曲线描述了该自由绘制曲线关键帧的变化率。 曲线陡度越大，关键帧更改其值的速度越快。 曲线趋于平缓时，关键帧更改其值的速度也趋于缓慢。  
  
 可以使用<xref:System.Windows.Media.Animation.KeySpline>，模拟下落的水滴或跳动的球，等的物理轨迹，或将其他"渐入"和"渐出"效果应用于运动动画。 对于用户交互效果（例如背景淡入/淡出或控制按钮弹跳等），可能要应用曲线内插，以便以特定方式提高或降低动画的变化率。  
  
 下面的示例指定<xref:System.Windows.Media.Animation.KeySpline>的 0，1 1，这会创建如下贝塞尔曲线，0。  
  
 ![贝塞尔曲线](./media/graphicsmm-keyspline-0-1-1-0.png "graphicsmm_keyspline_0_1_1_0")  
控制点为 (0.0, 1.0) 和 (1.0, 0.0) 的主曲线  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexample)]  
  
 此关键帧的动画处理在开始时快速进行，减速，然后再次加速，直到结束。  
  
 下面的示例指定<xref:System.Windows.Media.Animation.KeySpline>的 0.5,0.25 0.75,1.0，创建如下贝塞尔曲线。  
  
 ![贝塞尔曲线](./media/graphicsmm-keyspline-025-050-075-10.png "graphicsmm_keyspline_025_050_075_10")  
控制点为 (0.25, 0.5) 和 (0.75, 1.0) 的主曲线  
  
 [!code-xaml[keyframes_ovw_snippet#SingleSplineKeyFrameExampleInline3](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#singlesplinekeyframeexampleinline3)]  
  
 由于贝塞尔曲线的曲度变化幅度很小，因此该关键帧的动画处理速率几乎固定不变；只在接近结束时才开始减速。  
  
 下面的示例使用<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>矩形的位置进行动画处理。 因为<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>使用<xref:System.Windows.Media.Animation.SplineDoubleKeyFrame>对象，每个关键帧值之间的转换使用曲线内插。  
  
 [!code-xaml[keyframes_ovw_snippet#SplinedInterpolationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#splinedinterpolationexample)]  
  
 曲线内插可能很难理解；使用不同的设置进行体验有助于理解。 通过[主曲线动画示例](https://go.microsoft.com/fwlink/?LinkID=160011)，可以更改主曲线值，并查看由此所产生的动画结果。  
  
<a name="combininginterpolationmethods"></a>   
### <a name="combining-interpolation-methods"></a>组合内插方法  
 可在一个关键帧动画中使用具有不同内插类型的关键帧。 如果两个具有不同内插的关键帧动画彼此跟随，第二个关键帧的内插方法将用于创建从第一个值到第二个值的过渡。  
  
 在以下示例中，<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>创建该使用线性、 曲线和离散内插。  
  
 [!code-xaml[keyframes_ovw_snippet#ComboInterpolationExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/InterpolationMethodsExample.xaml#combointerpolationexample)]  
  
<a name="keytimes"></a>   
## <a name="more-about-duration-and-key-times"></a>有关持续时间和关键时间的更多信息  
 像其他动画关键帧动画具有<xref:System.Windows.Duration>属性。 除了指定动画的<xref:System.Windows.Duration>，您需要指定该持续时间的哪些部分提供给每个关键帧。 为此，描述<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>为每个动画的关键帧。 每个关键帧的<xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>指定该关键帧结束时。  
  
 <xref:System.Windows.Media.Animation.IKeyFrame.KeyTime%2A>属性未指定关键时间播放的时间长度。 关键帧的播放时长由关键帧的结束时间、前一个关键帧的结束时间以及动画的持续时间确定。 可能指定关键时间，为时间值，一个百分比，或者特殊值<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>或<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>。  
  
 下表描述了指定关键时间的不同方式。  
  
### <a name="timespan-values"></a>TimeSpan 值  
 可以使用<xref:System.TimeSpan>值，以指定<xref:System.Windows.Media.Animation.KeyTime>。 该值应大于或等于 0 并且小于或等于动画的持续时间。 以下示例演示一个持续时间为 10 秒钟、有四个关键帧（这些关键帧的关键时间指定为时间值）的动画。  
  
-   在前 3 秒钟内，第一个关键帧在基值和 100 之间进行动画处理，结束时间 = 0:0:03。  
  
-   第二个关键帧在 100 和 200 之间进行动画处理。 它在第一个关键帧结束后开始（开始时间 = 3 秒），播放 5 秒钟，结束时间 = 0:0:8。  
  
-   第三个关键帧在 200 和 500 之间进行动画处理。 它在第二个关键帧结束时开始（开始时间 = 8 秒），播放 1 秒钟，结束时间 = 0:0:9。  
  
-   第四个关键帧在 500 和 600 之间进行动画处理。 它在第三个关键帧结束时开始（开始时间 = 9 秒），播放 1 秒钟，结束时间 = 0:0:10。  
  
 [!code-xaml[keyframes_ovw_snippet#TimeSpanKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#timespankeytimeexample)]  
  
### <a name="percentage-values"></a>百分比值  
 百分比值指定关键帧的动画的百分比处结束<xref:System.Windows.Media.Animation.Timeline.Duration%2A>。 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，指定百分比作为 `%` 符号后的数字。 在代码中，您使用<xref:System.Windows.Media.Animation.KeyTime.FromPercent%2A>方法并将其传递<xref:System.Double>的百分比。 该值必须大于或等于 0 并且小于或等于 100%。 以下示例演示一个持续时间为 10 秒钟、有四个关键帧（这些关键帧的关键时间指定为百分比）的动画。  
  
-   在前 3 秒钟内，第一个关键帧将在基值和 100 之间进行动画处理，结束时间 = 0:0:3。  
  
-   第二个关键帧在 100 和 200 之间进行动画处理。 它在第一个关键帧结束后开始（开始时间 = 3 秒），播放 5 秒钟，结束时间 = 0:0:8 (0.8 * 10 = 8)。  
  
-   第三个关键帧在 200 和 500 之间进行动画处理。 它在第二个关键帧结束时开始（开始时间 = 8 秒），播放 1 秒钟，结束时间 = 0:0:9 (0.9 * 10 = 9)。  
  
-   第四个关键帧在 500 和 600 之间进行动画处理。 它在第三个关键帧结束时开始（开始时间 = 9 秒），播放 1 秒钟，结束时间 = 0:0:10 (1 * 10 = 10)。  
  
 [!code-xaml[keyframes_ovw_snippet#PercentageKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#percentagekeytimeexample)]  
  
### <a name="special-value-uniform"></a>特殊值 Uniform  
 使用<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>计时时所需占用同样的时间每个关键帧。  
  
 一个<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>关键时间划分的可用时间同样的关键帧，以确定每个关键帧的结束时间数。 下面的示例演示一个持续时间为 10 秒的动画和四个关键帧的关键时间指定为<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>。  
  
-   在前 2.5 秒钟内，第一个关键帧在基值和 100 之间进行动画处理，结束时间 = 0:0:2.5。  
  
-   第二个关键帧在 100 和 200 之间进行动画处理。 它在第一个关键帧结束后开始（开始时间 = 2.5 秒），播放大约 2.5 秒钟，结束时间 = 0:0:5。  
  
-   第三个关键帧在 200 和 500 之间进行动画处理。 它在第二个关键帧结束时开始（开始时间 = 5 秒），播放 2.5 秒钟，结束时间 = 0:0:7.5。  
  
-   第四个关键帧在 500 和 600 之间进行动画处理。 它在第二个关键帧结束时开始（开始时间 = 7.5 秒），播放 2.5 秒钟，结束时间 = 0:0:1。  
  
 [!code-xaml[keyframes_ovw_snippet#UniformKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#uniformkeytimeexample)]  
  
### <a name="special-value-paced"></a>特殊值 Paced  
 使用<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>计时时要进行动画处理的固定速度。  
  
 一个<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>关键时间来分配可用时间根据每个关键帧，以确定每个帧的持续时间的长度。  这样，动画的速度或速率将保持不变。  下面的示例演示一个持续时间为 10 秒的动画和三个关键帧的关键时间指定为<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>。  
  
 [!code-xaml[keyframes_ovw_snippet#PacedKeyTimeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_ovw_snippet/CS/KeyTimesExample.xaml#pacedkeytimeexample)]  
  
 请注意，如果最后一个关键帧的关键时间<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>或<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>，其解析的关键时间将设置为 100%。 如果多帧动画中的第一个关键帧为固定速度，其解析的关键时间将设置为 0。 （如果关键帧集合仅包含一个关键帧，并且是一个固定速度的关键帧，其解析的关键时间将设置为 100%。）  
  
 一个关键帧动画中的不同关键帧可使用不同的关键时间类型。  
  
<a name="combiningkeytimes"></a>   
## <a name="combining-key-times-out-of-order-key-frames"></a>组合关键时间，顺序紊乱的关键帧  
 可以使用关键帧具有不同<xref:System.Windows.Media.Animation.KeyTime>中同一个动画的值类型。 尽管建议以关键帧的实际播放顺序来添加关键帧，但此操作不是必需的。 动画和计时系统能够处理顺序紊乱的关键帧。 将忽略关键时间无效的关键帧。  
  
 下表描述了为关键帧动画的关键帧解析关键时间的过程。  
  
1.  解决<xref:System.TimeSpan><xref:System.Windows.Media.Animation.KeyTime>值。  
  
2.  确定动画的*总内插时间*，即关键帧动画完成向前迭代所需的全部时间。  
  
    1.  如果该动画<xref:System.Windows.Media.Animation.Timeline.Duration%2A>不是<xref:System.Windows.Duration.Automatic%2A>或<xref:System.Windows.Duration.Forever%2A>，总内插时间为动画的值<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性。  
  
    2.  否则，总内插时间是最大<xref:System.TimeSpan><xref:System.Windows.Media.Animation.KeyTime>指定其关键帧，如果存在任何值。  
  
    3.  否则，总内插时间为 1 秒。  
  
3.  使用总内插时间值来解决<xref:System.Windows.Media.Animation.KeyTimeType.Percent><xref:System.Windows.Media.Animation.KeyTime>值。  
  
4.  如果最后一个关键帧尚未在之前步骤中解析，则将解析该关键帧。 如果<xref:System.Windows.Media.Animation.KeyTime>的最后一个关键帧是<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>或<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>，其解析的时间将等于总内插时间。  
  
     如果<xref:System.Windows.Media.Animation.KeyTime>的第一个关键帧<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>和此动画具有多个关键帧，解决其<xref:System.Windows.Media.Animation.KeyTime>值为零; 如果只有一个关键帧并将其<xref:System.Windows.Media.Animation.KeyTime>值是<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>，被解析为总计内插时间，如前一步骤中所述。  
  
5.  解析其余<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A><xref:System.Windows.Media.Animation.KeyTime>值： 系统将每个提供的可用时间的相等份额。  在此过程中，无法解析<xref:System.Windows.Media.Animation.KeyTime.Paced%2A><xref:System.Windows.Media.Animation.KeyTime>值将临时视为<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A><xref:System.Windows.Media.Animation.KeyTime>值，并获得临时解析时间。  
  
6.  解决<xref:System.Windows.Media.Animation.KeyTime>的关键帧的值未指定关键时间使用声明距离它们最近解决的关键帧<xref:System.Windows.Media.Animation.KeyTime>值。  
  
7.  解析其余<xref:System.Windows.Media.Animation.KeyTime.Paced%2A><xref:System.Windows.Media.Animation.KeyTime>值。 <xref:System.Windows.Media.Animation.KeyTime.Paced%2A> <xref:System.Windows.Media.Animation.KeyTime> 使用<xref:System.Windows.Media.Animation.KeyTime>相邻的值的关键帧，以确定其解析的时间。  目的是确保动画速度在此关键帧的解析时间内保持固定不变。  
  
8.  即对关键帧的解析时间 （主键）、 顺序和声明 （辅助密钥） 的顺序进行排序，使用一个稳定排序根据解析关键帧<xref:System.Windows.Media.Animation.KeyTime>值。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Animation.KeyTime>
- <xref:System.Windows.Media.Animation.KeySpline>
- <xref:System.Windows.Media.Animation.Timeline>
- [主曲线动画示例](https://go.microsoft.com/fwlink/?LinkID=160011)
- [关键帧动画示例](https://go.microsoft.com/fwlink/?LinkID=160012)
- [动画概述](animation-overview.md)
- [演示图板概述](storyboards-overview.md)
- [关键帧操作说明主题](key-frame-animation-how-to-topics.md)
- [计时行为概述](timing-behaviors-overview.md)
