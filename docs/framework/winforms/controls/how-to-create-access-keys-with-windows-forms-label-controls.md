---
title: 如何：使用 Windows 窗体 Label 控件创建访问键
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [Windows Forms], access keys
- dialog box controls [Windows Forms], mnemonics
- access keys [Windows Forms], creating for controls
- Label control [Windows Forms], creating access keys
- mnemonics [Windows Forms], adding to dialog box controls
- mnemonics
- Windows Forms controls, access keys
- UseMnemonic property [Windows Forms], Label control
- keyboard shortcuts [Windows Forms], creating for controls
- access keys [Windows Forms], Windows Forms
ms.assetid: 5ee8f823-80be-4a4f-96a4-412671e2e306
ms.openlocfilehash: 227880ad15e452df3f05807c41f3923cccb6fe3a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708296"
---
# <a name="how-to-create-access-keys-with-windows-forms-label-controls"></a>如何：使用 Windows 窗体 Label 控件创建访问键
Windows 窗体<xref:System.Windows.Forms.Label>控件可用于定义其他控件的访问键。 在标签控件中定义访问键时，用户可以同时按 ALT 键和指定的字符，以便将焦点移到 Tab 键顺序中排在其后面的控件。 由于标签不能接收焦点，因此焦点会自动移到 Tab 键顺序中的下一个控件。 使用此方法可将访问键分配给文本框、组合框、列表框和数据网格。  
  
### <a name="to-assign-an-access-key-to-a-control-with-a-label"></a>若要向使用标签控件分配访问键  
  
1.  首先，绘制标签并画出另一个控件。  
  
     或  
  
     按任意顺序绘制控件，并设置<xref:System.Windows.Forms.Control.TabIndex%2A>标签为一个小于另一个控件的属性。  
  
2.  设置的标签<xref:System.Windows.Forms.Label.UseMnemonic%2A>属性设置为`true`。  
  
3.  在标签的 <xref:System.Windows.Forms.Label.Text%2A> 属性中使用与号 (&) 来分配标签的访问键。 有关详细信息，请参阅[为 Windows 窗体控件创建访问键](how-to-create-access-keys-for-windows-forms-controls.md)。  
  
    > [!NOTE]
    >  可能需要显示标签控件中的与号，而不使用它们来创建访问键。 如果将标签控件绑定到记录集中的一个字段，而该记录集中的数据包含与号，则可能会出现这种情况。 若要在标签控件中显示与号，请将 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 属性设置为 `false`。 若要显示与号，同时还要设置访问键，请将 <xref:System.Windows.Forms.Label.UseMnemonic%2A> 属性设置为 `true`，并用一个与号 (&) 来表示访问键，用两个与号来表示与号。  
  
    ```vb  
    Label1.UseMnemonic = True  
    Label1.Text = "&Print"  
    Label2.UseMnemonic = True  
    Label2.Text = "&Copy && Paste"  
    ```  
  
    ```csharp  
    label1.UseMnemonic = true;  
    label1.Text = "&Print";  
    label2.UseMnemonic = true;  
    label2.Text = "&Copy && Paste";  
    ```  
  
    ```cpp  
    label1->UseMnemonic = true;  
    label1->Text = "&Print";  
    label2->UseMnemonic = true;  
    label2->Text = "&Copy && Paste";  
    ```  
  
## <a name="see-also"></a>请参阅
- [如何：调整 Windows 窗体标签控件以适应其内容的大小](how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)
- [Label 控件概述](label-control-overview-windows-forms.md)
- [Label 控件](label-control-windows-forms.md)
