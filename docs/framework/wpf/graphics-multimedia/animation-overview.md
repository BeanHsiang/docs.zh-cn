---
title: 动画概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboards [WPF], animations
- animations [WPF], overview
ms.assetid: bd9ce563-725d-4385-87c9-d7ee38cf79ea
ms.openlocfilehash: cf95abc6780b1182582e567f78783388f1d377cb
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373733"
---
# <a name="animation-overview"></a>动画概述
<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了一组强大的图形和布局功能，使您能够创建极具吸引力的用户界面和有吸引力的文档。 动画不仅可以使引起注意的用户界面更加引人注目，还可以使其更加便于使用。 只需对背景色进行动画处理或应用动画的<xref:System.Windows.Media.Transform>，可以创建出生动的屏幕转换，也可以提供有帮助的视觉提示。  
  
 本概述介绍了[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画和计时系统。 它主要关注的动画[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]使用演示图板的对象。  

<a name="introducinganimations"></a>   
## <a name="introducing-animations"></a>动画简介  
 动画是快速循环播放一系列图像（其中每个图像与下一个图像略微不同）给人造成的一种幻觉。 大脑感觉这组图像是一个变化的场景。 在电影中，摄像机每秒钟拍摄许多照片（帧），便可使人形成这种幻觉。 用投影仪播放这些帧时，观众便可以看电影了。  
  
 计算机上的动画与此类似。 例如，使一个矩形图形逐渐从视野中消失的程序可能按以下方式工作。  
  
-   程序创建一个计时器。  
  
-   程序按照设定的时间间隔检查计时器以查看经历了多长时间。  
  
-   程序每次检查计时器时，它将根据经历的时间来计算矩形的当前不透明度值。  
  
-   然后，程序用新值更新矩形并重画此矩形。  
  
 早于[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)]开发人员必须创建和管理其自己的计时系统或使用特殊的自定义库。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包括通过托管代码公开的高效计时系统和[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]和的紧密地集成到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]框架。 通过使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 动画，可以轻松地对控件和其他图形对象进行动画处理。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可以高效地处理管理计时系统和重绘屏幕的所有后台任务。 它提供了计时类，使用户能够重点关注要创造的效果，而非实现这些效果的机制。 此外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 通过公开动画基类（你使用的类可以继承这些类）可以轻松创建自己的动画，这样便可以制作自定义动画。 这些自定义动画获得了标准动画类的许多性能优点。  
  
<a name="thewpftimingsystem"></a>   
## <a name="wpf-property-animation-system"></a>WPF 属性动画系统  
 如果您了解关于计时系统的一些重要概念[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画可以是易于使用。 最重要是，在[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，通过将动画应用于其各个属性动态显示对象。 例如，若要使框架元素增大，进行动画处理其<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性。 若要使从视图淡入的对象，动画处理其<xref:System.Windows.UIElement.Opacity%2A>属性。  
  
 若要使属性具有动画功能，属性必须满足以下三个要求：  
  
-   它必须是依赖属性。  
  
-   它必须属于继承的类<xref:System.Windows.DependencyObject>并实现<xref:System.Windows.Media.Animation.IAnimatable>接口。  
  
-   必须存在可用的兼容动画类型。 (如果[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]未提供，可以创建你自己。 请参阅[自定义动画概述](custom-animations-overview.md)。)  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 包含具有的许多对象<xref:System.Windows.Media.Animation.IAnimatable>属性。 控件，如<xref:System.Windows.Controls.Button>并<xref:System.Windows.Controls.TabControl>，以及<xref:System.Windows.Controls.Panel>并<xref:System.Windows.Shapes.Shape>对象继承自<xref:System.Windows.DependencyObject>。 其中大多数属性都是依赖属性。  
  
 几乎可以在任何地方使用动画，包括在样式和控件模板中使用。 动画未必可见；如果不属于用户界面的对象满足本部分中所述的条件，则可以对其进行动画处理。  
  
<a name="storyboardwalkthrough"></a>   
## <a name="example-make-an-element-fade-in-and-out-of-view"></a>示例:使元素淡入淡出和移出视图  
 此示例演示如何使用[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画进行动画处理的依赖项属性的值。 它使用<xref:System.Windows.Media.Animation.DoubleAnimation>，这是一种生成的动画<xref:System.Double>值进行动画处理<xref:System.Windows.UIElement.Opacity%2A>属性的<xref:System.Windows.Shapes.Rectangle>。 因此，<xref:System.Windows.Shapes.Rectangle>淡入淡出视图。  
  
 该示例的第一部分创建<xref:System.Windows.Shapes.Rectangle>元素。 遵循的步骤说明如何创建动画，并将其应用于矩形的<xref:System.Windows.UIElement.Opacity%2A>属性。
  
 以下示例演示如何创建<xref:System.Windows.Shapes.Rectangle>中的元素<xref:System.Windows.Controls.StackPanel>在 XAML 中。  
  
 [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_1)]  
  
 以下示例演示如何创建<xref:System.Windows.Shapes.Rectangle>中的元素<xref:System.Windows.Controls.StackPanel>在代码中。  
  
 [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_1)]
 [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_1)]  
  
<a name="opacity_animation_step1"></a>   
### <a name="part-1-create-a-doubleanimation"></a>第 1 部分：创建 DoubleAnimation  
 若要使淡入和移出视图元素的一种方法是要进行动画处理其<xref:System.Windows.UIElement.Opacity%2A>属性。 因为<xref:System.Windows.UIElement.Opacity%2A>属性属于类型<xref:System.Double>，需要生成双精度值的动画。 一个<xref:System.Windows.Media.Animation.DoubleAnimation>是这样的一个动画。 一个<xref:System.Windows.Media.Animation.DoubleAnimation>创建两个双精度值之间的转换。 若要指定其起始值，请设置其<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性。 若要指定其终止值，请设置其<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性。  
  
1.  不透明度值`1.0`使对象完全不透明，且不透明度值为`0.0`使完全不可见。 可以从动画过渡`1.0`到`0.0`将其<xref:System.Windows.Media.Animation.DoubleAnimation.From%2A>属性设置为`1.0`并将其<xref:System.Windows.Media.Animation.DoubleAnimation.To%2A>属性设置为`0.0`。 以下示例演示如何创建<xref:System.Windows.Media.Animation.DoubleAnimation>在 XAML 中。  
  
     [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_2)]  
  
     以下示例演示如何创建<xref:System.Windows.Media.Animation.DoubleAnimation>在代码中。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_2)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_2)]  
  
2.  接下来，必须指定<xref:System.Windows.Media.Animation.Timeline.Duration%2A>。 <xref:System.Windows.Media.Animation.Timeline.Duration%2A>动画的指定从其起始值转到其目标值所需的时间长度。 以下示例演示如何设置<xref:System.Windows.Media.Animation.Timeline.Duration%2A>为 XAML 中的五秒。  
  
     [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_3)]  
  
     以下示例演示如何设置<xref:System.Windows.Media.Animation.Timeline.Duration%2A>到代码中的五秒。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_3)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_3)]  
  
3.  上面的代码显示从转换的动画`1.0`到`0.0`，这将导致目标元素从完全不透明逐渐转变为完全不可见。 若要使元素后再逐渐回到视野，设置<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>到动画属性`true`。 若要使动画无限期地重复，设置其<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>属性设置为<xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>。以下示例演示如何设置<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>和<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>XAML 中的属性。  
  
     [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_4)]  
  
     以下示例演示如何设置<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>和<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>代码中的属性。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Class1.cs#rectangleopacityfadeexamplecode_4)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/Class1.vb#rectangleopacityfadeexamplecode_4)]  
  
<a name="opacity_animation_step2"></a>   
### <a name="part-2-create-a-storyboard"></a>第 2 部分：创建情节提要  
 若要向对象应用动画，您创建<xref:System.Windows.Media.Animation.Storyboard>并用<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>和<xref:System.Windows.Media.Animation.Storyboard.TargetProperty>附加属性指定的对象和属性进行动画处理。  
  
1.  创建<xref:System.Windows.Media.Animation.Storyboard>和将动画添加为子项。 以下示例演示如何创建<xref:System.Windows.Media.Animation.Storyboard>在 XAML 中。  
  
     [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_5](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_5)]    
  
     若要创建<xref:System.Windows.Media.Animation.Storyboard>在代码中，声明<xref:System.Windows.Media.Animation.Storyboard>在类级别变量。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_100)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_100)]  
  
     然后初始化<xref:System.Windows.Media.Animation.Storyboard>和将动画添加为子项。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_101)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_101)]  
  
2.  <xref:System.Windows.Media.Animation.Storyboard>必须知道应用动画的位置。 使用<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType>附加属性指定要进行动画处理的对象。 以下示例演示如何设置的目标名称<xref:System.Windows.Media.Animation.DoubleAnimation>到`MyRectangle`在 XAML 中。  
  
     [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_6](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_6)]  
  
     以下示例演示如何设置的目标名称<xref:System.Windows.Media.Animation.DoubleAnimation>到`MyRectangle`在代码中。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_102)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_102)]  
  
3.  使用<xref:System.Windows.Media.Animation.Storyboard.TargetProperty>附加属性指定要进行动画处理的属性。 下面演示了如何将动画配置为目标<xref:System.Windows.UIElement.Opacity%2A>属性的<xref:System.Windows.Shapes.Rectangle>在 XAML 中。
  
     [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml_7](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/Window1.xaml#rectangleopacityfadeexamplexaml_7)]  
  
     下面演示了如何将动画配置为目标<xref:System.Windows.UIElement.Opacity%2A>属性的<xref:System.Windows.Shapes.Rectangle>在代码中。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_103)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_103)]  
  
 有关详细信息<xref:System.Windows.Media.Animation.Storyboard.TargetProperty>语法和其他示例，请参阅[演示图板概述](storyboards-overview.md)。  
  
<a name="opacity_animation_step3"></a>   
### <a name="part-3-xaml-associate-the-storyboard-with-a-trigger"></a>第 3 (XAML) 部分：将演示图板与触发器关联  
 应用和启动的最简单办法<xref:System.Windows.Media.Animation.Storyboard>在[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]是使用事件触发器。 本部分演示如何将相关联<xref:System.Windows.Media.Animation.Storyboard>与 XAML 中的触发器。  
  
1.  创建<xref:System.Windows.Media.Animation.BeginStoryboard>对象，并将你的情节提要与它相关联。 一个<xref:System.Windows.Media.Animation.BeginStoryboard>是一种<xref:System.Windows.TriggerAction>应用和启动<xref:System.Windows.Media.Animation.Storyboard>。  
  
     [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_3](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_3)]  
  
2.  创建<xref:System.Windows.EventTrigger>并添加<xref:System.Windows.Media.Animation.BeginStoryboard>到其<xref:System.Windows.EventTrigger.Actions%2A>集合。 设置<xref:System.Windows.EventTrigger.RoutedEvent%2A>的属性<xref:System.Windows.EventTrigger>到想要启动的路由事件<xref:System.Windows.Media.Animation.Storyboard>。 (有关路由事件的详细信息，请参阅[路由事件概述](../advanced/routed-events-overview.md)。)  
  
     [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_2](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_2)]  
  
3.  添加<xref:System.Windows.EventTrigger>到<xref:System.Windows.FrameworkElement.Triggers%2A>矩形的集合。  
  
     [!code-xaml[animation_ovws_snippet#RectangleOpacityFadeExampleInline_1](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/RectangleOpacityFadeExample.xaml#rectangleopacityfadeexampleinline_1)]  
  
<a name="opacity_animation_step3code"></a>   
### <a name="part-3-code-associate-the-storyboard-with-an-event-handler"></a>第 3 （代码） 部分：将情节提要与事件处理程序相关联  
 应用和启动的最简单办法<xref:System.Windows.Media.Animation.Storyboard>在代码中是使用事件处理程序。 本部分演示如何将相关联<xref:System.Windows.Media.Animation.Storyboard>与代码中的事件处理程序。  
  
1.  注册<xref:System.Windows.FrameworkElement.Loaded>矩形的事件。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_104)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_104)]  
  
2.  声明事件处理程序。 在事件处理程序，使用<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法来应用演示图板。  
  
     [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode_105)]
     [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode_105](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode_105)]  
  
### <a name="complete-example"></a>完整的示例  
 下面演示了如何创建逐渐进入视野并从 XAML 中逐渐消失的矩形。  
  
 [!code-xaml[animation_ovws2#RectangleOpacityFadeExampleXaml](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml#rectangleopacityfadeexamplexaml)]  
  
 下面演示了如何在代码中创建逐渐进入视野并从视野中逐渐消失的矩形。  
  
 [!code-csharp[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws2/CSharp/MainWindow.xaml.cs#rectangleopacityfadeexamplecode)]
 [!code-vb[animation_ovws2#RectangleOpacityFadeExampleCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws2/VisualBasic/MainWindow.xaml.vb#rectangleopacityfadeexamplecode)]  
  
<a name="animationtypes"></a>   
## <a name="animation-types"></a>动画类型  
 由于动画生成属性值，因此不同的属性类型具有不同的动画类型。 若要对采用的属性进行动画处理<xref:System.Double>，如<xref:System.Windows.FrameworkElement.Width%2A>属性的元素，使用生成的动画，<xref:System.Double>值。 若要对采用的属性进行动画处理<xref:System.Windows.Point>，使用生成的动画，<xref:System.Windows.Point>值，等等。 由于存在许多不同的属性类型，有一些动画类中的<xref:System.Windows.Media.Animation>命名空间。 幸运的是，它们都遵循严格的命名约定，因此可以轻松地区分它们：  
  
-   \<*类型*> 动画  
  
     这些动画称为“From/To/By”或“基本”动画，它们在起始值和目标值之间进行动画处理，或者通过将偏移量值与其起始值相加来进行动画处理。  
  
    -   若要指定起始值，请设置动画的“From”属性。  
  
    -   若要指定终止值，请设置动画的“To”属性。  
  
    -   若要指定偏移量值，请设置动画的“By”属性。  
  
     此概述中的示例使用这些动画，因为这些动画使用起来最简单。 From/To/By 动画 From/To/By 动画概述中详细介绍。  
  
-   \<*Type*>AnimationUsingKeyFrames  
  
     关键帧动画的功能比“From/To/By”动画的功能更强大，因为可以指定任意多个目标值，甚至可以控制它们的插值方法。 某些类型只能用关键帧动画进行动画处理。 中详细描述了关键帧动画[关键帧动画概述](key-frame-animations-overview.md)。  
  
-   \<*Type*>AnimationUsingPath  
  
     路径动画支持使用几何路径来生成动画值。  
  
-   \<*Type*>AnimationBase  
  
     抽象类在实现时进行动画处理\<*类型*> 值。 此类用作类的基类\<*类型*> 动画并\<*类型*> AnimationUsingKeyFrames 类。 只有在想要创建自己的自定义动画时，才需要直接处理这些类。 否则，请使用\<*类型*> 动画或关键帧\<*类型*> 动画。  
  
 在大多数情况下，你将想要使用\<*类型*> 动画类，如<xref:System.Windows.Media.Animation.DoubleAnimation>和<xref:System.Windows.Media.Animation.ColorAnimation>。  
  
 下表显示了一些常用动画类型以及一些与这些类型一起使用的属性。  
  
|属性类型|对应的基本 (From/To/By) 动画|对应的关键帧动画|对应的路径动画|用法示例|  
|-------------------|----------------------------------------------------|---------------------------------------|----------------------------------|-------------------|  
|<xref:System.Windows.Media.Color>|<xref:System.Windows.Media.Animation.ColorAnimation>|<xref:System.Windows.Media.Animation.ColorAnimationUsingKeyFrames>|无|进行动画处理<xref:System.Windows.Media.SolidColorBrush.Color%2A>的<xref:System.Windows.Media.SolidColorBrush>或<xref:System.Windows.Media.GradientStop>。|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimation>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|进行动画处理<xref:System.Windows.FrameworkElement.Width%2A>的<xref:System.Windows.Controls.DockPanel>或<xref:System.Windows.FrameworkElement.Height%2A>的<xref:System.Windows.Controls.Button>。|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimation>|<xref:System.Windows.Media.Animation.PointAnimationUsingKeyFrames>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|进行动画处理<xref:System.Windows.Media.EllipseGeometry.Center%2A>位置<xref:System.Windows.Media.EllipseGeometry>。|  
|<xref:System.String>|无|<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>|无|进行动画处理<xref:System.Windows.Controls.TextBlock.Text%2A>的<xref:System.Windows.Controls.TextBlock>或<xref:System.Windows.Controls.ContentControl.Content%2A>的<xref:System.Windows.Controls.Button>。|  
  
<a name="animationsaretimelines"></a>   
### <a name="animations-are-timelines"></a>动画是时间线  
 所有动画类型均都继承自<xref:System.Windows.Media.Animation.Timeline>类; 因此，所有动画都是专用的类型的时间线。 一个<xref:System.Windows.Media.Animation.Timeline>定义一个时间段。 您可以指定*计时行为*的时间线： 其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>，它是重复，甚至快时间走得多少次。  
  
 因为动画是<xref:System.Windows.Media.Animation.Timeline>，它还表示时间段。 动画还会计算输出值变为运行其指定的时间段 (或<xref:System.Windows.Media.Animation.Timeline.Duration%2A>)。 在运行或“播放”动画时，动画将更新与其关联的属性。  
  
 这三个常用的计时属性<xref:System.Windows.Media.Animation.Timeline.Duration%2A>， <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>，和<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>。  
  
#### <a name="the-duration-property"></a>Duration 属性  
 如前文所述，时间线表示时间段。 该时间段的长度由<xref:System.Windows.Media.Animation.Timeline.Duration%2A>时间线，通常通过使用指定的<xref:System.Windows.Duration.TimeSpan%2A>值。 当时间线达到其持续时间的终点时，表示时间线完成了一次迭代。  
  
 动画使用其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性来确定其当前值。 如果未指定<xref:System.Windows.Media.Animation.Timeline.Duration%2A>值的动画，它使用 1 秒，这是默认值。  
  
 下面的语法演示的简化的版本[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]特性语法<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性。  
  
*小时* `:` *分钟* `:` *秒*
  
 下表显示了几个<xref:System.Windows.Duration>设置及其所得的值。  
  
|设置|所得值|  
|-------------|---------------------|  
|0:0:5.5|5.5 秒。|  
|0:30:5.5|30 分 5.5 秒。|  
|1:30:5.5|1 小时 30 分 5.5 秒。|  
  
 指定的一种方法<xref:System.Windows.Duration>代码中是使用<xref:System.TimeSpan.FromSeconds%2A>方法来创建<xref:System.TimeSpan>，然后，声明一个新<xref:System.Windows.Duration>结构在使用该<xref:System.TimeSpan>。  
  
 有关详细信息<xref:System.Windows.Duration>值和完整[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]语法，请参阅<xref:System.Windows.Duration>结构。  
  
#### <a name="autoreverse"></a>AutoReverse  
 <xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>属性指定时间线的向后播放到达结束后其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>。 如果此动画属性设置为`true`，动画反转到达结束后其<xref:System.Windows.Media.Animation.Timeline.Duration%2A>、 播放从其终止值回其起始值。 默认情况下，此属性是`false`。  
  
#### <a name="repeatbehavior"></a>RepeatBehavior  
 <xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>属性指定时间线播放的次数。 默认情况下，时间线具有的迭代次数为`1.0`，即播放一次，根本不进行重复。  
  
 有关这些属性和其他工具的详细信息，请参阅[计时行为概述](timing-behaviors-overview.md)。  
  
<a name="applyanimationstoproperty"></a>   
## <a name="applying-an-animation-to-a-property"></a>对属性应用动画  
 前面部分介绍了动画的不同类型及其计时属性。 本部分演示如何对要进行动画处理的属性应用动画。 <xref:System.Windows.Media.Animation.Storyboard> 对象提供对属性应用动画的一种方法。 一个<xref:System.Windows.Media.Animation.Storyboard>是*容器时间线*，提供它所包含的动画的目标信息。  
  
### <a name="targeting-objects-and-properties"></a>以对象和属性为目标  
 <xref:System.Windows.Media.Animation.Storyboard>类提供了<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>和<xref:System.Windows.Media.Animation.Storyboard.TargetProperty>附加属性。 通过在动画上设置这些属性，告诉动画对哪些内容进行动画处理。 但是，通常必须为对象提供一个名称，动画才能以该对象作为目标。  
  
 分配将名称传递给<xref:System.Windows.FrameworkElement>不同于分配将名称传递给<xref:System.Windows.Freezable>对象。 大多数控件和面板是框架元素；而大多数纯图形对象（如画笔、转换和几何图形）是 Freezable 对象。 如果您不确定某个类型是<xref:System.Windows.FrameworkElement>或<xref:System.Windows.Freezable>，请参阅**继承层次结构**参考文档的部分。  
  
-   若要使<xref:System.Windows.FrameworkElement>成为动画目标，您为其提供一个名称通过设置其<xref:System.Windows.FrameworkElement.Name%2A>属性。 在代码中，您必须使用<xref:System.Windows.FrameworkElement.RegisterName%2A>方法以向其所属的页面注册的元素名称。  
  
-   若要使<xref:System.Windows.Freezable>对象中的动画目标[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，则使用[X:name 指令](../../xaml-services/x-name-directive.md)以将其分配一个名称。 在代码中，您只需使用<xref:System.Windows.FrameworkElement.RegisterName%2A>方法以向其所属的页面注册该对象。  
  
 以下各节提供的命名中的元素示例[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]和代码。 有关命名和设定目标的更多详细信息，请参阅[情节提要概述](storyboards-overview.md)。  
  
### <a name="applying-and-starting-storyboards"></a>应用和启动演示图板  
 若要在启动情节提要[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，将其与<xref:System.Windows.EventTrigger>。 <xref:System.Windows.EventTrigger>是一个对象，描述当发生指定的事件时要执行的操作。 其中一个操作可以是<xref:System.Windows.Media.Animation.BeginStoryboard>操作，你用于启动你的情节提要。 事件触发器与事件处理程序的概念类似，因为通过它们可以指定应用程序响应特定事件的方式。 事件触发器可以与不同的事件处理程序中详细介绍了[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]; 不不需要任何其他代码。  
  
 若要启动<xref:System.Windows.Media.Animation.Storyboard>在代码中，可以使用<xref:System.Windows.EventTrigger>或使用<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法的<xref:System.Windows.Media.Animation.Storyboard>类。  
  
<a name="controllingstoryboards"></a>   
## <a name="interactively-control-a-storyboard"></a>以交互方式控制演示图板  
 前面的示例介绍了如何启动<xref:System.Windows.Media.Animation.Storyboard>事件的发生时间。 您可以采用交互方式控制<xref:System.Windows.Media.Animation.Storyboard>启动后对它： 可以暂停、 恢复、 停止、 转到其填充期、 搜索和删除<xref:System.Windows.Media.Animation.Storyboard>。 有关详细信息和示例，演示如何以交互方式控制<xref:System.Windows.Media.Animation.Storyboard>，请参阅[演示图板概述](storyboards-overview.md)。  
  
<a name="fillbehaviorsection"></a>   
## <a name="what-happens-after-an-animation-ends"></a>动画结束后，会发生什么情况？  
 <xref:System.Windows.Media.Animation.FillBehavior>属性指定时间线结束时的行为方式。 默认情况下，时间线开始<xref:System.Windows.Media.Animation.ClockState.Filling>结束的时候。 是的动画<xref:System.Windows.Media.Animation.ClockState.Filling>保持其最终输出值。  
  
 <xref:System.Windows.Media.Animation.DoubleAnimation>上一示例中不会终止，因为其<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>属性设置为<xref:System.Windows.Media.Animation.RepeatBehavior.Forever%2A>。 下面的示例使用类似的动画对矩形进行动画处理。 与上述示例中，不同<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>和<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>此动画的属性保留为其默认值。 因此，动画运行五秒钟使其不透明度值从 1 转变成 0，然后停止。  
  
 [!code-xaml[animation_ovws_snippet#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snippet/CS/FillBehaviorExample.xaml#fillbehaviorexamplerectangleinline)]  
  
 [!code-csharp[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/FillBehaviorExample.cs#fillbehaviorexamplerectangleinline)]
 [!code-vb[animation_ovws_procedural_snip#FillBehaviorExampleRectangleInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/fillbehaviorexample.vb#fillbehaviorexamplerectangleinline)]  
  
 因为其<xref:System.Windows.Media.Animation.Timeline.FillBehavior%2A>未发生变化，其默认值，即<xref:System.Windows.Media.Animation.FillBehavior.HoldEnd>，动画将保持最终值为 0，结束时。 因此，<xref:System.Windows.UIElement.Opacity%2A>矩形仍然为动画之后的 0 的结束。 如果您设置<xref:System.Windows.UIElement.Opacity%2A>的矩形与另一个值，你的代码似乎不起作用，因为动画仍将影响<xref:System.Windows.UIElement.Opacity%2A>属性。  
  
 若要重新获得的代码中的动画属性控制权的一种方法是使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>方法并指定为 null<xref:System.Windows.Media.Animation.AnimationTimeline>参数。 有关详细信息和示例，请参阅[后设置该属性进行动画处理使用演示图板](how-to-set-a-property-after-animating-it-with-a-storyboard.md)。  
  
 请注意，虽然设置属性值不起<xref:System.Windows.Media.Animation.ClockState.Active>或<xref:System.Windows.Media.Animation.ClockState.Filling>动画似乎不起作用，属性值确实更改。 有关详细信息，请参阅[动画和计时系统概述](animation-and-timing-system-overview.md)。  
  
<a name="databindingAndAnimatingAnimationsSection"></a>   
## <a name="data-binding-and-animating-animations"></a>对动画进行数据绑定和动画处理  
 大多数动画属性可以是数据绑定或动画处理;例如，您可以进行动画处理<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性的<xref:System.Windows.Media.Animation.DoubleAnimation>。 但是，由于计时系统工作方式的缘故，进行了数据绑定和动画处理的动画的行为与其他进行了数据绑定和动画处理的对象不同。 若要了解它们的行为，请了解对属性应用动画的意义，这将十分有用。  
  
 介绍了如何进行动画处理的上一节中的示例，请参阅<xref:System.Windows.UIElement.Opacity%2A>的矩形。 加载上一示例中的矩形时，它的事件触发器适用<xref:System.Windows.Media.Animation.Storyboard>。 计时系统会创建一份<xref:System.Windows.Media.Animation.Storyboard>及其动画。 这些副本均已冻结 （使只读的） 和<xref:System.Windows.Media.Animation.Clock>根据它们来创建对象。 这些时钟将执行对目标属性进行动画处理的实际工作。  
  
 计时系统创建时钟<xref:System.Windows.Media.Animation.DoubleAnimation>并将其应用到的对象和由指定的属性<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>并<xref:System.Windows.Media.Animation.Storyboard.TargetProperty>的<xref:System.Windows.Media.Animation.DoubleAnimation>。 在这种情况下，计时系统应用到时钟<xref:System.Windows.UIElement.Opacity%2A>名为"MyRectangle。"的对象属性  
  
 尽管还为创建一个时钟<xref:System.Windows.Media.Animation.Storyboard>，时钟不应用于任何属性。 其目的是控制其子时钟，为创建的时钟<xref:System.Windows.Media.Animation.DoubleAnimation>。  
  
 若要使动画反映数据绑定或动画更改，必须重新生成时钟。 时钟不会自动重新生成。 若要使动画反映更改，重新通过应用其情节提要<xref:System.Windows.Media.Animation.BeginStoryboard>或<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法。 当使用其中一种方法时，动画将重新启动。 在代码中，可以使用<xref:System.Windows.Media.Animation.Storyboard.Seek%2A>方法将演示图板移回其之前的位置。  
  
 有关数据的示例绑定动画，请参见[密钥样条动画示例](https://go.microsoft.com/fwlink/?LinkID=160011)。 有关动画和计时系统的工作原理的详细信息，请参阅[动画和计时系统概述](animation-and-timing-system-overview.md)。  
  
<a name="otherWaysToAnimateSection"></a>   
## <a name="other-ways-to-animate"></a>其他动画处理方式  
 此概述中的示例演示如何使用演示图板进行动画处理。 如果使用代码，可以采用一些其他方法进行动画处理。 有关详细信息，请参阅[属性动画技术概述](property-animation-techniques-overview.md)。  
  
<a name="animation_samples"></a>   
## <a name="animation-samples"></a>动画示例  
 以下示例有助于开始向应用程序添加动画。  
  
-   [From、To 和 By 动画目标值示例](https://go.microsoft.com/fwlink/?LinkID=159988)  
  
     演示不同的 From/To/By 设置。  
  
-   [动画计时行为示例](https://go.microsoft.com/fwlink/?LinkID=159970)  
  
     演示可控制动画计时行为的不同方法。 此示例还演示如何对动画的目标值进行数据绑定。  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>相关主题  
  
|标题|描述|  
|-----------|-----------------|  
|[动画和计时系统概述](animation-and-timing-system-overview.md)|描述计时系统如何使用<xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>类，允许你创建动画。|  
|[动画提示和技巧](animation-tips-and-tricks.md)|列出用于解决与动画有关的问题（如性能）的有用提示。|  
|[自定义动画概述](custom-animations-overview.md)|描述如何使用关键帧、动画类或逐帧回叫来扩展动画系统。|  
|From/To/By 动画概述|描述如何创建在两个值之间转换的动画。|  
|[关键帧动画概述](key-frame-animations-overview.md)|描述如何使用多个目标值创建动画（包括控制内插方法的功能）。|  
|[缓动函数](easing-functions.md)|说明如何将数学公式应用于动画以获得真实行为（如反弹）。|  
|[路径动画概述](path-animations-overview.md)|描述如何沿复杂路径移动或旋转对象。|  
|[属性动画技术概述](property-animation-techniques-overview.md)|描述使用演示图板、本地动画、时钟以及逐帧动画的属性动画。|  
|[演示图板概述](storyboards-overview.md)|描述如何将演示图板与多个时间线一起使用，以创建复杂动画。|  
|[计时行为概述](timing-behaviors-overview.md)|介绍<xref:System.Windows.Media.Animation.Timeline>类型和动画中使用的属性。|  
|[计时事件概述](timing-events-overview.md)|介绍可在上找到的事件<xref:System.Windows.Media.Animation.Timeline>和<xref:System.Windows.Media.Animation.Clock>对象的点上执行代码中在时间线，如开始、 暂停、 继续、 跳过，或停止。|  
|[帮助主题](animation-and-timing-how-to-topics.md)|包含演示在应用程序中使用动画和时间线的代码示例。|  
|[时钟操作说明主题](clocks-how-to-topics.md)|包含代码示例使用<xref:System.Windows.Media.Animation.Clock>在应用程序中的对象。|  
|[关键帧操作说明主题](key-frame-animation-how-to-topics.md)|包含在应用程序中使用关键帧动画的代码示例。|  
|[路径动画操作说明主题](path-animation-how-to-topics.md)|包含在应用程序中使用路径动画的代码示例。|  
  
<a name="reference"></a>   
## <a name="reference"></a>参考  
 <xref:System.Windows.Media.Animation.Timeline>  
  
 <xref:System.Windows.Media.Animation.Storyboard>  
  
 <xref:System.Windows.Media.Animation.BeginStoryboard>  
  
 <xref:System.Windows.Media.Animation.Clock>
