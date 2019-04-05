---
title: 如何：控制关键帧动画的计时
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- key frames [WPF], timing
- timing key-frame animation
ms.assetid: b059216f-7d4b-4ca8-a019-bc287ee7bf16
ms.openlocfilehash: d0ea56b24f8fffeb688d297a675681bce3fdc4e0
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57489872"
---
# <a name="how-to-control-key-frame-animation-timing"></a>如何：控制关键帧动画的计时

此示例演示如何控制关键帧动画中的关键帧的时间。 像其他动画关键帧动画具有<xref:System.Windows.Media.Animation.Timeline.Duration%2A>属性。 除了指定动画的持续时间，您需要指定该持续时间的哪一部分分配给每个其关键帧。 若要分配的时间，则指定<xref:System.Windows.Media.Animation.KeyTime>中每个关键帧动画。

<xref:System.Windows.Media.Animation.KeyTime>为每个关键帧指定 （未指定关键帧播放的时间长度） 的关键帧结束时。 您可以指定<xref:System.Windows.Media.Animation.KeyTime>作为<xref:System.TimeSpan>值，以百分比表示，或作为<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>或<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>特殊值。

## <a name="example"></a>示例

下面的示例使用<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>若要在屏幕上对矩形进行动画处理。 使用设置关键帧的关键时间<xref:System.TimeSpan>值。

[!code-csharp[keyframes_snip#KeyTimesTimeSpanExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimestimespanexample)]
[!code-vb[keyframes_snip#KeyTimesTimeSpanExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimestimespanexample)]
[!code-xaml[keyframes_snip#KeyTimesTimeSpanExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimestimespanexample)]

下图显示达到每个关键帧的值。

![在 3、 4 和 10 秒时达到的键值](./media/graphicsmm-keyframe-keytime1-timespan.png "graphicsmm_keyframe_keytime1_timespan")

下一个示例演示具有完全相同，只不过使用百分比值设置关键帧的关键时间的动画。

[!code-csharp[keyframes_snip#KeyTimesPercentageExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimespercentageexample)]
[!code-vb[keyframes_snip#KeyTimesPercentageExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimespercentageexample)]
[!code-xaml[keyframes_snip#KeyTimesPercentageExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimespercentageexample)]

下图显示达到每个关键帧的值。

![在 3、 4 和 10 秒时达到的键值](./media/graphicsmm-keyframe-keytime2-percentage.png "graphicsmm_keyframe_keytime2_percentage")

下面的示例使用<xref:System.Windows.Media.Animation.KeyTime.Uniform%2A>关键时间值。

[!code-csharp[keyframes_snip#KeyTimesUniformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimesuniformexample)]
[!code-vb[keyframes_snip#KeyTimesUniformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimesuniformexample)]
[!code-xaml[keyframes_snip#KeyTimesUniformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimesuniformexample)]

下图显示达到每个关键帧的值。

![在 3.3、 6.6 和 9.9 秒时达到的关键值](./media/graphicsmm-keyframe-keytime3-uniform.png "graphicsmm_keyframe_keytime3_uniform")

最后一个示例使用<xref:System.Windows.Media.Animation.KeyTime.Paced%2A>关键时间值。

[!code-csharp[keyframes_snip#KeyTimesPacedExample](~/samples/snippets/csharp/VS_Snippets_Wpf/keyframes_snip/CSharp/KeyTimesExample.cs#keytimespacedexample)]
[!code-vb[keyframes_snip#KeyTimesPacedExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/keyframes_snip/visualbasic/keytimesexample.vb#keytimespacedexample)]
[!code-xaml[keyframes_snip#KeyTimesPacedExample](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/KeyTimesExample.xaml#keytimespacedexample)]

下图显示达到每个关键帧的值。

![密钥值在 0、 5 和 10 秒时达到](./media/graphicsmm-keyframe-keytime4-paced.png "graphicsmm_keyframe_keytime4_paced")

为简单起见，此示例使用本地动画的代码版本不是演示图板，因为仅将一个动画应用到单个属性，但可以修改示例以改为使用情节提要。 有关演示如何声明中的代码将情节提要的示例，请参阅[使用情节提要对属性进行动画处理](how-to-animate-a-property-by-using-a-storyboard.md)。

有关完整示例，请参阅[关键帧动画示例](https://go.microsoft.com/fwlink/?LinkID=160012)。 关键帧动画的详细信息，请参阅[关键帧动画概述](key-frame-animations-overview.md)。

## <a name="see-also"></a>请参阅

- [关键帧动画概述](key-frame-animations-overview.md)
- [动画概述](animation-overview.md)
- [帮助主题](animation-and-timing-how-to-topics.md)
