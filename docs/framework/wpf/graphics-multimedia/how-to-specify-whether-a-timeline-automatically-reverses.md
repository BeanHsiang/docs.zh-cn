---
title: 如何：指定时间线是否自动反转
ms.date: 03/30/2017
helpviewer_keywords:
- AutoReverse property of timelines [WPF]
- Timelines [WPF], AutoReverse property
ms.assetid: 1648dd90-1bee-409a-ac69-ac729867f557
ms.openlocfilehash: 0fe2d337d8afa5197475e5b9ee40950226596e8b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354201"
---
# <a name="how-to-specify-whether-a-timeline-automatically-reverses"></a>如何：指定时间线是否自动反转
时间线的<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>属性确定是否反向播放完成向前迭代后。 下面的示例演示使用相同的持续时间和目标值，但使用不同的多个动画<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>设置。 若要演示如何<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>属性具有不同的行为与<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A>设置，某些动画设置为重复。 最后一个动画演示如何将<xref:System.Windows.Media.Animation.Timeline.AutoReverse%2A>属性嵌套时间线上的工作原理。  
  
## <a name="example"></a>示例  
 [!code-xaml[timingbehaviors_snip#AutoReverseAndRepeatBehaviorExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/AutoReverseExample.xaml#autoreverseandrepeatbehaviorexamplewholepage)]
