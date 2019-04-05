---
title: Windows 窗体和控件中的国际字体
ms.date: 03/30/2017
helpviewer_keywords:
- fonts [Windows Forms], international
- international applications [Windows Forms], character display
- fonts [Windows Forms], globalization considerations
- localization [Windows Forms], fonts
- Windows Forms controls, labels
- font fallback in Windows Forms
- globalization [Windows Forms], character sets
dev_langs:
- csharp
- vb
ms.assetid: 2c3066df-9bac-479a-82b2-79e484b346a3
ms.openlocfilehash: 1f9afd575e2de04e0b11556ad34436839e13d968
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54693235"
---
# <a name="international-fonts-in-windows-forms-and-controls"></a>Windows 窗体和控件中的国际字体

国际应用程序中选择字体的推荐的方法是尽可能使用字体回退。 属于系统确定哪一脚本字符的字体回退方法。

## <a name="using-font-fallback"></a>使用字体回退

若要充分利用此功能，不设置<xref:System.Drawing.Font>窗体或任何其他元素的属性。 应用程序将自动使用默认系统字体，这不同于操作系统的一种本地化语言到另一个。 运行程序时，系统将自动提供正确的字体选择操作系统中的区域性。

没有不设置字体，它是用于更改字体样式的规则的例外。 这可能是应用程序在其中用户单击一个按钮以使文本在文本框中显示以粗体显示。 为此，请将编写一个函数来更改文本框的字体加粗，基于任何窗体的字体。 务必要在两个位置调用此函数： 中的按钮<xref:System.Windows.Forms.Control.Click>事件处理程序并在<xref:System.Windows.Forms.Control.FontChanged>事件处理程序。 如果仅在调用该函数<xref:System.Windows.Forms.Control.Click>事件处理程序和某些其他代码段会更改整个窗体的字体系列，在文本框中不会更改与窗体的其余部分。

```vb
Private Sub MakeBold()
   ' Change the TextBox to a bold version of the form font
   TextBox1.Font = New Font(Me.Font, FontStyle.Bold)
End Sub

Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
   ' Clicking this button makes the TextBox bold
   MakeBold()
End Sub

Private Sub Form1_FontChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.FontChanged
   ' If the TextBox is already bold and the form's font changes,
   ' change the TextBox to a bold version of the new form font
   If (TextBox1.Font.Style = FontStyle.Bold) Then
      MakeBold()
   End If
End Sub
```

```csharp
private void button1_Click(object sender, System.EventArgs e)
{
   // Clicking this button makes the TextBox bold
   MakeBold();
}

private void MakeBold()
{
   // Change the TextBox to a bold version of the form's font
   textBox1.Font = new Font(this.Font, FontStyle.Bold);
}

private void Form1_FontChanged(object sender, System.EventArgs e)
{
   // If the TextBox is already bold and the form's font changes,
   // change the TextBox to a bold version of the new form font
   if (textBox1.Font.Style == FontStyle.Bold)
   {
      MakeBold();
   }
}
```

但是，当在本地化应用程序，粗体的字体可能效果不佳对于某些语言显示。 如果这是一个问题，您希望本地化人员可以选择切换到常规文本中加粗字体。 由于本地化人员通常不是开发人员，并且不能访问源代码，仅对资源的文件，此选项需要在资源文件中设置。 若要执行此操作，需要设置<xref:System.Drawing.Font.Bold%2A>属性设置为`true`。 这会导致正在写出到资源文件，本地化人员可以在其中编辑的字体设置。 然后编写代码后的`InitializeComponent`方法来重置字体基于任何窗体的字体，但使用的字体样式的资源文件中指定。

```vb
TextBox1.Font = New System.Drawing.Font(Me.Font, TextBox1.Font.Style)
```

```csharp
textBox1.Font = new System.Drawing.Font(this.Font, textBox1.Font.Style);
```
  
## <a name="see-also"></a>请参阅

- [全球化 Windows 窗体应用程序](globalizing-windows-forms.md)
- [使用字体和文本](using-fonts-and-text.md)
