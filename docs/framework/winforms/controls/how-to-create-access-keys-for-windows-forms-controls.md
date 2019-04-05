---
title: 如何：为 Windows 窗体控件创建访问密钥
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [Windows Forms], access keys
- Button control [Windows Forms], access keys
- dialog box controls [Windows Forms], mnemonics
- access keys [Windows Forms], creating for controls
- mnemonics [Windows Forms], adding to dialog box controls
- mnemonics
- ampersand character in shortcut key
- Windows Forms controls, access keys
- examples [Windows Forms], controls
- Text property [Windows Forms], specifying access keys for controls
- keyboard shortcuts [Windows Forms], creating for controls
- access keys [Windows Forms], Windows Forms
- ALT key
ms.assetid: 4faa0991-28ec-4eca-91db-51dc2cd6a7ac
ms.openlocfilehash: 5713bc9fa02e6122cc42348160dbe9315e023bc4
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707997"
---
# <a name="how-to-create-access-keys-for-windows-forms-controls"></a>如何：为 Windows 窗体控件创建访问密钥
*访问密钥*是中的菜单、 菜单项或如按钮控件的标签文本带下划线的字符。 使用访问密钥，用户可以"单击"按钮的同时按下 ALT 键和预定义的访问密钥。 例如，如果某个按钮可运行打印窗体的过程，因此其`Text`属性设置为"打印"、"P"在运行时，按钮文本加下划线的字母"P"将导致字母前添加一个与号。 用户可以运行通过按 ALT + P 与按钮关联的命令。 不能具有不能接收焦点的控件的访问密钥。  
  
### <a name="to-create-an-access-key-for-a-control"></a>若要创建用于控件的访问密钥  
  
1.  设置`Text`属性将成为快捷键的字母前为一个字符串，包含一个 & 号 (&)。  
  
    ```vb  
    ' Set the letter "P" as an access key.  
    Button1.Text = "&Print"  
    ```  
  
    ```csharp  
    // Set the letter "P" as an access key.  
    button1.Text = "&Print";  
    ```  
  
    ```cpp  
    // Set the letter "P" as an access key.  
    button1->Text = "&Print";  
    ```  
  
    > [!NOTE]
    >  若要包含在标题中而无需创建访问密钥与号，包括两个与号 (& &)。 标题中显示单个与号和带下划线的任何字符。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Button>
- [如何：响应 Windows 窗体按钮单击](how-to-respond-to-windows-forms-button-clicks.md)
- [如何：设置显示的文本的 Windows 窗体控件](how-to-set-the-text-displayed-by-a-windows-forms-control.md)
- [标记各个 Windows 窗体控件并创建它们的快捷键](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
