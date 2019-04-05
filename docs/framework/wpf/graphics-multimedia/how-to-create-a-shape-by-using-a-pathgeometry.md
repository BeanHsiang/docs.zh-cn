---
title: 如何：使用 PathGeometry 创建形状
ms.date: 03/30/2017
helpviewer_keywords:
- shapes [WPF], creating with PathGeometry class
- graphics [WPF], shapes
ms.assetid: 49a4a8b7-e738-45be-8dac-b54a6d8f5b21
ms.openlocfilehash: ce84f2509116207afa200ddf83dcdc1f8101da13
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356195"
---
# <a name="how-to-create-a-shape-by-using-a-pathgeometry"></a>如何：使用 PathGeometry 创建形状
此示例演示如何使用创建形状<xref:System.Windows.Media.PathGeometry>类。 <xref:System.Windows.Media.PathGeometry> 对象组成的一个或多个<xref:System.Windows.Media.PathFigure>对象; 每个<xref:System.Windows.Media.PathFigure>表示不同"图"或形状。 每个<xref:System.Windows.Media.PathFigure>本身由一个或多个<xref:System.Windows.Media.PathSegment>对象，每个资源表示图或形状的一个连接的部分。 线段的类型包括<xref:System.Windows.Media.LineSegment>， <xref:System.Windows.Media.ArcSegment>，和<xref:System.Windows.Media.BezierSegment>。  
  
## <a name="example"></a>示例  
 下面的示例使用<xref:System.Windows.Media.PathGeometry>进而形成一个三角形。 <xref:System.Windows.Media.PathGeometry>将显示使用<xref:System.Windows.Shapes.Path>元素。  
  
 [!code-xaml[GeometrySample#49](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/pathgeometryexample.xaml#49)]  
  
 下图显示在上一个示例中创建的形状。  
  
 ![PathGeometry](./media/wcpsdk-graphicsmm-pathgeometry-triangle.gif "wcpsdk_graphicsmm_pathgeometry_triangle")  
使用 PathGeometry 创建一个三角形  
  
 前面的示例介绍了如何创建一个相对简单的形状，一个三角形。 一个<xref:System.Windows.Media.PathGeometry>还可用于创建更复杂的形状，包括弧线和曲线。 有关示例，请参阅[创建椭圆弧](how-to-create-an-elliptical-arc.md)，[创建三次方贝塞尔曲线](how-to-create-a-cubic-bezier-curve.md)，并[创建二次贝塞尔曲线](how-to-create-a-quadratic-bezier-curve.md)。  
  
 此示例是更大示例的组成部分；有关完整示例，请参阅[几何图形示例](https://go.microsoft.com/fwlink/?LinkID=159989)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.GeometryDrawing>
- [Geometry 概述](geometry-overview.md)
- [几何图形示例](https://go.microsoft.com/fwlink/?LinkID=159989)
