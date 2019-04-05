---
title: 图形界面的结构
ms.date: 03/30/2017
helpviewer_keywords:
- GDI+, using managed interface
- graphics [Windows Forms], class structure
ms.assetid: 010a1e46-656b-40a1-8d5d-87aa05ee1243
ms.openlocfilehash: 33be9d4d4e5a1aca933bb84e948b2200cd96b152
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708103"
---
# <a name="structure-of-the-graphics-interface"></a>图形界面的结构
为托管的类接口[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]包含大约 60 个类、 50 个枚举和 8 个结构。 <xref:System.Drawing.Graphics>类的核心是[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]功能; 它是实际绘制线条、 曲线、 图形、 图像和文本的类。  
  
## <a name="important-classes"></a>重要的类  
 许多类处理一起<xref:System.Drawing.Graphics>类。 例如，<xref:System.Drawing.Graphics.DrawLine%2A>方法接收<xref:System.Drawing.Pen>对象，其中包含要绘制的行的属性 （颜色、 宽度、 短划线样式等）。 <xref:System.Drawing.Graphics.FillRectangle%2A>方法可以接收一个指向<xref:System.Drawing.Drawing2D.LinearGradientBrush>对象，适用于<xref:System.Drawing.Graphics>对象来填充渐变的颜色的矩形。 <xref:System.Drawing.Font> 并<xref:System.Drawing.StringFormat>对象会影响方式<xref:System.Drawing.Graphics>对象绘制的文本。 一个<xref:System.Drawing.Drawing2D.Matrix>对象存储和操作的世界转换<xref:System.Drawing.Graphics>用于旋转、 缩放和翻转图像的对象。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 提供了几种结构 (例如， <xref:System.Drawing.Rectangle>， <xref:System.Drawing.Point>，和<xref:System.Drawing.Size>) 用于组织图形数据。 此外，某些类提供数据的主要结构化的类型。 例如，<xref:System.Drawing.Imaging.BitmapData>类是一个帮助程序对于<xref:System.Drawing.Bitmap>类，并<xref:System.Drawing.Drawing2D.PathData>类是一个帮助程序对于<xref:System.Drawing.Drawing2D.GraphicsPath>类。  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 定义多个枚举，它们是相关常量的集合。 例如，<xref:System.Drawing.Drawing2D.LineJoin>枚举包含的元素<xref:System.Drawing.Drawing2D.LineJoin.Bevel>， <xref:System.Drawing.Drawing2D.LineJoin.Miter>，和<xref:System.Drawing.Drawing2D.LineJoin.Round>，它指定可用于联接两条线的样式。  
  
## <a name="see-also"></a>请参阅
- [图形概述](graphics-overview-windows-forms.md)
- [关于 GDI+ 托管代码](about-gdi-managed-code.md)
- [使用托管图形类](using-managed-graphics-classes.md)
