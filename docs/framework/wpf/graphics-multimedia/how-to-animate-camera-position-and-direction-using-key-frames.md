---
title: 如何：使用关键帧对照相机位置和方向进行动画处理
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], camera direction with key frames
- key frames [WPF], animating camera direction
- animation [WPF], camera position with key frames
- camera position [WPF], animating with key frames
- key frames [WPF], animating camera position
- camera direction [WPF], animating with key frames
ms.assetid: 5753024e-0057-454d-947f-43ea686879c7
ms.openlocfilehash: 5df3a201eaae4ddcf2e5d5aac3de6e0d5013947c
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57353395"
---
# <a name="how-to-animate-camera-position-and-direction-using-key-frames"></a>如何：使用关键帧对照相机位置和方向进行动画处理
在以下示例中，<xref:System.Windows.Media.Animation.Point3DAnimationUsingKeyFrames>使用的位置进行动画处理<xref:System.Windows.Media.Media3D.PerspectiveCamera>三维场景中。 此外，<xref:System.Windows.Media.Animation.Vector3DAnimationUsingKeyFrames>用于对三维场景中指照相机的方向进行动画处理。 这两个这些动画使用几个关键帧来创建一系列的动画效果：  
  
1.  <xref:System.Windows.Media.Animation.LinearPoint3DKeyFrame> 和<xref:System.Windows.Media.Animation.LinearVector3DKeyFrame>用于创建值之间的平滑的线性插值。  
  
2.  <xref:System.Windows.Media.Animation.DiscretePoint3DKeyFrame> 和<xref:System.Windows.Media.Animation.DiscreteVector3DKeyFrame>用于之间创建突然"跳跃"的值 （没有内插法）。  
  
3.  <xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame> 并<xref:System.Windows.Media.Animation.SplineVector3DKeyFrame>用来创建具体取决于值之间的变量转换<xref:System.Windows.Media.Animation.SplinePoint3DKeyFrame.KeySpline%2A>属性。 以下示例中，在动画启动较慢，但是即将结束的时间段，以指数方式加速。  
  
## <a name="example"></a>示例  
 [!code-xaml[Animation3DGallery_snip#PointVector3DAnimationUsingKeyFramesExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationUsingKeyFramesExample.xaml#pointvector3danimationusingkeyframesexamplewholepage)]  
  
## <a name="see-also"></a>请参阅
- [在 3D 场景中为照相机位置和方向设置动画效果](how-to-animate-camera-position-and-direction-in-a-3d-scene.md)
- [3D 图形概述](3-d-graphics-overview.md)
