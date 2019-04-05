---
title: 如何：对渐变应用灰度校正
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- gradient brushes [Windows Forms], gamma correction
- gradients [Windows Forms], gamma correction
ms.assetid: da4690e7-5fac-4fd2-b3f0-5cb35c165b92
ms.openlocfilehash: e7205058bc2b93ac453b8c37bfc8d5236433158d
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708072"
---
# <a name="how-to-apply-gamma-correction-to-a-gradient"></a>如何：对渐变应用灰度校正
可以通过设置画笔的启用线性渐变画笔的灰度校正<xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A>属性设置为`true`。 可以通过设置禁用灰度校正<xref:System.Drawing.Drawing2D.LinearGradientBrush.GammaCorrection%2A>属性设置为`false`。 默认情况下禁用灰度校正。  
  
## <a name="example"></a>示例  
 该示例创建线性渐变画笔，并使用该画笔来填充两个矩形。 第一个矩形填充而无需灰度校正和第二个矩形填充与灰度校正。  
  
 下图显示了两个实心的矩形。 不具有灰度校正的顶部矩形显示为灰色中间。 下面的矩形采用具有灰度校正，似乎亮度更均匀。  
  
 ![渐变](./media/gammagradient1.png "gammagradient1")  
  
 [!code-csharp[System.Drawing.UsingaGradientBrush#31](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.UsingaGradientBrush#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingaGradientBrush/VB/Class1.vb#31)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs> `e`，后者是 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Drawing2D.LinearGradientBrush>
- [使用渐变画笔填充形状](using-a-gradient-brush-to-fill-shapes.md)
