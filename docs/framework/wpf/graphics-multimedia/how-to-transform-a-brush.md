---
title: 如何：变换画笔
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], rotating contents
- brushes [WPF], Transform property
- rotating contents of brushes [WPF]
ms.assetid: ebada2f9-f01f-4863-9ea2-c2e4e51610f1
ms.openlocfilehash: 990c82b4844ce3ca7f5b553b180280b6b37496ca
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57373759"
---
# <a name="how-to-transform-a-brush"></a>如何：变换画笔
此示例演示如何转换<xref:System.Windows.Media.Brush>通过使用其两个转换属性对象：<xref:System.Windows.Media.Brush.RelativeTransform%2A>和<xref:System.Windows.Media.Brush.Transform%2A>。  
  
 下面的示例使用<xref:System.Windows.Media.RotateTransform>旋转的内容<xref:System.Windows.Media.ImageBrush>旋转 45 度。  
  
 如下图所示<xref:System.Windows.Media.ImageBrush>而无需<xref:System.Windows.Media.RotateTransform>，使用<xref:System.Windows.Media.RotateTransform>应用于<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性，并使用<xref:System.Windows.Media.RotateTransform>应用于<xref:System.Windows.Media.Brush.Transform%2A>属性。  
  
 ![画笔 RelativeTransform 和 Transform 设置](./media/wcpsdk-graphicsmm-transformandrelativetransform.png "wcpsdk_graphicsmm_transformandrelativetransform")  
  
## <a name="example"></a>示例  
 第一个示例应用<xref:System.Windows.Media.RotateTransform>到<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性的<xref:System.Windows.Media.ImageBrush>。 <xref:System.Windows.Media.RotateTransform.CenterX%2A>并<xref:System.Windows.Media.RotateTransform.CenterY%2A>的属性<xref:System.Windows.Media.RotateTransform>对象均设置为 0.5，这是此内容的中心点的相对坐标。 因此，<xref:System.Windows.Media.ImageBrush>内容围绕其中心旋转。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushrelativetransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushrelativetransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushRelativeTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushrelativetransformexample)]  
  
 第二个示例也适用<xref:System.Windows.Media.RotateTransform>到<xref:System.Windows.Media.ImageBrush>; 但是，此示例使用<xref:System.Windows.Media.Brush.Transform%2A>属性，而不是<xref:System.Windows.Media.Brush.RelativeTransform%2A>属性。  
  
 若要旋转画笔围绕其中心，该示例设置<xref:System.Windows.Media.RotateTransform.CenterX%2A>并<xref:System.Windows.Media.RotateTransform.CenterY%2A>的属性<xref:System.Windows.Media.RotateTransform>为绝对坐标的对象。 因为画笔绘制了一个 175x90 像素的矩形，所以该矩形的中心点为 (87.5, 45)。  
  
 [!code-csharp[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/BrushTransformExample.cs#imagebrushtransformexample)]
 [!code-vb[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/brushtransformexample.vb#imagebrushtransformexample)]
 [!code-xaml[BrushesIntroduction_snip#ImageBrushTransformExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/BrushTransformExample.xaml#imagebrushtransformexample)]  
  
 有关如何将说明<xref:System.Windows.Media.Brush.RelativeTransform%2A>并<xref:System.Windows.Media.Brush.Transform%2A>属性起作用，请参阅[画笔转换概述](brush-transformation-overview.md)。  
  
 有关完整示例，请参阅[画笔示例](https://go.microsoft.com/fwlink/?LinkID=159973)。 有关画笔的详细信息，请参阅[使用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)。  
  
## <a name="see-also"></a>请参阅
- [画笔转换概述](brush-transformation-overview.md)
- [使用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)
- [转换概述](transforms-overview.md)
