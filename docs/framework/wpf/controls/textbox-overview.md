---
title: TextBox 概述
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], TextBox
- TextBox control [WPF], about TextBox control
ms.assetid: 1ba6dc5b-11a7-4247-9213-36c6729ee35f
ms.openlocfilehash: 5ddd6600493cd127f8024f23594c628476cac19e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57361065"
---
# <a name="textbox-overview"></a>TextBox 概述
<xref:System.Windows.Controls.TextBox>类，可显示或编辑无格式的文本。 一个常见用途<xref:System.Windows.Controls.TextBox>编辑窗体中的无格式的文本。 例如，一个表单要求输入用户的姓名、 电话号码等使用<xref:System.Windows.Controls.TextBox>文本输入控件。 本主题介绍<xref:System.Windows.Controls.TextBox>类，并提供有关如何在两者中使用它的示例[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]和C#。  
  
 
  
<a name="textbox_or_richtextbox"></a>   
## <a name="textbox-or-richtextbox"></a>使用 TextBox 还是 RichTextBox？  
 这两<xref:System.Windows.Controls.TextBox>和<xref:System.Windows.Controls.RichTextBox>使用户可以输入文本，但两个控件用于不同的方案。 一个<xref:System.Windows.Controls.TextBox>需系统资源较少则<xref:System.Windows.Controls.RichTextBox>因此它非常适用于需要编辑纯文本 （即，在窗体中的使用情况）。 一个<xref:System.Windows.Controls.RichTextBox>是更好的选择时需要在用户编辑带格式的文本、 图像、 表或其他受支持的内容。 例如，编辑文档、 文章或博客需要格式、 图像，最好采用以下等<xref:System.Windows.Controls.RichTextBox>。 下表总结了的主要功能<xref:System.Windows.Controls.TextBox>和<xref:System.Windows.Controls.TextBox>。  
  
|控件|实时拼写检查|上下文菜单|等格式设置命令<xref:System.Windows.Documents.EditingCommands.ToggleBold%2A>(Ctr + B)|<xref:System.Windows.Documents.FlowDocument> 如图像、 段落、 表等内容。|  
|-------------|------------------------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Windows.Controls.TextBox>|是|是|否|不是。|  
|<xref:System.Windows.Controls.RichTextBox>|是|是|是（请参阅 [RichTextBox 概述](richtextbox-overview.md)）|是（请参阅 [RichTextBox 概述](richtextbox-overview.md)）|  
  
> [!NOTE]
>  尽管<xref:System.Windows.Controls.TextBox>不支持格式设置相关的编辑命令等的作用<xref:System.Windows.Documents.EditingCommands.ToggleBold%2A>(Ctr + B)，这两个控件如支持许多基本命令<xref:System.Windows.Documents.EditingCommands.MoveToLineEnd%2A>。 有关更多信息，请参见<xref:System.Windows.Documents.EditingCommands>。  
  
 支持的功能<xref:System.Windows.Controls.TextBox>在以下各节中介绍。 有关详细信息<xref:System.Windows.Controls.RichTextBox>，请参阅[RichTextBox 概述](richtextbox-overview.md)。  
  
### <a name="real-time-spellchecking"></a>实时拼写检查  
 可以启用实时拼写检查中的<xref:System.Windows.Controls.TextBox>或<xref:System.Windows.Controls.RichTextBox>。 启用拼写检查时，任何拼写错误的字词下方都会出现红线（见下图）。  
  
 ![具有拼写检查功能的 Textbox](./media/editing-textbox-with-spellchecking.png "Editing_TextBox_with_Spellchecking")  
  
 若要了解如何启用拼写检查，请参阅[在文本编辑控件中启用拼写检查](how-to-enable-spell-checking-in-a-text-editing-control.md)。  
  
### <a name="context-menu"></a>上下文菜单  
 默认情况下，同时<xref:System.Windows.Controls.TextBox>和<xref:System.Windows.Controls.RichTextBox>都会在用户右键单击该控件中时，将显示一个上下文菜单。 上下文菜单使用户可以剪切、复制或粘贴（见下图）。  
  
 ![具有上下文菜单的 TextBox](./media/editing-textbox-with-context-menu.png "Editing_TextBox_with_Context_Menu")  
  
 可以创建自己的自定义上下文菜单来重写默认行为。 有关详细信息，请参阅[通过 TextBox 使用自定义上下文菜单](how-to-use-a-custom-context-menu-with-a-textbox.md)。  
  
<a name="creating_textboxes"></a>   
## <a name="creating-textboxes"></a>创建 TextBox  
 一个<xref:System.Windows.Controls.TextBox>可以是单个行的高度，也可以包含多个行。 单个行<xref:System.Windows.Controls.TextBox>最适合用于输入少量纯文本 （即表单中的“姓名”、“电话号码”等）。 下面的示例演示如何创建单行<xref:System.Windows.Controls.TextBox>。  
  
 [!code-xaml[TextBoxMiscSnippets_snip#BasicTextBoxExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/basictextboxexample.xaml#basictextboxexamplewholepage)]  
  
 此外可以创建<xref:System.Windows.Controls.TextBox>，允许用户输入多行文本。 例如，如果表单要求输入用户的自传，你会想要使用<xref:System.Windows.Controls.TextBox>支持多行文本。 下面的示例演示如何使用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]来定义<xref:System.Windows.Controls.TextBox>自动扩展以容纳多行文本的控件。  
  
 [!code-xaml[TextBox_MiscCode#_MultilineTextBoxXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_multilinetextboxxaml)]  
  
 设置<xref:System.Windows.Controls.TextBox.TextWrapping%2A>归于`Wrap`会导致将文本换行到新行时的边缘<xref:System.Windows.Controls.TextBox>达到控件时，自动扩展<xref:System.Windows.Controls.TextBox>控件以包含为新行留出空间，如有必要。  
  
 设置<xref:System.Windows.Controls.Primitives.TextBoxBase.AcceptsReturn%2A>归于`true`会导致在新行时按 RETURN 键，再一次自动扩展插入<xref:System.Windows.Controls.TextBox>以便留出空间的新行，如有必要。  
  
 <xref:System.Windows.Controls.Primitives.TextBoxBase.VerticalScrollBarVisibility%2A>属性添加到一个滚动条<xref:System.Windows.Controls.TextBox>，这样的内容<xref:System.Windows.Controls.TextBox>可以滚动浏览如果<xref:System.Windows.Controls.TextBox>扩展到框架或窗口，其中包含它的大小。  
  
 有关详细信息与使用的不同任务<xref:System.Windows.Controls.TextBox>，请参阅[操作指南主题](textbox-how-to-topics.md)。  
  
<a name="editing_commands"></a>   
## <a name="detect-when-content-changes"></a>检测内容何时更改  
 通常<xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged>用于每当检测到事件中的文本<xref:System.Windows.Controls.TextBox>或<xref:System.Windows.Controls.RichTextBox>发生更改，而不是<xref:System.Windows.UIElement.KeyDown>正如您所料。 有关示例，请参阅[检测 TextBox 中的文本何时更改](how-to-detect-when-text-in-a-textbox-has-changed.md)。  
  
## <a name="see-also"></a>请参阅
- [帮助主题](textbox-how-to-topics.md)
- [RichTextBox 概述](richtextbox-overview.md)
