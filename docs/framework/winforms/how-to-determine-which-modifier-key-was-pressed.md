---
title: 如何：确定按下了哪个修改键
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- keyboard input
- shift keys
- events [Windows Forms], mouse
- Keys.ControlKey enumeration member
- keys [Windows Forms], control keys
- user input [Windows Forms], checking for keyboard
- keys [Windows Forms], determining last pressed
- keys [Windows Forms], shift keys
- keys [Windows Forms], modifier keys
- control keys
- keys [Windows Forms], alt keys
- alt keys
- Keys.Shift enumeration member
- events [Windows Forms], keyboard
- keyboards [Windows Forms], keyboard input
- Keys.Alt enumeration member
- modifier keys
ms.assetid: 1e184048-0ae3-4067-a200-d4ba31dbc2cb
ms.openlocfilehash: de8af53bbf065047541e030de7a174987e5785df
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715979"
---
# <a name="how-to-determine-which-modifier-key-was-pressed"></a>如何：确定按下了哪个修改键
在创建接受用户的击键的应用程序时，可能还想要监视修改键，如 SHIFT、 ALT 和 CTRL 键。 修改键按下时结合使用其他密钥，或者单击鼠标，你的应用程序做出正确响应。 例如，如果按下字母 S 时，这只是可能导致"s"出现在屏幕上，但如果按下了 CTRL + S 的密钥，可能会保存当前文档。 如果处理<xref:System.Windows.Forms.Control.KeyDown>事件，<xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A>属性的<xref:System.Windows.Forms.KeyEventArgs>收到的事件处理程序指定哪个修改键被按下。 或者，<xref:System.Windows.Forms.KeyEventArgs.KeyData%2A>属性的<xref:System.Windows.Forms.KeyEventArgs>指定按下了也与按位 OR 组合与任何修改键的字符。 但是，如果你是<xref:System.Windows.Forms.Control.KeyPress>事件或鼠标事件，事件处理程序不会接收此信息。 在这种情况下，必须使用<xref:System.Windows.Forms.Control.ModifierKeys%2A>属性的<xref:System.Windows.Forms.Control>类。 在任一情况下，您必须执行相应的按位 AND<xref:System.Windows.Forms.Keys>值和要测试的值。 <xref:System.Windows.Forms.Keys>枚举提供了变体的每个修改键，因此，必须执行的按位并使用正确的值。 例如，由表示 SHIFT 键<xref:System.Windows.Forms.Keys.Shift>， <xref:System.Windows.Forms.Keys.ShiftKey>，<xref:System.Windows.Forms.Keys.RShiftKey>并<xref:System.Windows.Forms.Keys.LShiftKey>正确的值来测试 SHIFT 修改键原样<xref:System.Windows.Forms.Keys.Shift>。 同样，若要测试 CTRL 和 ALT 修饰符作为您应使用<xref:System.Windows.Forms.Keys.Control>和<xref:System.Windows.Forms.Keys.Alt>值，分别。  
  
> [!NOTE]
>  Visual Basic 编程人员也可以访问密钥信息通过<xref:Microsoft.VisualBasic.Devices.Computer.Keyboard%2A>属性  
  
### <a name="to-determine-which-modifier-key-was-pressed"></a>若要确定哪个修改键已按下  
  
-   使用按位`AND`运算符，其中<xref:System.Windows.Forms.Control.ModifierKeys%2A>属性和值为<xref:System.Windows.Forms.Keys>枚举来确定是否按下某个特定修改键。 下面的代码示例演示如何确定是否在按下 SHIFT 键<xref:System.Windows.Forms.Control.KeyPress>事件处理程序。  
  
     [!code-cpp[System.Windows.Forms.DetermineModifierKey#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/cpp/form1.cpp#5)]
     [!code-csharp[System.Windows.Forms.DetermineModifierKey#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.DetermineModifierKey#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/VB/form1.vb#5)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Keys>
- <xref:System.Windows.Forms.Control.ModifierKeys%2A>
- [Windows 窗体应用程序中的键盘输入](keyboard-input-in-a-windows-forms-application.md)
- [如何：确定如果 CapsLock 在 Visual Basic 中已启用](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/9c9d1fz9(v=vs.100))
