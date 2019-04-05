---
title: 如何：使用上下文菜单中的拼写检查功能
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling spell checking in a text box [WPF]
- reenabling spell checking in a text box [WPF]
- spell checking with a context menu [WPF]
ms.assetid: 61f69a20-2ff3-4056-9060-e32f4483ec5e
ms.openlocfilehash: 38d41aa6710fd13ffd2a5d13a6900a1a05303f35
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377802"
---
# <a name="how-to-use-spell-checking-with-a-context-menu"></a>如何：使用上下文菜单中的拼写检查功能
默认情况下，当启用拼写检查的编辑控件中时喜欢<xref:System.Windows.Controls.TextBox>或<xref:System.Windows.Controls.RichTextBox>，上下文菜单中获取拼写检查功能的选项。 例如，当用户右键单击拼错的单词，会得到一组拼写建议或选项**忽略所有**。 但是时重写默认上下文菜单与自己的自定义上下文菜单，, 此功能将丢失，并且您需要自己编写代码以重新启用的上下文菜单中的拼写检查功能。 下面的示例演示如何启用此配置<xref:System.Windows.Controls.TextBox>。  
  
## <a name="example"></a>示例  
 下面的示例演示[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，创建<xref:System.Windows.Controls.TextBox>与用于实现的上下文菜单的某些事件。  
  
 [!code-xaml[TextBoxMiscSnippets_snip#SpellerCustomContextMenuExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml#spellercustomcontextmenuexamplewholepage)]  
  
## <a name="example"></a>示例  
 下面的示例显示了实现的上下文菜单的代码。  
  
 [!code-csharp[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/csharp/speller_custom_context_menu.xaml.cs#spellercustomcontextmenucodeexamplewholepage)]
 [!code-vb[TextBoxMiscSnippets_snip#SpellerCustomContextMenuCodeExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBoxMiscSnippets_snip/visualbasic/speller_custom_context_menu.xaml.vb#spellercustomcontextmenucodeexamplewholepage)]  
  
 使用实现这一点的代码<xref:System.Windows.Controls.RichTextBox>类似。 传递给在参数中的主要区别是`GetSpellingError`方法。 有关<xref:System.Windows.Controls.TextBox>，传递的插入符号位置的整数索引：  
  
 `spellingError = myTextBox.GetSpellingError(caretIndex);`  
  
 有关<xref:System.Windows.Controls.RichTextBox>，将传递<xref:System.Windows.Documents.TextPointer>，它指定插入符号位置：  
  
 `spellingError = myRichTextBox.GetSpellingError(myRichTextBox.CaretPosition);`  
  
## <a name="see-also"></a>请参阅
- [TextBox 概述](textbox-overview.md)
- [RichTextBox 概述](richtextbox-overview.md)
- [在文本编辑控件中启用拼写检查](how-to-enable-spell-checking-in-a-text-editing-control.md)
- [将自定义上下文菜单与 TextBox 结合使用](how-to-use-a-custom-context-menu-with-a-textbox.md)
