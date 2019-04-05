---
title: 如何：旋转对象
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [WPF], rotating objects [WPF]
- rotating objects [WPF]
ms.assetid: ee3466cd-e66f-4e8f-8a5a-71d77bc1e390
ms.openlocfilehash: 49de419f22980ab9101c388079e0348b4c1113f4
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360363"
---
# <a name="how-to-rotate-an-object"></a>如何：旋转对象
此示例演示如何旋转对象。 该示例首先创建<xref:System.Windows.Media.RotateTransform>，然后指定其<xref:System.Windows.Media.RotateTransform.Angle%2A>以度为单位。  
  
 下面的示例将旋转<xref:System.Windows.Shapes.Polyline>对象围绕其左上角的 45 度。  
  
## <a name="example"></a>示例  
 [!code-xaml[Transforms_snip#RotatePolylineAboutTopLeft](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineabouttopleft)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineabouttopleft)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutTopLeft](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineabouttopleft)]  
  
 <xref:System.Windows.Media.RotateTransform.CenterX%2A>并<xref:System.Windows.Media.RotateTransform.CenterY%2A>的属性<xref:System.Windows.Media.RotateTransform>指定哪些对象的旋转的点。 此中心点以要转换的元素的坐标空间表示。 默认情况下，将围绕着要转换的对象的左上角 (0,0) 进行旋转。  
  
 下一个示例旋转<xref:System.Windows.Shapes.Polyline>对象围绕点 (25，50) 顺时针旋转 45 度。  
  
 [!code-xaml[Transforms_snip#RotatePolylineAboutCenter](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_snip/CS/RotateTransformExample.xaml#rotatepolylineaboutcenter)]  
  
 [!code-csharp[Transforms_Procedural_snip#RotatePolylineAboutCenter](~/samples/snippets/csharp/VS_Snippets_Wpf/Transforms_Procedural_snip/CSharp/RotateTransformExample.cs#rotatepolylineaboutcenter)]
 [!code-vb[Transforms_Procedural_snip#RotatePolylineAboutCenter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Transforms_Procedural_snip/VisualBasic/RotateTransformExample.vb#rotatepolylineaboutcenter)]  
  
 下图显示了应用的结果<xref:System.Windows.Media.Transform>到两个对象。  
  
 ![围绕不同中心点旋转 45 度](./media/wcpsdk-graphicsmm-rotatetransform45degrees.gif "wcpsdk_graphicsmm_rotatetransform45degrees")  
两个对象以不同的旋转中心旋转 45 度  
  
 <xref:System.Windows.Shapes.Polyline>前面的示例中是<xref:System.Windows.UIElement>。 当应用<xref:System.Windows.Media.Transform>到<xref:System.Windows.UIElement.RenderTransform%2A>的属性<xref:System.Windows.UIElement>，可以使用<xref:System.Windows.UIElement.RenderTransformOrigin%2A>属性指定的 origin 每个<xref:System.Windows.Media.Transform>适用于元素。 因为<xref:System.Windows.UIElement.RenderTransformOrigin%2A>属性使用相对坐标，你可以将转换应用到元素的中心，即使您不知道其大小。 有关详细信息和示例，请参阅[指定使用相对值转换原点](how-to-specify-the-origin-of-a-transform-by-using-relative-values.md)。  
  
 有关完整示例，请参阅 [2D 转换示例](https://go.microsoft.com/fwlink/?LinkID=158252)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Transform>
- [转换概述](transforms-overview.md)
- [帮助主题](transformations-how-to-topics.md)
