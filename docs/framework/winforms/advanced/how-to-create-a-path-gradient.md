---
title: 如何：创建路径渐变
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- path gradients [Windows Forms], creating
- gradients [Windows Forms], creating path
- graphics paths [Windows Forms], creating gradient
ms.assetid: 1948e834-e104-481c-b71d-d8aa9e4d106e
ms.openlocfilehash: cbbffa7b9250c5e489a95f687ea58eaf2a08d1bf
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2019
ms.locfileid: "58126222"
---
# <a name="how-to-create-a-path-gradient"></a>如何：创建路径渐变
<xref:System.Drawing.Drawing2D.PathGradientBrush>类使您可以自定义用渐变颜色填充形状的方式。 例如，可以指定为路径的中心的一种颜色和路径的边界的另一种颜色。 此外可以为每个路径的多个点边界指定单独的颜色。  
  
> [!NOTE]
>  在中[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，路径是一系列直线和曲线由维护<xref:System.Drawing.Drawing2D.GraphicsPath>对象。 有关详细信息[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]路径，请参阅[GDI + 中的图形路径](graphics-paths-in-gdi.md)并[Constructing 和绘制路径](constructing-and-drawing-paths.md)。  
  
### <a name="to-fill-an-ellipse-with-a-path-gradient"></a>使用路径渐变填充椭圆，  
  
-   下面的示例用填充椭圆路径渐变画笔。 从中心色设置为蓝色并的边界颜色设置为浅绿色。 下图显示了实心的椭圆。  
  
     ![渐变路径填充椭圆。](./media/how-to-create-a-path-gradient/gradient-path-filled-ellipse.png)  
  
     默认情况下，路径渐变画笔不会扩展路径的边界之外。 如果路径渐变画笔用于填充图形超出路径的边界，则不会填充路径外部屏幕区域。  
  
     如果更改会发生什么情况如下图所示<xref:System.Drawing.Graphics.FillEllipse%2A>到下面的代码中调用`e.Graphics.FillRectangle(pthGrBrush, 0, 10, 200, 40)`:  
  
     ![渐变路径扩展的路径中的边界之外。](./media/how-to-create-a-path-gradient/gradient-path-extended-beyond-boundary.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#11)]
     [!code-vb[System.Drawing.UsingaGradientBrush#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#11)]  
  
     前面的代码示例设计为使用 Windows 窗体，并且它需要<xref:System.Windows.Forms.PaintEventArgs>e，这是参数的<xref:System.Windows.Forms.PaintEventHandler>。  
  
### <a name="to-specify-points-on-the-boundary"></a>若要指定点的边界上  
  
-   下面的示例构造路径渐变画笔星形路径中。 代码集<xref:System.Drawing.Drawing2D.PathGradientBrush.CenterColor%2A>属性设置为红色的星号的形心处的颜色。 然后代码集<xref:System.Drawing.Drawing2D.PathGradientBrush.SurroundColors%2A>属性来指定不同的颜色 (存储在`colors`数组) 中的各个点处`points`数组。 最终代码语句将填充与路径渐变画笔星形路径。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#12)]
     [!code-vb[System.Drawing.UsingaGradientBrush#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#12)]  
  
-   下面的示例绘制路径渐变，而无需<xref:System.Drawing.Drawing2D.GraphicsPath>在代码中的对象。 特定<xref:System.Drawing.Drawing2D.PathGradientBrush.%23ctor%2A>示例中的构造函数接收的点数组，但不需要<xref:System.Drawing.Drawing2D.GraphicsPath>对象。 另请注意，<xref:System.Drawing.Drawing2D.PathGradientBrush>用于填充矩形，不是路径。 矩形大于封闭路径用于定义画笔，以便画笔不绘制矩形的某些部分。 下图显示了矩形 （虚线） 和路径渐变画笔绘制矩形的部分： 
  
     ![绘制路径渐变画笔的渐变的部分。](./media/how-to-create-a-path-gradient/gradient-painted-path-gradient-brush.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#13](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#13)]
     [!code-vb[System.Drawing.UsingaGradientBrush#13](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#13)]  
  
### <a name="to-customize-a-path-gradient"></a>若要自定义路径渐变  
  
-   若要自定义路径渐变画笔的一种方法是设置其<xref:System.Drawing.Drawing2D.PathGradientBrush.FocusScales%2A>属性。 聚焦缩放指定的内部路径位于主路径内。 在内部轨迹中而不是仅在中心点无处不在显示中心色。  
  
     以下示例创建路径渐变画笔基于椭圆的路径。 代码设置为蓝色的边界颜色、 将 center 颜色设置为水绿色，，然后使用路径渐变画笔填充椭圆的路径。  
  
     接下来，该代码设置路径渐变画笔的聚焦缩放。 X 焦点规模设置为 0.3，并且 y 焦点规模设置为 0.8。 该代码调用<xref:System.Drawing.Graphics.TranslateTransform%2A>方法<xref:System.Drawing.Graphics>对象，以便后续调用<xref:System.Drawing.Graphics.FillPath%2A>填充椭圆位于右侧的第一个椭圆。  
  
     若要查看的聚焦缩放效果，假设其中心共享与主椭圆小型椭圆。 小 （内部） 椭圆是 0.3 的主要的椭圆 （围绕其中心） 横向扩展到原来，在垂直方向 0.8 的因素。 当从外部椭圆的边界移动到内部椭圆的边界时，颜色会逐渐从蓝色为水绿色。 当您移动到共享的中心，颜色保持浅绿色从内部椭圆的边界。  
  
     下图显示以下代码的输出。 在左侧椭圆为仅在中心点的浅绿色。 在右侧的省略号为浅绿色无处不在内部的路径。  
  
 ![渐变效果的焦点规模](./media/how-to-create-a-path-gradient/focus-scales-aqua-inner-outer-ellipse.png)  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#14](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#14)]
 [!code-vb[System.Drawing.UsingaGradientBrush#14](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#14)]  
  
### <a name="to-customize-with-interpolation"></a>若要自定义使用内插  
  
-   若要自定义路径渐变画笔的另一种方法是指定的内插颜色数组和数组的内插位置。  
  
     以下示例创建路径渐变画笔，基于一个三角形。 该代码设置<xref:System.Drawing.Drawing2D.PathGradientBrush.InterpolationColors%2A>指定一个内插颜色 （深绿色、 水绿色、 蓝色） 数组和数组的内插位置 （0，0.25，1） 的路径渐变画笔的属性。 将移到中心点从的三角形的边界，颜色更改逐渐从深绿色为浅绿色，然后从浅绿色变成蓝色。 为浅绿色从深绿色更改发生在从深绿色为蓝色的距离的 25%。  
  
     下图显示了使用自定义路径渐变画笔填充的三角形。  
  
     ![使用自定义路径渐变画笔填充三角形。](./media/how-to-create-a-path-gradient/gradient-brush-filled-triangle.png)  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#15](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#15)]
     [!code-vb[System.Drawing.UsingaGradientBrush#15](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#15)]  
  
### <a name="to-set-the-center-point"></a>若要设置的中心点  
  
-   默认情况下，路径渐变画笔的中心点是路径的在用于构造画笔的形心。 您可以通过设置更改的中心点的位置<xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A>属性的<xref:System.Drawing.Drawing2D.PathGradientBrush>类。  
  
     以下示例创建路径渐变画笔，基于一个椭圆。 椭圆的中心是在 （70、 35），但路径渐变画笔的中心点设置为 120 (40）。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#16](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#16)]
     [!code-vb[System.Drawing.UsingaGradientBrush#16](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#16)]  
  
     下图显示了实心的椭圆和路径渐变画笔的中心点：  
  
     ![渐变填充椭圆和中心点的路径。](./media/how-to-create-a-path-gradient/gradient-path-filled-ellipse-center-point.png)  
  
-   可以将路径渐变画笔的中心点设置为用于构造画笔的路径之外的位置。 下面的示例将用于设置调用<xref:System.Drawing.Drawing2D.PathGradientBrush.CenterPoint%2A>在上述代码中的属性。  
  
     [!code-csharp[System.Drawing.UsingaGradientBrush#17](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#17)]
     [!code-vb[System.Drawing.UsingaGradientBrush#17](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#17)]  
  
     下图显示了进行此更改后的输出：  
  
     ![渐变路径与路径外部的中心点。](./media/how-to-create-a-path-gradient/gradient-path-center-point-outside.png)  
  
     在上图中，在最右侧的椭圆的点不是纯蓝色 （尽管它们非常接近）。 像是填充到颜色将纯蓝色 （0，0，255） 的点 （145、 35） 定位在渐变中的颜色。 但永远不会达到填充 （145、 35） 因为路径渐变画笔绘制仅在其路径内。  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例设计为使用 Windows 窗体，它们需要<xref:System.Windows.Forms.PaintEventArgs> `e`，这是一个参数的<xref:System.Windows.Forms.Control.Paint>事件处理程序。  
  
## <a name="see-also"></a>请参阅
- [使用渐变画笔填充形状](using-a-gradient-brush-to-fill-shapes.md)
