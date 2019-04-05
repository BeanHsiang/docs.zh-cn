---
title: 如何：使用图像绘制区域
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [WPF], painting with
- painting [WPF], with images
- brushes [WPF], painting with images
ms.assetid: 3432c533-1fc7-492d-94ee-0b13d60125ae
ms.openlocfilehash: c1db803aacad85ce90fec519b5eabdd8df7bb584
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57369118"
---
# <a name="how-to-paint-an-area-with-an-image"></a>如何：使用图像绘制区域
此示例演示如何使用<xref:System.Windows.Media.ImageBrush>类，以使用图像绘制区域。 <xref:System.Windows.Media.ImageBrush>显示由指定的单个映像及其<xref:System.Windows.Media.ImageBrush.ImageSource%2A>属性。  
  
## <a name="example"></a>示例  
 以下示例绘制<xref:System.Windows.Controls.Control.Background%2A>通过使用一个按钮<xref:System.Windows.Media.ImageBrush>。  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/PaintingWithImagesExample.cs#imagebrushexamplewholepage)]  
  
 默认情况下，<xref:System.Windows.Media.ImageBrush>拉伸其图像以完全填充要绘制的区域。 在以上示例中，拉伸图像以填充按钮，可能会使图像失真。 可以通过设置控制此行为<xref:System.Windows.Media.TileBrush.Stretch%2A>的属性<xref:System.Windows.Media.TileBrush>到<xref:System.Windows.Media.Stretch.Uniform>或<xref:System.Windows.Media.Stretch.UniformToFill>，这将导致要保持图像的纵横比的画笔。  
  
 如果您设置<xref:System.Windows.Media.TileBrush.Viewport%2A>并<xref:System.Windows.Media.TileBrush.TileMode%2A>的属性<xref:System.Windows.Media.ImageBrush>，可以创建一个重复图案。 以下示例通过使用从图像创建的图案来绘制按钮。  
  
 [!code-csharp[UsingImageBrush_snip#TiledImageBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TiledImageBrushExample.cs#tiledimagebrushexamplewholepage)]
 [!code-vb[UsingImageBrush_snip#TiledImageBrushExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UsingImageBrush_snip/VisualBasic/TiledImageBrushExample.vb#tiledimagebrushexamplewholepage)]  
  
 有关详细信息<xref:System.Windows.Media.ImageBrush>类，请参阅[使用图像、 绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)。  
  
 此代码示例是为提供一个更大示例的一部分<xref:System.Windows.Media.ImageBrush>类。 有关完整示例，请参阅[ImageBrush 示例](https://go.microsoft.com/fwlink/?LinkID=160005)。  
  
## <a name="see-also"></a>请参阅
- [使用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)
