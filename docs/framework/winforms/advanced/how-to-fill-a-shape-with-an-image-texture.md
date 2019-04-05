---
title: 如何：用图像纹理填充形状
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], using with brushes
- bitmaps [Windows Forms], using texture
- shapes [Windows Forms], filling with images
ms.assetid: 508da5a6-2433-4d2b-9680-eaeae4e96e3b
ms.openlocfilehash: 89ebad6773b076514f5a745db653e0e0a18d4b48
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708439"
---
# <a name="how-to-fill-a-shape-with-an-image-texture"></a>如何：用图像纹理填充形状
可以通过用纹理填充闭合的形状<xref:System.Drawing.Image>类和<xref:System.Drawing.TextureBrush>类。  
  
## <a name="example"></a>示例  
 下面的示例填充椭圆的映像。 该代码构造<xref:System.Drawing.Image>对象，并随后将传递该地址<xref:System.Drawing.Image>对象的参数作为<xref:System.Drawing.TextureBrush.%23ctor%2A>构造函数。 第三个语句缩放图像，并第四个语句填充椭圆的缩放的图像的重复副本。  
  
 在下面的代码，<xref:System.Drawing.TextureBrush.Transform%2A>属性包含的转换，以应用于映像。 假设原始图像的宽度为 640 像素，高度为 480 像素。 转换将图像缩小到 75 × 75 设置了水平和垂直缩放值。  
  
> [!NOTE]
>  在以下示例中，映像大小为 75 × 75，和椭圆大小为 150 × 250 个字符。 由于映像是小于它所填充的椭圆，椭圆与图像平铺。 达到了平铺意味着，重复图像水平和垂直直到形状的边界。 有关平铺的详细信息，请参阅[如何：使用图像形状中平铺](how-to-tile-a-shape-with-an-image.md)。  
  
 [!code-csharp[System.Drawing.UsingABrush#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.UsingABrush#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs> `e`，后者是 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数。  
  
## <a name="see-also"></a>请参阅
- [使用画笔填充形状](using-a-brush-to-fill-shapes.md)
