---
title: 如何：使用子时间线简化动画
ms.date: 03/30/2017
helpviewer_keywords:
- simplifying animations by child timelines [WPF]
- animation [WPF], simplifying by child timelines
- child timelines [WPF]
ms.assetid: 8335d770-d13d-42bd-8dfa-63f92c0327e2
ms.openlocfilehash: 933ba2dff86b99bddd8d8f75bafcd94833b2e066
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57370353"
---
# <a name="how-to-simplify-animations-by-using-child-timelines"></a>如何：使用子时间线简化动画
此示例演示如何使用子简化动画<xref:System.Windows.Media.Animation.ParallelTimeline>对象。 一个<xref:System.Windows.Media.Animation.Storyboard>是一种<xref:System.Windows.Media.Animation.Timeline>提供它所包含的时间线目标信息。 使用<xref:System.Windows.Media.Animation.Storyboard>提供时间线目标信息，包括对象和属性信息。  
  
 若要开始动画，请使用一个或多个<xref:System.Windows.Media.Animation.ParallelTimeline>对象的嵌套的子元素作为<xref:System.Windows.Media.Animation.Storyboard>。 这些<xref:System.Windows.Media.Animation.ParallelTimeline>对象可以包含其他动画，因此，可以更好地封装复杂动画中的计时序列。 例如，如果您设置动画<xref:System.Windows.Controls.TextBlock>和相同的多个形状<xref:System.Windows.Media.Animation.Storyboard>，可以分隔的动画<xref:System.Windows.Controls.TextBlock>和形状，将放到单独的每个<xref:System.Windows.Media.Animation.ParallelTimeline>。 因为每个<xref:System.Windows.Media.Animation.ParallelTimeline>都有自己<xref:System.Windows.Media.Animation.Timeline.BeginTime%2A>和所有子元素<xref:System.Windows.Media.Animation.ParallelTimeline>开始相对于此<xref:System.Windows.Media.Animation.Timeline.BeginTime%2A>，更好地封装计时。  
  
 下面的示例进行动画处理的两段文本 (<xref:System.Windows.Controls.TextBlock>对象) 从在同一<xref:System.Windows.Media.Animation.Storyboard>。 一个<xref:System.Windows.Media.Animation.ParallelTimeline>封装之一的动画<xref:System.Windows.Controls.TextBlock>对象。  
  
 **性能说明：** 尽管可以嵌套<xref:System.Windows.Media.Animation.Storyboard>时间线相互，<xref:System.Windows.Media.Animation.ParallelTimeline>是更适用于嵌套，因为它们需要更少的开销。 (<xref:System.Windows.Media.Animation.Storyboard>类继承自<xref:System.Windows.Media.Animation.ParallelTimeline>类。)  
  
## <a name="example"></a>示例  
 [!code-xaml[Timelines_snip#ParallelTimelineWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Timelines_snip/CS/ParallelTimelineExample.xaml#paralleltimelinewholepage)]  
  
## <a name="see-also"></a>请参阅
- [动画概述](animation-overview.md)
- [指定演示图板动画之间的 HandoffBehavior](how-to-specify-handoffbehavior-between-storyboard-animations.md)
