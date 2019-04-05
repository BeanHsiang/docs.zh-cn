---
title: WPF 中的形状和基本图形概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- shapes [WPF], about shapes
- basic drawing [WPF]
- vector drawing [WPF], overview
- vectors [WPF], drawing
- Shape objects [WPF]
ms.assetid: 66d7a6d6-e3b6-47bc-8dfe-8a1b26f7d901
ms.openlocfilehash: 9852c811b00ee7f8d86b7c1daaaa28f28fa5a89f
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372732"
---
# <a name="shapes-and-basic-drawing-in-wpf-overview"></a>WPF 中的形状和基本图形概述
本主题概述了如何绘制与<xref:System.Windows.Shapes.Shape>对象。 一个<xref:System.Windows.Shapes.Shape>是一种<xref:System.Windows.UIElement>，使您可以在屏幕上绘制一个形状。 由于它们是 UI 元素<xref:System.Windows.Shapes.Shape>对象可以用在<xref:System.Windows.Controls.Panel>元素和多数控件。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 为图形和绘制服务提供多层访问。 在顶层，<xref:System.Windows.Shapes.Shape>对象是易于使用和提供许多有用的功能，例如布局和参与[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]事件系统。  
  
  
<a name="shapes"></a>   
## <a name="shape-objects"></a>形状对象  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了随时可用的大量<xref:System.Windows.Shapes.Shape>对象。  所有形状对象都继承自<xref:System.Windows.Shapes.Shape>类。 可用形状对象包括<xref:System.Windows.Shapes.Ellipse>， <xref:System.Windows.Shapes.Line>， <xref:System.Windows.Shapes.Path>， <xref:System.Windows.Shapes.Polygon>， <xref:System.Windows.Shapes.Polyline>，并<xref:System.Windows.Shapes.Rectangle>。 <xref:System.Windows.Shapes.Shape> 对象共享以下通用属性。  
  
-   <xref:System.Windows.Shapes.Shape.Stroke%2A>：介绍了如何绘制形状的轮廓。  
  
-   <xref:System.Windows.Shapes.Shape.StrokeThickness%2A>：描述形状的轮廓的粗细。  
  
-   <xref:System.Windows.Shapes.Shape.Fill%2A>：介绍了如何绘制形状的内部。  
  
-   用于指定坐标和顶点的数据属性，以与设备无关的像素来度量。  
  
 由于它们源自<xref:System.Windows.UIElement>，形状对象可以用在面板和多数控件。 <xref:System.Windows.Controls.Canvas>面板是特别适合用于创建复杂的图形，因为它支持绝对定位子对象。  
  
 <xref:System.Windows.Shapes.Line>类使您能够在两点之间绘制线条。 以下示例演示了指定线坐标和笔划属性的几种方法。  
  
 [!code-xaml[drawingwithshapeelements#LineExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 [!code-cpp[shapesprocedural#ShapesProceduralLine](~/samples/snippets/cpp/VS_Snippets_Wpf/ShapesProcedural/CPP/ShapesProcedural.cpp#shapesproceduralline)]
 [!code-csharp[shapesprocedural#ShapesProceduralLine](~/samples/snippets/csharp/VS_Snippets_Wpf/ShapesProcedural/Csharp/ShapesProcedural.cs#shapesproceduralline)]
 [!code-vb[shapesprocedural#ShapesProceduralLine](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ShapesProcedural/VisualBasic/ShapesProceduralVB.vb#shapesproceduralline)]  
  
 下图显示了呈现<xref:System.Windows.Shapes.Line>。  
  
 ![Line illustration](./media/shape-ovw-line2.gif "shape_ovw_line2")  
  
 尽管<xref:System.Windows.Shapes.Line>确实提供了类<xref:System.Windows.Shapes.Shape.Fill%2A>属性，将其设置没有任何作用，因为<xref:System.Windows.Shapes.Line>没有区域。  
  
 另一个常见形状是<xref:System.Windows.Shapes.Ellipse>。  创建<xref:System.Windows.Shapes.Ellipse>通过定义的形状<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性。 若要绘制一个圆圈，指定<xref:System.Windows.Shapes.Ellipse>其<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>值是否相等。  
  
 [!code-xaml[ShapeOverviews#ShapesOVW1](~/samples/snippets/csharp/VS_Snippets_Wpf/ShapeOverviews/CS/Window1.xaml#shapesovw1)]  
  
 [!code-csharp[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/CSharp/SetBackgroundColorOfShapeExample.cs#setbackgroundcolorofshapecodeexamplewholepage)]
 [!code-vb[brushesmiscsnippets_procedural_snip#SetBackgroundColorOfShapeCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesMiscSnippets_procedural_snip/visualbasic/setbackgroundcolorofshapeexample.vb#setbackgroundcolorofshapecodeexamplewholepage)]  
  
 下图显示了示例的呈现<xref:System.Windows.Shapes.Ellipse>。  
  
 ![Ellipse illustration](./media/shape-ovw-ellipse2.png "shape_ovw_ellipse2")  
  
<a name="paths"></a>   
## <a name="using-paths-and-geometries"></a>使用路径和几何图形  
 <xref:System.Windows.Shapes.Path>类可以绘制曲线和复杂的形状。 这些曲线和形状使用描述<xref:System.Windows.Media.Geometry>对象。 若要使用<xref:System.Windows.Shapes.Path>，创建<xref:System.Windows.Media.Geometry>并使用它来设置<xref:System.Windows.Shapes.Path>对象的<xref:System.Windows.Shapes.Path.Data%2A>属性。  
  
 有各种<xref:System.Windows.Media.Geometry>对象可供选择。 <xref:System.Windows.Media.LineGeometry>， <xref:System.Windows.Media.RectangleGeometry>，和<xref:System.Windows.Media.EllipseGeometry>类描述了相对简单的形状。 若要创建更复杂的形状或创建曲线，使用<xref:System.Windows.Media.PathGeometry>。  
  
<a name="pathgeometry"></a>   
### <a name="pathgeometry-and-pathsegments"></a>PathGeometry and PathSegments  
 <xref:System.Windows.Media.PathGeometry> 对象由一个或多个组成<xref:System.Windows.Media.PathFigure>对象; 每个<xref:System.Windows.Media.PathFigure>表示不同"图"或形状。 每个<xref:System.Windows.Media.PathFigure>本身包含一个或多个<xref:System.Windows.Media.PathSegment>对象，每个资源表示图或形状的一个连接的部分。 段类型包括以下类型： <xref:System.Windows.Media.LineSegment>， <xref:System.Windows.Media.BezierSegment>，和<xref:System.Windows.Media.ArcSegment>。  
  
 在以下示例中，<xref:System.Windows.Shapes.Path>用于绘制二次贝塞尔曲线。  
  
 [!code-xaml[geometrysample#34](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#34)]  
  
 下图显示了呈现的形状。  
  
 ![Path illustration](./media/shape-ovw-path2.gif "shape_ovw_path2")  
  
 有关详细信息<xref:System.Windows.Media.PathGeometry>和其他<xref:System.Windows.Media.Geometry>类，请参见[几何概述](geometry-overview.md)。  
  
<a name="pathdatastring"></a>   
### <a name="xaml-abbreviated-syntax"></a>XAML 缩写语法  
 在中[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，还可以使用特殊的缩写的语法来描述<xref:System.Windows.Shapes.Path>。 以下示例中，使用了缩写语法绘制复杂的形状。  
  
```xaml  
      <Path Stroke="DarkGoldenRod" StrokeThickness="3"   
Data="M 100,200 C 100,25 400,350 400,175 H 280" />  
```  
  
 下图显示了呈现<xref:System.Windows.Shapes.Path>。  
  
 ![Path illustration](./media/shape-ovw-path.PNG "shape_ovw_path")  
  
 <xref:System.Windows.Shapes.Path.Data%2A>属性字符串以"moveto"命令，用 M 表示，这建立路径的起始点的坐标系统中<xref:System.Windows.Controls.Canvas>。 <xref:System.Windows.Shapes.Path> 数据参数是区分大小写。 大写字母 M 指示新的当前点的绝对位置。 小写字母 m 指示相对坐标。 第一段是一条三次贝塞尔曲线，该曲线以 (100,200) 开始，至 (400,175) 结束，使用 (100,25) 和 (400,350) 这两个控制点绘制。 此段中的 C 命令指示<xref:System.Windows.Shapes.Path.Data%2A>属性字符串。 同样，大写的 C 指示绝对路径；小写的 c 指示相对路径。  
  
 第二段以绝对水平“lineto”命令 H 开头，它指定绘制一条从前面的子路径的终点 (400,175) 到新终点 (280,175) 的直线。 它是一个水平"lineto"命令，因为指定的值是*x*-协调。  
  
 有关完整的路径语法，请参阅<xref:System.Windows.Shapes.Path.Data%2A>引用和[使用 PathGeometry 创建形状](how-to-create-a-shape-by-using-a-pathgeometry.md)。  
  
<a name="fillpaint"></a>   
## <a name="painting-shapes"></a>绘制形状  
 <xref:System.Windows.Media.Brush> 对象用于绘制的形状<xref:System.Windows.Shapes.Shape.Stroke%2A>和<xref:System.Windows.Shapes.Shape.Fill%2A>。 在下面的示例、 笔划和填充<xref:System.Windows.Shapes.Ellipse>指定。 注意画笔属性的有效输入可以是关键字或十六进制颜色值。 有关可用颜色关键字的详细信息，请参阅的属性<xref:System.Windows.Media.Colors>类中<xref:System.Windows.Media>命名空间。  
  
```xaml
<Canvas Background="LightGray">   
   <Ellipse  
      Canvas.Top="50"  
      Canvas.Left="50"  
      Fill="#FFFFFF00"  
      Height="75"  
      Width="75"  
      StrokeThickness="5"  
      Stroke="#FF0000FF"/>  
</Canvas>  
```  
  
 下图显示了呈现<xref:System.Windows.Shapes.Ellipse>。  
  
 ![椭圆](./media/shape-ovw-ellipsefill.PNG "shape_ovw_ellipsefill")  
  
 或者，可以使用属性元素语法显式创建<xref:System.Windows.Media.SolidColorBrush>对象绘制形状用纯色。  
  
```xaml
<!-- This polygon shape uses pre-defined color values for its Stroke and  
     Fill properties.   
     The SolidColorBrush's Opacity property affects the fill color in   
     this case by making it slightly transparent (opacity of 0.4) so   
     that it blends with any underlying color. -->  
  
<Polygon  
    Points="300,200 400,125 400,275 300,200"  
    Stroke="Purple"   
    StrokeThickness="2">  
    <Polygon.Fill>  
       <SolidColorBrush Color="Blue" Opacity="0.4"/>  
    </Polygon.Fill>  
</Polygon>  
```  
  
 下图显示了呈现的形状。  
  
 ![SolidColorBrush illustration](./media/shape-ovw-solidcolorbrush.PNG "shape_ovw_solidcolorbrush")  
  
 还可以使用渐变、图像、模式等绘制形状的笔划或填充。 有关详细信息，请参阅[使用纯色和渐变概述进行绘制](painting-with-solid-colors-and-gradients-overview.md)。  
  
<a name="stretchableshapessection"></a>   
## <a name="stretchable-shapes"></a>可拉伸的形状  
 <xref:System.Windows.Shapes.Line>， <xref:System.Windows.Shapes.Path>， <xref:System.Windows.Shapes.Polygon>， <xref:System.Windows.Shapes.Polyline>，并<xref:System.Windows.Shapes.Rectangle>类都具有<xref:System.Windows.Shapes.Shape.Stretch%2A>属性。 此属性确定如何<xref:System.Windows.Shapes.Shape>对象的内容 （要绘制的形状） 拉伸以填充<xref:System.Windows.Shapes.Shape>对象的布局空间。 一个<xref:System.Windows.Shapes.Shape>对象的布局空间是空间量<xref:System.Windows.Shapes.Shape>分配由布局系统，是由于显式<xref:System.Windows.FrameworkElement.Width%2A>并<xref:System.Windows.FrameworkElement.Height%2A>设置或由于其<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>和<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>设置。 在 Windows Presentation Foundation 中的布局的其他信息，请参阅[布局](../advanced/layout.md)概述。  
  
 Stretch 属性采用下列值之一：  
  
-   <xref:System.Windows.Media.Stretch.None>：<xref:System.Windows.Shapes.Shape>对象的内容未拉伸。  
  
-   <xref:System.Windows.Media.Stretch.Fill>：<xref:System.Windows.Shapes.Shape>对象的内容被拉伸以填充布局空间。  不保留纵横比。  
  
-   <xref:System.Windows.Media.Stretch.Uniform>：<xref:System.Windows.Shapes.Shape>对象的内容将被拉伸以尽可能以填充布局空间，同时保留原始纵横比。  
  
-   <xref:System.Windows.Media.Stretch.UniformToFill>：<xref:System.Windows.Shapes.Shape>对象的内容被拉伸以完全填充布局空间，同时保留原始纵横比。  
  
 请注意，当<xref:System.Windows.Shapes.Shape>对象的内容将被拉伸，<xref:System.Windows.Shapes.Shape>在拉伸后绘制对象的轮廓。  
  
 在以下示例中，<xref:System.Windows.Shapes.Polygon>用于绘制从 (0，0) 到 (0，1) 很小的三角形到 (1，1)。 <xref:System.Windows.Shapes.Polygon>对象的<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>设置为 100，并且其拉伸属性设置为 Fill。 因此，<xref:System.Windows.Shapes.Polygon>对象的内容 （三角形） 被拉伸以填充较大的空间。  
  
```xaml
<Polygon  
  Points="0,0 0,1 1,1"  
  Fill="Blue"  
  Width="100"  
  Height="100"  
  Stretch="Fill"  
  Stroke="Black"  
  StrokeThickness="2" />  
```

```csharp
PointCollection myPointCollection = new PointCollection();  
myPointCollection.Add(new Point(0,0));  
myPointCollection.Add(new Point(0,1));  
myPointCollection.Add(new Point(1,1));  
  
Polygon myPolygon = new Polygon();  
myPolygon.Points = myPointCollection;  
myPolygon.Fill = Brushes.Blue;  
myPolygon.Width = 100;  
myPolygon.Height = 100;  
myPolygon.Stretch = Stretch.Fill;  
myPolygon.Stroke = Brushes.Black;  
myPolygon.StrokeThickness = 2;  
```

<a name="transforms"></a>   
## <a name="transforming-shapes"></a>转换形状  
 <xref:System.Windows.Media.Transform>类提供了转换形状在二维平面中的方法。  不同类型的转换包括旋转 (<xref:System.Windows.Media.RotateTransform>)，小数位数 (<xref:System.Windows.Media.ScaleTransform>)、 倾斜 (<xref:System.Windows.Media.SkewTransform>)，和转换 (<xref:System.Windows.Media.TranslateTransform>)。  
  
 应用于形状的常见转换就是旋转。  若要旋转形状，创建<xref:System.Windows.Media.RotateTransform>并指定其<xref:System.Windows.Media.RotateTransform.Angle%2A>。 <xref:System.Windows.Media.RotateTransform.Angle%2A>的 45 将元素旋转 45 度顺时针旋转; 90 的角度将元素旋转 90 度顺时针旋转; 依此类推。 设置<xref:System.Windows.Media.RotateTransform.CenterX%2A>和<xref:System.Windows.Media.RotateTransform.CenterY%2A>属性，如果你想要控制元素旋转所围绕的点。 这些属性值在被转换的元素的坐标空间中表示。 <xref:System.Windows.Media.RotateTransform.CenterX%2A> 和<xref:System.Windows.Media.RotateTransform.CenterY%2A>默认值为零。 最后，将应用<xref:System.Windows.Media.RotateTransform>到元素。 如果不希望转换影响布局，设置形状的<xref:System.Windows.UIElement.RenderTransform%2A>属性。  
  
 在以下示例中，<xref:System.Windows.Media.RotateTransform>用于旋转形状的左上角 (0，0) 形状 45 度。  
  
 [!code-xaml[transformssample#14](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#14)]  
  
 在以下示例中，另一个形状也旋转了 45 度，但这次它围绕点 (25,50) 旋转。  
  
 [!code-xaml[transformssample#15](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/RotateTransformExample.xaml#15)]  
  
 下图显示了应用两次转换的结果。  
  
 ![围绕不同中心点旋转 45 度](./media/wcpsdk-graphicsmm-rotatetransform45degrees.gif "wcpsdk_graphicsmm_rotatetransform45degrees")  
  
 在前面的示例中，对每一个形状对象应用了一次转换。 若要将多个转换应用到一个形状 （或任何其他 UI 元素），使用<xref:System.Windows.Media.TransformGroup>。  
  
## <a name="see-also"></a>请参阅
- [2D 图形和图像处理](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [使用纯色和渐变进行绘制概述](painting-with-solid-colors-and-gradients-overview.md)
- [Geometry 概述](geometry-overview.md)
- [演练：我的第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
- [动画概述](animation-overview.md)
