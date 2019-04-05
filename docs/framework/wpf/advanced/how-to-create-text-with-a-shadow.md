---
title: 如何：创建具有阴影的文本
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], shadow effects
- shadow effects in text [WPF]
- text [WPF], shadowed
ms.assetid: 6ab9c754-6001-4708-b479-5367f2fd1a35
ms.openlocfilehash: a2225e297dbc0b5f9d49799cb34eb5539746e62e
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2019
ms.locfileid: "58125780"
---
# <a name="how-to-create-text-with-a-shadow"></a>如何：创建具有阴影的文本
本节中的示例演示如何为所显示的文本创建阴影效果。  
  
## <a name="example"></a>示例  
 <xref:System.Windows.Media.Effects.DropShadowEffect>对象允许你创建的阴影效果的各种[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]对象。 以下示例显示了应用于文本的投影效果。 在本例中，阴影是柔和阴影，这意味着阴影颜色模糊化。  
  
 ![文本阴影的柔和度&#61;0.25](./media/how-to-create-text-with-a-shadow/drop-shadow-text-effect.jpg) 
  
 您可以通过设置来控制阴影的宽度<xref:System.Windows.Media.Effects.DropShadowEffect.ShadowDepth%2A>属性。 值为`4.0`指示阴影宽度为 4 个像素。 您可以控制柔和度，或通过修改阴影的模糊<xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A>属性。 值为`0.0`指示无模糊。 以下代码示例演示如何创建柔和阴影。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet1)]  
  
> [!NOTE]
>  这些柔和效果不会[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]文本呈现管道。 因此，在使用这些效果时，将禁用 ClearType。  
  
 以下示例显示了应用于文本的硬投影效果。 在此例中，阴影不模糊。  
  
 ![文本阴影的柔和度&#61;0](./media/how-to-create-text-with-a-shadow/text-shadow-softness.jpg) 
  
 可以通过设置创建硬阴影<xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A>属性设置为`0.0`，指示使用无模糊。 可以通过修改控制阴影的方向<xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A>属性。 设置此属性的方向值为之间的度数`0`和`360`。 下图显示了的方向值<xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A>属性设置。  
  
 ![阴影的 DropShadow 程度设置](./media/how-to-create-text-with-a-shadow/drop-shadow-degree-setting.png)
  
 以下代码示例演示如何创建硬阴影。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet2)]  
  
## <a name="using-a-blur-effect"></a>使用模糊效果  
 一个<xref:System.Windows.Media.Effects.BlurBitmapEffect>可用于创建可放置在文本对象之后的类似于阴影的效果。 应用于文本的模糊位图效果在各个方向上均匀地对文本进行模糊化。  
  
 以下示例显示了应用于文本的模糊效果。  
  
 ![使用 BlurBitmapEffect 的文本阴影](./media/how-to-create-text-with-a-shadow/text-shadow-blur-effect.jpg)  
  
 以下代码示例演示如何创建模糊效果。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet6](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/BlurShadows.xaml#textshadowsnippet6)]  
  
## <a name="using-a-translate-transform"></a>使用转换变换  
 一个<xref:System.Windows.Media.TranslateTransform>可用于创建可放置在文本对象之后的类似于阴影的效果。  
  
 下面的代码示例使用<xref:System.Windows.Media.TranslateTransform>来偏移文本。 在本示例中，主要文本下方略微偏移的文本副本营造出了阴影效果。  
  
 ![使用 TranslateTransform 的文本阴影](./media/how-to-create-text-with-a-shadow/text-transform-shadow-effect.jpg)    
  
 以下代码示例演示如何创建转换以实现阴影效果。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/TransformShadows.xaml#textshadowsnippet7)]
