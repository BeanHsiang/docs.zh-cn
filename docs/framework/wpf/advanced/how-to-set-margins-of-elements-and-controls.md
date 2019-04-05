---
title: 如何：设置元素和控件的边距
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- setting [WPF], Margin property
- properties [WPF], Margin property
- Margin property [WPF], setting
ms.assetid: 70ebee01-6f87-4352-8dd4-402c65eaaed6
ms.openlocfilehash: 3263810806b6b4bbec15eadfd1f1da3a57d12698
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356268"
---
# <a name="how-to-set-margins-of-elements-and-controls"></a>如何：设置元素和控件的边距
此示例介绍了如何设置<xref:System.Windows.FrameworkElement.Margin%2A>属性，通过更改在代码隐藏中的边距的任何现有属性值。 <xref:System.Windows.FrameworkElement.Margin%2A>属性是属性的<xref:System.Windows.FrameworkElement>基元素，并因此由各种控件和其他元素继承。  
  
 此示例用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，使用代码隐藏文件[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]引用。 代码隐藏显示在C#和 Microsoft Visual Basic 版本。  
  
## <a name="example"></a>示例  
 [!code-xaml[FEMarginProgrammatic#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[FEMarginProgrammatic#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/FEMarginProgrammatic/CSharp/default.xaml.cs#handler)]
 [!code-vb[FEMarginProgrammatic#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FEMarginProgrammatic/VisualBasic/default.xaml.vb#handler)]
