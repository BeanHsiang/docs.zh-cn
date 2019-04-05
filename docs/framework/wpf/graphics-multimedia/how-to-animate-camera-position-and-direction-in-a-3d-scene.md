---
title: 如何：在三维场景中对照相机位置和方向进行动画处理
ms.date: 03/30/2017
helpviewer_keywords:
- animation [WPF], camera position in 3-D scenes
- camera direction [WPF], animating in 3-D scenes
- 3-D scenes [WPF], animating camera position
- 3-D scenes [WPF], animating camera direction
- camera position [WPF], animating in 3-D scenes
- animation [WPF], camera direction in 3-D scenes
ms.assetid: 480224b7-a5e5-4165-ba7f-ef760ddff94a
ms.openlocfilehash: 459b668c134e31afe295dd311094ac9cf84d884a
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374019"
---
# <a name="how-to-animate-camera-position-and-direction-in-a-3d-scene"></a>如何：在三维场景中对照相机位置和方向进行动画处理
下面的示例演示如何将照相机位置进行动画处理和对三维场景中指向的方向进行动画处理。 这是通过使用<xref:System.Windows.Media.Animation.Point3DAnimation>并<xref:System.Windows.Media.Animation.Vector3DAnimation>进行动画处理<xref:System.Windows.Media.Media3D.ProjectionCamera.Position%2A>并<xref:System.Windows.Media.Media3D.ProjectionCamera.LookDirection%2A>分别的属性<xref:System.Windows.Media.Media3D.PerspectiveCamera>。 可能使用如下的动画可以更改的事件响应场景旁观者的视图。  
  
## <a name="example"></a>示例  
 [!code-xaml[Animation3DGallery_snip#PointVector3DAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/PointVector3DAnimationExample.xaml#pointvector3danimationexamplewholepage)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Animation.Vector3DAnimation>
- <xref:System.Windows.Media.Animation.Point3DAnimation>
- [使用关键帧为照相机位置和方向设置动画效果](how-to-animate-camera-position-and-direction-using-key-frames.md)
- [3D 图形概述](3-d-graphics-overview.md)
