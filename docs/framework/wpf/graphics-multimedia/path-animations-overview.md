---
title: 路径动画概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- animation [WPF], paths
- path animations [WPF]
ms.assetid: 979c732c-df74-47a6-be96-8e07b3707d53
ms.openlocfilehash: c8e628e11debadb88c365ac95d355f1ee641bdbc
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367851"
---
# <a name="path-animations-overview"></a>路径动画概述
<a name="introduction"></a>本主题介绍了路径动画，使你能够使用几何路径来生成输出值。 路径动画可用于沿着复杂路径移动和旋转对象。  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>系统必备  
 若要了解本主题，您应熟悉[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]动画功能。 有关动画功能的简介，请参阅[动画概述](animation-overview.md)。  
  
 因为你使用<xref:System.Windows.Media.PathGeometry>对象来定义一个路径的动画，您还应熟悉<xref:System.Windows.Media.PathGeometry>以及不同类型的<xref:System.Windows.Media.PathSegment>对象。 有关详细信息，请参阅[几何概述](geometry-overview.md)。  
  
<a name="what_is_a_path_animation"></a>   
## <a name="what-is-a-path-animation"></a>什么是路径动画？  
 路径动画是一种<xref:System.Windows.Media.Animation.AnimationTimeline>，它使用<xref:System.Windows.Media.PathGeometry>作为其输入。 而不是设置 From、 To 或 By 属性 (像对 From/To/By 动画) 或使用关键帧 （如用于关键帧动画），定义一个几何路径并使用它来设置`PathGeometry`路径动画的属性。 路径动画运行时，会从路径中读取 x、y 和角度信息并使用该信息生成其输出。  
  
 路径动画对沿着复杂路径的对象进行动画处理非常有用。 移动沿着路径针对对象是使用的一种方法<xref:System.Windows.Media.MatrixTransform>和一个<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>转换沿着复杂路径对象。 下面的示例演示通过使用此技术<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>对象进行动画处理<xref:System.Windows.Media.MatrixTransform.Matrix%2A>属性的<xref:System.Windows.Media.MatrixTransform>。 <xref:System.Windows.Media.MatrixTransform>应用于按钮，并使其沿着曲线路径移动。 因为<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A>属性设置为`true`，矩形将沿着路径的切线旋转。  
  
 [!code-xaml[PathAnimationGallery_snippet#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/matrixanimationusingpathdoesrotatewithtangentexample.xaml#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/MatrixAnimationUsingPathDoesRotateWithTangentExample.cs#matrixanimationusingpathdoesrotatewithtangentwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#MatrixAnimationUsingPathDoesRotateWithTangentWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/MatrixAnimationUsingPathDoesRotateWithTangentExample.vb#matrixanimationusingpathdoesrotatewithtangentwholepage)]  
  
 有关详细信息中使用的路径语法[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]示例中，请参阅[路径标记语法](path-markup-syntax.md)概述。 有关完整示例，请参阅[路径动画示例](https://go.microsoft.com/fwlink/?LinkID=160028)。  
  
 通过使用应用于属性路径动画<xref:System.Windows.Media.Animation.Storyboard>中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]和代码，或通过使用<xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A>中代码的方法。 您还可以使用路径动画创建<xref:System.Windows.Media.Animation.AnimationClock>并将其应用到一个或多个属性。 有关应用动画的不同方法的详细信息，请参阅[属性动画技术概述](property-animation-techniques-overview.md)。  
  
<a name="animation_types"></a>   
## <a name="path-animation-types"></a>路径动画类型  
 由于动画会生成属性值，因此不同的属性类型具有不同的动画类型。 采用属性进行动画处理<xref:System.Double>(如<xref:System.Windows.Media.TranslateTransform.X%2A>的属性<xref:System.Windows.Media.TranslateTransform>)，可以使用生成的动画<xref:System.Double>值。 采用属性进行动画处理<xref:System.Windows.Point>，可以使用生成的动画<xref:System.Windows.Point>值，等等。  
  
 路径动画类属于<xref:System.Windows.Media.Animation>命名空间，并使用以下命名约定：  
  
 *\<Type>* `AnimationUsingPath`  
  
 其中 *\<Type>* 为该类进行动画处理的值的类型。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供以下路径动画类。  
  
|属性类型|相应的路径动画类|示例|  
|-------------------|----------------------------------------|-------------|  
|<xref:System.Double>|<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>|[沿着路径针对对象进行动画处理（双重动画）](how-to-animate-an-object-along-a-path-double-animation.md)|  
|<xref:System.Windows.Media.Matrix>|<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>|[沿着路径针对对象进行动画处理（矩阵动画）](how-to-animate-an-object-along-a-path-matrix-animation.md)|  
|<xref:System.Windows.Point>|<xref:System.Windows.Media.Animation.PointAnimationUsingPath>|[沿着路径针对对象进行动画处理（点动画）](how-to-animate-an-object-along-a-path-point-animation.md)|  
  
 一个<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>生成<xref:System.Windows.Media.Matrix>值，从其<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.PathGeometry%2A>。 与一起使用时<xref:System.Windows.Media.MatrixTransform>、<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>可以移动沿着路径针对对象。 如果您设置<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath.DoesRotateWithTangent%2A>的属性<xref:System.Windows.Media.Animation.MatrixAnimationUsingPath>到`true`，它还会沿着曲线路径针对对象。  
  
 一个<xref:System.Windows.Media.Animation.PointAnimationUsingPath>生成<xref:System.Windows.Point>值从 x 坐标和 y 坐标的其<xref:System.Windows.Media.Animation.PointAnimationUsingPath.PathGeometry%2A>。 通过使用<xref:System.Windows.Media.Animation.PointAnimationUsingPath>采用属性进行动画处理<xref:System.Windows.Point>值，可以移动沿着路径针对对象。 一个<xref:System.Windows.Media.Animation.PointAnimationUsingPath>无法旋转对象。  
  
 一个<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>生成<xref:System.Double>值，从其<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.PathGeometry%2A>。 通过设置<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath.Source%2A>属性，可指定是否<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>使用 x 坐标、 y 坐标或路径角度作为其输出。 可以使用<xref:System.Windows.Media.Animation.DoubleAnimationUsingPath>来旋转对象或将其移动沿 x 轴或 y 轴。  
  
<a name="pathanimationinput"></a>   
## <a name="path-animation-input"></a>路径动画输入  
 每个路径动画类提供了<xref:System.Windows.Media.PathGeometry>属性用于指定其输入。 路径动画使用<xref:System.Windows.Media.PathGeometry>来生成其输出值。 <xref:System.Windows.Media.PathGeometry>类能够描述组成弧线、 曲线和直线的多个复杂图形。  
  
 核心<xref:System.Windows.Media.PathGeometry>是一系列<xref:System.Windows.Media.PathFigure>对象，这些对象如此命名是因为每个图形都描述中的一个离散形状<xref:System.Windows.Media.PathGeometry>。 每个<xref:System.Windows.Media.PathFigure>包含一个或多个<xref:System.Windows.Media.PathSegment>对象，其中每个描述该图的段。  
  
 有多种类型的线段。  
  
|线段类型|描述|  
|------------------|-----------------|  
|<xref:System.Windows.Media.ArcSegment>|创建两个点之间的椭圆弧。|  
|<xref:System.Windows.Media.BezierSegment>|创建两个点之间的三次方贝塞尔曲线。|  
|<xref:System.Windows.Media.LineSegment>|创建两个点之间的直线。|  
|<xref:System.Windows.Media.PolyBezierSegment>|创建一系列三次方贝塞尔曲线。|  
|<xref:System.Windows.Media.PolyLineSegment>|创建一系列直线。|  
|<xref:System.Windows.Media.PolyQuadraticBezierSegment>|创建一系列的二次贝塞尔曲线。|  
|<xref:System.Windows.Media.QuadraticBezierSegment>|创建一条二次贝塞尔曲线。|  
  
 中的各段<xref:System.Windows.Media.PathFigure>合并成一个几何形状，它使用段的终点作为下一段的起始点。 <xref:System.Windows.Media.PathFigure.StartPoint%2A>属性的<xref:System.Windows.Media.PathFigure>指定从中绘制第一条线段的点。 每个后续线段都从上一线段的终点开始。 例如，从竖线`10,50`到`10,150`可以通过设置定义<xref:System.Windows.Media.PathFigure.StartPoint%2A>属性设置为`10,50`和创建<xref:System.Windows.Media.LineSegment>与<xref:System.Windows.Media.LineSegment.Point%2A>属性设置`10,150`。  
  
 有关详细信息<xref:System.Windows.Media.PathGeometry>对象，请参阅[Geometry 概述](geometry-overview.md)。  
  
 在中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，还可以使用特殊的缩写的语法来设置<xref:System.Windows.Media.PathGeometry.Figures%2A>属性的<xref:System.Windows.Media.PathGeometry>。 有关详细信息，请参阅[路径标记语法](path-markup-syntax.md)概述。  
  
 有关详细信息中使用的路径语法[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]示例中，请参阅[路径标记语法](path-markup-syntax.md)概述。  
  
## <a name="see-also"></a>请参阅
- [路径动画示例](https://go.microsoft.com/fwlink/?LinkID=160028)
- [路径标记语法](path-markup-syntax.md)
- [路径动画操作说明主题](path-animation-how-to-topics.md)
- [动画概述](animation-overview.md)
- [属性动画技术概述](property-animation-techniques-overview.md)
