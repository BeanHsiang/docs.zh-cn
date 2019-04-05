---
title: 如何：设置动画的持续时间
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], duration
- Timelines [WPF], description
- duration of animations [WPF]
ms.assetid: 155034ef-7d00-4416-a73c-b1713992d2eb
ms.openlocfilehash: 83f87e911d9d5412eaba1eb88aea74b9325bc899
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57351620"
---
# <a name="how-to-set-a-duration-for-an-animation"></a>如何：设置动画的持续时间
一个<xref:System.Windows.Media.Animation.Timeline>表示一个时间段和段的长度由时间线的<xref:System.Windows.Duration>。 当<xref:System.Windows.Media.Animation.Timeline>到达其持续时间，就会停止播放。 如果<xref:System.Windows.Media.Animation.Timeline>具有子时间线，它们也会停止播放。 播放动画时，<xref:System.Windows.Duration>指定动画需要花多长转换从其起始值为终止值。  
  
 您可以指定<xref:System.Windows.Duration>与特定的有限时间或特殊值<xref:System.Windows.Duration.Automatic%2A>或<xref:System.Windows.Duration.Forever%2A>。 动画的持续时间必须始终为时间值，因为动画必须始终具有已定义的有限长度 — 否则，动画将不知道如何在其目标值之间转换。 容器时间线 (<xref:System.Windows.Media.Animation.TimelineGroup>对象)，如<xref:System.Windows.Media.Animation.Storyboard>并<xref:System.Windows.Media.Animation.ParallelTimeline>，默认持续时间为<xref:System.Windows.Duration.Automatic%2A>，这意味着它们将自动结束其最后一个子级停止播放时。  
  
 在下面的示例、 宽度、 高度和填充颜色的<xref:System.Windows.Shapes.Rectangle>进行动画处理。 从而导致动画效果，包括控制动画的感知的速度和重写的子时间线与容器时间线的持续时间的持续时间的动画和容器时间线上设置持续时间。  
  
## <a name="example"></a>示例  
 [!code-xaml[timingbehaviors_snip#DurationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/DurationExample.xaml#durationexamplewholepage)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Duration>
- [动画概述](animation-overview.md)
