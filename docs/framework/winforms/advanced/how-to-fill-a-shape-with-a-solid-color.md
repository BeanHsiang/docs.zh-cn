---
title: 如何：用纯色填充形状
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- colors [Windows Forms], adding to shapes
- shapes [Windows Forms], filling
ms.assetid: 06088b31-bac9-4ef3-9ebe-06c2c764d6df
ms.openlocfilehash: 8bc782f9496a9c1562bad2df1ba196fb39572e68
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704424"
---
# <a name="how-to-fill-a-shape-with-a-solid-color"></a>如何：用纯色填充形状
若要使用纯色填充形状，创建<xref:System.Drawing.SolidBrush>对象，，然后将其传递<xref:System.Drawing.SolidBrush>对象的填充方法之一的参数作为<xref:System.Drawing.Graphics>类。 下面的示例演示如何使用的颜色为红色填充椭圆。  
  
## <a name="example"></a>示例  
 在下面的代码中，<xref:System.Drawing.SolidBrush.%23ctor%2A>构造函数采用<xref:System.Drawing.Color>对象作为其唯一参数。 使用的值<xref:System.Drawing.Color.FromArgb%2A>方法表示颜色的 alpha、 红色、 绿色和蓝色组件。 每个值必须在范围 0 到 255 之间。 第一个 255 表示颜色完全不透明，，第二个 255 表示该红色组件达到最大亮度。 两个零表示绿色和蓝色分量的强度为 0。  
  
 四个数字 （0，0，100，60） 传递给<xref:System.Drawing.Graphics.FillEllipse%2A>方法指定的位置和大小的椭圆的边框。 矩形具有的左上角 （0，0），100，宽度和高度为 60。  
  
 [!code-csharp[System.Drawing.UsingABrush#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.UsingABrush#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs> `e`，后者是 <xref:System.Windows.Forms.Control.Paint> 事件处理程序的参数。  
  
## <a name="see-also"></a>请参阅
- [使用画笔填充形状](using-a-brush-to-fill-shapes.md)
