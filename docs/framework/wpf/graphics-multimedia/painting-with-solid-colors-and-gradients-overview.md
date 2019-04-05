---
title: 使用纯色和渐变进行绘制概述
ms.date: 03/30/2017
helpviewer_keywords:
- solid colors [WPF], painting with
- painting with gradients [WPF]
- gradients [WPF], painting with
- brushes [WPF], painting with solid colors
- brushes [WPF], painting with gradients
- painting with solid colors [WPF]
ms.assetid: f5b182f3-c5c7-4cbe-9f2f-65e690d08255
ms.openlocfilehash: 18a08c9bec8436399cd3acbf27198e0912e32d09
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57362378"
---
# <a name="painting-with-solid-colors-and-gradients-overview"></a>使用纯色和渐变进行绘制概述
本主题介绍如何使用<xref:System.Windows.Media.SolidColorBrush>， <xref:System.Windows.Media.LinearGradientBrush>，和<xref:System.Windows.Media.RadialGradientBrush>对象用纯色、 线性渐变和径向渐变进行绘制。  
  

  
<a name="solidcolor"></a>   
## <a name="painting-an-area-with-a-solid-color"></a>使用纯色绘制区域  
 在任何平台中最常见的操作之一是使用纯色绘制区域<xref:System.Windows.Media.Color>。 若要完成此任务中，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]提供了<xref:System.Windows.Media.SolidColorBrush>类。 以下部分介绍的不同方法来绘制与<xref:System.Windows.Media.SolidColorBrush>。  
  
<a name="solidcolorinxaml"></a>   
### <a name="using-a-solidcolorbrush-in-xaml"></a>在“XAML”中使用 SolidColorBrush  
 若要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中使用纯色绘制某个区域，请使用以下选项之一。  
  
-   按照名称选择预定义的纯色画笔。  例如，可以设置按钮的<xref:System.Windows.Controls.Control.Background%2A>为"红色"或"中度蓝色"。  另一系列预定义的纯色画笔，请参阅的静态属性<xref:System.Windows.Media.Brushes>类。 下面是一个示例。  
  
     [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushNamedColor1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushnamedcolor1xaml)]  
  
-   通过指定红色、绿色和蓝色的分量从 32 位调色板中选择一种颜色，以合并为单个纯色。  从 32 位调色板指定一种颜色的格式为“*#rrggbb*”，其中 *rr* 为两位十六进制数，用于指定红色的相对量，*gg* 指定绿色的相对量，*bb* 指定蓝色的相对量。  此外，该颜色可指定为“#*aarrggbb*”，其中，*aa* 指定该颜色的 *alpha* 值或透明度。 使用此方法能够创建部分透明的颜色。  在以下示例中，<xref:System.Windows.Controls.Control.Background%2A>的<xref:System.Windows.Controls.Button>设置为完全不透明红色使用十六进制表示法。  
  
     [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushHex1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushhex1xaml)]  
  
-   使用属性标记语法来描述<xref:System.Windows.Media.SolidColorBrush>。 此语法更详细，并且能够指定其他设置，例如画笔的不透明度。 在以下示例中，<xref:System.Windows.Controls.Control.Background%2A>的两个属性<xref:System.Windows.Controls.Button>元素设置为完全不透明红色。 第一个画笔的颜色使用预定义的颜色名称描述。 第二个画笔的颜色使用十六进制表示法描述。  
  
     [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushPropertyTag1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushpropertytag1xaml)]  
  
<a name="solidcolorsincode"></a>   
### <a name="painting-with-a-solidcolorbrush-in-code"></a>在代码中使用 SolidColorBrush 进行绘制  
 若要在代码中使用纯色绘制某个区域，请使用下列选项之一。  
  
-   使用提供的预定义画笔之一<xref:System.Windows.Media.Brushes>类。 在以下示例中，<xref:System.Windows.Controls.Control.Background%2A>的<xref:System.Windows.Controls.Button>设置为<xref:System.Windows.Media.Brushes.Red%2A>。  
  
     [!code-csharp[BrushOverviewExamples_snip#SolidColorBrushPredefinedBrush1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushpredefinedbrush1csharp)]  
  
-   创建<xref:System.Windows.Media.SolidColorBrush>并设置其<xref:System.Windows.Media.SolidColorBrush.Color%2A>属性使用<xref:System.Windows.Media.Color>结构。 可以使用从预定义的颜色<xref:System.Windows.Media.Colors>类也可以创建<xref:System.Windows.Media.Color>使用静态<xref:System.Windows.Media.Color.FromArgb%2A>方法。  
  
     下面的示例演示如何设置<xref:System.Windows.Media.SolidColorBrush.Color%2A>属性的<xref:System.Windows.Media.SolidColorBrush>使用预定义的颜色。  
  
     [!code-csharp[BrushOverviewExamples_snip#SolidColorBrushPredefinedColor1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushpredefinedcolor1csharp)]  
  
 静态<xref:System.Windows.Media.Color.FromArgb%2A>可用于指定颜色的 alpha、 红色、 绿色和蓝色值。 每个值的常规范围介于 0 与 255 之间。 例如：alpha 值为 0 表示某种颜色完全透明，而值为 255 则表示该颜色完全不透明。 同样地，红色值为 0 表示某种颜色里没有红色，而值为 255 则表示某种颜色里红色最多。  在下面的示例中，画笔的颜色通过指定 alpha、红色、绿色和蓝色值描述。  
  
 [!code-csharp[BrushOverviewExamples_snip#SolidColorBrushfromArgbExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushfromargbexample1csharp)]  
  
 有关其他方法指定颜色，请参阅<xref:System.Windows.Media.Color>参考主题。  
  
<a name="gradient"></a>   
## <a name="painting-an-area-with-a-gradient"></a>使用渐变绘制区域  
 渐变画笔使用沿轴相互混合的多种颜色绘制区域。 可以使用它们创建光和影的效果，使控件具有三维外观。 还可以使用它们来模拟玻璃、镶边、水和其他光滑表面。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了两种类型的渐变画笔：<xref:System.Windows.Media.LinearGradientBrush>和<xref:System.Windows.Media.RadialGradientBrush>。  
  
<a name="lineargradientbrush"></a>   
## <a name="linear-gradients"></a>线性渐变  
 一个<xref:System.Windows.Media.LinearGradientBrush>沿着一条线，定义的渐变绘制区域*渐变轴*。  指定渐变颜色和它们的位置沿渐变轴使用<xref:System.Windows.Media.GradientStop>对象。  还可以修改渐变轴，从而能够创建水平和垂直渐变以及反转渐变方向。 渐变轴将在下一节中介绍。 默认情况下，将创建对角渐变。  
  
 下面的示例显示了使用四种颜色创建线性渐变的代码。  
  
 [!code-xaml[GradientBrushExamples_snip#DiagonalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#diagonalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#DiagonalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#diagonalgradient1csharp)]  
  
 此代码生成以下渐变：  
  
 ![A diagonal linear gradient](./media/wcpsdk-graphicsmm-diaglgradient-nolabel.jpg "wcpsdk_graphicsmm_diaglgradient_nolabel")  
  
 **注意：** 本主题中的渐变示例使用默认坐标系统的设置起点和终点。 默认坐标系与边界框是：0 指示边界框和 1 的 0%指示边界框的 100%。 您可以通过设置更改此坐标系<xref:System.Windows.Media.GradientBrush.MappingMode%2A>属性的值<xref:System.Windows.Media.BrushMappingMode.Absolute>。 绝对坐标系与范围框无关。 值直接在本地空间中解释。  
  
 <xref:System.Windows.Media.GradientStop>是渐变画笔的基本构造块。  梯度停止点指定<xref:System.Windows.Media.GradientStop.Color%2A>在<xref:System.Windows.Media.GradientStop.Offset%2A>沿渐变轴。  
  
-   渐变停止点的<xref:System.Windows.Media.GradientStop.Color%2A>属性指定梯度停止点的颜色。 您可以通过使用预定义的颜色设置颜色 (由<xref:System.Windows.Media.Colors>类) 或通过指定 ScRGB 或 ARGB 值。 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，还可以使用十六进制表示法描述一种颜色。 有关详细信息，请参阅<xref:System.Windows.Media.Color>结构。  
  
-   渐变停止点的<xref:System.Windows.Media.GradientStop.Offset%2A>属性指定的位置的渐变停止点的颜色渐变轴上。 偏移量是<xref:System.Double>范围从 0 到 1。 梯度停止点的偏移值越接近 0，颜色就越接近渐变的起点。 梯度停止点的偏移值越接近 1，颜色就越接近渐变的终点。  
  
 梯度停止点之间每个点的颜色按两个边界梯度停止点指定的颜色组合执行线性内插。 下图突出显示了上一示例中的梯度停止点。 圆圈标记梯度停止点的位置，虚线显示渐变轴。  
  
 ![Gradient stops in a linear gradient](./media/wcpsdk-graphicsmm-4gradientstops.png "wcpsdk_graphicsmm_4gradientstops")  
  
 第一个梯度停止点指定偏移量 `0.0` 处的颜色为黄色。  第二个梯度停止点指定偏移量 `0.25` 处的颜色为红色。  这两个点之间的点在沿渐变轴由左向右移动时，颜色渐渐由黄色变为红色。  第三个梯度停止点指定偏移量 `0.75` 处的颜色为蓝色。  第二个和第三个梯度停止点之间的点渐渐由红色变为蓝色。 第四个梯度停止点指定偏移量 `1.0` 处的颜色为浅绿色。 第三个和第四个梯度停止点之间的点渐渐由蓝色变为浅绿色。  
  
<a name="gradientaxis"></a>   
### <a name="the-gradient-axis"></a>渐变轴  
 如前文中提到，线性渐变画笔的梯度停止点位于一条线上，即渐变轴上。 您可能会更改方向和使用画笔的线的大小<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>和<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>属性。 通过操作画笔<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>和<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>，可以创建水平和垂直渐变、 反转渐变方向、 压缩渐变范围等。  
  
 默认情况下，线性渐变画笔的<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>和<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>相对于所绘制的区域。 点 (0,0) 表示正在绘制的区域的左上角，点 (1,1) 表示绘制区域的右下角。 默认值<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>的<xref:System.Windows.Media.LinearGradientBrush>为 (0，0) 和其默认<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>(1，1)，这将创建从左上角处开始，并将扩展到当前所绘制的区域的右下角的对角线渐变。 下图显示了默认值的线性渐变画笔的渐变轴<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>和<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>。  
  
 ![Gradient axis for a diagonal linear gradient](./media/wcpsdk-graphicsmm-diagonalgradientaxis.png "wcpsdk_graphicsmm_diagonalgradientaxis")  
  
 下面的示例演示如何创建水平渐变通过指定画笔<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>和<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>。 请注意，梯度停止点是与前面的示例; 相同只需更改<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A>和<xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A>，渐变已从对角线更改为水平。  
  
 [!code-xaml[GradientBrushExamples_snip#HorizontalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#horizontalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#HorizontalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#horizontalgradient1csharp)]  
  
 下图显示了创建的渐变。 渐变轴用虚线标记，梯度停止点用圆圈标记。  
  
 ![Gradient axis for a horizontal linear gradient](./media/wcpsdk-graphicsmm-horizontalgradient.jpg "wcpsdk_graphicsmm_horizontalgradient")  
  
 下一个示例演示如何创建垂直渐变。  
  
 [!code-xaml[GradientBrushExamples_snip#VerticalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#verticalgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#VerticalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#verticalgradient1csharp)]  
  
 下图显示了创建的渐变。 渐变轴用虚线标记，梯度停止点用圆圈标记。  
  
 ![Gradient axis for a vertical gradient](./media/wcpsdk-graphicsmm-verticalgradient.jpg "wcpsdk_graphicsmm_verticalgradient")  
  
<a name="radialgradients"></a>   
## <a name="radial-gradients"></a>径向渐变  
 像<xref:System.Windows.Media.LinearGradientBrush>、<xref:System.Windows.Media.RadialGradientBrush>使用沿轴混合在一起的颜色绘制区域。 前面的示例演示线性渐变画笔的轴是一条直线。 径向渐变画笔的轴由圆圈定义；它的颜色从原点开始向外“辐射”。  
  
 在下面的示例中，用径向渐变画笔绘制矩形内部。  
  
 [!code-xaml[GradientBrushExamples_snip#RadialGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/RadialGradientBrushExample.xaml#radialgradient1xaml)]  
  
 [!code-csharp[GradientBrushExamples_snip#RadialGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/RadialGradientBrushExample.cs#radialgradient1csharp)]  
  
 下图显示了上一示例中创建的渐变。 画笔的梯度停止点得到突出显示。 请注意，虽然结果不同，但该示例中梯度停止点与前面几个线性渐变画笔示例中的梯度停止点相同。  
  
 ![径向渐变中的梯度停止点](./media/wcpsdk-graphicsmm-4gradientstops-rg.png "wcpsdk_graphicsmm_4gradientstops_rg")  
  
 <xref:System.Windows.Media.RadialGradientBrush.GradientOrigin%2A>指定径向渐变画笔的渐变轴起点。 渐变轴从渐变原点向渐变圆辐射开来。 画笔的渐变圆圈由其<xref:System.Windows.Media.RadialGradientBrush.Center%2A>， <xref:System.Windows.Media.RadialGradientBrush.RadiusX%2A>，和<xref:System.Windows.Media.RadialGradientBrush.RadiusY%2A>属性。  
  
 下图显示了具有不同的多个径向渐变<xref:System.Windows.Media.RadialGradientBrush.GradientOrigin%2A>， <xref:System.Windows.Media.RadialGradientBrush.Center%2A>， <xref:System.Windows.Media.RadialGradientBrush.RadiusX%2A>，和<xref:System.Windows.Media.RadialGradientBrush.RadiusY%2A>设置。  
  
 ![RadialGradientBrush 设置](./media/wcpsdk-graphicsmm-originscirclesandradii.gif "wcpsdk_graphicsmm_originscirclesandradii")  
具有不同 GradientOrigin、Center、RadiusX 和 RadiusY 设置的 RadialGradientBrush。  
  
<a name="specifyinggradientcolors"></a>   
## <a name="specifying-transparent-or-partially-transparent-gradient-stops"></a>指定透明或部分透明的梯度停止点  
 由于梯度停止点不提供 opacity 属性，因此必须指定使用的颜色的 alpha 通道[!INCLUDE[TLA#tla_argb](../../../../includes/tlasharptla-argb-md.md)]标记或使用十六进制表示法<xref:System.Windows.Media.Color.FromScRgb%2A?displayProperty=nameWithType>方法创建透明或部分透明的梯度停止点。 下面的几节介绍如何在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 和代码中创建部分透明的梯度停止点。  
  
<a name="argbsyntax"></a>   
### <a name="specifying-color-opacity-in-xaml"></a>在“XAML”中指定颜色不透明度  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中，使用 [!INCLUDE[TLA2#tla_argb](../../../../includes/tla2sharptla-argb-md.md)] 十六进制表示法指定个别颜色的不透明度。 [!INCLUDE[TLA2#tla_argb](../../../../includes/tla2sharptla-argb-md.md)] 十六进制表示法使用下面语法：  
  
 `#` **aa** *rrggbb*  
  
 上一行中的 *aa* 表示用于指定颜色不透明度的两位十六进制值。 *rr*、*gg* 和 *bb* 分别表示用于指定颜色中的红色、绿色和蓝色量的两位十六进制值。 每个十六进制数字介于 0-9 或 A-F 之间。 0 是最小值，F 是最大值。 00 的 alpha 值指定完全透明的颜色，而 FF 的 alpha 值创建完全不透明的颜色。  在下面的示例中，十六进制 [!INCLUDE[TLA2#tla_argb](../../../../includes/tla2sharptla-argb-md.md)] 表示法用于指定两种颜色。 第一种为部分透明（alpha 值为 x20），而第二种为完全不透明。  
  
 [!code-xaml[GradientBrushExamples_snip#TransparentGradientStopExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/GradientStopsExample.xaml#transparentgradientstopexample1xaml)]  
  
<a name="fromscrgbsyntax"></a>   
### <a name="specifying-color-opacity-in-code"></a>在代码中指定颜色的不透明度  
 使用代码时，静态<xref:System.Windows.Media.Color.FromArgb%2A>方法可用于创建一种颜色时指定的 alpha 值。 该方法采用四个参数的类型<xref:System.Byte>。 第一个参数指定颜色的 alpha 通道；其他三个参数指定颜色的红色值、绿色值和蓝色值。 每个值应介于 0 与 255 之间（含 0 和 255）。 alpha 值为 0 表示颜色完全透明，alpha 值为 255 表示颜色完全不透明。 在以下示例中，<xref:System.Windows.Media.Color.FromArgb%2A>方法用于生成两种颜色。 第一种颜色为部分透明（alpha 值为 32），而第二种颜色为完全不透明。  
  
 [!code-csharp[GradientBrushExamples_snip#TransparentGradientStopExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/GradientStopsExample.cs#transparentgradientstopexample1csharp)]  
  
 或者，可能会使用<xref:System.Windows.Media.Color.FromScRgb%2A>方法，使您可以使用 ScRGB 值创建一种颜色。  
  
<a name="otherbrushes"></a>   
## <a name="painting-with-images-drawings-visuals-and-patterns"></a>使用图像、绘图、Visual 和模式进行绘制  
 <xref:System.Windows.Media.ImageBrush><xref:System.Windows.Media.DrawingBrush>，和<xref:System.Windows.Media.VisualBrush>类使您可以使用图像、 绘图或视觉对象绘制区域。 有关使用图像、绘图和模式进行绘制的详细信息，请参阅[使用图像、绘图和 Visual 进行绘制](painting-with-images-drawings-and-visuals.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.SolidColorBrush>
- <xref:System.Windows.Media.LinearGradientBrush>
- <xref:System.Windows.Media.RadialGradientBrush>
- [使用图像、绘图和视觉对象进行绘制](painting-with-images-drawings-and-visuals.md)
- [画笔转换概述](brush-transformation-overview.md)
- [图形呈现层](../advanced/graphics-rendering-tiers.md)
