---
title: 如何：使用颜色矩阵在图像中设置 Alpha 值
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- images [Windows Forms], using color matrices for semi-transparent
- transparency [Windows Forms], color matrices
- matrices [Windows Forms], alpha values
- bitmaps [Windows Forms], using color matrices for semi-transparent
ms.assetid: a27121e6-f7e9-4c09-84e2-f05aa9d2a1bb
ms.openlocfilehash: 9e102f51d00953d05ed1d217a345e32178676ffe
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716322"
---
# <a name="how-to-use-a-color-matrix-to-set-alpha-values-in-images"></a>如何：使用颜色矩阵在图像中设置 Alpha 值
<xref:System.Drawing.Bitmap>类 (派生自<xref:System.Drawing.Image>类) 和<xref:System.Drawing.Imaging.ImageAttributes>类提供用于获取和设置像素值的功能。 可以使用<xref:System.Drawing.Imaging.ImageAttributes>类来修改 alpha 值为整个图像，也可以调用<xref:System.Drawing.Bitmap.SetPixel%2A>方法的<xref:System.Drawing.Bitmap>类来修改单个像素的值。  
  
## <a name="example"></a>示例  
 <xref:System.Drawing.Imaging.ImageAttributes>类具有许多属性，可用于在呈现期间修改映像。 在以下示例中，<xref:System.Drawing.Imaging.ImageAttributes>对象用于将所有 alpha 值设置为它们的 80%。 这是通过初始化颜色矩阵并设置缩放到 0.8 矩阵中的值的 alpha。 颜色矩阵的地址传递给<xref:System.Drawing.Imaging.ImageAttributes.SetColorMatrix%2A>方法<xref:System.Drawing.Imaging.ImageAttributes>对象，并<xref:System.Drawing.Imaging.ImageAttributes>对象传递给<xref:System.Drawing.Graphics.DrawString%2A>方法<xref:System.Drawing.Graphics>对象。  
  
 在呈现期间，在位图中的 alpha 值将转换为它们的 80%。 这会导致混合和背景的图像。 如下图所示，位图图像看起来透明;您可以看到通过它黑色实线。  
  
 ![使用矩阵的 alpha 混合](./media/image2.png "image2")  
  
 图像是通过背景的白色部分，其中具有已与白色混合映像。 图像和黑色线条相交的位置与黑色混合映像。  
  
 [!code-csharp[System.Drawing.AlphaBlending#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.AlphaBlending/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.AlphaBlending#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.AlphaBlending/VB/Class1.vb#21)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs>`e`，这是 <xref:System.Windows.Forms.PaintEventHandler> 的参数。  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体中的图形和绘制](graphics-and-drawing-in-windows-forms.md)
- [alpha 值混合处理直线和填充](alpha-blending-lines-and-fills.md)
