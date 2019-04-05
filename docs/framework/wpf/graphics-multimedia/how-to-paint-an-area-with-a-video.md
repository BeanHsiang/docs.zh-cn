---
title: 如何：使用视频绘制区域
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- painting with a video [WPF]
- video [WPF], painting with
- brushes [WPF], painting with a video
ms.assetid: 04dd6600-4a6e-4b43-a93e-21cce7dfbcb8
ms.openlocfilehash: 0756a9e87840648b55ecad4b3f1ce6e0e5452eb7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57363288"
---
# <a name="how-to-paint-an-area-with-a-video"></a>如何：使用视频绘制区域
此示例演示如何使用媒体绘制区域。 使用媒体绘制区域的一种方法是使用<xref:System.Windows.Controls.MediaElement>一起使用<xref:System.Windows.Media.VisualBrush>。 使用<xref:System.Windows.Controls.MediaElement>若要加载和播放媒体，并使用它来设置<xref:System.Windows.Media.VisualBrush.Visual%2A>属性的<xref:System.Windows.Media.VisualBrush>。 然后，可以使用<xref:System.Windows.Media.VisualBrush>要加载的介质使用绘制区域。  
  
## <a name="example"></a>示例  
 下面的示例使用<xref:System.Windows.Controls.MediaElement>和一个<xref:System.Windows.Media.VisualBrush>绘制<xref:System.Windows.Controls.TextBlock.Foreground%2A>的<xref:System.Windows.Controls.TextBlock>控件使用的视频。 此示例设置<xref:System.Windows.Controls.MediaElement.IsMuted%2A>的属性<xref:System.Windows.Controls.MediaElement>到`true`，以便它不发出声音。  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundinline)]
 [!code-xaml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundInline](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundinline)]  
  
## <a name="example"></a>示例  
 因为<xref:System.Windows.Media.VisualBrush>继承<xref:System.Windows.Media.TileBrush>类，它提供了几个平铺模式。 通过设置<xref:System.Windows.Media.TileBrush.TileMode%2A>的属性<xref:System.Windows.Media.VisualBrush>到<xref:System.Windows.Media.TileMode.Tile>并设置其<xref:System.Windows.Media.TileBrush.Viewport%2A>属性的值小于要绘制的区域，可以创建一个平铺的图案。  
  
 下面的示例等同于上一示例中，不同之处在于<xref:System.Windows.Media.VisualBrush>来自视频将生成一种模式。  
  
 [!code-csharp[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/PaintWithVideoExample.cs#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-vb[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/paintwithvideoexample.vb#graphicsmmvideoastextbackgroundtiledinline)]
 [!code-xaml[Visualbrush_markup_snip#GraphicsMMVideoAsTextBackgroundTiledInline](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/PaintWithVideoExample.xaml#graphicsmmvideoastextbackgroundtiledinline)]  
  
 了解如何将内容文件，例如媒体文件添加到您的应用程序，请参阅[WPF 应用程序资源、 内容和数据文件](../app-development/wpf-application-resource-content-and-data-files.md)。 当添加媒体文件时，必须将其添加，作为内容文件，而不是资源文件。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.VisualBrush>
- [使用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)
- [TileBrush 概述](tilebrush-overview.md)
- [多媒体概述](multimedia-overview.md)
