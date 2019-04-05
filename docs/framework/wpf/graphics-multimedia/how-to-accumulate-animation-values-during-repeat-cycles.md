---
title: 如何：在重复循环过程中累积动画值
ms.date: 03/30/2017
helpviewer_keywords:
- accumulating animation values across repeating cycles [WPF]
- animation [WPF], accumulating values across repeating cycles
ms.assetid: 548df369-c7cc-4dab-b569-08b95ced2e7e
ms.openlocfilehash: e38e1601e2f4eeab2b53918924bc21e05163d948
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57357256"
---
# <a name="how-to-accumulate-animation-values-during-repeat-cycles"></a>如何：在重复循环过程中累积动画值
此示例演示如何使用<xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A>属性以通过重复循环累积动画值。  
  
## <a name="example"></a>示例  
 使用<xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A>属性通过重复循环累积动画的基值。 例如，如果你设置重复 9 次的动画 (<xref:System.Windows.Media.Animation.Timeline.RepeatBehavior%2A> ="9 x") 和设置的属性进行动画处理介于 10 到 15 之间 (从 = 10 到 = 15)，该属性进行动画处理从 10 到 15 在第一个周期中，从 15 到 20 在第二个周期内从 20%到 25 期间的第三个周期，依此类推。 因此，每个动画循环使用从以前的动画循环的动画结束值作为其基础值。  
  
 可以使用`IsCumulative`具有最基本的动画和大多数关键帧动画的属性。 有关详细信息，请参阅[动画概述](animation-overview.md)并[关键帧动画概述](key-frame-animations-overview.md)。  
  
 下面的示例演示此行为由四个矩形的宽度进行动画处理。 下面的示例：  
  
-   与第一个矩形进行动画处理<xref:System.Windows.Media.Animation.DoubleAnimation>，并设置<xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A>属性设置为`true`。  
  
-   与第二个矩形进行动画处理<xref:System.Windows.Media.Animation.DoubleAnimation>，并设置<xref:System.Windows.Media.Animation.DoubleAnimation.IsCumulative%2A>属性设置的默认值为`false`。  
  
-   使用第三个矩形进行动画处理<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>，并设置<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A>属性设置为`true`。  
  
-   包含的最后一个矩形进行动画处理<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames>，并设置<xref:System.Windows.Media.Animation.DoubleAnimationUsingKeyFrames.IsCumulative%2A>属性设置为`false`。  
  
 [!code-xaml[timingbehaviors_snip#IsCumulativeWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_snip/CSharp/IsCumulativeExample.xaml#iscumulativewholepage)]  
  
## <a name="see-also"></a>请参阅
- [向动画起始值添加动画输出值](how-to-add-an-animation-output-value-to-an-animation-starting-value.md)
- [重复动画](how-to-repeat-an-animation.md)
- [动画概述](animation-overview.md)
- [关键帧动画概述](key-frame-animations-overview.md)
- [帮助主题](animation-and-timing-how-to-topics.md)
