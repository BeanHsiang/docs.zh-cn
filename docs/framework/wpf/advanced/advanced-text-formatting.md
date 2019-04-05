---
title: 高级文本格式设置
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [WPF]
- text [WPF]
- typography [WPF], text formatting
ms.assetid: f0a7986e-f5b2-485c-a27d-f8e922022212
ms.openlocfilehash: 7d2408104ee3cf206734c5a1904129c3b71f7229
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368228"
---
# <a name="advanced-text-formatting"></a>高级文本格式设置
Windows Presentation Foundation (WPF) 提供了一套稳健的[!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)]用于在你的应用程序中包括的文本。 布局和[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，如<xref:System.Windows.Controls.TextBlock>、 提供了最常见和常规使用用于呈现文本元素。 绘制[!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，如<xref:System.Windows.Media.GlyphRunDrawing>和<xref:System.Windows.Media.FormattedText>，在绘图中加入格式化的文本提供一种方法。 在最高级别，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]提供了一个可扩展的文本格式引擎，用于控制文本呈现，如文本存储管理、 文本运行格式管理和嵌入的对象管理的各个方面。  
  
 本主题介绍了[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]文本格式设置。 它主要关注客户端实现和利用[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]文本格式引擎。  
  
> [!NOTE]
>  本文档中的所有代码示例都可在[高级文本格式设置示例](https://go.microsoft.com/fwlink/?LinkID=159965)。  
  

  
<a name="prereq"></a>   
## <a name="prerequisites"></a>系统必备  
 本主题假定你熟悉的较高级别[!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]用于呈现文本。 大多数用户方案都不需要的高级的文本格式[!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]本主题中讨论。 有关不同的文本的介绍[!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，请参阅[WPF 中的文档](documents-in-wpf.md)。  
  
<a name="section1"></a>   
## <a name="advanced-text-formatting"></a>高级文本格式设置  
 文本布局和[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]中的控件[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]提供可用于轻松地在应用程序中加入格式化的文本的格式设置属性。 这些控件会公开许多用于处理文本呈现（包括字样、大小和颜色）的属性。 一般情况下，这些控件可以处理应用程序中的大部分文本呈现。 但是，某些高级方案要求控制文本存储和文本呈现。 为此，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 提供了一个可扩展的文本格式引擎。  
  
 高级的文本格式设置功能中找到[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]包括文本格式引擎、 文本存储、 文本运行和格式设置属性。 文本格式引擎， <xref:System.Windows.Media.TextFormatting.TextFormatter>，创建要用于显示的文本行。 这通过初始化行格式设置过程并调用文本格式化程序的实现<xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A>。 文本格式化程序通过调用的存储从文本存储检索文本运行<xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>方法。 <xref:System.Windows.Media.TextFormatting.TextRun>然后形成的对象<xref:System.Windows.Media.TextFormatting.TextLine>文本格式化程序对象和提供给应用程序进行检查或显示。  
  
<a name="section2"></a>   
## <a name="using-the-text-formatter"></a>使用文本格式化程序  
 <xref:System.Windows.Media.TextFormatting.TextFormatter> 是[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]文本格式引擎，提供服务，用于设置格式及断开文本行。 文本格式化程序可处理各种文本字符格式和段落样式，并提供对国际文本布局的支持。  
  
 与传统文本不同[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]，则<xref:System.Windows.Media.TextFormatting.TextFormatter>与通过回调方法的一组文本布局客户端进行交互。 它要求客户端提供这些方法的实现中<xref:System.Windows.Media.TextFormatting.TextSource>类。 下图说明了客户端应用程序之间的文本布局交互和<xref:System.Windows.Media.TextFormatting.TextFormatter>。  
  
 ![文本布局客户端和 TextFormatter 示意图](./media/textformatter01.png "TextFormatter01")  
应用程序和 TextFormatter 之间的交互  
  
 文本格式化程序用于从文本存储中检索带格式的文本行即的实现<xref:System.Windows.Media.TextFormatting.TextSource>。 这是通过首先通过使用创建文本格式化程序实例<xref:System.Windows.Media.TextFormatting.TextFormatter.Create%2A>方法。 此方法可创建一个文本格式化程序实例，并设置最大行高值和行宽值。 一旦创建文本格式化程序的实例，通过调用来启动行创建过程<xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A>方法。 <xref:System.Windows.Media.TextFormatting.TextFormatter> 回拨到要检索的文本和格式设置参数的文本运行的文本源构成一条线。  
  
 下例演示文本存储的格式设置过程。 <xref:System.Windows.Media.TextFormatting.TextFormatter>对象用于从文本存储中检索文本行，然后设置格式绘制到的文本行<xref:System.Windows.Media.DrawingContext>。  
  
 [!code-csharp[TextFormatterExample#100](~/samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextFormatterExample#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/Window1.xaml.vb#100)]  
  
<a name="section3"></a>   
## <a name="implementing-the-client-text-store"></a>实现客户端文本存储  
 扩展文本格式引擎时，需要实现和管理文本存储的各个方面。 该任务不是无关紧要的。 文本存储负责跟踪文本运行属性、段落属性、嵌入对象和其他类似内容。 它还提供文本格式化程序包含单个<xref:System.Windows.Media.TextFormatting.TextRun>对象的文本格式化程序用于创建<xref:System.Windows.Media.TextFormatting.TextLine>对象。  
  
 若要处理文本存储的虚拟化，文本存储必须派生自<xref:System.Windows.Media.TextFormatting.TextSource>。 <xref:System.Windows.Media.TextFormatting.TextSource> 定义文本格式化程序用于从文本存储中检索文本运行的方法。 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 是文本格式化程序用来检索文本的方法运行行格式设置中使用。 对调用<xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>反复进行文本格式化程序直到发生以下情况之一：  
  
-   一个<xref:System.Windows.Media.TextFormatting.TextEndOfLine>或返回子类。  
  
-   文本运行的累积的宽度超出创建文本格式化程序是调用或对文本格式化程序的调用中指定的最大线条宽度<xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A>方法。  
  
-   一个[!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)]返回换行序列，如"CF"、"LF"或"CRLF"。  
  
<a name="section4"></a>   
## <a name="providing-text-runs"></a>提供文本运行  
 文本格式设置过程的核心是文本格式化程序和文本存储之间的交互。 实现<xref:System.Windows.Media.TextFormatting.TextSource>提供了为文本格式化程序<xref:System.Windows.Media.TextFormatting.TextRun>对象和要设置的格式与运行的文本的属性。 通过处理此交互<xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>调用文本格式化程序的方法。  
  
 下表显示了一些预定义<xref:System.Windows.Media.TextFormatting.TextRun>对象。  
  
|TextRun 类型|用法|  
|------------------|-----------|  
|<xref:System.Windows.Media.TextFormatting.TextCharacters>|专用文本运行，用于将字符标志符号的表示形式传回给文本格式化程序。|  
|<xref:System.Windows.Media.TextFormatting.TextEmbeddedObject>|专用文本运行，用于提供其中的度量、命中测试和绘制将作为整体执行的内容，例如文本中的按钮或图像。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfLine>|专用文本运行，用于对行尾进行标记。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>|专用文本运行，用于对段落结尾进行标记。|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfSegment>|专用的文本运行用于标记如段的结尾结束先前受影响的作用域<xref:System.Windows.Media.TextFormatting.TextModifier>运行。|  
|<xref:System.Windows.Media.TextFormatting.TextHidden>|专用文本运行，用于对一系列隐藏字符进行标记。|  
|<xref:System.Windows.Media.TextFormatting.TextModifier>|专用文本运行，用于在其范围内修改文本运行属性。 该范围可扩展到下一个匹配<xref:System.Windows.Media.TextFormatting.TextEndOfSegment>文本运行或下一个<xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>。|  
  
 任意预定义<xref:System.Windows.Media.TextFormatting.TextRun>可以子类化的对象。 这样，文本源便可为文本格式化程序提供包含自定义数据的文本运行。  
  
 下面的示例演示<xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>方法。 返回此文本存储<xref:System.Windows.Media.TextFormatting.TextRun>文本格式化程序以进行处理的对象。  
  
 [!code-csharp[TextFormatterExample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/CustomTextSource.cs#101)]
 [!code-vb[TextFormatterExample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/CustomTextSource.vb#101)]  
  
> [!NOTE]
>  在此示例中，文本存储为所有文本提供了相同的文本属性。 高级文本存储需要实现各自的范围管理，以便单个字符具有不同的属性。  
  
<a name="section5"></a>   
## <a name="specifying-formatting-properties"></a>指定格式设置属性  
 <xref:System.Windows.Media.TextFormatting.TextRun> 使用提供的文本存储属性设置格式的对象。 这些属性有两种类型，<xref:System.Windows.Media.TextFormatting.TextParagraphProperties>和<xref:System.Windows.Media.TextFormatting.TextRunProperties>。 <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> 处理涉及段落的属性，如<xref:System.Windows.TextAlignment>和<xref:System.Windows.FlowDirection>。 <xref:System.Windows.Media.TextFormatting.TextRunProperties> 可以为每个文本运行中一个段落，如前景画笔、 不同的属性<xref:System.Windows.Media.Typeface>，和字体大小。 若要实现自定义段落和自定义文本运行属性类型，你的应用程序必须创建派生的类<xref:System.Windows.Media.TextFormatting.TextParagraphProperties>和<xref:System.Windows.Media.TextFormatting.TextRunProperties>分别。  
  
## <a name="see-also"></a>请参阅
- [WPF 中的版式](typography-in-wpf.md)
- [WPF 中的文档](documents-in-wpf.md)
