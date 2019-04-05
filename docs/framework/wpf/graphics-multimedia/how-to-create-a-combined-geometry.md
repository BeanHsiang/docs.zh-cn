---
title: 如何：创建组合的几何图形
ms.date: 03/30/2017
helpviewer_keywords:
- combining geometries [WPF]
- graphics [WPF], combining geometries
- geometries [WPF], combining
ms.assetid: 54c3277c-6b6e-4b25-91be-fda0bbc706b4
ms.openlocfilehash: c5ebe87abd4c2cf70f8fa17f1fcc773293f3ad27
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364783"
---
# <a name="how-to-create-a-combined-geometry"></a>如何：创建组合的几何图形
此示例演示如何合并几何图形。 若要组合两个几何图形，使用<xref:System.Windows.Media.CombinedGeometry>对象。 设置其<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>和<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>具有两个几何图形以组合和设置的属性<xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A>属性，用于确定如何将一起组合几何图形，到`Union`， `Intersect`， `Exclude`，或者`Xor`.  
  
 若要从两个或多个几何图形中创建的复合几何图形，请使用<xref:System.Windows.Media.GeometryGroup>。  
  
## <a name="example"></a>示例  
 在以下示例中，<xref:System.Windows.Media.CombinedGeometry>使用的几何图形合并模式定义`Exclude`。  这两<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>和<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>定义为圆的半径相同，但中心偏移 50。  
  
 [!code-xaml[GeometrySample#21](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#21)]  
  
 ![组合模式的排除结果](./media/mil-task-combined-geometry-exclude.PNG "mil_task_combined_geometry_exclude")  
组合的几何图形排除  
  
 在下列标记中，<xref:System.Windows.Media.CombinedGeometry>使用的合并模式定义`Intersect`。  这两<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>和<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>定义为圆的半径相同，但中心偏移 50。  
  
 [!code-xaml[GeometrySample#22](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#22)]  
  
 ![组合模式的 Intersect 结果](./media/mil-task-combined-geometry-intersect.PNG "mil_task_combined_geometry_intersect")  
组合的几何图形相交  
  
 在下列标记中，<xref:System.Windows.Media.CombinedGeometry>使用的合并模式定义`Union`。  这两<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>和<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>定义为圆的半径相同，但中心偏移 50。  
  
 [!code-xaml[GeometrySample#23](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![Results of the Union combine mode](./media/mil-task-combined-geometry-union.PNG "mil_task_combined_geometry_union")  
组合的几何图形并集  
  
 在下列标记中，<xref:System.Windows.Media.CombinedGeometry>使用的合并模式定义`Xor`。  这两<xref:System.Windows.Media.CombinedGeometry.Geometry1%2A>和<xref:System.Windows.Media.CombinedGeometry.Geometry2%2A>定义为圆的半径相同，但中心偏移 50。  
  
 [!code-xaml[GeometrySample#24](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Results of the Xor combine mode](./media/mil-task-combined-geometry-xor.PNG "mil_task_combined_geometry_xor")  
组合的几何图形 Xor
