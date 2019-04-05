---
title: 如何：为使用设计器的 Windows 窗体控件创建访问密钥
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], access keys
- Button control [Windows Forms], access keys
- dialog box controls [Windows Forms], mnemonics
- access keys [Windows Forms], creating for controls
- mnemonics [Windows Forms], adding to dialog box controls
- ampersand character in shortcut key
- Windows Forms controls, access keys
- examples [Windows Forms], controls
- Text property [Windows Forms], specifying access keys for controls
- keyboard shortcuts [Windows Forms], creating for controls
- access keys [Windows Forms], Windows Forms
- ALT key
ms.assetid: 4c374c4c-4ca9-4a68-ac96-9dc3ab0f518a
ms.openlocfilehash: 3d4112d87dbd448c7e34d2b84d11b49f56e1dc44
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713340"
---
# <a name="how-to-create-access-keys-for-windows-forms-controls-using-the-designer"></a>如何：为使用设计器的 Windows 窗体控件创建访问密钥
*访问密钥*是中的菜单、 菜单项或如按钮控件的标签文本带下划线的字符。 它使用户能够通过同时按下 ALT 键和预定义的访问键"单击"按钮。 例如，如果某个按钮可运行打印窗体的过程，因此其`Text`属性设置前以字母"P"使得字母"P"以带有下划线的按钮文本中在运行时为"Print"，添加一个与号 (&)。 用户可以运行通过按 ALT + P 与按钮关联的命令。 不能具有不能接收焦点的控件的访问密钥。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-create-an-access-key-for-a-control"></a>若要创建用于控件的访问密钥  
  
1.  在中**属性**窗口中，设置`Text`属性将成为访问键的字母前为一个字符串，包含一个 & 号 (&)。 例如，若要设置为访问键的字母"P"，键入**和打印**到网格中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Button>
- [如何：响应 Windows 窗体按钮单击](how-to-respond-to-windows-forms-button-clicks.md)
- [如何：设置显示的文本的 Windows 窗体控件](how-to-set-the-text-displayed-by-a-windows-forms-control.md)
- [标记各个 Windows 窗体控件并创建它们的快捷键](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
