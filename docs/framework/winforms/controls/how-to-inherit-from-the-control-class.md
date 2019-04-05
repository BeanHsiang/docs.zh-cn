---
title: 如何：从 Control 类继承
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [Windows Forms], Windows Forms custom controls
- Control class [Windows Forms], inheriting from
- custom controls [Windows Forms], inheritance
- OnPaint method [Windows Forms]
- custom controls [Windows Forms], creating
ms.assetid: 46ba0df3-5cf7-443c-a3b4-a72660172476
ms.openlocfilehash: cf1b3c7d7d530710c4c7e0fbd137667c3598500a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57702966"
---
# <a name="how-to-inherit-from-the-control-class"></a>如何：从 Control 类继承
如果你想要创建 Windows 窗体上使用的完全自定义控件，则应从继承<xref:System.Windows.Forms.Control>类。 同时继承自<xref:System.Windows.Forms.Control>类需要执行更多的规划和实施，它还提供了最大程度的选项。 从继承时<xref:System.Windows.Forms.Control>，继承使控件能够工作的最基本功能。 中的固有功能<xref:System.Windows.Forms.Control>类处理用户通过键盘和鼠标输入，定义的边界和控件的大小，提供 windows 句柄，并提供消息处理和安全性。 它没有纳入任何绘图功能（这里指的是控件的图形界面的实际呈现），也没有纳入任何特定的用户交互功能。 必须通过自定义代码提供所有的这些功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-create-a-custom-control"></a>创建自定义控件  
  
1.  创建一个新的 **Windows 应用程序**或 **Windows 控件库**项目。  
  
2.  从“项目”菜单中，选择“添加类”。  
  
3.  在“添加新项”对话框中，单击“自定义控件”。  
  
     一个新的自定义控件将被添加到项目中。  
  
4.  按 F7 打开自定义控件的“代码编辑器”。  
  
5.  找到<xref:System.Windows.Forms.Control.OnPaint%2A>方法，将为空 （除外） 的调用<xref:System.Windows.Forms.Control.OnPaint%2A>基类的方法。  
  
6.  修改代码以纳入控件所需的任何自定义绘图。  
  
     有关编写代码来呈现控件的图形的信息，请参阅[自定义控件的绘制和呈现](custom-control-painting-and-rendering.md)。  
  
7.  实现控件将纳入的任何自定义方法、属性或事件。  
  
8.  保存并测试控件。  
  
## <a name="see-also"></a>请参阅
- [各种自定义控件](varieties-of-custom-controls.md)
- [如何：从 UserControl 类继承](how-to-inherit-from-the-usercontrol-class.md)
- [如何：从现有 Windows 窗体控件继承](how-to-inherit-from-existing-windows-forms-controls.md)
- [如何：Windows 窗体的作者控件](how-to-author-controls-for-windows-forms.md)
- [Visual Basic 中继承的事件处理程序疑难解答](~/docs/visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)
- [设计时开发 Windows 窗体控件](developing-windows-forms-controls-at-design-time.md)
