---
title: 如何：创建空心文字
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- typography [WPF], linear gradient brush
- outlined text [WPF]
- gradient brush [WPF]
- linear gradient brush [WPF]
- typography [WPF], outline effects
ms.assetid: 4aa3cf6e-1953-4f26-8230-7c1409e5f28d
ms.openlocfilehash: 5de1068401dac61c5de5b86604da9417e18a94ae
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2019
ms.locfileid: "58125936"
---
# <a name="how-to-create-outlined-text"></a>如何：创建空心文字
在大多数情况下，当要将装饰添加到中的文本字符串时您[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]应用程序中，使用的根据一系列离散的字符或字形的文本。 例如，您可以创建线性渐变画笔，并将其应用于<xref:System.Windows.Controls.Control.Foreground%2A>属性的<xref:System.Windows.Controls.TextBox>对象。 当显示或编辑文本框中时，线性渐变画笔是自动应用于当前集的文本字符串中的字符。  
  
 ![使用线性渐变画笔显示的文本](./media/how-to-create-outlined-text/text-linear-gradient.jpg)    
  
 但是，您还可以将转换到的文本<xref:System.Windows.Media.Geometry>对象，它允许您创建其他类型的可视化多格式文本。 例如，可以创建<xref:System.Windows.Media.Geometry>基于对象的轮廓上的文本字符串。  
  
 ![使用线性渐变画笔的文本轮廓](./media/how-to-create-outlined-text/text-outline-linear-gradient.jpg)  
  
 当文本转换为<xref:System.Windows.Media.Geometry>对象，它不再是一系列字符，不能修改文本字符串中的字符。 但是，可修改已转换文本的笔划和填充属性，以此来影响该文本的外观。 笔划是指已转换文本的轮廓；填充是指已转换文本的轮廓的内部区域。  
  
 下面的示例演示了多种方法可以通过修改的笔划和填充的已转换的文本来创建视觉效果。  
  
 ![对填充和笔画使用不同颜色的文本](./media/how-to-create-outlined-text/fill-stroke-text-effect.jpg)  
  
 ![笔画应用了图像画笔的文本](./media/how-to-create-outlined-text/image-brush-application.jpg)
  
 还有可能要修改的边界框矩形或突出显示，已转换的文本。 下面的示例演示通过修改笔划和突出显示的已转换的文本的一种方法来创建视觉效果。  
  
 ![应用绘制笔画，并突出显示了图像画笔的文本](./media/how-to-create-outlined-text/image-brush-text-application.jpg)

## <a name="example"></a>示例  
 将文本转换为密钥<xref:System.Windows.Media.Geometry>对象是使用<xref:System.Windows.Media.FormattedText>对象。 创建此对象后，可以使用<xref:System.Windows.Media.FormattedText.BuildGeometry%2A>并<xref:System.Windows.Media.FormattedText.BuildHighlightGeometry%2A>方法将转换为文本<xref:System.Windows.Media.Geometry>对象。 第一种方法将返回带格式的文本; 的几何图形第二种方法返回带格式的文本的几何图形的边界框。 下面的代码示例演示如何创建<xref:System.Windows.Media.FormattedText>对象以及如何检索几何图形的带格式的文本和其边界框。  
  
 [!code-csharp[OutlineTextControlViewer#CreateText](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#createtext)]
 [!code-vb[OutlineTextControlViewer#CreateText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#createtext)]  
  
 要显示检索<xref:System.Windows.Media.Geometry>对象，您需要访问<xref:System.Windows.Media.DrawingContext>显示已转换的文本的对象。 在这些代码示例中，这可通过创建从支持用户定义的呈现的类派生的自定义控件对象。  
  
 若要显示<xref:System.Windows.Media.Geometry>自定义控件中的对象提供的替代<xref:System.Windows.UIElement.OnRender%2A>方法。 重写的方法应使用<xref:System.Windows.Media.DrawingContext.DrawGeometry%2A>方法，以便绘制<xref:System.Windows.Media.Geometry>对象。  
  
 [!code-csharp[OutlineTextControlViewer#OnRender](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#onrender)]
 [!code-vb[OutlineTextControlViewer#OnRender](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#onrender)]  
  
  示例自定义用户控件对象的源，请参阅[OutlineTextControl.cs 为C#](https://github.com/dotnet/samples/blob/master/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs)并[OutlineTextControl.vb 适用于 Visual Basic](https://github.com/dotnet/samples/blob/master/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb)。 
  
## <a name="see-also"></a>请参阅
- [绘制格式化文本](drawing-formatted-text.md)
