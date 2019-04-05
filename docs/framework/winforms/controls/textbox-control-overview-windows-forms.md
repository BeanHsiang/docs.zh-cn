---
title: TextBox 控件概述（Windows 窗体）
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- TextBox
helpviewer_keywords:
- TextBox control [Windows Forms], about TextBox controls
- text boxes [Windows Forms], adding
ms.assetid: d1a9c7f5-fa53-480a-a75c-158f8649ea2f
ms.openlocfilehash: 716195238e99938c8c416466fc84c2eff0bc7ba9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709769"
---
# <a name="textbox-control-overview-windows-forms"></a>TextBox 控件概述（Windows 窗体）
若要获取用户输入或显示文本使用 Windows 窗体的文本框。 <xref:System.Windows.Forms.TextBox>控件通常用于可编辑文本，尽管也可将其只读的。 文本框可以显示多个行，该控件的大小的文本换行并添加基本格式设置。 <xref:System.Windows.Forms.TextBox>控件提供了用于显示或输入到控件中的文本的格式样式。 若要显示多种类型的格式化文本，请使用<xref:System.Windows.Forms.RichTextBox>控件。 有关详细信息，请参阅[RichTextBox 控件概述](richtextbox-control-overview-windows-forms.md)。  
  
## <a name="working-with-the-textbox-control"></a>使用 TextBox 控件  
 由控件显示的文本包含在<xref:System.Windows.Forms.TextBox.Text%2A>属性。 默认情况下，您可以输入最多 2048年个字符，在文本框中。 如果您设置<xref:System.Windows.Forms.TextBox.Multiline%2A>属性设置为`true`，可以输入最多 32 KB 的文本。 <xref:System.Windows.Forms.TextBox.Text%2A>属性可以设置在设计时使用属性窗口中，在运行时在运行时在代码中，或用户的输入。 通过阅读，可以在运行时检索文本框的当前内容<xref:System.Windows.Forms.TextBox.Text%2A>属性。  
  
 下面的代码示例在运行时设置控件中的文本。 `InitializeMyControl`过程将不会自动执行; 它必须在调用。  
  
```vb  
Private Sub InitializeMyControl()  
   ' Put some text into the control first.  
   TextBox1.Text = "This is a TextBox control."  
End Sub  
```  
  
```csharp  
private void InitializeMyControl() {  
   // Put some text into the control first.  
   textBox1.Text = "This is a TextBox control.";  
}  
```  
  
```cpp  
private:  
   void InitializeMyControl()  
   {  
      // Put some text into the control first.  
      textBox1->Text = "This is a TextBox control.";  
   }  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.TextBox>
- [如何：控制 Windows 窗体 TextBox 控件中的插入点](how-to-control-the-insertion-point-in-a-windows-forms-textbox-control.md)
- [如何：使用 Windows 窗体 TextBox 控件创建密码文本框](how-to-create-a-password-text-box-with-the-windows-forms-textbox-control.md)
- [如何：创建只读文本框](how-to-create-a-read-only-text-box-windows-forms.md)
- [如何：在字符串中放置引号](how-to-put-quotation-marks-in-a-string-windows-forms.md)
- [如何：在 Windows 窗体 TextBox 控件中选择文本](how-to-select-text-in-the-windows-forms-textbox-control.md)
- [如何：查看 Windows 窗体 TextBox 控件中的多个行](how-to-view-multiple-lines-in-the-windows-forms-textbox-control.md)
- [TextBox 控件](textbox-control-windows-forms.md)
