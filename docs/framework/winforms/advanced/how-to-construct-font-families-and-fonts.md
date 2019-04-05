---
title: 如何：构造字体系列和字体
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- font families [Windows Forms], constructing
- fonts [Windows Forms], constructing
ms.assetid: d3a4a223-9492-4b54-9afd-db1c31c3cefd
ms.openlocfilehash: b651671e525ae5cfc365a392b96d258ac835a21c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708547"
---
# <a name="how-to-construct-font-families-and-fonts"></a>如何：构造字体系列和字体
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 分组为字体系列字样相同但不同的样式使用的字体。 例如，Arial 字体系列包含以下字体：  
  
-   Arial 常规  
  
-   Arial 粗体  
  
-   Arial 斜体  
  
-   宋体  
  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 使用四种字形形成系列： 常规、 粗体、 斜体和粗体斜体。 如形容词*缩小*并*舍入*不被视为样式; 而不是它们是系列名称的一部分。 例如，Arial 窄是字体系列包含下列成员：  
  
-   Arial 窄常规  
  
-   姚粗体  
  
-   Arial 窄斜体  
  
-   Arial 窄的加粗倾斜  
  
 您可以绘制与文本之前[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]，则需构造<xref:System.Drawing.FontFamily>对象和一个<xref:System.Drawing.Font>对象。 <xref:System.Drawing.FontFamily>对象指定 （例如，Arial） 字样和<xref:System.Drawing.Font>对象指定的大小、 样式和单位。  
  
## <a name="example"></a>示例  
 下面的示例构造正则样式 Arial 字体大小为 16 像素。 下面的代码中的第一个参数传递给<xref:System.Drawing.Font.%23ctor%2A>构造函数是<xref:System.Drawing.FontFamily>对象。 第二个参数指定度量单位由第四个参数标识的字体的大小。 第三个参数标识的样式。  
  
 <xref:System.Drawing.GraphicsUnit.Pixel> 是的成员<xref:System.Drawing.GraphicsUnit>枚举，并<xref:System.Drawing.FontStyle.Regular>属于<xref:System.Drawing.FontStyle>枚举。  
  
 [!code-csharp[System.Drawing.FontsAndText#61](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#61)]
 [!code-vb[System.Drawing.FontsAndText#61](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#61)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs>`e`，这是 <xref:System.Windows.Forms.PaintEventHandler> 的参数。  
  
## <a name="see-also"></a>请参阅
- [使用字体和文本](using-fonts-and-text.md)
- [Windows 窗体中的图形和绘制](graphics-and-drawing-in-windows-forms.md)
