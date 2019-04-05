---
title: 如何：绘制带有线性渐变的区域
ms.date: 03/30/2017
helpviewer_keywords:
- linear gradients [WPF], painting with
- brushes [WPF], painting with linear gradients
- painting [WPF], with linear gradients
ms.assetid: 00e0cd04-48c0-4ec5-850e-d321beb37a34
ms.openlocfilehash: c48ff13811d784ecc7042b73b964a9e6f2d42a34
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367240"
---
# <a name="how-to-paint-an-area-with-a-linear-gradient"></a>如何：绘制带有线性渐变的区域
此示例演示如何使用<xref:System.Windows.Media.LinearGradientBrush>类来绘制带有线性渐变的区域。 在以下示例中，<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Rectangle>用黄色从过渡到红色变为蓝色变为浅绿色对角线方向线性渐变绘制。  
  
## <a name="example"></a>示例  
 [!code-xaml[GradientBrushExamples_snip#DiagonalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#diagonalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#DiagonalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#diagonalgradient1csharp)]  
  
 下图显示上一示例所创建的渐变。  
  
 ![对角线方向线性渐变](./media/graphicsmm-diagonallgb.jpg "graphicsmm_DiagonalLGB")  
  
 若要创建水平方向线性渐变，更改<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>并<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>的<xref:System.Windows.Media.LinearGradientBrush>到 (0,0.5) 和 (1,0.5)。 在以下示例中，<xref:System.Windows.Shapes.Rectangle>使用水平线性渐变绘制。  
  
 [!code-xaml[GradientBrushExamples_snip#HorizontalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#horizontalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#HorizontalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#horizontalgradient1csharp)]  
  
 下图显示上一示例所创建的渐变。  
  
 ![水平方向线性渐变](./media/graphicsmm-horizontallgb.jpg "graphicsmm_HorizontalLGB")  
  
 若要创建一个垂直线性渐变，更改<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>并<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>的<xref:System.Windows.Media.LinearGradientBrush>为 (0.5，0) 和 (0.5，1)。 在以下示例中，<xref:System.Windows.Shapes.Rectangle>使用一个垂直线性渐变绘制。  
  
 [!code-xaml[GradientBrushExamples_snip#VerticalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#verticalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#VerticalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#verticalgradient1csharp)]  
  
 下图显示上一示例所创建的渐变。  
  
 ![垂直线性渐变](./media/graphicsmm-verticallgb.jpg "graphicsmm_VerticalLGB")  
  
> [!NOTE]
>  本主题中的示例设置起始点和终结点使用默认坐标系统。 默认坐标系与边界框是：0 指示边界框的 0 %1 指示边界框的 100%。 您可以通过设置更改此坐标系<xref:System.Windows.Media.GradientBrush.MappingMode%2A>属性的值<xref:System.Windows.Media.BrushMappingMode.Absolute?displayProperty=nameWithType>。 绝对坐标系与范围框无关。 值直接在本地空间中解释。  
  
 有关其他示例，请参阅[画笔示例](https://go.microsoft.com/fwlink/?LinkID=159973)。 渐变和画笔的其他类型的详细信息，请参阅[使用纯色和渐变概述进行绘制](painting-with-solid-colors-and-gradients-overview.md)。
