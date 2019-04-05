---
title: 如何：对 Visual 中的几何图形进行命中测试
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit tests [WPF], on visual objects comprising Geometry objects [WPF]
- visual objects [WPF], hit tests on
- Geometry objects [WPF], visual objects comprising
ms.assetid: 8bf2643f-d7f9-4cb4-9ea6-5b893c23200d
ms.openlocfilehash: e51dd73a65666ffee5958325079e8f06f13ac61b
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57363795"
---
# <a name="how-to-hit-test-geometry-in-a-visual"></a>如何：对 Visual 中的几何图形进行命中测试
此示例演示如何以组成一个或多针对视觉对象执行命中的测试<xref:System.Windows.Media.Geometry>对象。  
  
## <a name="example"></a>示例  
 下面的示例演示如何检索<xref:System.Windows.Media.DrawingGroup>使用的视觉对象从<xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A>方法。 然后，每个绘图的呈现内容执行命中的测试<xref:System.Windows.Media.DrawingGroup>以确定命中了哪个几何图形。  
  
> [!NOTE]
>  在大多数情况下，您将使用<xref:System.Windows.Media.VisualTreeHelper.HitTest%2A>方法，以确定是否在点相交的任何视觉对象呈现内容。  
  
 [!code-csharp[VisualsOverview#VisualsOverviewSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsOverview/CSharp/Window1.xaml.cs#visualsoverviewsnippet4)]
 [!code-vb[VisualsOverview#VisualsOverviewSnippet4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsOverview/visualbasic/window1.xaml.vb#visualsoverviewsnippet4)]  
  
 <xref:System.Windows.Media.Geometry.FillContains%2A>方法是重载的方法，您可以使用指定的命中测试<xref:System.Windows.Point>或<xref:System.Windows.Media.Geometry>。 绘制几何图形时，笔画可以延伸到填充边界之外。 在这种情况下，可能想要调用<xref:System.Windows.Media.Geometry.StrokeContains%2A>除了<xref:System.Windows.Media.Geometry.FillContains%2A>。  
  
 此外可以提供<xref:System.Windows.Media.ToleranceType>用于贝塞尔拉平操作目的。  
  
> [!NOTE]
>  此示例并未考虑可能应用到几何图形中的任何变形或剪裁。 此外，此示例不会使用已设置样式的控件，因为这种控件没有与它直接关联的绘图。  
  
## <a name="see-also"></a>请参阅
- [可视化层中的命中测试](hit-testing-in-the-visual-layer.md)
- [将几何图形用作参数的命中测试](how-to-hit-test-using-geometry-as-a-parameter.md)
