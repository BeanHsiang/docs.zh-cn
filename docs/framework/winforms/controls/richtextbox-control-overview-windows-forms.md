---
title: RichTextBox 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- RichTextBox
helpviewer_keywords:
- RichTextBox control [Windows Forms], about RichTextBox control
- text boxes [Windows Forms], about text boxes
ms.assetid: 95081194-3dd4-4b84-9545-dd373e491eca
ms.openlocfilehash: ded2c9bb0e5b3320de700ce6126710314ed9e4f2
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720234"
---
# <a name="richtextbox-control-overview-windows-forms"></a>RichTextBox 控件概述（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.RichTextBox>控件用于显示、 输入和操作带有格式的文本。 <xref:System.Windows.Forms.RichTextBox>控件的功能无所不包<xref:System.Windows.Forms.TextBox>控件的作用，但它还可以显示字体、 颜色和链接; 从文件; 加载文本和嵌入的图像并查找指定的字符。 <xref:System.Windows.Forms.RichTextBox>控件通常用于提供文本操作和显示功能，类似于 Microsoft Word 等文字处理应用程序。 像<xref:System.Windows.Forms.TextBox>控件，<xref:System.Windows.Forms.RichTextBox>控件可以显示滚动条; 但不同于<xref:System.Windows.Forms.TextBox>控件，其默认设置将显示水平和垂直滚动条，根据需要并包含额外的滚动条设置。  
  
## <a name="working-with-the-richtextbox-control"></a>使用 RichTextBox 控件  
 如同<xref:System.Windows.Forms.TextBox>控件，显示的文本设置<xref:System.Windows.Forms.RichTextBox.Text%2A>属性。 <xref:System.Windows.Forms.RichTextBox>控件具有许多属性来设置文本的格式。 有关这些属性的详细信息，请参阅[如何：为 Windows 窗体 RichTextBox 控件设置字体特性](how-to-set-font-attributes-for-the-windows-forms-richtextbox-control.md)和[如何：设置缩进、 悬挂缩进和使用 Windows 窗体 RichTextBox 控件项目符号的段落](set-indents-hanging-indents-bulleted-paragraphs-with-wf-richtextbox.md)。 若要处理文件，<xref:System.Windows.Forms.RichTextBox.LoadFile%2A>和<xref:System.Windows.Forms.RichTextBox.SaveFile%2A>方法可以显示和编写多个文件格式包括纯文本、 Unicode 纯文本和丰富文本格式 (RTF)。 中列出的可能的文件格式<xref:System.Windows.Forms.RichTextBoxStreamType>。 可以使用<xref:System.Windows.Forms.RichTextBox.Find%2A>方法查找的文本或特定的字符的字符串。  
  
 此外可以使用<xref:System.Windows.Forms.RichTextBox>用于 Web 样式的链接通过设置控件<xref:System.Windows.Forms.RichTextBox.DetectUrls%2A>属性设置为`true`和编写代码来处理<xref:System.Windows.Forms.RichTextBox.LinkClicked>事件。 有关详细信息，请参阅[如何：显示 Web 样式链接使用 Windows 窗体 RichTextBox 控件](how-to-display-web-style-links-with-the-windows-forms-richtextbox-control.md)。 您可以防止用户通过设置操作部分或全部控件中的文本<xref:System.Windows.Forms.RichTextBox.SelectionProtected%2A>属性设置为`true`。  
  
 可以撤消和重复大多数编辑操作中的<xref:System.Windows.Forms.RichTextBox>控件通过调用<xref:System.Windows.Forms.TextBoxBase.Undo%2A>和<xref:System.Windows.Forms.RichTextBox.Redo%2A>方法。 <xref:System.Windows.Forms.RichTextBox.CanRedo%2A>方法使您能够确定用户已撤消的上一个操作是否可以重新应用到控件。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 控件](richtextbox-control-windows-forms.md)
- [TextBox 控件概述](textbox-control-overview-windows-forms.md)
