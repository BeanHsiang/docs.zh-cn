---
title: 如何：使用 SystemFonts
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- system fonts [WPF]
- fonts [WPF], system fonts
- classes [WPF], SystemFonts
ms.assetid: 3f46a4ec-2225-408a-8123-8838a8f7057a
ms.openlocfilehash: 5ed44da316ddee5ea3a83262f913da571bf75276
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378894"
---
# <a name="how-to-use-systemfonts"></a>如何：使用 SystemFonts
此示例演示如何使用的静态资源<xref:System.Windows.SystemFonts>样式或自定义按钮的类。  
  
## <a name="example"></a>示例  
 系统资源将系统确定的许多值以资源和属性的形式公开，以帮助创建与系统设置一致的视觉效果。 <xref:System.Windows.SystemFonts> 是包含这两个系统字体值作为静态属性和引用可用于在运行时动态访问这些值的资源键的属性的类。 例如，<xref:System.Windows.SystemFonts.CaptionFontFamily%2A>是<xref:System.Windows.SystemFonts>值，和<xref:System.Windows.SystemFonts.CaptionFontFamilyKey%2A>是相应的资源键。  
  
 在中[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，你可以使用的成员<xref:System.Windows.SystemFonts>作为静态属性或动态资源引用 （静态属性值作为键）。 如果希望字体规格在应用程序运行时自动更新，请使用动态资源引用；否则，请使用静态值引用。  
  
> [!NOTE]
>  资源键属性名称后面附有“Key”后缀。  
  
 下面的示例演示如何访问和使用的属性<xref:System.Windows.SystemFonts>作为静态值来设置样式或自定义按钮。 此标记示例将分配<xref:System.Windows.SystemFonts>至一个按钮的值。  
  
 [!code-xaml[SystemRes_snip#FontStaticResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml#fontstaticresources)]  
  
 若要使用的值<xref:System.Windows.SystemFonts>不需要在代码中，使用静态值或动态资源引用。 相反，使用的非键属性<xref:System.Windows.SystemFonts>类。 尽管非键属性已明确定义的运行时行为的静态属性形式[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]承载系统将重新评估在真实时间中的属性，并且会适当考虑对系统值面向用户的更改。 以下示例演示如何指定按钮的字体设置。  
  
 [!code-csharp[SystemRes_snip#FontResourcesCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/Pane1.xaml.cs#fontresourcescode)]
 [!code-vb[SystemRes_snip#FontResourcesCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SystemRes_snip/VisualBasic/Pane1.xaml.vb#fontresourcescode)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.SystemFonts>
- [使用系统画笔绘制区域](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [使用 SystemParameters](how-to-use-systemparameters.md)
- [使用系统字体键](how-to-use-system-fonts-keys.md)
- [帮助主题](resources-how-to-topics.md)
- [x:Static 标记扩展](../../xaml-services/x-static-markup-extension.md)
- [XAML 资源](xaml-resources.md)
- [DynamicResource 标记扩展](dynamicresource-markup-extension.md)
