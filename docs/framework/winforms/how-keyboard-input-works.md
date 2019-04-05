---
title: 键盘输入工作原理
ms.date: 03/30/2017
helpviewer_keywords:
- keyboard input [Windows Forms], about keyboard input
- keyboards [Windows Forms], keyboard input
- Windows Forms, keyboard input
ms.assetid: 9a29433c-a180-49bb-b74c-d187786584c8
ms.openlocfilehash: a7965c1dcf36e956abd7930b8ff0154b13173b76
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57718020"
---
# <a name="how-keyboard-input-works"></a>键盘输入工作原理
Windows 窗体通过引发键盘事件来处理键盘输入，以响应 Windows 消息。 大多数 Windows 窗体应用程序都通过处理键盘事件来以独占方式处理键盘输入。 但是，必须了解键盘消息的工作方式，才能实现更高级的键盘输入方案（如在按键到达控件之前截获它们）。 本主题描述 Windows 窗体能够识别的按键数据的类型，并概述键盘消息的传送方式。 有关键盘事件的信息，请参阅[使用键盘事件](using-keyboard-events.md)。  
  
## <a name="types-of-keys"></a>按键的类型  
 Windows 窗体将键盘输入标识为虚拟键代码表示的按位<xref:System.Windows.Forms.Keys>枚举。 使用<xref:System.Windows.Forms.Keys>枚举，可以综合一系列按键以生成单个值。 这些值与 WM_KEYDOWN 和 WM_SYSKEYDOWN Windows 消息所伴随的值相对应。 可以通过处理检测大多数物理按键<xref:System.Windows.Forms.Control.KeyDown>或<xref:System.Windows.Forms.Control.KeyUp>事件。 字符键是的子集<xref:System.Windows.Forms.Keys>枚举和 WM_CHAR 和 WM_SYSCHAR Windows 消息所伴随的值相对应。 如果组合按键得到一个字符，您可以通过处理来检测该字符<xref:System.Windows.Forms.Control.KeyPress>事件。 或者，可以使用<xref:Microsoft.VisualBasic.Devices.Keyboard>、 Visual Basic 编程接口，若要发现哪些键已按下的键并发送由其公开。 有关详细信息，请参阅[访问键盘](~/docs/visual-basic/developing-apps/programming/computer-resources/accessing-the-keyboard.md)。  
  
## <a name="order-of-keyboard-events"></a>键盘事件的顺序  
 正如上面列出的那样，在一个控件上可能出现三个与键盘相关的事件。 以下顺序是发生这些事件的常规顺序：  
  
1.  用户按"a"键，该键将被预处理和调度，和一个<xref:System.Windows.Forms.Control.KeyDown>事件发生。  
  
2.  用户按住"a"键，该键将被预处理和调度，和一个<xref:System.Windows.Forms.Control.KeyPress>事件发生。  
  
     当用户按住某个键时，此事件会发生多次。  
  
3.  用户松开"a"键，该键将被预处理和调度和<xref:System.Windows.Forms.Control.KeyUp>事件发生。  
  
## <a name="preprocessing-keys"></a>键的预处理  
 在与其他消息一样处理键盘消息<xref:System.Windows.Forms.Control.WndProc%2A>的窗体或控件的方法。 但是，在键盘之前处理消息，<xref:System.Windows.Forms.Control.PreProcessMessage%2A>方法调用可以重写以处理特殊字符键和物理密钥的一个或多个方法。 可以重写这些方法，以便在控件处理消息之前检测并筛选某些按键。 下表按照方法出现的顺序列出了正在执行的操作以及所出现的相关方法。  
  
### <a name="preprocessing-for-a-keydown-event"></a>KeyDown 事件的预处理  
  
|操作|相关方法|说明|  
|------------|--------------------|-----------|  
|检查命令键（如快捷键或菜单快捷键）。|<xref:System.Windows.Forms.Control.ProcessCmdKey%2A>|此方法处理命令键，命令键的优先级高于常规键。 如果此方法返回 `true`，则不调度键消息，而且不发生键事件。 如果它返回`false`，<xref:System.Windows.Forms.Control.IsInputKey%2A>称为`.`|  
|请检查是否需要预处理的特殊键或应引发的普通字符键<xref:System.Windows.Forms.Control.KeyDown>事件和调度到某个控件。|<xref:System.Windows.Forms.Control.IsInputKey%2A>|如果该方法返回`true`，则表示该控件为常规字符和一个<xref:System.Windows.Forms.Control.KeyDown>引发事件。 如果`false`，<xref:System.Windows.Forms.Control.ProcessDialogKey%2A>调用。 **注意：** 若要确保控件获取密钥的组合，你可以处理<xref:System.Windows.Forms.Control.PreviewKeyDown>事件并设置<xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A>的<xref:System.Windows.Forms.PreviewKeyDownEventArgs>到`true`的或多个所需的键。|  
|检查该键是否为导航键（Esc、Tab、回车键或箭头键）。|<xref:System.Windows.Forms.Control.ProcessDialogKey%2A>|此方法处理在控件内实现特殊功能（如在控件与其父级之间切换焦点）的物理按键。 如果中间控件不处理键，<xref:System.Windows.Forms.Control.ProcessDialogKey%2A>等的层次结构中最顶端控件的父控件上调用。 如果此方法返回 `true`，则完成预处理，而且不生成按键事件。 如果它返回`false`、<xref:System.Windows.Forms.Control.KeyDown>事件发生。|  
  
### <a name="preprocessing-for-a-keypress-event"></a>KeyPress 事件的预处理  
  
|操作|相关方法|说明|  
|------------|--------------------|-----------|  
|检查该键是否为控件应当处理的普通字符|<xref:System.Windows.Forms.Control.IsInputChar%2A>|如果字符是普通字符，此方法返回`true`，则<xref:System.Windows.Forms.Control.KeyPress>引发事件和不再进行预处理。 否则为<xref:System.Windows.Forms.Control.ProcessDialogChar%2A>将调用。|  
|检查该字符是否为助记键（如按钮上的“确定(&O)”）|<xref:System.Windows.Forms.Control.ProcessDialogChar%2A>|此方法类似于<xref:System.Windows.Forms.Control.ProcessDialogKey%2A>，将调用控件层次结构。 如果该控件是容器控件，它会检查助记键通过调用<xref:System.Windows.Forms.Control.ProcessMnemonic%2A>本身及其子控件上。 如果<xref:System.Windows.Forms.Control.ProcessDialogChar%2A>将返回`true`、<xref:System.Windows.Forms.Control.KeyPress>事件不会发生。|  
  
## <a name="processing-keyboard-messages"></a>处理键盘消息  
 键盘消息在到达后<xref:System.Windows.Forms.Control.WndProc%2A>方法由一组可重写的方法进行处理的窗体或控件。 每个这些方法将返回<xref:System.Boolean>值，该值指定是否已处理并使用该控件的键盘消息。 如果其中的某种方法返回 `true`，则键盘消息被视为已处理，而且它不传递到控件的基控件或父控件进行进一步处理。 否则，消息停留在消息队列中，而且可能会在控件的基控件或父控件的其他方法中进行处理。 下表显示用来处理键盘消息的方法。  
  
|方法|说明|  
|------------|-----------|  
|<xref:System.Windows.Forms.Control.ProcessKeyMessage%2A>|此方法处理所接收的所有键盘消息<xref:System.Windows.Forms.Control.WndProc%2A>控件的方法。|  
|<xref:System.Windows.Forms.Control.ProcessKeyPreview%2A>|此方法将键盘消息发送到控件的父控件。 如果<xref:System.Windows.Forms.Control.ProcessKeyPreview%2A>将返回`true`，密钥未生成任何事件，否则<xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A>调用。|  
|<xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A>|此方法将引发<xref:System.Windows.Forms.Control.KeyDown>， <xref:System.Windows.Forms.Control.KeyPress>，和<xref:System.Windows.Forms.Control.KeyUp>事件，根据需要。|  
  
## <a name="overriding-keyboard-methods"></a>重写键盘方法  
 在预处理和处理键盘消息时，可以使用许多方法进行重写；但是，这些方法有好有坏。 下表显示可能需要完成的任务以及重写键盘方法的最佳方式。 重写方法的详细信息，请参阅[重写属性和方法在派生类](~/docs/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md#overriding-properties-and-methods-in-derived-classes)。  
  
|任务|方法|  
|----------|------------|  
|截获导航键并引发<xref:System.Windows.Forms.Control.KeyDown>事件。 例如，希望在文本框中处理 Tab 键和回车键。|重写 <xref:System.Windows.Forms.Control.IsInputKey%2A>。 **注意：** 或者，可以处理<xref:System.Windows.Forms.Control.PreviewKeyDown>事件并设置<xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A>的<xref:System.Windows.Forms.PreviewKeyDownEventArgs>到`true`的或多个所需的键。|  
|在控件上执行特殊的输入或导航处理。 例如，你可能希望在列表控件中使用箭头键更改选定项。|重写 <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>|  
|截获导航键并引发<xref:System.Windows.Forms.Control.KeyPress>事件。 例如，你希望在数字调整框控件中，多次按箭头键来加快项的调整进度。|重写 <xref:System.Windows.Forms.Control.IsInputChar%2A>。|  
|执行特殊的输入或导航处理期间<xref:System.Windows.Forms.Control.KeyPress>事件。 例如，在列表控件中，按住“r”键将跳到以字母 r 开头的项并在这些项间切换。|重写 <xref:System.Windows.Forms.Control.ProcessDialogChar%2A>|  
|执行自定义的助记键处理；例如，你希望处理所有者描述的、包含在工具栏中的按钮上的助记键。|重写 <xref:System.Windows.Forms.Control.ProcessMnemonic%2A>。|  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Keys>
- <xref:System.Windows.Forms.Control.WndProc%2A>
- <xref:System.Windows.Forms.Control.PreProcessMessage%2A>
- [My.Computer.Keyboard 对象](~/docs/visual-basic/language-reference/objects/my-computer-keyboard-object.md)
- [访问键盘](~/docs/visual-basic/developing-apps/programming/computer-resources/accessing-the-keyboard.md)
- [使用键盘事件](using-keyboard-events.md)
