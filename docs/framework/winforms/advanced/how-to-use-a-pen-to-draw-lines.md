---
title: 如何：使用笔绘制直线
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- lines [Windows Forms], drawing
- pens [Windows Forms], drawing lines
ms.assetid: 0828c331-a438-4bdd-a4d6-3ef1e59e8795
ms.openlocfilehash: 3af91611eef4b97dc3461ad8cd7e36c7aa10a16f
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713359"
---
# <a name="how-to-use-a-pen-to-draw-lines"></a>如何：使用笔绘制直线
若要绘制线条，需要<xref:System.Drawing.Graphics>对象和一个<xref:System.Drawing.Pen>对象。 <xref:System.Drawing.Graphics>对象提供<xref:System.Drawing.Graphics.DrawLine%2A>方法，和<xref:System.Drawing.Pen>对象将存储的行中，如颜色和宽度的功能。  
  
## <a name="example"></a>示例  
 下面的示例绘制中的一行 （20、 10） 到 （300，100）。 第一个语句使用<xref:System.Drawing.Pen.%23ctor%2A>类构造函数创建黑色的笔。 一个自变量传递给<xref:System.Drawing.Pen.%23ctor%2A>构造函数是<xref:System.Drawing.Color>使用创建的对象<xref:System.Drawing.Color.FromArgb%2A>方法。 用来创建的值<xref:System.Drawing.Color>对象 — （255，0，0，0） — 对应于颜色的 alpha、 红色、 绿色和蓝色组件。 这些值定义不透明的黑色笔。  
  
 [!code-csharp[System.Drawing.UsingAPen#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingAPen/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingAPen#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingAPen/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs>`e`，后者是 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Pen>
- [使用笔绘制直线和形状](using-a-pen-to-draw-lines-and-shapes.md)
- [GDI+ 中的笔、直线和矩形](pens-lines-and-rectangles-in-gdi.md)
