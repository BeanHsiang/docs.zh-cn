---
title: 如何：使用多边形元素来绘制闭合形状
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], Polygon elements
- closed shapes [WPF], drawing with Polygon elements
- Polygon elements [WPF]
- drawing [WPF], closed shapes with Polygon elements
ms.assetid: 4b0ca008-29ce-48dd-8bc3-f3a20ffca6a6
ms.openlocfilehash: 533c341e2fae528ec896bf38bafa13974af1d127
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57360027"
---
# <a name="how-to-draw-a-closed-shape-by-using-the-polygon-element"></a>如何：使用多边形元素来绘制闭合形状
此示例演示如何使用来绘制闭合的形状<xref:System.Windows.Shapes.Polygon>元素。 若要绘制闭合的形状，创建<xref:System.Windows.Shapes.Polygon>元素，并使用其<xref:System.Windows.Shapes.Polygon.Points%2A>属性指定形状顶点。 自动绘制连接的第一个和最后一个点行。 最后，指定<xref:System.Windows.Shapes.Shape.Fill%2A>、 <xref:System.Windows.Shapes.Shape.Stroke%2A>，和 / 或。  
  
## <a name="example"></a>示例  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，点的有效语法是以逗号分隔的 x 和 y 坐标对的空格分隔列表。  
  
 [!code-xaml[drawingwithshapeelements#PolygonExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/polygonexample.xaml#polygonexample1)]  
  
 尽管该示例使用<xref:System.Windows.Controls.Canvas>来包含多边形，但是您可以使用多边形元素 （和所有其他形状元素） 以及任何<xref:System.Windows.Controls.Panel>或<xref:System.Windows.Controls.Control>支持非文本内容。  
  
 此示例摘自一个更大的示例;有关完整示例，请参阅[形状元素示例](https://go.microsoft.com/fwlink/?LinkID=160037)。
