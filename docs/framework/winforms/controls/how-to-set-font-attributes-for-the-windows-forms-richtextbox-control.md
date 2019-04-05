---
title: 如何：Windows 窗体 RichTextBox 控件设置字体特性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- .rtf files [Windows Forms], formatting in RichTextBox control
- fonts [Windows Forms], changing attributes in RichTextBox control
- RTF files [Windows Forms], formatting in RichTextBox control
- RichTextBox control [Windows Forms], setting font attributes
- text [Windows Forms]
- text boxes [Windows Forms], formatting text
- formatting [Windows Forms]
ms.assetid: 2bc23ddb-0529-4489-a1a2-ad253cb43f9a
ms.openlocfilehash: 92578bd267230f5878bda9533bd117e8f98d8f13
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57714679"
---
# <a name="how-to-set-font-attributes-for-the-windows-forms-richtextbox-control"></a>如何：Windows 窗体 RichTextBox 控件设置字体特性
Windows 窗体<xref:System.Windows.Forms.RichTextBox>控件具有许多选项用于设置所显示的文本的格式。 您可以使所选的字符粗体、 带下划线或斜体，使用<xref:System.Windows.Forms.RichTextBox.SelectionFont%2A>属性。 也可以使用此属性来更改所选字符的大小和字样。 <xref:System.Windows.Forms.RichTextBox.SelectionColor%2A>属性使您能够更改所选的字符的颜色。  
  
### <a name="to-change-the-appearance-of-characters"></a>更改字符的外观  
  
1.  设置<xref:System.Windows.Forms.RichTextBox.SelectionFont%2A>属性设置为合适的字体。  
  
     若要使用户能够在应用程序中设置字体系列、 大小和字样，通常可以使用<xref:System.Windows.Forms.FontDialog>组件。 有关概述，请参阅 [FontDialog 组件概述](fontdialog-component-overview-windows-forms.md)。  
  
2.  设置<xref:System.Windows.Forms.RichTextBox.SelectionColor%2A>属性设置为适当的颜色。  
  
     若要使用户能够在应用程序中设置颜色，通常可以使用<xref:System.Windows.Forms.ColorDialog>组件。 有关概述，请参阅 [ColorDialog 组件概述](colordialog-component-overview-windows-forms.md)。  
  
    ```vb  
    RichTextBox1.SelectionFont = New Font("Tahoma", 12, FontStyle.Bold)  
    RichTextBox1.SelectionColor = System.Drawing.Color.Red  
    ```  
  
    ```csharp  
    richTextBox1.SelectionFont = new Font("Tahoma", 12, FontStyle.Bold);  
    richTextBox1.SelectionColor = System.Drawing.Color.Red;  
    ```  
  
    ```cpp  
    richTextBox1->SelectionFont =  
       gcnew System::Drawing::Font("Tahoma", 12, FontStyle::Bold);  
    richTextBox1->SelectionColor = System::Drawing::Color::Red;  
    ```  
  
    > [!NOTE]
    >  这些属性只影响所选的文本，如果未选择文本，则只影响当前插入点位置处键入的文本。 有关以编程方式选择文本的信息，请参阅<xref:System.Windows.Forms.TextBoxBase.Select%2A>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.RichTextBox>
- [RichTextBox 控件](richtextbox-control-windows-forms.md)
- [在 Windows 窗体上使用的控件](controls-to-use-on-windows-forms.md)
