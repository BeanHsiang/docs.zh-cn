---
title: 使用图像、图形和视觉对象进行绘制
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- brushes [WPF], painting with drawings
- painting [WPF], with drawings
- painting [WPF], with images
- painting with visuals [WPF]
- brushes [WPF], painting with images
- brushes [WPF], painting with visuals
ms.assetid: 779aac3f-8d41-49d8-8130-768244aa2240
ms.openlocfilehash: bb66c34a847f78f7921ae925d0c3d0640c11aeec
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57361313"
---
# <a name="painting-with-images-drawings-and-visuals"></a>使用图像、图形和视觉对象进行绘制
本主题介绍如何使用<xref:System.Windows.Media.ImageBrush>， <xref:System.Windows.Media.DrawingBrush>，并<xref:System.Windows.Media.VisualBrush>对象，若要使用图像绘制区域<xref:System.Windows.Media.Drawing>，或<xref:System.Windows.Media.Visual>。  
    
  
<a name="prereqs"></a>   
## <a name="prerequisites"></a>系统必备  
 要了解本主题，应熟悉 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供的不同画笔类型及其基本功能。 有关介绍，请参阅 [WPF 画笔概述](wpf-brushes-overview.md)。  
  
<a name="image"></a>   
## <a name="paint-an-area-with-an-image"></a>使用图像绘制区域  
 <xref:System.Windows.Media.ImageBrush>使用绘制区域<xref:System.Windows.Media.ImageSource>。 最常见的类型<xref:System.Windows.Media.ImageSource>要用于<xref:System.Windows.Media.ImageBrush>是<xref:System.Windows.Media.Imaging.BitmapImage>，它描述了位图图形。 可以使用<xref:System.Windows.Media.DrawingImage>进行绘制<xref:System.Windows.Media.Drawing>对象，但它是使用简单得多<xref:System.Windows.Media.DrawingBrush>相反。 有关详细信息<xref:System.Windows.Media.ImageSource>对象，请参阅[图像概述](imaging-overview.md)。  
  
 若要用绘图<xref:System.Windows.Media.ImageBrush>，创建<xref:System.Windows.Media.Imaging.BitmapImage>并将其加载位图内容。 然后，使用<xref:System.Windows.Media.Imaging.BitmapImage>若要设置<xref:System.Windows.Media.ImageBrush.ImageSource%2A>属性的<xref:System.Windows.Media.ImageBrush>。 最后，将应用<xref:System.Windows.Media.ImageBrush>到想要绘制的对象。  在中[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，可以只设置<xref:System.Windows.Media.ImageBrush.ImageSource%2A>属性的<xref:System.Windows.Media.ImageBrush>要加载的图像的路径。  
  
 像所有<xref:System.Windows.Media.Brush>对象，<xref:System.Windows.Media.ImageBrush>可用于绘制形状、 面板、 控件和文本框之类的对象。 下图显示了可以使用实现某些效果<xref:System.Windows.Media.ImageBrush>。  
  
 ![ImageBrush 输出示例](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
使用 ImageBrush 绘制的对象  
  
 默认情况下，<xref:System.Windows.Media.ImageBrush>拉伸其图像以完全填充的区域正在绘制，很可能会扭曲图像绘制的区域是否与映像不同的纵横比。 可以通过更改来更改此行为<xref:System.Windows.Media.TileBrush.Stretch%2A>属性从其默认值<xref:System.Windows.Media.Stretch.Fill>到<xref:System.Windows.Media.Stretch.None>， <xref:System.Windows.Media.Stretch.Uniform>，或<xref:System.Windows.Media.Stretch.UniformToFill>。 因为<xref:System.Windows.Media.ImageBrush>是一种<xref:System.Windows.Media.TileBrush>，可以指定正好如何了图像画笔填充输出区域，甚至创建图案。 有关高级详细信息<xref:System.Windows.Media.TileBrush>功能，请参阅[TileBrush 概述](tilebrush-overview.md)。  
  
<a name="fillingpanelwithimage"></a>   
## <a name="example-paint-an-object-with-a-bitmap-image"></a>示例:使用位图图像绘制对象  
 下面的示例使用<xref:System.Windows.Media.ImageBrush>绘制<xref:System.Windows.Controls.Panel.Background%2A>的<xref:System.Windows.Controls.Canvas>。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/ImageBrushExample.xaml#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/ImageBrushExample.cs#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMImageBrushAsCanvasBackgroundExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/imagebrushexample.vb#graphicsmmimagebrushascanvasbackgroundexamplewholepage)]  
  
<a name="drawingbrushintro"></a>   
## <a name="paint-an-area-with-a-drawing"></a>使用图形绘制区域  
 一个<xref:System.Windows.Media.DrawingBrush>使您能够使用形状、 文本、 图像和视频绘制区域。 图形画笔内部的形状可能会自行绘制使用纯色、 渐变、 图像，或甚至另一个<xref:System.Windows.Media.DrawingBrush>。 下图演示的一些用途<xref:System.Windows.Media.DrawingBrush>。  
  
 ![DrawingBrush 输出示例](./media/wcpsdk-mmgraphics-drawingbrushexamples.png "wcpsdk_mmgraphics_drawingbrushexamples")  
使用 DrawingBrush 绘制的对象  
  
 一个<xref:System.Windows.Media.DrawingBrush>使用绘制区域<xref:System.Windows.Media.Drawing>对象。 一个<xref:System.Windows.Media.Drawing>对象描述可见内容，如形状、 位图、 视频或文本行。 不同类型的图形描述不同类型的内容。 下面是不同类型图形对象的列表。  
  
-   <xref:System.Windows.Media.GeometryDrawing> – 绘制形状。  
  
-   <xref:System.Windows.Media.ImageDrawing> – 绘制图像。  
  
-   <xref:System.Windows.Media.GlyphRunDrawing> – 绘制文本。  
  
-   <xref:System.Windows.Media.VideoDrawing> – 播放音频或视频文件。  
  
-   <xref:System.Windows.Media.DrawingGroup> – 绘制其他绘图。 使用图形组将其他图形合并到单个复合图形。  
  
 有关详细信息<xref:System.Windows.Media.Drawing>对象，请参阅[Drawing 对象概述](drawing-objects-overview.md)。  
  
 像<xref:System.Windows.Media.ImageBrush>、 一个<xref:System.Windows.Media.DrawingBrush>拉伸其<xref:System.Windows.Media.DrawingBrush.Drawing%2A>以填充输出区域。 可以通过更改重写此行为<xref:System.Windows.Media.TileBrush.Stretch%2A>属性从其默认设置为<xref:System.Windows.Media.Stretch.Fill>。 有关更多信息，请参见 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性。  
  
<a name="fillingareawithdrawingbrushexample"></a>   
## <a name="example-paint-an-object-with-a-drawing"></a>示例:使用 Drawing 绘制对象  
 下面的示例显示如何使用三个椭圆形的图形绘制对象。 一个<xref:System.Windows.Media.GeometryDrawing>用于描述椭圆形。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/DrawingBrushExample.xaml#graphicsmmdrawingbrushasbuttonbackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/DrawingBrushExample.cs#graphicsmmdrawingbrushasbuttonbackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMDrawingBrushAsButtonBackgroundExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/drawingbrushexample.vb#graphicsmmdrawingbrushasbuttonbackgroundexample1)]  
  
<a name="visualbrushsection"></a>   
## <a name="paint-an-area-with-a-visual"></a>使用视觉对象绘制区域  
 最灵活、 最强大的所有画笔<xref:System.Windows.Media.VisualBrush>使用绘制区域<xref:System.Windows.Media.Visual>。 一个<xref:System.Windows.Media.Visual>是用作许多有用图形组件的上级的低级别图形类型。 例如， <xref:System.Windows.Window>， <xref:System.Windows.FrameworkElement>，并<xref:System.Windows.Controls.Control>类是所有类型的<xref:System.Windows.Media.Visual>对象。 使用<xref:System.Windows.Media.VisualBrush>，可以绘制区域使用几乎所有[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]图形对象。  
  
> [!NOTE]
>  尽管<xref:System.Windows.Media.VisualBrush>是一种<xref:System.Windows.Freezable>对象，它不能冻结 （使其只读的） 时其<xref:System.Windows.Media.VisualBrush.Visual%2A>属性设置为值`null`。  
  
 有两种方法来指定<xref:System.Windows.Media.VisualBrush.Visual%2A>内容的<xref:System.Windows.Media.VisualBrush>。  
  
-   创建一个新<xref:System.Windows.Media.Visual>并使用它来设置<xref:System.Windows.Media.VisualBrush.Visual%2A>属性的<xref:System.Windows.Media.VisualBrush>。 有关示例，请参阅[示例：使用视觉对象绘制对象](#examplevisualbrush1)下一节。  
  
-   使用现有<xref:System.Windows.Media.Visual>，这将创建目标的重复图像<xref:System.Windows.Media.Visual>。 然后，可以使用<xref:System.Windows.Media.VisualBrush>创建有趣的效果，例如反射和放大效果。 有关示例，请参阅[示例：创建反射](#examplevisualbrush2)部分。  
  
 定义一个新<xref:System.Windows.Media.VisualBrush.Visual%2A>有关<xref:System.Windows.Media.VisualBrush>并且<xref:System.Windows.Media.Visual>是<xref:System.Windows.UIElement>布局系统 （如面板或控件） 上运行<xref:System.Windows.UIElement>及其子元素时<xref:System.Windows.Media.VisualBrush.AutoLayoutContent%2A>属性设置为`true`。 但是，根<xref:System.Windows.UIElement>实质上独立于系统的其余部分： 样式和外部布局不能渗透此边界。 因此，应显式指定根的大小<xref:System.Windows.UIElement>，因为其唯一父级是<xref:System.Windows.Media.VisualBrush>，因此它不能自动调整自身大小到当前所绘制的区域。 有关 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的布局的更多信息，请参阅[布局](../advanced/layout.md)。  
  
 像<xref:System.Windows.Media.ImageBrush>并<xref:System.Windows.Media.DrawingBrush>、<xref:System.Windows.Media.VisualBrush>拉伸其内容以填充输出区域。 可以通过更改重写此行为<xref:System.Windows.Media.TileBrush.Stretch%2A>属性从其默认设置为<xref:System.Windows.Media.Stretch.Fill>。 有关更多信息，请参见 <xref:System.Windows.Media.TileBrush.Stretch%2A> 属性。  
  
<a name="examplevisualbrush1"></a>   
## <a name="example-paint-an-object-with-a-visual"></a>示例:使用视觉对象绘制对象  
 在下面的示例中，许多控件和面板用于绘制矩形。  
  
 [!code-xaml[BrushOverviewExamples_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/VisualBrushExample.xaml#graphicsmmvisualbrushasrectanglebackgroundexample)]  
  
 [!code-csharp[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/CSharp/VisualBrushExample.cs#graphicsmmvisualbrushasrectanglebackgroundexample1)]
 [!code-vb[BrushOverviewExamples_procedural_snip#GraphicsMMVisualBrushAsRectangleBackgroundExample1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushOverviewExamples_procedural_snip/visualbasic/visualbrushexample.vb#graphicsmmvisualbrushasrectanglebackgroundexample1)]  
  
<a name="examplevisualbrush2"></a>   
## <a name="example-create-a-reflection"></a>示例:创建反射  
 前面的示例介绍了如何创建一个新<xref:System.Windows.Media.Visual>用作背景。 此外可以使用<xref:System.Windows.Media.VisualBrush>显示现有视觉对象; 此功能使您能够生成有趣的视觉效果，例如反射和放大。 下面的示例使用<xref:System.Windows.Media.VisualBrush>若要创建的反射<xref:System.Windows.Controls.Border>包含多个元素。 下图显示了此示例生成的输出。  
  
 ![一个反映视觉对象](./media/graphicsmm-visualbrush-reflection-small.jpg "graphicsmm_visualbrush_reflection_small")  
反射的 Visual 对象  
  
 [!code-csharp[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/ReflectionExample.cs#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-vb[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/reflectionexample.vb#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-xaml[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/ReflectionExample.xaml#graphicsmmvisualbrushreflectionexamplewholepage)]  
  
 有关显示如何放大屏幕部分以及如何创建反射的更多示例，请参阅 [VisualBrush 示例](https://go.microsoft.com/fwlink/?LinkID=160049)。  
  
<a name="tilebrush"></a>   
## <a name="tilebrush-features"></a>TileBrush 功能  
 <xref:System.Windows.Media.ImageBrush><xref:System.Windows.Media.DrawingBrush>，并<xref:System.Windows.Media.VisualBrush>类型的<xref:System.Windows.Media.TileBrush>对象。 <xref:System.Windows.Media.TileBrush> 对象提供了大量的控制如何使用图像、 绘图或 visual 绘制区域。 例如，不使用单个拉伸图像绘制区域，而是使用创建图案的一系列平铺图像绘制区域。  
  
 一个<xref:System.Windows.Media.TileBrush>有三个主要组件： 内容、 磁贴和输出区域。  
  
 ![TileBrush 组件](./media/wcpsdk-mmgraphics-defaultcontentprojection2.png "wcpsdk_mmgraphics_defaultcontentprojection2")  
具有单个图块的 TileBrush 的组成部分  
  
 ![平铺的 TileBrush 的组成部分](./media/graphicsmm-tiledprojection.png "graphicsmm_tiledprojection")  
使用多个平铺的 TileBrush 组件  
  
 有关平铺功能的详细信息<xref:System.Windows.Media.TileBrush>对象，请参阅[TileBrush 概述](tilebrush-overview.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.ImageBrush>
- <xref:System.Windows.Media.DrawingBrush>
- <xref:System.Windows.Media.VisualBrush>
- <xref:System.Windows.Media.TileBrush>
- [TileBrush 概述](tilebrush-overview.md)
- [WPF 画笔概述](wpf-brushes-overview.md)
- [图像处理概述](imaging-overview.md)
- [Drawing 对象概述](drawing-objects-overview.md)
- [不透明蒙板概述](opacity-masks-overview.md)
- [WPF 图形呈现概述](wpf-graphics-rendering-overview.md)
- [ImageBrush 示例](https://go.microsoft.com/fwlink/?LinkID=160005)
- [VisualBrush 示例](https://go.microsoft.com/fwlink/?LinkID=160049)
