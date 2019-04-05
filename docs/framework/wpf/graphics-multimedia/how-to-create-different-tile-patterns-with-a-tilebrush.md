---
title: 如何：使用 TileBrush 创建不同的平铺模式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TileBrush [WPF], creating tile patterns
- tile patterns [WPF], creating
- creating [WPF], tile patterns with TileBrush
ms.assetid: 5aa46632-3527-4668-9d8d-0375c8af28aa
ms.openlocfilehash: 2efd070ac9ad502f2539d100fa450f95bcdddced
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367773"
---
# <a name="how-to-create-different-tile-patterns-with-a-tilebrush"></a>如何：使用 TileBrush 创建不同的平铺模式
此示例演示如何使用<xref:System.Windows.Media.TileBrush.TileMode%2A>属性的<xref:System.Windows.Media.TileBrush>创建模式。  
  
 <xref:System.Windows.Media.TileBrush.TileMode%2A>属性可用于指定如何将内容的<xref:System.Windows.Media.TileBrush>重复，也就是说，平铺来填充输出区域。 若要创建一种模式，您可以设置<xref:System.Windows.Media.TileBrush.TileMode%2A>到<xref:System.Windows.Media.TileMode.Tile>， <xref:System.Windows.Media.TileMode.FlipX>， <xref:System.Windows.Media.TileMode.FlipY>，或<xref:System.Windows.Media.TileMode.FlipXY>。 您还必须设置<xref:System.Windows.Media.TileBrush.Viewport%2A>的<xref:System.Windows.Media.TileBrush>以便小于区域要绘制; 否则，单个磁贴是生成，而不考虑其<xref:System.Windows.Media.TileBrush.TileMode%2A>您使用的设置。  
  
## <a name="example"></a>示例  
 下面的示例创建五个<xref:System.Windows.Media.DrawingBrush>对象，每个不同<xref:System.Windows.Media.TileBrush.TileMode%2A>设置，并使用它们来绘制五个矩形。 虽然此示例使用<xref:System.Windows.Media.DrawingBrush>类，以演示<xref:System.Windows.Media.TileBrush.TileMode%2A>行为，<xref:System.Windows.Media.TileBrush.TileMode%2A>属性的工作方式完全相同的所有<xref:System.Windows.Media.TileBrush>对象，也就是说，对于<xref:System.Windows.Media.ImageBrush>， <xref:System.Windows.Media.VisualBrush>，和<xref:System.Windows.Media.DrawingBrush>。  
  
 下图显示了此示例生成的输出。  
  
 ![TileBrush 平铺示例输出](./media/graphicsmm-drawingbrushtilemodeexample.png "graphicsmm_DrawingBrushTileModeExample")  
使用 TileMode 属性创建平铺模式  
  
 [!code-csharp[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/TileModeExample.cs#graphicsmmdrawingbrushtilemodeexample)]
 [!code-vb[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/tilemodeexample.vb#graphicsmmdrawingbrushtilemodeexample)]
 [!code-xaml[BrushesIntroduction_snip#GraphicsMMDrawingBrushTileModeExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/TileModeExample.xaml#graphicsmmdrawingbrushtilemodeexample)]  
  
## <a name="see-also"></a>请参阅
- [设置 TileBrush 的平铺大小](how-to-set-the-tile-size-for-a-tilebrush.md)
- [使用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)
