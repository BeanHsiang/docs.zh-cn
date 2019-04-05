---
title: 三维变换概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- 3-D transformations
- transformations [WPF], 3-D
ms.assetid: e45e555d-ac1e-4b36-aced-e433afe7f27f
ms.openlocfilehash: 578c8061271e08e4eac1ec5f11c84e63a3fa37bd
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57361884"
---
# <a name="3-d-transformations-overview"></a>三维变换概述
本主题描述如何向 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 图形系统中的 3D 模型应用转换。 开发人员可以借助转换功能对模型进行重定位、大小调整和重定向，而无需更改用来定义模型的基值。  
  

  
## <a name="3-d-coordinate-space"></a>3D 坐标空间  
 三维图形中的内容[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]封装在一个元素， <xref:System.Windows.Controls.Viewport3D>，该元素可以参与二维元素结构。 该图形系统将 Viewport3D 视为一个像 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的许多其他元素一样的二维视觉元素。 Viewport3D 充当三维场景中的窗口（即视区）。 更准确地说，它是 3D 场景所投影到的图面。  尽管可以将 Viewport3D 与其他 2D 绘图对象用在同一个场景图中，但是不能在 Viewport3D 中渗透 2D 和 3D 对象。 以下讨论中所描述的坐标空间包含在 Viewport3D 元素中。  
  
 2D 图形的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 坐标系将原点定位在呈现图面（通常是屏幕）的左上角。 在 2D 系统中，x 轴上的正值朝右，y 轴上的正值朝下。 但是在 3D 坐标系中，原点位于屏幕中心，x 轴上的正值朝右，但是 y 轴上的正值朝上，z 轴上的正值从原点向外朝向观察者。  
  
 ![坐标系](./media/coordsystem-1.png "CoordSystem 1")  
坐标系比较  
  
 由这些轴定义的空间是 3D 对象在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的固定参考框架。 当在该空间中生成模型并创建光源和照相机以查看这些模型时，一定要在向每个模型应用转换时，将固定参考框架或“全局空间”与为该模型创建的局部参考框架区分开。 另请记住，根据光源和照相机设置，全局空间中的对象可能会看上去完全不同或者根本不可见，但是照相机的位置不会改变对象在全局空间中的位置。  
  
## <a name="transforming-models"></a>转换模型  
 创建模型时，它们在场景中有特定的位置。 为了在场景中移动、旋转这些模型或者更改这些模型的大小而更改用来定义模型本身的顶点不切实际。 而正如在 2D 中一样，可以向模型应用转换。  
  
 每个模型对象具有<xref:System.Windows.Media.Media3D.Model3D.Transform%2A>属性与其可以移动、 重定向或调整模型的大小。 应用转换时，实际上是按照由转换功能指定的矢量或值（以适用者为准）来偏移模型的所有点。 换言之，用户已经转换了在其中定义模型的坐标空间（“模型空间”），但是尚未更改在整个场景的坐标系（“全局空间”）中构成模型几何形状的值。  
  
## <a name="translation-transformations"></a>平移转换  
 3d 转换继承自的抽象基类<xref:System.Windows.Media.Media3D.Transform3D>; 其中包括仿射转换类<xref:System.Windows.Media.Media3D.TranslateTransform3D>， <xref:System.Windows.Media.Media3D.ScaleTransform3D>，和<xref:System.Windows.Media.Media3D.RotateTransform3D>。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 3d 系统还提供了<xref:System.Windows.Media.Media3D.MatrixTransform3D>类可以让您在更简明的矩阵操作中指定相同的转换。  
  
 <xref:System.Windows.Media.Media3D.TranslateTransform3D> 将所有点都移动 model3d 中与指定的偏移矢量的方向<xref:System.Windows.Media.Media3D.TranslateTransform3D.OffsetX%2A>， <xref:System.Windows.Media.Media3D.TranslateTransform3D.OffsetY%2A>，和<xref:System.Windows.Media.Media3D.TranslateTransform3D.OffsetZ%2A>属性。 例如，假设立方体的一个顶点位于 (2,2,2)，偏移矢量 (0,1.6,1) 会将该顶点 (2,2,2) 移到 (2,3.6,3)。 该立方体的顶点在模型空间中仍位于 (2,2,2)，但是现在，该模型空间与全局空间的关系已经发生改变，因此，模型空间中的 (2,2,2) 是世界空间中的 (2,3.6,3)。  
  
 ![平移图](./media/transforms-translate.png "转换转换")  
偏移后的平移  
  
 下面的代码示例演示如何应用平移。  
  
 [!code-xaml[animation3dgallery_snip#Translation3DAnimationExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Translation3DAnimationExample.xaml#translation3danimationexamplewholepage)]  
  
## <a name="scale-transformations"></a>缩放转换  
 <xref:System.Windows.Media.Media3D.ScaleTransform3D> 由中心点指定的缩放矢量更改模型的比例。 可以指定等比缩放，即在 X、Y 和 Z 轴上将模型缩放同样的值来按比例更改模型的大小。 例如，将该转换<xref:System.Windows.Media.ScaleTransform.ScaleX%2A>， <xref:System.Windows.Media.ScaleTransform.ScaleY%2A>，和<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleZ%2A>属性设置为 0.5 会模型; 将相同的属性设置为 2 两倍，其在所有三个轴的刻度。  
  
 ![统一 ScaleTransform3D](./media/threecubes-uniformscale-1.png "threecubes_uniformscale_1")  
ScaleVector 示例  
  
 通过指定非等比转换（X、Y 和 Z 值不相等的缩放转换），可以使模型在一个或两个维度上拉伸或收缩，而不会影响其他维度。 例如，设置<xref:System.Windows.Media.ScaleTransform.ScaleX%2A>为 1，<xref:System.Windows.Media.ScaleTransform.ScaleY%2A>为 2，和<xref:System.Windows.Media.Media3D.ScaleTransform3D.ScaleZ%2A>为 1 会导致转换后的模型以高度增加一倍，但仍保持不变的 X 和 Z 轴。  
  
 默认情况下，ScaleTransform3D 会使顶点围绕原点 (0,0,0) 拉伸或收缩。 但是，如果要转换的模型不是围绕原点绘制，则围绕原点缩放模型时，模型将不会“就地”缩放。 相反，当模型的顶点与缩放矢量相乘时，缩放操作对模型的平移和缩放都会产生影响。  
  
 ![通过指定中心点的三个多维数据集调整](./media/threecubes-scaledwithcenter-1.png "threecubes_scaledwithcenter_1")  
缩放中心示例  
  
 若要向"就地"模型，通过设置 ScaleTransform3D 的指定模型的中心<xref:System.Windows.Media.ScaleTransform.CenterX%2A>， <xref:System.Windows.Media.ScaleTransform.CenterY%2A>，和<xref:System.Windows.Media.Media3D.ScaleTransform3D.CenterZ%2A>属性。 这可确保图形系统缩放模型空间，然后平移该，在指定中心<xref:System.Windows.Media.Media3D.Point3D>。 相反，如果模型围绕原点生成，而且指定了其他中心点，则将看到模型会背离原点平移。  
  
## <a name="rotation-transformations"></a>旋转转换  
 可以通过几种不同的方法来旋转 3D 模型。 典型的旋转转换指定一个轴以及围绕该轴旋转的角度。 <xref:System.Windows.Media.Media3D.RotateTransform3D>类，可定义<xref:System.Windows.Media.Media3D.Rotation3D>使用其<xref:System.Windows.Media.Media3D.RotateTransform3D.Rotation%2A>属性。 然后指定<xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Axis%2A>并<xref:System.Windows.Media.Media3D.AxisAngleRotation3D.Angle%2A>属性上，在此情况下在 Rotation3D <xref:System.Windows.Media.Media3D.AxisAngleRotation3D>，来定义转换。 下面的几个示例围绕 Y 轴将模型旋转 60 度。  
  
 [!code-xaml[animation3dgallery_snip#Rotate3DUsingAxisAngleRotation3DExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/Animation3DGallery_snip/CS/Rotat3DUsingAxisAngleRotation3DExample.xaml#rotate3dusingaxisanglerotation3dexamplewholepage)]  
  
 注意：[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]三维效果是一个右手系统，这意味着，旋转的正角度值会导致围绕轴逆时针旋转。  
  
 如果没有为指定一个值，轴和角度的旋转假设围绕原点旋转<xref:System.Windows.Media.Media3D.RotateTransform3D.CenterX%2A>， <xref:System.Windows.Media.Media3D.RotateTransform3D.CenterY%2A>，和<xref:System.Windows.Media.Media3D.RotateTransform3D.CenterZ%2A>RotateTransform3D 上的属性。 与缩放一样，牢记旋转时会转换模型的整个坐标空间，这会很有帮助。 如果模型不是围绕原点创建，或者它以前平移过，则旋转可能会围绕原点“转动”，而不是就地旋转。  
  
 ![采用新中心点旋转](./media/threecubes-rotationwithcenter-1.png "threecubes_rotationwithcenter_1")  
围绕指定的新中心旋转  
  
 若要“就地”旋转模型，请将模型的实际中心指定为旋转中心。 由于几何形状通常围绕原点建模，因此，在依次执行下列操作时通常将获取一组预期的转换结果：调整模型大小（缩放该模型），然后设置模型方向（旋转该模型），最后将模型移到所需的位置（平移该模型）。  
  
 ![旋转 60 度 x 中&#45;和 y&#45;轴](./media/twocubes-rotation2axes-1.png "twocubes_rotation2axes_1")  
旋转示例  
  
 指定了轴和角度的旋转非常适于静态转换和某些动画。 但是，请考虑围绕 X 轴将立方体模型旋转 60 度，然后围绕 Z 轴将其旋转 45 度。 可以将这种转换描述为两个离散的仿射转换，也可以将其描述为一个矩阵。 但是，对于按照这种方式定义的旋转，可能很难顺利地进行动画处理。 尽管按照这两种方法计算的模型起始位置和结束位置相同，但是，从计算的角度来看，无法确定该模型经过的中间位置。 四元数提供了一种用来在旋转的起始位置和结束位置之间计算内插值的替代方法。  
  
 四元数表示 3D 空间中的一个轴以及围绕该轴的旋转。 例如，四元数可以表示 (1,1,2) 轴以及 50 度的旋转角度。 四元数在定义旋转方面的价值在于可以针对它们执行的两个运算：合成和内插。 应用于一个几何形状的两个四元数的合成是指“围绕 axis2 将几何形状旋转 rotation2 度，然后围绕 axis1 将其旋转 rotation1 度”。 通过使用合成运算，可以将应用于几何形状的两个旋转合成在一起，以便获得一个代表合成结果的四元数。 由于四元数内插可以计算出从一个轴和方向到另一个轴和方向的顺利而又合理的路径，因此可以从原始位置到合成的四元数之间进行内插，以便实现从一个位置到另一个位置的顺利过渡，从而可以对该转换进行动画处理。 对于要进行动画处理的模型，可以指定目标<xref:System.Windows.Media.Media3D.Quaternion>通过使用旋转<xref:System.Windows.Media.Media3D.QuaternionRotation3D>为<xref:System.Windows.Media.Media3D.RotateTransform3D.Rotation%2A>属性。  
  
## <a name="using-transformation-collections"></a>使用转换集合  
 生成场景时，通常会向模型应用多个转换。 添加到转换<xref:System.Windows.Media.Media3D.Transform3DGroup.Children%2A>的集合<xref:System.Windows.Media.Media3D.Transform3DGroup>类进行分组可以方便地转换来将应用于场景中的各种模型。 通常，可以很方便地在几个不同的组中重复使用某个转换，这与通过向每个实例应用一组不同的转换来重复使用模型大体相同。 请注意，将转换添加到集合中的顺序至关重要：集合中的转换按照从第一个到最后一个的顺序应用。  
  
## <a name="animating-transformations"></a>对转换进行动画处理  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 3D 实现与 2D 图形参与同一个计时和动画系统。 换言之，若要对 3D 场景进行动画处理，需要对其模型的属性进行动画处理。 可以直接对基元的属性进行动画处理，但是通常很容易对用来更改模型位置或外观的转换进行动画处理。 由于转换可以应用于<xref:System.Windows.Media.Media3D.Model3DGroup>对象、 单个模型，可以将一组动画应用于向 Model3Dgroup 的子级和另一组对象的一组动画。  有关 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 计时和动画系统的背景信息，请参阅[动画概述](animation-overview.md)和[演示图板概述](storyboards-overview.md)。  
  
 若要对 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的对象进行动画处理，可以创建时间线、定义动画（实际上是随着时间的推移而更改某个属性值）并指定要向其应用动画的属性。 此属性必须是 FrameworkElement 的属性。 由于 3D 场景中的所有对象都是 Viewport3D 的子级，因此要应用于场景的任何动画所面向的属性都是 Viewport3D 属性的属性。 请务必仔细设计动画的属性路径，因为语法可能会极为冗长。  
  
 假设用户希望就地旋转某个对象，而且还希望应用摆动动作以公开要查看的对象的更多内容。 可以选择向模型应用 RotateTransform3D，并对模型从一个矢量旋转到另一个矢量时所围绕的轴进行动画处理。 下面的代码示例演示如何将<xref:System.Windows.Media.Animation.Vector3DAnimation>转换的 Rotation3D 的 Axis 属性，假设 RotateTransform3D 是应用于模型的多个转换之一<xref:System.Windows.Media.TransformGroup>。  
  
 [!code-csharp[3doverview#3DOverview3DN1](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn1)]
 [!code-vb[3doverview#3DOverview3DN1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn1)]  
  
 [!code-csharp[3doverview#3DOverview3DN3](~/samples/snippets/csharp/VS_Snippets_Wpf/3DOverview/CSharp/Window1.xaml.cs#3doverview3dn3)]
 [!code-vb[3doverview#3DOverview3DN3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/3DOverview/visualbasic/window1.xaml.vb#3doverview3dn3)]  
  
 使用类似的语法面向其他转换属性来移动或缩放该对象。  例如，您可能要应用<xref:System.Windows.Media.Animation.Point3DAnimation>到缩放转换的模型，以便顺利扭曲其形状 ScaleCenter 属性。  
  
 尽管前面的示例转换的属性<xref:System.Windows.Media.Media3D.GeometryModel3D>，还有可能要转换的场景中其他模型的属性。  例如，通过对应用于 Light 对象的平移进行动画处理来创建移动灯光和阴影效果，这些效果可以显著改变模型的外观。  
  
 由于照相机也是模型，因此也可以对照相机属性进行转换。  尽管确实可以通过改变照相机的位置或平面距离来改变场景的外观（实际上是变换整个场景的投影），但应注意，对于观察者来说，以这种方法实现的许多效果不如将转换应用于场景中模型的地点或位置更有“视觉意义”。  
  
## <a name="see-also"></a>请参阅
- [3D 图形概述](3-d-graphics-overview.md)
- [转换概述](transforms-overview.md)
- [2D 转换示例](https://go.microsoft.com/fwlink/?LinkID=158252)
