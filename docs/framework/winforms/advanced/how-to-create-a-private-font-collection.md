---
title: 如何：创建专用的字体集合
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- private font collections [Windows Forms], creating
- fonts [Windows Forms], creating private collections
ms.assetid: 6533d5e5-a8dc-4b76-9fc4-3bf75c8b9212
ms.openlocfilehash: 7cfd2a1fd29b58019d49c8cd5df9adb5b0873302
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723772"
---
# <a name="how-to-create-a-private-font-collection"></a>如何：创建专用的字体集合
<xref:System.Drawing.Text.PrivateFontCollection>类继承自<xref:System.Drawing.Text.FontCollection>抽象基类。 可以使用<xref:System.Drawing.Text.PrivateFontCollection>对象来维护一组专门为应用程序的字体。 专用字体集合可以包含已安装的系统字体，以及在计算机尚未安装的字体。 若要将字体文件添加到专用字体集合，调用<xref:System.Drawing.Text.PrivateFontCollection.AddFontFile%2A>方法的<xref:System.Drawing.Text.PrivateFontCollection>对象。  
  
 <xref:System.Drawing.Text.FontCollection.Families%2A>的属性<xref:System.Drawing.Text.PrivateFontCollection>对象包含的数组<xref:System.Drawing.FontFamily>对象。  
  
 专用字体集合中的字体系列数不一定是已添加到集合的字体文件数量相同。 例如，假设 ArialBd.tff、 Times.tff 和 TimesBd.tff 文件添加到集合。 将有三个文件，但在集合中的只有两个系列因为 Times.tff TimesBd.tff 属于同一系列。  
  
## <a name="example"></a>示例  
 以下示例将添加到以下三个字体文件<xref:System.Drawing.Text.PrivateFontCollection>对象：  
  
-   C:\\*systemroot*\Fonts\Arial.tff (Arial, regular)  
  
-   C:\\*systemroot*\Fonts\CourBI.tff (Courier New，加粗倾斜)  
  
-   C:\\*systemroot*\Fonts\TimesBd.tff (Times New Roman，粗体显示)  
  
 该代码检索的数组<xref:System.Drawing.FontFamily>中的对象<xref:System.Drawing.Text.FontCollection.Families%2A>属性的<xref:System.Drawing.Text.PrivateFontCollection>对象。  
  
 每个<xref:System.Drawing.FontFamily>对象在集合中，该代码调用<xref:System.Drawing.FontFamily.IsStyleAvailable%2A>方法，以确定是否有可用的各种样式 （常规、 粗体、 斜体、 粗体斜体、 下划线和删除线）。 自变量传递给<xref:System.Drawing.FontFamily.IsStyleAvailable%2A>方法均隶属于<xref:System.Drawing.FontStyle>枚举。  
  
 如果给定的系列样式组合不可用，<xref:System.Drawing.Font>构造对象时使用该系列和样式。 第一个参数传递给<xref:System.Drawing.Font.%23ctor%2A>构造函数是字体系列名称 (不<xref:System.Drawing.FontFamily>对象的所有其他变体情况一样<xref:System.Drawing.Font.%23ctor%2A>构造函数)。 之后<xref:System.Drawing.Font>构造对象时，传递到<xref:System.Drawing.Graphics.DrawString%2A>方法的<xref:System.Drawing.Graphics>类，以显示该系列的名称以及的样式的名称。  
  
 以下代码的输出结果类似于下图中所示的输出。  
  
 ![字体文本](./media/csfontstext7.png "csfontstext7")  
  
 Arial.tff （其中已添加到下面的代码示例中的专用字体集合） 是 Arial 常规字形的字体文件。 但请注意，该程序的输出显示了几种可用样式不是常规的 Arial 字体系列。 这是因为[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]可以模拟中的正则样式的粗体、 斜体和粗体斜体样式。 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 可以还字形生成下划线和从常规的样式。  
  
 同样，[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]可以模拟从粗体样式或斜体样式的粗体斜体样式。 程序输出显示即使 TimesBd.tff (Times New Roman，粗体显示) 是唯一的粗体斜体样式是可用于时间系列集合中的次文件。  
  
 [!code-csharp[System.Drawing.FontsAndText#51](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#51)]
 [!code-vb[System.Drawing.FontsAndText#51](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#51)]  
  
## <a name="compiling-the-code"></a>编译代码  
 前面的示例专用于 Windows 窗体，它需要 <xref:System.Windows.Forms.PaintEventArgs> `e`，这是 <xref:System.Windows.Forms.PaintEventHandler> 的参数。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Drawing.Text.PrivateFontCollection>
- [使用字体和文本](using-fonts-and-text.md)
