---
title: 最大程度地提高 WPF 三维性能
ms.date: 03/30/2017
helpviewer_keywords:
- 3-D graphics [WPF]
ms.assetid: 4bcf949d-d92f-4d8d-8a9b-1e4c61b25bf6
ms.openlocfilehash: 48e8310e003dcd3ebca579654b81363efaac9068
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364003"
---
# <a name="maximize-wpf-3d-performance"></a>最大程度地提高 WPF 三维性能
因为你使用[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]若要生成三维控件和应用程序中包含三维场景，务必要考虑性能优化。 本主题提供 3D 类和属性的可能对性能产生影响的应用程序，以及使用它们时优化性能的建议的列表。  
  
 本主题假定您了解高级的[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]3D 功能。 本文档中的建议适用于"呈现层 2"— 大致定义为支持像素着色器版本 2.0 和顶点着色器版本 2.0 的硬件。 有关更多详细信息，请参阅[图形呈现层](../advanced/graphics-rendering-tiers.md)。  
  
## <a name="performance-impact-high"></a>对性能的影响：高  
  
|属性|建议|  
|-|-|  
|<xref:System.Windows.Media.Brush>|画笔速度 （最快到速度最慢）：<br /><br /> <xref:System.Windows.Media.SolidColorBrush><br /><br /> <xref:System.Windows.Media.LinearGradientBrush><br /><br /> <xref:System.Windows.Media.ImageBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush> （已缓存）<br /><br /> <xref:System.Windows.Media.VisualBrush> （已缓存）<br /><br /> <xref:System.Windows.Media.RadialGradientBrush><br /><br /> <xref:System.Windows.Media.DrawingBrush> （未缓存）<br /><br /> <xref:System.Windows.Media.VisualBrush> （未缓存）|  
|<xref:System.Windows.UIElement.ClipToBoundsProperty>|设置`Viewport3D.ClipToBounds`为 false 时不需要具有[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]显式剪切的内容内容<xref:System.Windows.Controls.Viewport3D>到 Viewport3D 的矩形。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 抗锯齿剪辑可能会很慢，并且`ClipToBounds`（较慢） 默认情况下启用上<xref:System.Windows.Controls.Viewport3D>。|  
|<xref:System.Windows.UIElement.IsHitTestVisible%2A>|设置`Viewport3D.IsHitTestVisible`为 false 时不需要[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]要考虑的内容<xref:System.Windows.Controls.Viewport3D>执行鼠标命中测试。  命中测试的 3D 内容在软件中完成，并可能会遇到大型网格很慢。 <xref:System.Windows.UIElement.IsHitTestVisible%2A> （较慢） 默认情况下启用上<xref:System.Windows.Controls.Viewport3D>。|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D>|仅当它们需要不同的材料或转换时，请创建不同的模型。  否则，尝试 coalesce 许多<xref:System.Windows.Media.Media3D.GeometryModel3D>实例具有相同的材料和转换成更大一些<xref:System.Windows.Media.Media3D.GeometryModel3D>和<xref:System.Windows.Media.Media3D.MeshGeometry3D>实例。|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|网格动画 — 更改每个帧以在网格的各个顶点 — 并不总是有效[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]。  若要修改的每个顶点时，最小化的更改通知的性能影响，在执行每个顶点修改之前分离从可视化树网格。  一旦已修改网格，将其重新附加到可视化树。  此外，尝试尽量减少这种方式进行动画处理的网格的大小。|  
|3D 抗锯齿|若要提高呈现速度上, 禁用多重采样<xref:System.Windows.Controls.Viewport3D>通过设置附加的属性<xref:System.Windows.Media.RenderOptions.EdgeMode%2A>到`Aliased`。  默认情况下上, 禁用 3D 抗锯齿[!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)]并且在上启用[!INCLUDE[TLA#tla_longhorn](../../../../includes/tlasharptla-longhorn-md.md)]使用每像素 4 个样本。|  
|Text|Live 三维场景中的文本 (因为它在 live<xref:System.Windows.Media.DrawingBrush>或<xref:System.Windows.Media.VisualBrush>) 可能会很慢。 尝试改为使用映像的文本 (通过<xref:System.Windows.Media.Imaging.RenderTargetBitmap>) 除非文本将更改。|  
|<xref:System.Windows.Media.TileBrush>|如果必须使用<xref:System.Windows.Media.VisualBrush>或<xref:System.Windows.Media.DrawingBrush>三维场景中由于画笔的内容不是静态的请尝试缓存画笔 (设置附加的属性<xref:System.Windows.Media.RenderOptions.CachingHint%2A>到`Cache`)。  设置失效阈值最小值和最大缩放 (带有附加属性<xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMinimum%2A>和<xref:System.Windows.Media.RenderOptions.CacheInvalidationThresholdMaximum%2A>)，以便缓存的画笔都不会同时仍保持所需的质量级别过于频繁地重新生成。  默认情况下<xref:System.Windows.Media.DrawingBrush>和<xref:System.Windows.Media.VisualBrush>未缓存，这意味着，每次使用画笔绘制的内容必须是重新呈现，画笔的整个内容必须首先重新呈现到中间的图面。|  
|<xref:System.Windows.Media.Effects.BitmapEffect>|<xref:System.Windows.Media.Effects.BitmapEffect> 强制所有受影响的内容，如果不进行硬件加速呈现。  为了获得最佳性能，不要使用<xref:System.Windows.Media.Effects.BitmapEffect>。|  
  
## <a name="performance-impact-medium"></a>对性能的影响：中等  
  
|属性|建议|  
|-|-|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|当网格定义为邻接通过共享顶点的三角形，这些顶点拥有相同的位置、 正常、 和纹理坐标时，定义共享的每个顶点仅一次，然后通过使用索引来定义三角形<xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>。|  
|<xref:System.Windows.Media.ImageBrush>|尝试时你可以显式控制大小最大程度减少纹理大小 (当使用<xref:System.Windows.Media.Imaging.RenderTargetBitmap>和/或<xref:System.Windows.Media.ImageBrush>)。  请注意，较低分辨率纹理可以降低视觉质量，因此尝试查找质量和性能之间的最佳平衡。|  
|不透明度|当呈现半透明的三维内容 （如反射），画笔或材料上使用的不透明度属性 (通过<xref:System.Windows.Media.Brush.Opacity%2A>或<xref:System.Windows.Media.Media3D.DiffuseMaterial.Color%2A>) 而不是创建单独的半透明<xref:System.Windows.Controls.Viewport3D>通过设置`Viewport3D.Opacity`为小于 1 的值。|  
|<xref:System.Windows.Controls.Viewport3D>|数量降至最低<xref:System.Windows.Controls.Viewport3D>对象在场景中使用。  多个三维模型置于同一个 Viewport3D，而无需创建单独的 Viewport3D 实例为每个模型。|  
|<xref:System.Windows.Freezable>|通常最好重用<xref:System.Windows.Media.Media3D.MeshGeometry3D>， <xref:System.Windows.Media.Media3D.GeometryModel3D>，画笔和材料。  所有是 multiparentable，因为它们派生自`Freezable`。|  
|<xref:System.Windows.Freezable>|调用<xref:System.Windows.Freezable.Freeze%2A>上时将保留它们的属性的可冻结对象的方法在应用程序中保持不变。  冻结可以减少工作集，并提高速度。|  
|<xref:System.Windows.Media.Brush>|使用<xref:System.Windows.Media.ImageBrush>而不是<xref:System.Windows.Media.VisualBrush>或<xref:System.Windows.Media.DrawingBrush>时画笔的内容将不会更改。  2D 内容可以转换为<xref:System.Windows.Controls.Image>通过<xref:System.Windows.Media.Imaging.RenderTargetBitmap>，然后再在<xref:System.Windows.Media.ImageBrush>。|  
|<xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A>|不要使用<xref:System.Windows.Media.Media3D.GeometryModel3D.BackMaterial%2A>除非确实需要查看的背面，否则你<xref:System.Windows.Media.Media3D.GeometryModel3D>。|  
|<xref:System.Windows.Media.Media3D.Light>|浅速度 （最快到速度最慢）：<br /><br /> <xref:System.Windows.Media.Media3D.AmbientLight><br /><br /> <xref:System.Windows.Media.Media3D.DirectionalLight><br /><br /> <xref:System.Windows.Media.Media3D.PointLight><br /><br /> <xref:System.Windows.Media.Media3D.SpotLight>|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|尝试使网格大小小于这些限制：<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>：20001<xref:System.Windows.Media.Media3D.Point3D>实例<br /><br /> <xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>：60,003<xref:System.Int32>实例|  
|<xref:System.Windows.Media.Media3D.Material>|材料的速度 （最快到速度最慢）：<br /><br /> <xref:System.Windows.Media.Media3D.EmissiveMaterial><br /><br /> <xref:System.Windows.Media.Media3D.DiffuseMaterial><br /><br /> <xref:System.Windows.Media.Media3D.SpecularMaterial>|  
|<xref:System.Windows.Media.Brush>|[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 3D 不一致的方式不参与 （黑色的环境画笔、 透明画笔等） 不可见的画笔。  请考虑您的场景中省略这些画笔。|  
|<xref:System.Windows.Media.Media3D.MaterialGroup>|每个<xref:System.Windows.Media.Media3D.Material>在<xref:System.Windows.Media.Media3D.MaterialGroup>会导致另一个呈现处理过程，因此包含多个材料，甚至简单的材料，可以极大地提高了对您的 GPU 的填充要求。  中的材料的数量降至最低你<xref:System.Windows.Media.Media3D.MaterialGroup>。|  
  
## <a name="performance-impact-low"></a>对性能的影响：低  
  
|属性|建议|  
|-|-|  
|<xref:System.Windows.Media.Media3D.Transform3DGroup>|当不需要动画或数据绑定，而不使用包含多个转换的转换组使用单个<xref:System.Windows.Media.Media3D.MatrixTransform3D>，将其设置为要转换组中将否则独立存在的所有转换的产品。|  
|<xref:System.Windows.Media.Media3D.Light>|您的场景中的光源数量降至最低。 将强制在场景中太多的光源[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]回退到软件呈现。  限制大约为 110<xref:System.Windows.Media.Media3D.DirectionalLight>对象，70<xref:System.Windows.Media.Media3D.PointLight>对象或 40<xref:System.Windows.Media.Media3D.SpotLight>对象。|  
|<xref:System.Windows.Media.Media3D.ModelVisual3D>|单独的静态对象从移动对象，通过将它们放在单独<xref:System.Windows.Media.Media3D.ModelVisual3D>实例。  ModelVisual3D 高于""<xref:System.Windows.Media.Media3D.GeometryModel3D>由于缓存转换后的边界。  GeometryModel3D 经过优化，可将模型;ModelVisual3D 经过优化，可以场景节点。  使用 ModelVisual3D 放入场景 GeometryModel3D 的共享的实例。|  
|<xref:System.Windows.Media.Media3D.Light>|最大程度减少更改的灯场景中的次数。  浅计数每次更改强制着色器重新生成和重新编译，除非之前已存在该配置 （并因此缓存其着色器）。|  
|浅|黑色光源是不可见，但它们将添加要呈现时间;请考虑省略它们。|  
|<xref:System.Windows.Media.Media3D.MeshGeometry3D>|若要最大程度减少大型集合中的构造时间[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]，如 MeshGeometry3D <xref:System.Windows.Media.Media3D.MeshGeometry3D.Positions%2A>， <xref:System.Windows.Media.Media3D.MeshGeometry3D.Normals%2A>， <xref:System.Windows.Media.Media3D.MeshGeometry3D.TextureCoordinates%2A>，和<xref:System.Windows.Media.Media3D.MeshGeometry3D.TriangleIndices%2A>，预调整大小之前值填充的集合。 如果可能，请将传递集合的构造函数预先填充的数据结构，例如数组或列表。|  
  
## <a name="see-also"></a>请参阅
- [3D 图形概述](3-d-graphics-overview.md)
