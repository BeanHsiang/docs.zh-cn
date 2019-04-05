---
title: 如何：使用关键帧对字符串进行动画处理
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], strings with key frames
- strings [WPF], animating with key frames
- key frames [WPF], animating strings with
ms.assetid: c62bc9fd-c09a-4227-bce0-0a1ab82049dd
ms.openlocfilehash: 70c5766da2ea91f519756cb47b20d688b33253e0
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356202"
---
# <a name="how-to-animate-a-string-by-using-key-frames"></a>如何：使用关键帧对字符串进行动画处理
此示例演示如何对字符串，它在此示例中为动画处理<xref:System.Windows.Controls.ContentControl.Content%2A>属性的<xref:System.Windows.Controls.Button>控件，使用关键帧。  
  
## <a name="example"></a>示例  
 下面的示例使用<xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>类进行动画处理<xref:System.Windows.Controls.ContentControl.Content%2A>属性的<xref:System.Windows.Controls.Button>。  
  
 在此示例中的所有关键帧使用的实例<xref:System.Windows.Media.Animation.DiscreteStringKeyFrame>类，因为使用关键帧创建一个字符串动画只能使用离散关键帧。 之类的离散关键帧<xref:System.Windows.Media.Animation.DiscreteStringKeyFrame>之间创建突然跳跃的值，也就是说，动画变化快速发生的而不是。  
  
 [!code-xaml[keyframes_snip#StringAnimationUsingKeyFramesWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/keyframes_snip/XAML/StringAnimationUsingKeyFramesExample.xaml#stringanimationusingkeyframeswholepage)]  
  
 有关完整示例，请参阅[关键帧动画示例](https://go.microsoft.com/fwlink/?LinkID=160012)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Animation.StringAnimationUsingKeyFrames>
- <xref:System.Windows.Controls.ContentControl.Content%2A>
- <xref:System.Windows.Controls.Button>
- <xref:System.Windows.Media.Animation.DiscreteStringKeyFrame>
- [关键帧动画概述](key-frame-animations-overview.md)
- [关键帧操作说明主题](key-frame-animation-how-to-topics.md)
