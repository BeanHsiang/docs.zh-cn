---
title: 如何：使用演示图板对属性进行动画处理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], Storyboards
- Storyboards [WPF], animation
ms.assetid: f4a314e9-1da2-4367-85fc-1232487efa7a
ms.openlocfilehash: f6064368b4f5e4fa8324b4039d734d4430cd9174
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364705"
---
# <a name="how-to-animate-a-property-by-using-a-storyboard"></a>如何：使用演示图板对属性进行动画处理
此示例演示如何使用<xref:System.Windows.Media.Animation.Storyboard>属性进行动画处理。 若要使用属性进行动画处理<xref:System.Windows.Media.Animation.Storyboard>，创建动画，以你想要进行动画处理，同时还创建每个属性<xref:System.Windows.Media.Animation.Storyboard>来包含动画。  
  
 属性类型确定要使用的动画类型。 例如，若要对采用的属性进行动画处理<xref:System.Double>值，请使用<xref:System.Windows.Media.Animation.DoubleAnimation>。 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A>和<xref:System.Windows.Media.Animation.Storyboard.TargetProperty>附加的属性指定的对象和向其应用动画属性。  
  
 若要在启动情节提要[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，使用<xref:System.Windows.Media.Animation.BeginStoryboard>操作和<xref:System.Windows.EventTrigger>。 <xref:System.Windows.EventTrigger>开始<xref:System.Windows.Media.Animation.BeginStoryboard>操作事件时指定其<xref:System.Windows.EventTrigger.RoutedEvent%2A>属性时发生。 <xref:System.Windows.Media.Animation.BeginStoryboard>操作将启动<xref:System.Windows.Media.Animation.Storyboard>。  
  
 下面的示例使用<xref:System.Windows.Media.Animation.Storyboard>对象进行动画处理两个<xref:System.Windows.Controls.Button>控件。 若要使第一个按钮大小，更改其<xref:System.Windows.FrameworkElement.Width%2A>进行动画处理。 若要使更改颜色，第二个按钮<xref:System.Windows.Media.SolidColorBrush.Color%2A>的属性<xref:System.Windows.Media.SolidColorBrush>用于设置<xref:System.Windows.Controls.Control.Background%2A>按钮进行动画处理。  
  
## <a name="example"></a>示例  
 [!code-xaml[AnimatePropertyStoryboards#1](~/samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/StoryboardExample.xaml#1)]  
  
> [!NOTE]
>  尽管动画可以针对这两<xref:System.Windows.FrameworkElement>对象，例如<xref:System.Windows.Controls.Control>或<xref:System.Windows.Controls.Panel>，和一个<xref:System.Windows.Freezable>对象，如<xref:System.Windows.Media.Brush>或<xref:System.Windows.Media.Transform>，只有框架元素具有<xref:System.Windows.FrameworkElement.Name%2A>属性。 若要向 Freezable 分配名称以便动画可以针对它，请使用 [x:Name 指令](../../xaml-services/x-name-directive.md)，如前面的示例所示。  
  
 如果你使用代码，则必须创建<xref:System.Windows.NameScope>有关<xref:System.Windows.FrameworkElement>注册的对象进行动画处理的名称和<xref:System.Windows.FrameworkElement>。 若要在代码中启动动画，请使用<xref:System.Windows.Media.Animation.BeginStoryboard>操作具有<xref:System.Windows.EventTrigger>。 或者，可以使用事件处理程序和<xref:System.Windows.Media.Animation.Storyboard.Begin%2A>方法的<xref:System.Windows.Media.Animation.Storyboard>。 下面的示例显示如何使用 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法。  
  
 [!code-csharp[AnimatePropertyStoryboards#11](~/samples/snippets/csharp/VS_Snippets_Wpf/AnimatePropertyStoryboards/CSharp/StoryboardExample.cs#11)]
 [!code-vb[AnimatePropertyStoryboards#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AnimatePropertyStoryboards/VisualBasic/StoryboardExample.vb#11)]  
  
 有关动画和情节提要的详细信息，请参阅[动画概述](animation-overview.md)。  
  
 如果使用代码，您并不局限于使用<xref:System.Windows.Media.Animation.Storyboard>属性进行动画处理的对象。 有关详细信息和示例，请参阅[在不使用情节提要的情况下对属性进行动画处理](how-to-animate-a-property-without-using-a-storyboard.md)和[使用 AnimationClock 对属性进行动画处理](how-to-animate-a-property-by-using-an-animationclock.md)。
