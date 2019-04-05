---
title: 如何：设计很好地响应本地化 Windows 窗体布局
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TableLayoutPanel control [Windows Forms]
- application design [Windows Forms], localization
- Windows Forms, localization
- localization [Windows Forms], Windows Forms layout
ms.assetid: d13eff2d-701c-4b6e-8838-3885cbfb7223
ms.openlocfilehash: ff88d876ffc05c85c6d3c1011df776b814ed7aea
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709709"
---
# <a name="how-to-design-a-windows-forms-layout-that-responds-well-to-localization"></a>如何：设计很好地响应本地化 Windows 窗体布局
创建可供进行本地化的窗体极大地加速了国际市场的开发。 可以使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件实现在控件因 <xref:System.Windows.Forms.Control.Text%2A> 属性值更改而调整大小时正常响应的布局。  
  
## <a name="example"></a>示例  
 此窗体演示如何创建在将显示的字符串值翻译成其它语言时按比例进行调整的布局。 这一翻译过程称为*本地化*。 有关详细信息，请参阅[本地化](../../../standard/globalization-localization/localization.md)。  
  
 Visual Studio 中对此任务提供广泛支持。  另请参阅[演练：创建布局根据本地化需要调整比例](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/7k9fa71y(v=vs.100))。  
  
 [!code-csharp[System.Windows.Forms.TableLayoutPanel.LocalizableForm#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.LocalizableForm/CS/localizableform.cs#1)]
 [!code-vb[System.Windows.Forms.TableLayoutPanel.LocalizableForm#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.TableLayoutPanel.LocalizableForm/VB/localizableform.vb#1)]  
  
## <a name="additional-resources"></a>其他资源
1.  [如何：对齐和拉伸控件在 TableLayoutPanel 控件中](how-to-align-and-stretch-a-control-in-a-tablelayoutpanel-control.md)  
  
2.  [演练：使用 FlowLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)  

3.  [如何：TableLayoutPanel 控件中 s p a n 行和列](how-to-span-rows-and-columns-in-a-tablelayoutpanel-control.md)  
  
4.  [如何：编辑 TableLayoutPanel 控件中的行和列](how-to-edit-columns-and-rows-in-a-tablelayoutpanel-control.md)  
  
5.  [演练：执行常见任务使用智能标记在 Windows 窗体控件](performing-common-tasks-using-smart-tags-on-wf-controls.md)  
  
6.  [演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)  

7.  [演练：布局 Windows 窗体控件与 Padding、 Margins 和 AutoSize 属性](windows-forms-controls-padding-autosize.md)  
  
8.  [如何：支持对使用 AutoSize 和 TableLayoutPanel 控件的 Windows 窗体的本地化](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/1zkt8b33(v=vs.100))  
  
9. [演练：创建数据输入可调整大小的 Windows 窗体](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/991eahec(v=vs.100))  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 System、System.Data、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 Visual Basic 或 Visual C# 生成命令行中的此示例的信息，请参阅[从命令行生成](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 也可以通过将代码粘贴到新的项目中生成此示例在 Visual Studio 中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.TableLayoutPanel>
- <xref:System.Windows.Forms.FlowLayoutPanel>
- [本地化](../../../standard/globalization-localization/localization.md)
