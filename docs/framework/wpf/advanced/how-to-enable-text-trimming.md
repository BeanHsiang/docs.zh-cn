---
title: 如何：启用文本修整
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text [WPF], trimming
- documents [WPF], trimming text
- trimming text [WPF]
ms.assetid: dd8c9191-d2be-45fd-9fb4-3c75b65578c5
ms.openlocfilehash: 25fff566868e792004a915fee195485c4a1f385f
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57474133"
---
# <a name="how-to-enable-text-trimming"></a>如何：启用文本修整

此示例演示使用情况和中的可用值的效果<xref:System.Windows.TextTrimming>枚举。

## <a name="example"></a>示例

下面的示例定义<xref:System.Windows.Controls.TextBlock>具有元素<xref:System.Windows.Controls.TextBlock.TextTrimming%2A>属性设置。

[!code-xaml[TextTrimmingSnippets#_TextTrimmingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml#_texttrimmingxaml)]

设置相应<xref:System.Windows.TextTrimming>下面演示如何在代码中的属性。

[!code-csharp[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](~/samples/snippets/csharp/VS_Snippets_Wpf/TextTrimmingSnippets/CSharp/Window1.xaml.cs#_texttrimmingsettexttrimming)]
[!code-vb[TextTrimmingSnippets#_TextTrimmingSetTextTrimming](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextTrimmingSnippets/VisualBasic/Window1.xaml.vb#_texttrimmingsettexttrimming)]

有三个选项用于修整文本：**CharacterEllipsis**， **WordEllipsis**，和**None**。

当<xref:System.Windows.Controls.TextBlock.TextTrimming%2A>设置为**CharacterEllipsis**，文本进行修整，并使用靠近修整边缘的字符处省略号。  此设置旨在修整文本以使其更适应修整边界，但可能会导致某些单词仅部分修整。  下图显示了在此设置的效果<xref:System.Windows.Controls.TextBlock>类似于上面定义的一个。

![示例：TextTrimming.CharacterEllipsis](./media/texttrimming-character.png "TextTrimming_Character")

当<xref:System.Windows.Controls.TextBlock.TextTrimming%2A>设置为**WordEllipsis**，文本进行修整，并使用靠近修整边缘的第一个完整单词结尾处省略号。  此设置将不会显示单词部分修整，但通常不会修整那样靠近修整边缘作为文本**CharacterEllipsis**设置。  下图显示了在此设置的效果<xref:System.Windows.Controls.TextBlock>上面定义。

![示例：TextTrimming.WordEllipsis](./media/texttrimming-word.png "TextTrimming_Word")

当<xref:System.Windows.Controls.TextBlock.TextTrimming%2A>设置为**None**，会执行任何文本修整。  在这种情况下，只会将文本裁切到父文本容器的边界。  下图显示了在此设置的效果<xref:System.Windows.Controls.TextBlock>类似于上面定义的一个。

![示例：TextTrimming.None](./media/texttrimming-none.png "TextTrimming_None")
