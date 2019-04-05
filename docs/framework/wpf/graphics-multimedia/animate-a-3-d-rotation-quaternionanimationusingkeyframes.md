---
title: 如何：使用关键帧对三维旋转进行动画处理 (QuaternionAnimationUsingKeyFrames)
ms.date: 03/30/2017
helpviewer_keywords:
- 3-D translations [WPF], animating [WPF], with key frames (QuaternionAnimationUsingKeyFrames)
- key frames [WPF], QuaternionAnimationUsingKeyFrames
- animation [WPF], 3-D translations [WPF], with key frames (QuaternionAnimationUsingKeyFrames)
ms.assetid: 09e5707b-7523-4a08-9aa7-bb13cbedccdf
ms.openlocfilehash: b524e9a37f778243cdf25255461f7f6607051264
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354266"
---
# <a name="how-to-animate-a-3-d-rotation-using-key-frames-quaternionanimationusingkeyframes"></a>如何：使用关键帧对三维旋转进行动画处理 (QuaternionAnimationUsingKeyFrames)
在以下示例中，<xref:System.Windows.Media.Animation.QuaternionAnimationUsingKeyFrames>用于使旋转三维对象。 此动画使用以下关键帧：  
  
1.  <xref:System.Windows.Media.Animation.LinearRotation3DKeyFrame> 用于创建值之间的平滑的线性插值。  
  
2.  <xref:System.Windows.Media.Animation.DiscreteRotation3DKeyFrame> 用于之间创建突然"跳跃"的值 （没有内插法）。  
  
3.  <xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame> 用于创建具体取决于值之间的变量转换<xref:System.Windows.Media.Animation.SplineRotation3DKeyFrame.KeySpline%2A>属性。 在下面的示例中，此部分动画启动较慢，但是即将结束的时间段，以指数方式加速。  
  
## <a name="example"></a>示例  
 [!code-xaml[Animation3DGallery_snip#QuaternionAnimationUsingKeyFramesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/QuaternionAnimationUsingKeyFramesExample.xaml#quaternionanimationusingkeyframesexamplewholepage)]  
  
## <a name="see-also"></a>请参阅
- [使用情节提要为 3D 旋转设置动画效果](how-to-animate-a-3-d-rotation-using-storyboards.md)
- [使用 Rotation3DAnimation 为 3D 旋转设置动画效果](how-to-animate-a-3-d-rotation-using-rotation3danimation.md)
- [使用四元数为 3D 旋转设置动画效果](how-to-animate-a-3-d-rotation-using-quaternions.md)
- [使用关键帧为 3D 旋转设置动画效果 (Rotation3DAnimationUsingKeyFrames)](how-to-animate-a-3-d-rotation-using-key-frames.md)
- [3D 图形概述](3-d-graphics-overview.md)
- [关键帧动画概述](key-frame-animations-overview.md)
