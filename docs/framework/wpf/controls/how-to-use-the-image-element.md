---
title: 如何：使用 Image 元素
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], Image
- Image control [WPF]
- rendering images [WPF]
ms.assetid: 5b92e74b-1b56-4756-ac64-d5e9e08d9854
ms.openlocfilehash: ec3ca16915038ebbb68df24bfd071168c346663d
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372459"
---
# <a name="how-to-use-the-image-element"></a>如何：使用 Image 元素
此示例演示如何通过使用应用程序中包含图像<xref:System.Windows.Controls.Image>元素。  
  
## <a name="example"></a>示例  
 下面的示例演示如何呈现宽为 200 像素的图像。 在此 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 示例中，同时使用特性语法和属性标记语法来定义图像。 有关特性语法和属性语法的详细信息，请参阅[依赖属性概述](../advanced/dependency-properties-overview.md)。 一个<xref:System.Windows.Media.Imaging.BitmapImage>用于定义图像的源数据并为属性标记语法示例显式定义。 此外，<xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A>的<xref:System.Windows.Media.Imaging.BitmapImage>设置为宽度相同<xref:System.Windows.FrameworkElement.Width%2A>的<xref:System.Windows.Controls.Image>。 这样做是为了确保呈现图像所使用的内存量最小。  
  
> [!NOTE]
>  如果你想要指定呈现图像的大小，一般情况下，仅指定<xref:System.Windows.FrameworkElement.Width%2A>或<xref:System.Windows.FrameworkElement.Height%2A>但不可同时使用两者。 如果仅指定一个，则会保持图像的纵横比。 否则，图像可能会出现意外的拉伸或扭曲。 若要控制图像的拉伸行为，请使用<xref:System.Windows.Controls.Image.Stretch%2A>和<xref:System.Windows.Controls.Image.StretchDirection%2A>属性。  
  
> [!NOTE]
>  映像的大小指定的<xref:System.Windows.FrameworkElement.Width%2A>或<xref:System.Windows.FrameworkElement.Height%2A>，你还应设置<xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelWidth%2A>或<xref:System.Windows.Media.Imaging.BitmapImage.DecodePixelHeight%2A>的相应大小。  
  
 <xref:System.Windows.Controls.Image.Stretch%2A>属性确定如何拉伸图像源来填充图像元素。 有关详细信息，请参见 <xref:System.Windows.Media.Stretch> 枚举。  
  
 [!code-xaml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
## <a name="example"></a>示例  
 以下示例演示如何使用代码呈现宽度为 200 像素的图像。  
  
> [!NOTE]
>  设置<xref:System.Windows.Media.Imaging.BitmapImage>属性必须在完成<xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A>和<xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A>块。  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
## <a name="see-also"></a>请参阅
- [图像处理概述](../graphics-multimedia/imaging-overview.md)
