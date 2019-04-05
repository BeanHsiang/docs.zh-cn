---
title: 位图效果概述
ms.date: 03/30/2017
helpviewer_keywords:
- bitmap effects [WPF]
ms.assetid: 23cb338e-4b59-4b52-b294-96431f9c9568
ms.openlocfilehash: e82a9596778a3c71aca6bdb8efcb9b3aa227cadb
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368215"
---
# <a name="bitmap-effects-overview"></a>位图效果概述
位图效果，设计人员和开发人员应用到视觉效果呈现 Windows Presentation Foundation (WPF) 内容。 例如，位图效果，您可以轻松地将应用<xref:System.Windows.Media.Effects.DropShadowBitmapEffect>效果或模糊效果到图像或按钮。  
  
> [!IMPORTANT]
>  在中[!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]或更高版本，<xref:System.Windows.Media.Effects.BitmapEffect>类已过时。 如果尝试使用<xref:System.Windows.Media.Effects.BitmapEffect>类，您将收到已过时异常。 非过时替代项为<xref:System.Windows.Media.Effects.BitmapEffect>类是<xref:System.Windows.Media.Effects.Effect>类。 在大多数情况下，<xref:System.Windows.Media.Effects.Effect>类是快得多。  
  
  
  
<a name="wpf_effects"></a>   
## <a name="wpf-bitmap-effects"></a>WPF 位图效果  
 位图效果 (<xref:System.Windows.Media.Effects.BitmapEffect>对象) 是简单的像素处理操作。 位图效果采用<xref:System.Windows.Media.Imaging.BitmapSource>作为输入并生成一个新<xref:System.Windows.Media.Imaging.BitmapSource>后应用效果，如模糊或投影。 每个位图效果公开用于控制筛选的属性，如<xref:System.Windows.Media.Effects.BlurBitmapEffect.Radius%2A>的<xref:System.Windows.Media.Effects.BlurBitmapEffect>。  
  
 作为一种特殊情况，在[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，可以将效果设置为属性上实时<xref:System.Windows.Media.Visual>对象，如<xref:System.Windows.Controls.Button>或<xref:System.Windows.Controls.TextBox>。 像素处理在运行时应用并呈现。 在这种情况下，在呈现时<xref:System.Windows.Media.Visual>自动转换为其<xref:System.Windows.Media.Imaging.BitmapSource>等效和作为输入发送给<xref:System.Windows.Media.Effects.BitmapEffect>。 输出将替换<xref:System.Windows.Media.Visual>对象的默认呈现行为。 这就是为什么<xref:System.Windows.Media.Effects.BitmapEffect>对象强制视觉对象在软件中呈现仅即视觉对象上的没有硬件加速，应用效果时。  
  
-   <xref:System.Windows.Media.Effects.BlurBitmapEffect> 模拟显示聚焦不准的对象。  
  
-   <xref:System.Windows.Media.Effects.OuterGlowBitmapEffect> 创建一个对象周围的颜色的。  
  
-   <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> 创建对象后的阴影。  
  
-   <xref:System.Windows.Media.Effects.BevelBitmapEffect> 创建凹凸效果，根据指定的曲线图像表面。  
  
-   <xref:System.Windows.Media.Effects.EmbossBitmapEffect> 创建的凹凸贴图<xref:System.Windows.Media.Visual>以便从人工光源的深度和纹理效果。  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 位图效果在软件模式下呈现。 应用效果的任何对象也都将以软件形式呈现。 在大型视觉对象上使用位图效果或对位图效果的属性进行动画处理时，性能的下降幅度最大。 这并不表示完全不应该以这种方式使用位图效果，而是应谨慎使用，并进行全面测试以确保用户得到预期的体验。  
  
> [!NOTE]
>  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 位图效果不支持部分信任执行。 应用程序必须具有完全信任权限才能使用位图效果。  
  
<a name="applyeffects"></a>   
## <a name="how-to-apply-an-effect"></a>如何应用效果  
 <xref:System.Windows.Media.Effects.BitmapEffect> 一个属性<xref:System.Windows.Media.Visual>。 因此将效果应用于视觉对象，如<xref:System.Windows.Controls.Button>， <xref:System.Windows.Controls.Image>， <xref:System.Windows.Media.DrawingVisual>，或<xref:System.Windows.UIElement>，就像设置属性一样简单。 <xref:System.Windows.UIElement.BitmapEffect%2A> 可以将设置为单个<xref:System.Windows.Media.Effects.BitmapEffect>可以通过使用链接对象或多个效果<xref:System.Windows.Media.Effects.BitmapEffectGroup>对象。  
  
 下面的示例演示如何将应用<xref:System.Windows.Media.Effects.BitmapEffect>在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。  
  
 [!code-xaml[EffectsGallery_snip#BlurSimpleExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blursimpleexample.xaml#blursimpleexampleinline)]  
  
 下面的示例演示如何将应用<xref:System.Windows.Media.Effects.BitmapEffect>在代码中。  
  
 [!code-csharp[EffectsGallery_snip#CodeBehindBlurCodeBehindExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blurcodebehindexample.xaml.cs#codebehindblurcodebehindexampleinline)]  
  
> [!NOTE]
>  当<xref:System.Windows.Media.Effects.BitmapEffect>应用到布局容器，如<xref:System.Windows.Controls.DockPanel>或<xref:System.Windows.Controls.Canvas>，效果应用到元素或视觉对象，包括其所有子元素的可视化树。  
  
<a name="customeffects"></a>   
## <a name="creating-custom-effects"></a>创建自定义效果  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 还提供非托管接口，用于创建可在托管 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序中使用的自定义效果。 有关创建自定义位图效果的其他参考资料，请参阅[非托管 WPF 位图效果](https://docs.microsoft.com/previous-versions/windows/desktop/wibe/-wibe-lh)文档。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Media.Effects.BitmapEffectGroup>
- <xref:System.Windows.Media.Effects.BitmapEffectInput>
- <xref:System.Windows.Media.Effects.BitmapEffectCollection>
- [非托管的 WPF 位图效果](https://docs.microsoft.com/previous-versions/windows/desktop/wibe/-wibe-lh)
- [图像处理概述](imaging-overview.md)
- [安全性](../security-wpf.md)
- [WPF 图形呈现概述](wpf-graphics-rendering-overview.md)
- [2D 图形和图像处理](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
