---
title: Windows 窗体设计器中的设计时错误
ms.date: 03/30/2017
f1_keywords:
- DTELErrorList
- WhyDTELPage
helpviewer_keywords:
- errors [Windows Forms Designer]
- design-time errors [Windows Forms Designer]
ms.assetid: ad408380-825a-46d8-9a4a-531b130b88ce
ms.openlocfilehash: 64a0b8d0d0d9f0cc2bc2a841b999af58f29b4f75
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57718046"
---
# <a name="design-time-errors-in-the-windows-forms-designer"></a>Windows 窗体设计器中的设计时错误
本主题说明 Windows 窗体设计器加载失败时出现在 Microsoft Visual Studio 中的设计时错误列表的含义和用法。 如果出现此错误列表，则不应将其视为设计器中的 Bug，而应作为纠正代码中的错误的辅助手段。  
  
 此错误列表提供有关错误的详细信息和建议的可能解决方案，对此错误列表有一个基本了解可帮助调试应用程序。  
  
## <a name="the-design-time-error-list-interface"></a>设计时错误列表界面  
 如果 Windows 窗体设计器无法加载，设计器中会显示一个错误列表。 错误按类别进行分组。 例如，如果具有四个未声明变量的实例，则这些实例会归到同一错误类别中。 每个错误类别包含一个概述错误的简短说明。  
  
 通过单击错误类别标题或单击 V 形展开/折叠按钮，可展开或折叠错误类别。 展开错误类别时，将显示以下附加帮助信息：  
  
-   此错误的实例。  
  
-   有关此错误的帮助。  
  
-   有关此错误的论坛帖子。  
  
### <a name="instances-of-this-error"></a>此错误的实例  
 附加帮助信息中列出了当前项目中所含错误的所有实例。 许多错误包含用以下格式表示的确切位置：[项目名称] [窗体名称] 行:[行号] 列:[列号]。 单击“转到代码”链接可跳转到代码中发生错误的位置。  
  
 如果调用堆栈与错误关联，则可单击“显示调用堆栈”链接，这会进一步展开错误以显示调用堆栈。 检查堆栈可获取有价值的调试信息。 例如，可跟踪错误发生之前调用过的函数。 调用堆栈是可选定的，以便进行复制并保存。  
  
> [!NOTE]
>  在 Visual Basic 中，设计时错误列表不显示多个错误，但可能显示同一错误的多个实例。 在 Visual C++ 中，错误不含“转到代码”链接/行号链接。  
  
### <a name="help-with-this-error"></a>有关此错误的帮助  
 如果错误包含一个指向关联的 MSDN 帮助主题的链接，则附加帮助信息会包含一个指向该帮助主题的链接。 单击该链接后，Visual Studio 中会显示关联的帮助主题。  
  
### <a name="forum-posts-about-this-error"></a>有关此错误的论坛帖子  
 附加帮助信息包含一个指向与该错误相关的 MSDN 论坛帖子的链接。 将基于错误消息字符串来搜索论坛。 还可尝试搜索以下论坛：  
  
-   [Windows 窗体设计器论坛](https://go.microsoft.com/fwlink/?LinkId=203524)  
  
-   [Windows 窗体论坛](https://go.microsoft.com/fwlink/?LinkId=203523)  
  
### <a name="ignore-and-continue"></a>忽略并继续  
 可选择忽略错误条件并继续加载设计器。 选择此操作可能会导致意外行为。 例如，控件可能不会显示在设计图面上。  
  
## <a name="see-also"></a>请参阅
- [设计时开发故障排除](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171843(v=vs.120))
- [控件和组件创作疑难解答](troubleshooting-control-and-component-authoring.md)
- [设计时开发 Windows 窗体控件](developing-windows-forms-controls-at-design-time.md)
- [Windows 窗体设计器错误信息](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233640(v=vs.100))
