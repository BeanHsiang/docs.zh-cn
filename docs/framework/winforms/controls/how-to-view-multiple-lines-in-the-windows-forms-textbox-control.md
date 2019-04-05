---
title: 如何：查看 Windows 窗体 TextBox 控件中的多个行
ms.date: 03/30/2017
helpviewer_keywords:
- newline
- end of line
- ScrollBars property [Windows Forms], in TextBox control
- CRLF
- MultiLine property in TextBox control
- line-feed
- TextBox control [Windows Forms], viewing multiple lines
- carriage return
ms.assetid: 43173201-0b74-4067-a472-605029ca5f35
ms.openlocfilehash: d80a0262455b9b5e0e8535d88eb6292ab60e3ea8
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716005"
---
# <a name="how-to-view-multiple-lines-in-the-windows-forms-textbox-control"></a>如何：查看 Windows 窗体 TextBox 控件中的多个行
默认情况下，Windows 窗体<xref:System.Windows.Forms.TextBox>控件显示单行文本并不会显示滚动条。 文本的长度超过可用空间，仅部分文本可见。 可以通过设置更改此默认行为<xref:System.Windows.Forms.TextBox.Multiline%2A>， <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A>，和<xref:System.Windows.Forms.TextBox.ScrollBars%2A>为适当的值的属性。  
  
### <a name="to-display-a-carriage-return-in-the-textbox-control"></a>若要显示在 TextBox 控件中返回一个回车符  
  
-   若要显示多行的回车<xref:System.Windows.Forms.TextBox>，使用<xref:System.Environment.NewLine%2A>属性。  
  
     请注意，解释转义符 (\\) 是特定于语言的。 Visual Basic 则使用`Chr$(13) & Chr$(10)`为回车符和换行符字符组合。  
  
### <a name="to-view-multiple-lines-in-the-textbox-control"></a>若要查看 TextBox 控件中的多个行  
  
1.  将 <xref:System.Windows.Forms.TextBox.Multiline%2A> 属性设置为 `true`。 如果<xref:System.Windows.Forms.TextBoxBase.WordWrap%2A>是`true`（默认值），然后在控件中的文本将显示为一个或多个段落; 否则它将显示为列表中，某些行可能会剪裁在控件的边缘。  
  
2.  将 <xref:System.Windows.Forms.TextBox.ScrollBars%2A> 属性设置为适当的值。  
  
    |值|描述|  
    |-----------|-----------------|  
    |<xref:System.Windows.Forms.ScrollBars.None>|使用此值，如果该文本则为一个段落，几乎总是能适合控件。 用户可以使用鼠标指针在控件内移动，如果文本太长而无法一次性全部显示。|  
    |<xref:System.Windows.Forms.ScrollBars.Horizontal>|如果你想要显示的行，其中一些可能会比的宽度更长列表，请使用此值<xref:System.Windows.Forms.TextBox>控件。|  
    |<xref:System.Windows.Forms.ScrollBars.Both>|如果该列表可能会超过控件的高度，则使用此值。|  
  
3.  将 <xref:System.Windows.Forms.TextBoxBase.WordWrap%2A> 属性设置为适当的值。  
  
    |值|描述|  
    |-----------|-----------------|  
    |`false`|控件中的文本不会自动换行，所以它将滚动到右侧，直到到达一个分行符。 使用此值，如果你选择了<xref:System.Windows.Forms.ScrollBars.Horizontal>滚动条或<xref:System.Windows.Forms.ScrollBars.Both>、 更高版本。|  
    |`true`（默认值）|不会出现水平滚动条。 使用此值，如果你选择了<xref:System.Windows.Forms.ScrollBars.Vertical>滚动条或<xref:System.Windows.Forms.ScrollBars.None>、 更高版本来显示一个或多个段落。|  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.TextBox>
- [TextBox 控件概述](textbox-control-overview-windows-forms.md)
- [如何：控制 Windows 窗体 TextBox 控件中的插入点](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [如何：创建只读文本框](how-to-create-a-read-only-text-box-windows-forms.md)
- [如何：在字符串中放置引号](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [如何：在 Windows 窗体 TextBox 控件中选择文本](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [TextBox 控件](textbox-control-windows-forms.md)
