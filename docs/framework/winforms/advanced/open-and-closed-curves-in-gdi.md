---
title: GDI+ 中的开放曲线和闭合曲线
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- curves [Windows Forms], filling
- GDI+, curves
- curves [Windows Forms], drawing
- curves
ms.assetid: 08d2cc9a-dc9d-4eed-bcbb-2c8e2ca5d3ae
ms.openlocfilehash: bc78077be45f22826eaa23a746dcf272601d51b4
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711455"
---
# <a name="open-and-closed-curves-in-gdi"></a>GDI+ 中的开放曲线和闭合曲线
下图显示了两条曲线： 一个打开和关闭。  
  
 ![开放曲线和闭合曲线](./media/aboutgdip02-art24.gif "Aboutgdip02_art24")  
  
## <a name="managed-interface-for-curves"></a>曲线的管理的界面  
 已关闭的曲线具有内部，因此可以使用画笔填充。 <xref:System.Drawing.Graphics>类中[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]提供了用于填充绘制闭合的形状和曲线的以下方法： <xref:System.Drawing.Graphics.FillRectangle%2A>， <xref:System.Drawing.Graphics.FillEllipse%2A>， <xref:System.Drawing.Graphics.FillPie%2A>， <xref:System.Drawing.Graphics.FillPolygon%2A>， <xref:System.Drawing.Graphics.FillClosedCurve%2A>， <xref:System.Drawing.Graphics.FillPath%2A>，和<xref:System.Drawing.Graphics.FillRegion%2A>。 无论您调用下列方法之一，您必须通过一个特定的画笔类型 (<xref:System.Drawing.SolidBrush>， <xref:System.Drawing.Drawing2D.HatchBrush>， <xref:System.Drawing.TextureBrush>， <xref:System.Drawing.Drawing2D.LinearGradientBrush>，或<xref:System.Drawing.Drawing2D.PathGradientBrush>) 作为参数。  
  
 <xref:System.Drawing.Graphics.FillPie%2A>方法是一起提供<xref:System.Drawing.Graphics.DrawArc%2A>方法。 就像<xref:System.Drawing.Graphics.DrawArc%2A>方法绘制的椭圆的边框的一部分<xref:System.Drawing.Graphics.FillPie%2A>方法填充的椭圆的内部的一部分。 下面的示例绘制一段弧线，并填充椭圆的内部的相应部分：  
  
 [!code-csharp[LinesCurvesAndShapes#21](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#21)]
 [!code-vb[LinesCurvesAndShapes#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#21)]  
  
 下图显示了弧线和已填充的饼图。  
  
 ![开放曲线和闭合曲线](./media/aboutgdip02-art25.gif "Aboutgdip02_art25")  
  
 <xref:System.Drawing.Graphics.FillClosedCurve%2A>方法是一起提供<xref:System.Drawing.Graphics.DrawClosedCurve%2A>方法。 这两种方法会自动通过连接到的起始点的结束点闭合曲线。 下面的示例绘制传递一条曲线 （0，0） （60，20） 和 （40、 50）。 然后，通过连接自动关闭曲线 （40、 50） 到起始点 （0，0），并使用纯色填充其内部。  
  
 [!code-csharp[LinesCurvesAndShapes#22](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#22)]
 [!code-vb[LinesCurvesAndShapes#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#22)]  
  
 <xref:System.Drawing.Graphics.FillPath%2A>方法填充的路径的不同部分的内部。 如果路径的一段不会形成闭合的曲线或形状，<xref:System.Drawing.Graphics.FillPath%2A>方法会自动填充它之前关闭该路径的段。 下面的示例绘制并填充一段弧线、 基数样条、 字符串和饼图组成的路径：  
  
 [!code-csharp[LinesCurvesAndShapes#23](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#23)]
 [!code-vb[LinesCurvesAndShapes#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#23)]  
  
 下图显示使用和不使用纯色填充的路径。 请注意，在字符串中的文本是所述，但未填充，由<xref:System.Drawing.Graphics.DrawPath%2A>方法。 它是<xref:System.Drawing.Graphics.FillPath%2A>绘制的字符串中字符的内部的方法。  
  
 ![在路径中的字符串](./media/aboutgdip02-art26.gif "Aboutgdip02_art26")  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=nameWithType>
- <xref:System.Drawing.Pen?displayProperty=nameWithType>
- <xref:System.Drawing.Point?displayProperty=nameWithType>
- [直线、曲线和形状](lines-curves-and-shapes.md)
- [如何：创建用于绘制图形对象](how-to-create-graphics-objects-for-drawing.md)
- [构造并绘制路径](constructing-and-drawing-paths.md)
