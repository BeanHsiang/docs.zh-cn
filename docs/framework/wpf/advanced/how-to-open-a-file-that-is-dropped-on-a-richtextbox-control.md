---
title: 如何：打开放置在 RichTextBox 控件上的文件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drag-and-drop [WPF], RichTextBox
- RichTextBox [WPF], drag-and-drop
- drag-and-drop [WPF], open a dropped file
ms.assetid: 6bb8bb54-f576-41db-a9a7-24102ddeb490
ms.openlocfilehash: 8ffa4c9919788060dc4524e127c181ee8282e6f9
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378906"
---
# <a name="how-to-open-a-file-that-is-dropped-on-a-richtextbox-control"></a>如何：打开放置在 RichTextBox 控件上的文件
在中[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]，则<xref:System.Windows.Controls.TextBox>， <xref:System.Windows.Controls.RichTextBox>，和<xref:System.Windows.Documents.FlowDocument>控件都具有内置的拖放功能。 内置功能，可拖放文本内和控件之间。 但是，它不会启用通过拖放控件上的文件来打开文件。 这些控件还会将拖放事件标记为已处理。 因此，默认情况下，无法添加你自己的事件处理程序，以提供功能以打开拖放的文件。  
  
 若要在这些控件中添加额外处理拖放事件，请使用<xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>方法添加拖放事件在事件处理程序。 设置`handledEventsToo`参数`true`具有已标记为由事件路由的另一个元素处理的路由事件调用指定的处理程序。  
  
> [!TIP]
>  您可以替换的内置拖放功能<xref:System.Windows.Controls.TextBox>， <xref:System.Windows.Controls.RichTextBox>，和<xref:System.Windows.Documents.FlowDocument>通过处理拖放事件的预览版本并将预览事件标记为已处理。 但是，这将禁用内置的拖放功能，并且不建议。  
  
## <a name="example"></a>示例  
 下面的示例演示如何将处理程序添加<xref:System.Windows.DragDrop.DragOver>并<xref:System.Windows.DragDrop.Drop>上的事件<xref:System.Windows.Controls.RichTextBox>。 此示例使用<xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>方法并设置`handledEventsToo`参数`true`，以便将即使调用事件处理程序<xref:System.Windows.Controls.RichTextBox>标记为已处理这些事件。 事件处理程序中的代码的新增功能可打开放置在一个文本文件<xref:System.Windows.Controls.RichTextBox>。  
  
 若要测试此示例中，将文本文件或丰富文本格式 (RTF) 文件从 Windows 资源管理器到<xref:System.Windows.Controls.RichTextBox>。 该文件将在中打开<xref:System.Windows.Controls.RichTextBox>。 如果按下 SHIFT 键之前删除该文件，将以明文形式打开文件。  
  
 [!code-xaml[DragDropSnippets#RtbXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#rtbxaml)]  
  
 [!code-csharp[DragDropSnippets#RtbHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#rtbhandlers)]
 [!code-vb[DragDropSnippets#RtbHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#rtbhandlers)]
