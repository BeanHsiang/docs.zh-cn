---
title: Drawing 对象概述
ms.date: 03/30/2017
helpviewer_keywords:
- ImageDrawing objects [WPF]
- GlyphRunDrawing objects [WPF]
- GeometryDrawing objects [WPF]
- drawings [WPF], about drawings
- Drawing objects [WPF]
- DrawingGroup objects [WPF]
ms.assetid: 9b5ce5c0-e204-4320-a7a8-0b2210d62f88
ms.openlocfilehash: 3589ba1d13c4ec57cfcec8c52b61556344e8def2
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368332"
---
# <a name="drawing-objects-overview"></a>Drawing 对象概述
本主题介绍<xref:System.Windows.Media.Drawing>对象，并说明如何使用它们来有效地绘制形状、 位图、 文本和媒体。 使用<xref:System.Windows.Media.Drawing>对象在创建剪贴画时绘制<xref:System.Windows.Media.DrawingBrush>，或使用<xref:System.Windows.Media.Visual>对象。  
  
 
  
<a name="whatisadrawingsection"></a>   
## <a name="what-is-a-drawing-object"></a>什么是 Drawing 对象？  
 一个<xref:System.Windows.Media.Drawing>对象描述可见内容，如形状、 位图、 视频或文本行。 不同类型的图形描述不同类型的内容。 下面是不同类型图形对象的列表。  
  
-   <xref:System.Windows.Media.GeometryDrawing> – 绘制形状。  
  
-   <xref:System.Windows.Media.ImageDrawing> – 绘制图像。  
  
-   <xref:System.Windows.Media.GlyphRunDrawing> – 绘制文本。  
  
-   <xref:System.Windows.Media.VideoDrawing> – 播放音频或视频文件。  
  
-   <xref:System.Windows.Media.DrawingGroup> – 绘制其他绘图。 使用图形组将其他图形合并到单个复合图形。  
  
 <xref:System.Windows.Media.Drawing> 对象具有多种功能;有许多方法可以使用<xref:System.Windows.Media.Drawing>对象。  
  
-   您可以通过将其显示为图像<xref:System.Windows.Media.DrawingImage>和一个<xref:System.Windows.Controls.Image>控件。  
  
-   可以使用其与<xref:System.Windows.Media.DrawingBrush>绘制一个对象，如<xref:System.Windows.Controls.Page.Background%2A>的<xref:System.Windows.Controls.Page>。  
  
-   可以使用它来描述的外观<xref:System.Windows.Media.DrawingVisual>。  
  
-   可用来枚举的内容<xref:System.Windows.Media.Visual>。  
  
 WPF 提供能够绘制形状、位图、文本和媒体的其他对象类型。 例如，您还可以使用<xref:System.Windows.Shapes.Shape>对象绘制形状，和<xref:System.Windows.Controls.MediaElement>控件提供了另一种方法将视频添加到你的应用程序。 因此何时应使用<xref:System.Windows.Media.Drawing>对象？ 当可以牺牲框架级别功能来获得性能优势或需要<xref:System.Windows.Freezable>功能。 因为<xref:System.Windows.Media.Drawing>对象缺乏对支持[布局](../advanced/layout.md)、 输入和焦点，它们提供性能优势，使它们非常适合用于描述背景、 剪贴画，以及与低级别绘图<xref:System.Windows.Media.Visual>对象。  
  
 因为它们是一种<xref:System.Windows.Freezable>对象，<xref:System.Windows.Media.Drawing>对象具有一些特殊功能，包括以下： 它们可以声明为[资源](../advanced/xaml-resources.md)、 在多个对象，变为只读以提高共享性能、 克隆以及变为线程安全。 有关所提供的不同功能的详细信息<xref:System.Windows.Freezable>对象，请参阅[Freezable 对象概述](../advanced/freezable-objects-overview.md)。  
  
<a name="drawinggeometriessection"></a>   
## <a name="draw-a-shape"></a>绘制形状  
 若要绘制形状，请使用<xref:System.Windows.Media.GeometryDrawing>。 几何绘图<xref:System.Windows.Media.GeometryDrawing.Geometry%2A>属性描述要绘制的形状及其<xref:System.Windows.Media.GeometryDrawing.Brush%2A>属性描述应如何绘制形状的内部，并将其<xref:System.Windows.Media.GeometryDrawing.Pen%2A>属性描述应如何绘制其轮廓。  
  
 下面的示例使用<xref:System.Windows.Media.GeometryDrawing>绘制形状。 由描述形状<xref:System.Windows.Media.GeometryGroup>和两个<xref:System.Windows.Media.EllipseGeometry>对象。 用来绘制形状内部<xref:System.Windows.Media.LinearGradientBrush>并使用绘制其轮廓<xref:System.Windows.Media.Brushes.Black%2A> <xref:System.Windows.Media.Pen>。  
  
 此示例将创建以下<xref:System.Windows.Media.GeometryDrawing>。  
  
 ![两个椭圆的 GeometryDrawing](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
一个 GeometryDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GeometryDrawingExample.cs#geometrydrawingexampleinline)]
 [!code-xaml[DrawingMiscSnippets_snip#GeometryDrawingExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GeometryDrawingExample.xaml#geometrydrawingexampleinline)]  
  
 有关完整示例，请参阅[创建 GeometryDrawing](how-to-create-a-geometrydrawing.md)。  
  
 其他<xref:System.Windows.Media.Geometry>类，如<xref:System.Windows.Media.PathGeometry>，可以通过创建曲线和弧线来创建更复杂的形状。 有关详细信息<xref:System.Windows.Media.Geometry>对象，请参阅[Geometry 概述](geometry-overview.md)。  
  
 有关其他方法来绘制形状不使用的详细信息<xref:System.Windows.Media.Drawing>对象，请参阅[形状和基本绘图中 WPF 概述](shapes-and-basic-drawing-in-wpf-overview.md)。  
  
<a name="drawingimagessection"></a>   
## <a name="draw-an-image"></a>绘制图像  
 若要绘制图像，请使用<xref:System.Windows.Media.ImageDrawing>。 <xref:System.Windows.Media.ImageDrawing>对象的<xref:System.Windows.Media.ImageDrawing.ImageSource%2A>属性描述要绘制图像，并将其<xref:System.Windows.Media.ImageDrawing.Rect%2A>属性定义绘制图像的区域。  
  
 以下示例将在一个矩形的 (75,75) 处绘制一个 100 x 100 像素的图像。 下图显示<xref:System.Windows.Media.ImageDrawing>创建的示例。 添加了灰色边框以显示的边界<xref:System.Windows.Media.ImageDrawing>。  
  
 ![100 的 100 ImageDrawing 绘制在&#40;75，75&#41;](./media/graphicsmm-simple-imagedrawing-offset.png "graphicsmm_simple_imagedrawing_offset")  
100 x 100 的 ImageDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/ImageDrawingExample.cs#imagedrawing100by100inline)]
 [!code-xaml[DrawingMiscSnippets_snip#ImageDrawing100by100Inline](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/ImageDrawingExample.xaml#imagedrawing100by100inline)]  
  
 有关图像的详细信息，请参阅[图像处理概述](imaging-overview.md)。  
  
<a name="playmedia"></a>   
## <a name="play-media-code-only"></a>播放媒体（仅代码）  
  
> [!NOTE]
>  虽然可以声明<xref:System.Windows.Media.VideoDrawing>在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，仅可以加载并播放其媒体使用的代码。 若要播放视频[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，使用<xref:System.Windows.Controls.MediaElement>相反。  
  
 若要播放音频或视频文件，请使用<xref:System.Windows.Media.VideoDrawing>和一个<xref:System.Windows.Media.MediaPlayer>。 加载并播放媒体有两种方法。 第一种是使用<xref:System.Windows.Media.MediaPlayer>和一个<xref:System.Windows.Media.VideoDrawing>通过本身，第二个方法是创建您自己<xref:System.Windows.Media.MediaTimeline>要用于<xref:System.Windows.Media.MediaPlayer>和<xref:System.Windows.Media.VideoDrawing>。  
  
> [!NOTE]
>  当媒体随应用程序一起分发时，无法像图像那样将媒体文件用作项目资源。 在项目文件中，必须改为将媒体类型设置为 `Content` 并将 `CopyToOutputDirectory` 设置为 `PreserveNewest` 或 `Always`。  
  
 若要播放的媒体，而无需创建您自己<xref:System.Windows.Media.MediaTimeline>，执行以下步骤。  
  
1.  创建 <xref:System.Windows.Media.MediaPlayer> 对象。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline1)]  
  
2.  使用<xref:System.Windows.Media.MediaPlayer.Open%2A>方法加载媒体文件。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline2](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline2)]  
  
3.  创建 <xref:System.Windows.Media.VideoDrawing>。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline3](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline3)]  
  
4.  指定的大小和位置，通过设置绘制媒体<xref:System.Windows.Media.VideoDrawing.Rect%2A>属性的<xref:System.Windows.Media.VideoDrawing>。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline4](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline4)]  
  
5.  设置<xref:System.Windows.Media.VideoDrawing.Player%2A>的属性<xref:System.Windows.Media.VideoDrawing>与<xref:System.Windows.Media.MediaPlayer>创建。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline5](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline5)]  
  
6.  使用<xref:System.Windows.Media.MediaPlayer.Play%2A>方法的<xref:System.Windows.Media.MediaPlayer>开始播放媒体。  
  
     [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline6](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline6)]  
  
 下面的示例使用<xref:System.Windows.Media.VideoDrawing>和一个<xref:System.Windows.Media.MediaPlayer>播放视频文件一次。  
  
 [!code-csharp[DrawingMiscSnippets_snip#VideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#videodrawingexampleinline)]  
  
 若要获得对媒体的额外计时控制，请使用<xref:System.Windows.Media.MediaTimeline>与<xref:System.Windows.Media.MediaPlayer>和<xref:System.Windows.Media.VideoDrawing>对象。 <xref:System.Windows.Media.MediaTimeline>使您能够指定是否应重复显示视频。 若要使用<xref:System.Windows.Media.MediaTimeline>与<xref:System.Windows.Media.VideoDrawing>，执行以下步骤：  
  
1.  声明<xref:System.Windows.Media.MediaTimeline>并设置其计时行为。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline1)]  
  
2.  创建<xref:System.Windows.Media.MediaClock>从<xref:System.Windows.Media.MediaTimeline>。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline2](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline2)]  
  
3.  创建<xref:System.Windows.Media.MediaPlayer>并用<xref:System.Windows.Media.MediaClock>若要设置其<xref:System.Windows.Media.MediaPlayer.Clock%2A>属性。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline3](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline3)]  
  
4.  创建<xref:System.Windows.Media.VideoDrawing>，并将分配<xref:System.Windows.Media.MediaPlayer>到<xref:System.Windows.Media.VideoDrawing.Player%2A>属性的<xref:System.Windows.Media.VideoDrawing>。  
  
     [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline4](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline4)]  
  
 下面的示例使用<xref:System.Windows.Media.MediaTimeline>与<xref:System.Windows.Media.MediaPlayer>和一个<xref:System.Windows.Media.VideoDrawing>以重复播放视频。  
  
 [!code-csharp[DrawingMiscSnippets_snip#RepeatingVideoDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/VideoDrawingExample.cs#repeatingvideodrawingexampleinline)]  
  
 请注意，当您使用<xref:System.Windows.Media.MediaTimeline>，使用交互式<xref:System.Windows.Media.Animation.ClockController>从返回<xref:System.Windows.Media.Animation.Clock.Controller%2A>属性<xref:System.Windows.Media.MediaClock>而不是交互式的方法控制媒体播放<xref:System.Windows.Media.MediaPlayer>。  
  
<a name="drawtext"></a>   
## <a name="draw-text"></a>绘制文本  
 若要绘制的文本，请使用<xref:System.Windows.Media.GlyphRunDrawing>和一个<xref:System.Windows.Media.GlyphRun>。 下面的示例使用<xref:System.Windows.Media.GlyphRunDrawing>绘制文本"Hello World"。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/GlyphRunDrawingExample.cs#glyphrundrawingexampleinline)]
 [!code-xaml[DrawingMiscSnippets_snip#GlyphRunDrawingExampleInline](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/GlyphRunExample.xaml#glyphrundrawingexampleinline)]  
  
 一个<xref:System.Windows.Media.GlyphRun>是适用于固定格式文档演示和打印方案的低级别对象。 在屏幕上绘制文本的更简单方法是使用<xref:System.Windows.Controls.Label>或<xref:System.Windows.Controls.TextBlock>。 有关详细信息<xref:System.Windows.Media.GlyphRun>，请参阅[GlyphRun 对象和 Glyphs 元素简介](../advanced/introduction-to-the-glyphrun-object-and-glyphs-element.md)概述。  
  
<a name="compositedrawingssection"></a>   
## <a name="composite-drawings"></a>复合绘图  
 一个<xref:System.Windows.Media.DrawingGroup>可以合并到单个复合图形的多个绘图。 通过使用<xref:System.Windows.Media.DrawingGroup>，可以将形状、 图像和文本合并到单个<xref:System.Windows.Media.Drawing>对象。  
  
 下面的示例使用<xref:System.Windows.Media.DrawingGroup>以组合两个<xref:System.Windows.Media.GeometryDrawing>对象和一个<xref:System.Windows.Media.ImageDrawing>对象。 本示例生成以下输出。  
  
 ![具有多个绘图的 DrawingGroup](./media/graphicsmm-simple.jpg "graphicsmm_simple")  
复合绘图  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingGroupExample.cs#graphicsmmsimpledrawinggroupexample)]
 [!code-xaml[DrawingMiscSnippets_snip#GraphicsMMSimpleDrawingGroupExample](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingGroupExample.xaml#graphicsmmsimpledrawinggroupexample)]  
  
 一个<xref:System.Windows.Media.DrawingGroup>还使您能够对其内容应用不透明蒙板、 转换、 位图效果和其他操作。 <xref:System.Windows.Media.DrawingGroup> 操作按以下顺序应用： <xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>， <xref:System.Windows.Media.DrawingGroup.Opacity%2A>， <xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>， <xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>， <xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>，，然后<xref:System.Windows.Media.DrawingGroup.Transform%2A>。  
  
 下图中的显示顺序<xref:System.Windows.Media.DrawingGroup>操作将应用。  
  
 ![DrawingGroup 操作顺序](./media/graphcismm-drawinggroup-order.png "graphcismm_drawinggroup_order")  
DrawingGroup 操作的顺序  
  
 下表介绍可用于操作的属性<xref:System.Windows.Media.DrawingGroup>对象的内容。  
  
|属性|描述|图示|  
|--------------|-----------------|------------------|  
|<xref:System.Windows.Media.DrawingGroup.OpacityMask%2A>|更改选定部分的不透明度<xref:System.Windows.Media.DrawingGroup>内容。 有关示例，请参见 [如何：控制绘图的不透明度](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms748242(v=vs.90))。|![具有不透明蒙版的 DrawingGroup](./media/graphicsmm-opmask.png "graphicsmm_opmask")|  
|<xref:System.Windows.Media.DrawingGroup.Opacity%2A>|统一更改的不透明度<xref:System.Windows.Media.DrawingGroup>内容。 使用此属性可以使<xref:System.Windows.Media.Drawing>透明或部分透明。 有关示例，请参见 [如何：向绘图应用不透明蒙板](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms753195(v=vs.90))。|![具有不同不透明度设置的 DrawingGroup](./media/graphicsmm-opacity.png "graphicsmm_opacity")|  
|<xref:System.Windows.Media.DrawingGroup.BitmapEffect%2A>|适用<xref:System.Windows.Media.Effects.BitmapEffect>到<xref:System.Windows.Media.DrawingGroup>内容。 有关示例，请参见 [如何：向绘图应用 BitmapEffect](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752341(v=vs.90))。|![具有 BlurBitmapEffect 的 DrawingGroup](./media/graphicsmm-bitmap.png "graphicsmm_bitmap")|  
|<xref:System.Windows.Media.DrawingGroup.ClipGeometry%2A>|剪辑<xref:System.Windows.Media.DrawingGroup>内容区域向您介绍如何使用<xref:System.Windows.Media.Geometry>。 有关示例，请参见 [如何：剪裁绘图](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms743068(v=vs.90))。|![具有定义的剪裁区域的 DrawingGroup](./media/graphicsmm-clipgeom.png "graphicsmm_clipgeom")|  
|<xref:System.Windows.Media.DrawingGroup.GuidelineSet%2A>|根据指定的基准将与设备无关的像素与设备像素对齐。 此属性对于确保细节丰富的图形在低 DPI 屏幕上清晰地呈现很有用。 有关示例，请参阅[向绘图应用 GuidelineSet](how-to-apply-a-guidelineset-to-a-drawing.md)。|![具有和没有 GuidelineSet 的 DrawingGroup](./media/graphicsmm-drawinggroup-guidelineset.png "graphicsmm_drawinggroup_guidelineset")|  
|<xref:System.Windows.Media.DrawingGroup.Transform%2A>|转换<xref:System.Windows.Media.DrawingGroup>内容。 有关示例，请参见 [如何：向绘图应用转换](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms742304(v=vs.90))。|![旋转后的 DrawingGroup](./media/graphicsmm-rotate.png "graphicsmm_rotate")|  
  
<a name="usingimagedrawing"></a>   
## <a name="display-a-drawing-as-an-image"></a>将绘图显示为图像  
 若要显示<xref:System.Windows.Media.Drawing>与<xref:System.Windows.Controls.Image>控制，请使用<xref:System.Windows.Media.DrawingImage>作为<xref:System.Windows.Controls.Image>控件的<xref:System.Windows.Controls.Image.Source%2A>并设置<xref:System.Windows.Media.DrawingImage>对象的<xref:System.Windows.Media.DrawingImage.Drawing%2A?displayProperty=nameWithType>属性设置为你想要显示的绘图。  
  
 下面的示例使用<xref:System.Windows.Media.DrawingImage>和一个<xref:System.Windows.Controls.Image>控件来显示<xref:System.Windows.Media.GeometryDrawing>。 本示例生成以下输出。  
  
 ![两个椭圆的 GeometryDrawing](./media/graphicsmm-geodraw.jpg "graphicsmm_geodraw")  
一个 DrawingImage  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingImageExample.cs#drawingimageexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#DrawingImageExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingImageExample.xaml#drawingimageexamplewholepage)]  
  
<a name="renderingwithdrawingbrushsection"></a>   
## <a name="paint-an-object-with-a-drawing"></a>使用 Drawing 绘制对象  
 一个<xref:System.Windows.Media.DrawingBrush>是一种使用 drawing 对象绘制区域的画笔。 几乎可以使用它绘制任何带有绘图的图形对象。 <xref:System.Windows.Media.Drawing>的属性<xref:System.Windows.Media.DrawingBrush>介绍了其<xref:System.Windows.Media.DrawingBrush.Drawing%2A>。 若要呈现<xref:System.Windows.Media.Drawing>与<xref:System.Windows.Media.DrawingBrush>，将其添加到使用画笔的画笔<xref:System.Windows.Media.Drawing>属性，然后使用画笔绘制图形对象，如控件或面板。  
  
 以下示例使用<xref:System.Windows.Media.DrawingBrush>绘制<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Rectangle>从创建的图案<xref:System.Windows.Media.GeometryDrawing>。 本示例生成以下输出。  
  
 ![平铺的 DrawingBrush](./media/graphicsmm-drawingbrush-geometrydrawing.png "graphicsmm_drawingbrush_geometrydrawing")  
与 DrawingBrush 结合使用的 GeometryDrawing  
  
 [!code-csharp[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/DrawingBrushExample.cs#drawingbrushexamplewholepage)]
 [!code-xaml[DrawingMiscSnippets_snip#DrawingBrushExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/DrawingMiscSnippets_snip/XAML/DrawingBrushExample.xaml#drawingbrushexamplewholepage)]  
  
 <xref:System.Windows.Media.DrawingBrush>类提供了各种用于拉伸和平铺其内容的选项。 有关详细信息<xref:System.Windows.Media.DrawingBrush>，请参阅[使用图像、 绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)概述。  
  
<a name="renderingwithvisualsection"></a>   
## <a name="render-a-drawing-with-a-visual"></a>使用视觉对象呈现绘图  
 一个<xref:System.Windows.Media.DrawingVisual>是一种旨在呈现绘图的视觉对象。 对于希望生成高度自定义的图形环境的开发者来说，可以选择直接在视觉对象层上工作，但在本概述中不作介绍。 有关详细信息，请参阅[使用 DrawingVisual 对象](using-drawingvisual-objects.md)概述。  
  
<a name="drawingcontextobjects"></a>   
## <a name="drawingcontext-objects"></a>DrawingContext 对象  
 <xref:System.Windows.Media.DrawingContext>类使你能够填充<xref:System.Windows.Media.Visual>或<xref:System.Windows.Media.Drawing>可视化内容。 许多此类低级别图形对象使用<xref:System.Windows.Media.DrawingContext>因为它非常高效地描述图形内容。  
  
 尽管<xref:System.Windows.Media.DrawingContext>绘制方法看起来类似于的绘制方法<xref:System.Drawing.Graphics?displayProperty=nameWithType>类型，它们为实际大不相同。 <xref:System.Windows.Media.DrawingContext> 是用于保留的模式图形系统，而<xref:System.Drawing.Graphics?displayProperty=nameWithType>类型用于即时模式图形系统。 当你使用<xref:System.Windows.Media.DrawingContext>对象的绘图命令时，实际上存储组绘制指令 (尽管具体的存储机制取决于提供的对象的类型<xref:System.Windows.Media.DrawingContext>)，稍后将使用由图形系统; 你都不绘制到屏幕上实时。 有关 Windows Presentation Foundation (WPF) 图形系统的工作原理的详细信息，请参阅[WPF 图形呈现概述](wpf-graphics-rendering-overview.md)。  
  
 您永远不会直接实例化<xref:System.Windows.Media.DrawingContext>; 但是，可以获取绘图上下文通过某些方法，如<xref:System.Windows.Media.DrawingGroup.Open%2A?displayProperty=nameWithType>和<xref:System.Windows.Media.DrawingVisual.RenderOpen%2A?displayProperty=nameWithType>。  
  
<a name="enumeratevisualcontents"></a>   
## <a name="enumerate-the-contents-of-a-visual"></a>枚举 Visual 的内容  
 除了其其他用途，请<xref:System.Windows.Media.Drawing>对象还提供用于枚举的内容的对象模型<xref:System.Windows.Media.Visual>。  
  
 下面的示例使用<xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A>方法来检索<xref:System.Windows.Media.DrawingGroup>的值<xref:System.Windows.Media.Visual>并枚举该值。  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Drawing>
- <xref:System.Windows.Media.DrawingGroup>
- [2D 图形和图像处理](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [使用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)
- [Geometry 概述](geometry-overview.md)
- [WPF 中的形状和基本绘图概述](shapes-and-basic-drawing-in-wpf-overview.md)
- [WPF 图形呈现概述](wpf-graphics-rendering-overview.md)
- [Freezable 对象概述](../advanced/freezable-objects-overview.md)
- [帮助主题](drawings-how-to-topics.md)
