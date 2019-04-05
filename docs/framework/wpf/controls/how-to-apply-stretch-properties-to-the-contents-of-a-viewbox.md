---
title: 如何：向 Viewbox 的内容应用 Stretch 属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- StretchDirection properties [WPF]
- Stretch properties [WPF]
- controls [WPF], Viewbox
- Viewbox control [WPF]
ms.assetid: b9c22ef4-bce4-4300-9e0c-8260b7db83cc
ms.openlocfilehash: 96d6584debe3e0dc85121cbcde5e6b4d1ac8c75c
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352472"
---
# <a name="how-to-apply-stretch-properties-to-the-contents-of-a-viewbox"></a>如何：向 Viewbox 的内容应用 Stretch 属性
## <a name="example"></a>示例  
 此示例演示如何更改的值<xref:System.Windows.Controls.Viewbox.StretchDirection%2A>并<xref:System.Windows.Controls.Viewbox.Stretch%2A>的属性<xref:System.Windows.Controls.Viewbox>。  
  
 第一个示例使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]来定义<xref:System.Windows.Controls.Viewbox>元素。 它将分配<xref:System.Windows.FrameworkElement.MaxWidth%2A>和<xref:System.Windows.FrameworkElement.MaxHeight%2A>为 400。 示例嵌套<xref:System.Windows.Controls.Image>元素内的<xref:System.Windows.Controls.Viewbox>。 <xref:System.Windows.Controls.Button> 有关的属性值相对应的元素<xref:System.Windows.Controls.Viewbox.Stretch%2A>并<xref:System.Windows.Controls.StretchDirection>枚举操作的嵌套的拉伸行为<xref:System.Windows.Controls.Image>。  
  
 [!code-xaml[viewboxStretchLayoutSamp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml#1)]  
  
 下面的代码隐藏文件句柄<xref:System.Windows.Controls.Button><xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件的上一个[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]的示例定义。  
  
 [!code-csharp[viewboxStretchLayoutSamp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/viewboxStretchLayoutSamp/CSharp/Window1.xaml.cs#2)]
 [!code-vb[viewboxStretchLayoutSamp#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/viewboxStretchLayoutSamp/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Controls.Viewbox>
- <xref:System.Windows.Media.Stretch>
- <xref:System.Windows.Controls.StretchDirection>
