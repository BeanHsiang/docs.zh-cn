---
title: 如何：创建复合形状
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- shapes [WPF], composite
- composite shapes [WPF]
- graphics [WPF], composite shapes
ms.assetid: 8e5c7ef4-d7ed-4c43-afc9-ca01325c300b
ms.openlocfilehash: de9f7972c7a51ea623c3630fe62bb48f6109317e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57353486"
---
# <a name="how-to-create-a-composite-shape"></a>如何：创建复合形状
此示例演示如何创建使用复合形状<xref:System.Windows.Media.Geometry>对象并将其显示使用<xref:System.Windows.Shapes.Path>元素。 在以下示例中， <xref:System.Windows.Media.LineGeometry>， <xref:System.Windows.Media.EllipseGeometry>，和一个<xref:System.Windows.Media.RectangleGeometry>与一起使用<xref:System.Windows.Media.GeometryGroup>创建复合形状。 然后使用绘制几何图形的<xref:System.Windows.Shapes.Path>元素。  
  
## <a name="example"></a>示例  
 [!code-xaml[GeometrySample#19](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#19)]  
  
 [!code-csharp[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/CSharp/CompositeShapeExample.cs#compositeshapecodeexampleinline1)]
 [!code-vb[GeometriesMiscSnippets_procedural_snip#CompositeShapeCodeExampleInline1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/GeometriesMiscSnippets_procedural_snip/visualbasic/compositeshapeexample.vb#compositeshapecodeexampleinline1)]  
  
 下图显示在上一个示例中创建的形状。  
  
 ![使用 GeometryGroup 创建的复合几何图形](./media/wcpsdk-graphicsmm-compositegeometryexample1.jpg "wcpsdk_graphicsmm_compositegeometryexample1")  
复合几何图形  
  
 可以使用创建更复杂的形状的多边形和形状使用曲线段，如<xref:System.Windows.Media.PathGeometry>。 有关示例显示了如何使用创建形状<xref:System.Windows.Media.PathGeometry>，请参阅[使用 PathGeometry 创建形状](how-to-create-a-shape-by-using-a-pathgeometry.md)。  虽然此示例的呈现到屏幕使用形状<xref:System.Windows.Shapes.Path>元素中，<xref:System.Windows.Media.Geometry>也可能会使用对象来描述的内容<xref:System.Windows.Media.GeometryDrawing>或<xref:System.Windows.Media.DrawingContext>。 此外可用于剪辑和命中测试它们。  
  
 此示例是更大示例的组成部分；有关完整示例，请参阅[几何图形示例](https://go.microsoft.com/fwlink/?LinkID=159989)。
