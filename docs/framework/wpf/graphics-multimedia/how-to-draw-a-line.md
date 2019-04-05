---
title: 如何：绘制线条
ms.date: 03/30/2017
helpviewer_keywords:
- drawing [WPF], lines
- graphics [WPF], lines
- lines [WPF], drawing
ms.assetid: 0513ee01-6b27-4bb3-85f3-3a3e6710d80e
ms.openlocfilehash: a194fad5471cafcb567aa00522a597a4186ef4af
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374176"
---
# <a name="how-to-draw-a-line"></a>如何：绘制线条
此示例演示如何通过使用绘制线条<xref:System.Windows.Shapes.Line>元素。  
  
 若要绘制一条线，请创建<xref:System.Windows.Shapes.Line>元素。 使用其<xref:System.Windows.Shapes.Line.X1%2A>并<xref:System.Windows.Shapes.Line.Y1%2A>属性来设置其开始点; 并使用其<xref:System.Windows.Shapes.Line.X2%2A>和<xref:System.Windows.Shapes.Line.Y2%2A>要设置其终结点的属性。 最后，设置其<xref:System.Windows.Shapes.Shape.Stroke%2A>和<xref:System.Windows.Shapes.Shape.StrokeThickness%2A>因为没有笔画行是不可见。  
  
 设置<xref:System.Windows.Shapes.Shape.Fill%2A>行的元素具有不起作用，由于直线没有内部区域。  
  
 下面的示例绘制内的三个行<xref:System.Windows.Controls.Canvas>元素。  
  
## <a name="example"></a>示例  
 [!code-xaml[drawingwithshapeelements#LineExample1](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingWithShapeElements/CS/lineexample.xaml#lineexample1)]  
  
 此示例摘自一个更大的示例;有关完整示例，请参阅[形状元素示例](https://go.microsoft.com/fwlink/?LinkID=160037)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Shapes.Line>
- [形状元素示例](https://go.microsoft.com/fwlink/?LinkID=160037)
