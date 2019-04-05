---
title: 动画提示和技巧
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- troubleshooting [WPF], animation
- animations [WPF], FillBehavior property
- troubleshooting animation [WPF]
- animating objects [WPF], troubleshooting
- animation tips and tricks [WPF]
- tips and tricks [WPF], animation
- performance troubleshooting [WPF], animation
- animations [WPF], use of system resources
ms.assetid: e467796b-d5d4-45a6-a108-8c5d7ff69a0f
ms.openlocfilehash: e8b2a6b5386ec33ad8aa5281d808bb7089149764
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57362430"
---
# <a name="animation-tips-and-tricks"></a>动画提示和技巧
使用中的动画时[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]，有一些提示和技巧，可使动画更好地执行，并避免挫折。  
  
<a name="generalissuessection"></a>   
## <a name="general-issues"></a>一般问题  
  
### <a name="animating-the-position-of-a-scroll-bar-or-slider-freezes-it"></a>对滚动条或滑块的位置进行动画处理将冻结它  
 如果滚动条或滑块使用的动画位置进行动画处理<xref:System.Windows.Media.Animation.FillBehavior>的<xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>（默认值），用户将不再能够移动滚动条或滑块。 这是因为，即使动画已结束，它仍然在重写目标属性的基值。 若要停止动画不再重写属性的当前值，将其删除，或为其赋予<xref:System.Windows.Media.Animation.FillBehavior>的<xref:System.Windows.Media.Animation.FillBehavior.Stop>。 有关详细信息和示例，请参阅[后设置该属性进行动画处理使用演示图板](how-to-set-a-property-after-animating-it-with-a-storyboard.md)。  
  
### <a name="animating-the-output-of-an-animation-has-no-effect"></a>对动画的输出进行动画处理没有效果  
 如果某个对象是另一个动画的输出，则无法对该对象进行动画处理。 例如，如果您使用<xref:System.Windows.Media.Animation.ObjectAnimationUsingKeyFrames>进行动画处理<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Rectangle>从<xref:System.Windows.Media.RadialGradientBrush>到<xref:System.Windows.Media.SolidColorBrush>，不能进行动画处理的任何属性<xref:System.Windows.Media.RadialGradientBrush>或<xref:System.Windows.Media.SolidColorBrush>。  
  
### <a name="cant-change-the-value-of-a-property-after-animating-it"></a>在对属性进行动画处理后无法更改该属性的值  
 在某些情况下，在对属性进行动画处理后，即使在动画结束后，看起来仍无法更改该属性的值。 这是因为即使动画已结束，它仍然在重写该属性的基值。 若要停止动画不再重写属性的当前值，将其删除，或为其赋予<xref:System.Windows.Media.Animation.FillBehavior>的<xref:System.Windows.Media.Animation.FillBehavior.Stop>。 有关详细信息和示例，请参阅[后设置该属性进行动画处理使用演示图板](how-to-set-a-property-after-animating-it-with-a-storyboard.md)。  
  
### <a name="changing-a-timeline-has-no-effect"></a>更改时间线没有效果  
 尽管大多数<xref:System.Windows.Media.Animation.Timeline>属性可进行动画处理，并且可数据绑定，更改活动的属性值<xref:System.Windows.Media.Animation.Timeline>似乎不起作用。 这是因为，当<xref:System.Windows.Media.Animation.Timeline>是开始，计时系统生成的副本<xref:System.Windows.Media.Animation.Timeline>并使用它来创建<xref:System.Windows.Media.Animation.Clock>对象。 修改原件对系统的副本没有影响。  
  
 有关<xref:System.Windows.Media.Animation.Timeline>以反映更改，它的时钟必须重新生成并用于替换以前创建的时钟。 时钟不会自动重新生成。 以下是应用时间线更改的几种方法：  
  
-   如果时间线是或属于<xref:System.Windows.Media.Animation.Storyboard>，你可以使其通过重新应用其情节提要使用反映更改<xref:System.Windows.Media.Animation.BeginStoryboard>或<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法。 这还会产生重新启动动画的附带影响。 在代码中，可以使用<xref:System.Windows.Media.Animation.Storyboard.Seek%2A>方法将情节提要回其之前的位置。  
  
-   如果您将动画应用于属性使用直接<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>方法中，调用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>再次方法并将其传递已修改的动画。  
  
-   如果要直接在时钟级别上工作，请创建并应用一组新的时钟，然后用它们替换之前生成的一组时钟。  
  
 有关时间线和时钟的详细信息，请参阅[动画和计时系统概述](animation-and-timing-system-overview.md)。  
  
### <a name="fillbehaviorstop-doesnt-work-as-expected"></a>FillBehavior.Stop 不按预期方式工作  
 有些时候设置时<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>属性设置为<xref:System.Windows.Media.Animation.FillBehavior.Stop>似乎不起作用，例如当一个动画"切换"到另一个因为它具有<xref:System.Windows.Media.Animation.BeginStoryboard.HandoffBehavior%2A>设置为<xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace>。  
  
 下面的示例创建<xref:System.Windows.Controls.Canvas>、 一个<xref:System.Windows.Shapes.Rectangle>和一个<xref:System.Windows.Media.TranslateTransform>。 <xref:System.Windows.Media.TranslateTransform>将对其进行动画处理，以移动<xref:System.Windows.Shapes.Rectangle>围绕<xref:System.Windows.Controls.Canvas>。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipAnimatedObject](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipanimatedobject)]  
  
 在本部分中的示例使用上述对象演示几种情况其中<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>属性可能预期的行为不符合。  
  
#### <a name="fillbehaviorstop-and-handoffbehavior-with-multiple-animations"></a>针对多个动画的 FillBehavior="Stop" 和 HandoffBehavior  
 有时，似乎动画会忽略其<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>时它替换为第二个动画的属性。 执行下面的示例创建两个<xref:System.Windows.Media.Animation.Storyboard>对象，并使用它们来进行动画处理相同<xref:System.Windows.Media.TranslateTransform>在前面的示例所示。  
  
 第一个<xref:System.Windows.Media.Animation.Storyboard>， `B1`，进行动画处理<xref:System.Windows.Media.TranslateTransform.X%2A>属性的<xref:System.Windows.Media.TranslateTransform>从 0 到 350，该矩形 350 像素向右移动。 当动画到达其持续时间的末尾并停止播放，<xref:System.Windows.Media.TranslateTransform.X%2A>属性会恢复为其原始值为 0。 因此，矩形向右移动 350 像素，然后跳回其原始位置。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB1Button](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb1button)]  
  
 第二个<xref:System.Windows.Media.Animation.Storyboard>， `B2`，还进行动画处理<xref:System.Windows.Media.TranslateTransform.X%2A>属性的相同<xref:System.Windows.Media.TranslateTransform>。 因为仅<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>在此动画属性<xref:System.Windows.Media.Animation.Storyboard>，则动画使用它进行动画处理的属性的当前值作为其起始值。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardB2Button](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardb2button)]  
  
 如果单击第二个按钮时第一个<xref:System.Windows.Media.Animation.Storyboard>是播放，可能会出现以下行为：  
  
1.  第一个情节提要结束，并将矩形送回其原始位置，因为该动画<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>的<xref:System.Windows.Media.Animation.FillBehavior.Stop>。  
  
2.  第二个情节提要生效，从当前位置（现在为 0）播放动画到 500。  
  
 **但情况并非如此。** 矩形没有跳回，而是继续向右移动。 这是因为第二个动画使用第一个动画的当前值作为其起始值，并从该值开始播放动画到 500。 当第二个动画替换第一个，因为<xref:System.Windows.Media.Animation.HandoffBehavior.SnapshotAndReplace><xref:System.Windows.Media.Animation.HandoffBehavior>使用，则<xref:System.Windows.Media.Animation.FillBehavior>第一个动画并不重要。  
  
#### <a name="fillbehavior-and-the-completed-event"></a>FillBehavior 和 Completed 事件  
 下一步的示例演示了另一个方案，其中<xref:System.Windows.Media.Animation.FillBehavior.Stop><xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>似乎不起作用。 同样，该示例使用演示图板进行动画处理<xref:System.Windows.Media.TranslateTransform.X%2A>属性的<xref:System.Windows.Media.TranslateTransform>从 0 到 350。 但是，这一次该示例会注册<xref:System.Windows.Media.Animation.Timeline.Completed>事件。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardCButton](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipstoryboardcbutton)]  
  
 <xref:System.Windows.Media.Animation.Timeline.Completed>事件处理程序将启动另一个<xref:System.Windows.Media.Animation.Storyboard>从其当前值为 500 的同一属性进行动画处理。  
  
 [!code-csharp[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml.cs#fillbehaviortipstoryboardc1completedhandler)]
 [!code-vb[AnimationTipsAndTricksSample_snip#FillBehaviorTipStoryboardC1CompletedHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/VisualBasic/FillBehaviorTip.xaml.vb#fillbehaviortipstoryboardc1completedhandler)]  
  
 下面是定义第二个标记<xref:System.Windows.Media.Animation.Storyboard>作为资源。  
  
 [!code-xaml[AnimationTipsAndTricksSample_snip#FillBehaviorTipResources](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimationTipsAndTricksSample_snip/CSharp/FillBehaviorTip.xaml#fillbehaviortipresources)]  
  
 运行时<xref:System.Windows.Media.Animation.Storyboard>，您所料<xref:System.Windows.Media.TranslateTransform.X%2A>的属性<xref:System.Windows.Media.TranslateTransform>进行动画处理从 0 到 350，然后还原成 0 它完成后 (因为它具有<xref:System.Windows.Media.Animation.FillBehavior>设置的<xref:System.Windows.Media.Animation.FillBehavior.Stop>)，并动态变化从 0 到 500。 相反，<xref:System.Windows.Media.TranslateTransform>之间进行动画处理从 0 到 350 再到 500。  
  
 这是因为依据的顺序[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]引发事件，而且除非该属性失效属性值已缓存，不是重新计算。 <xref:System.Windows.Media.Animation.Timeline.Completed>因为它由根时间线触发的第一次处理事件 (第一个<xref:System.Windows.Media.Animation.Storyboard>)。 在此期间，<xref:System.Windows.Media.TranslateTransform.X%2A>属性仍然返回其经过动画处理的值，因为它尚未失效。 第二个<xref:System.Windows.Media.Animation.Storyboard>使用缓存的值作为其起始值并开始播放动画。  
  
<a name="performancesection"></a>   
## <a name="performance"></a>性能  
  
### <a name="animations-continue-to-run-after-navigating-away-from-a-page"></a>在导航离开页面后动画继续运行  
 导航离开<xref:System.Windows.Controls.Page>，其中包含正在运行的动画，这些动画将继续播放，直到<xref:System.Windows.Controls.Page>进行垃圾回收。 根据正在使用的导航系统，导航离开的页面可能无限期地保留在内存中，在此期间始终通过动画消耗资源。 当页面包含不断运行的（“氛围”）动画时，这一点最明显。  
  
 出于此原因，它是一个好办法使用<xref:System.Windows.FrameworkElement.Unloaded>事件删除动画时导航离开页面。  
  
 删除动画有多种不同的方法。 可以使用以下方法删除属于的动画<xref:System.Windows.Media.Animation.Storyboard>。  
  
-   若要删除<xref:System.Windows.Media.Animation.Storyboard>开始使用事件触发器，请参阅[如何：删除情节提要](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms749412(v=vs.90))。  
  
-   若要使用代码来删除<xref:System.Windows.Media.Animation.Storyboard>，请参阅<xref:System.Windows.Media.Animation.Storyboard.Remove%2A>方法。  
  
 无论动画如何启动，都可以使用下一个技术。  
  
-   若要从特定的属性中删除动画，请使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29>方法。 指定要进行动画处理的第一个参数的属性和`null`为第二个。 这将从该属性中删除所有动画时钟。  
  
 有关属性进行动画处理的不同方式的详细信息，请参阅[属性动画技术概述](property-animation-techniques-overview.md)。  
  
### <a name="using-the-compose-handoffbehavior-consumes-system-resources"></a>使用组合 HandoffBehavior 会消耗系统资源  
 当应用<xref:System.Windows.Media.Animation.Storyboard>， <xref:System.Windows.Media.Animation.AnimationTimeline>，或<xref:System.Windows.Media.Animation.AnimationClock>属性使用<xref:System.Windows.Media.Animation.HandoffBehavior.Compose> <xref:System.Windows.Media.Animation.HandoffBehavior>，则所有<xref:System.Windows.Media.Animation.Clock>之前与该属性相关联的对象继续消耗系统资源时，计时系统将不会自动删除这些时钟。  
  
 若要避免出现性能问题时应用大量时钟使用<xref:System.Windows.Media.Animation.HandoffBehavior.Compose>，它们完成后，您应该从属性的基值删除组合时钟。 删除时钟有多种方法。  
  
-   若要从属性中删除所有时钟，请使用<xref:System.Windows.Media.Animation.Animatable.ApplyAnimationClock%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationClock%29>或<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%28System.Windows.DependencyProperty%2CSystem.Windows.Media.Animation.AnimationTimeline%29>经过动画处理的对象的方法。 指定要进行动画处理的第一个参数的属性和`null`为第二个。 这将从该属性中删除所有动画时钟。  
  
-   若要删除特定<xref:System.Windows.Media.Animation.AnimationClock>从列表中的时钟，使用<xref:System.Windows.Media.Animation.Clock.Controller%2A>属性<xref:System.Windows.Media.Animation.AnimationClock>检索<xref:System.Windows.Media.Animation.ClockController>，然后调用<xref:System.Windows.Media.Animation.ClockController.Remove%2A>方法<xref:System.Windows.Media.Animation.ClockController>。 这通常是<xref:System.Windows.Media.Animation.Clock.Completed>时钟的事件处理程序。 请注意，只有根时钟可以受<xref:System.Windows.Media.Animation.ClockController>;<xref:System.Windows.Media.Animation.Clock.Controller%2A>子时钟的属性将返回`null`。 另请注意，<xref:System.Windows.Media.Animation.Clock.Completed>如果时钟的有效持续时间将永远不会调用事件。  在这种情况下，用户将需要确定何时调用<xref:System.Windows.Media.Animation.ClockController.Remove%2A>。  
  
 此动画问题主要出现在生存期较长的对象上。  当对某个对象进行垃圾回收时，它的时钟也会断开连接并进行垃圾回收。  
  
 有关时钟对象的详细信息，请参阅[动画和计时系统概述](animation-and-timing-system-overview.md)。  
  
## <a name="see-also"></a>请参阅
- [动画概述](animation-overview.md)
