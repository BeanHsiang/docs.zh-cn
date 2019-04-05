---
title: GDI+ 中的基数样条
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- splines [Windows Forms], cardinal
- GDI+, cardinal splines
- cardinal splines
ms.assetid: 09b3797a-6294-422d-9adf-a5a0a7695c0c
ms.openlocfilehash: 6cc57698c8e43aefff0e0a63b0384417483d3b48
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705280"
---
# <a name="cardinal-splines-in-gdi"></a>GDI+ 中的基数样条
基数样条是一系列单个系统联合起来以形成更大的曲线的曲线。 由一系列点和张力参数指定样条。 基数样条平滑地通过在数组; 每个点有没有尖角中的和任何突然更改曲线的拟合度。 下图显示了一系列点和经过集中每个点的基数样条。  
  
 ![基数样条曲线](./media/aboutgdip02-art09.gif "Aboutgdip02_art09")  
  
## <a name="physical-and-mathematical-splines"></a>物理和数学自由绘制曲线  
 物理样条是一个精简的木片或其他灵活的材料。 之前的数学自由绘制曲线问世，设计人员使用物理样条绘制曲线。 设计器会将样条放在一张纸上并定位到一组给定的点。 在设计器可以然后创建一条曲线样条沿绘制的笔或铅笔。 一组给定的点可能会产生各种曲线，具体取决于物理自由绘制曲线的属性。 例如，使用高不易弯曲的样条会产生极其灵活的样条曲线是不同。  
  
 数学自由绘制曲线的公式基于弹性棒的属性，因此生成的数学自由绘制曲线的曲线是类似于一次由物理样条曲线。 就像物理自由绘制曲线的张力不同将生成不同的曲线通过一组给定的点，数学自由绘制曲线的张力参数不同的值与将生成不同的曲线通过一组给定的点。 下图显示了通过一组相同的点的四个基本样条。 显示张力是针对每个样条。 张力 0 对应于无限物理张力，以强制执行点之间最短路径 （直线） 的曲线。 张力为 1 对应于任何物理张力，使样条采用最小完全弯曲的路径。 张力值大于 1，该曲线的行为类似于压缩 spring，推送到需要较长的路径。  
  
 ![基数样条曲线](./media/aboutgdip02-art10.gif "Aboutgdip02_art10")  
  
 在上图中四个自由绘制曲线共享处的起始点的相同切线。 正切值是从起始点绘制到的下一个点沿曲线的行。 同样，在结束点的共享正切值是从结束的点到上一个点上绘制曲线的行。  
  
 若要绘制的基数样条，您需要的实例<xref:System.Drawing.Graphics>类， <xref:System.Drawing.Pen>，和一个数组<xref:System.Drawing.Point>对象的实例<xref:System.Drawing.Graphics>类提供了<xref:System.Drawing.Graphics.DrawCurve%2A>方法，绘制样条，和<xref:System.Drawing.Pen>将存储样条线宽和颜色等的属性。 数组<xref:System.Drawing.Point>对象存储将传递该曲线的点。 下面的代码示例显示了如何绘制经过的点的基数样条`myPointArray`。 第三个参数是张力。  
  
 [!code-csharp[LinesCurvesAndShapes#31](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#31)]
 [!code-vb[LinesCurvesAndShapes#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#31)]  
  
## <a name="see-also"></a>请参阅
- [直线、曲线和形状](lines-curves-and-shapes.md)
- [构造并绘制曲线](constructing-and-drawing-curves.md)
