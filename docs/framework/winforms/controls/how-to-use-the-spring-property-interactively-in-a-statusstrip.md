---
title: 如何：在 StatusStrip 中以交互方式使用 Spring 属性
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- StatusStrip control [Windows Forms]
- ToolStrip control [Windows Forms]
- status bars [Windows Forms], examples
- Spring property [Windows Forms]
ms.assetid: 18bde842-a93c-48dd-9db3-15738a1775ce
ms.openlocfilehash: 13a9809507f30f70d751d24ec68de1e5a62011cd
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57714835"
---
# <a name="how-to-use-the-spring-property-interactively-in-a-statusstrip"></a>如何：在 StatusStrip 中以交互方式使用 Spring 属性
可以使用 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 属性来定位 <xref:System.Windows.Forms.StatusStrip> 控件中的 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件。 
  <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 属性确定 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件是否自动填充 <xref:System.Windows.Forms.StatusStrip> 控件中的可用空间。  
  
## <a name="example"></a>示例  
 下面的代码示例演示了如何使用 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 属性定位 <xref:System.Windows.Forms.StatusStrip> 控件中的 <xref:System.Windows.Forms.ToolStripStatusLabel> 控件。 
  <xref:System.Windows.Forms.ToolStripItem.Click> 事件处理程序执行异或 (XOR) 运算，以便切换 <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A> 属性的值。  
  
 若要使用此代码示例，编译并运行该应用程序，然后单击**中间 （弹簧）** 上<xref:System.Windows.Forms.StatusStrip>控制切换的值<xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>属性。  
  
 [!code-csharp[System.Windows.Forms.ToolStrip.Misc#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStrip.Misc#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#1)]  
[!code-csharp[System.Windows.Forms.ToolStrip.Misc#50](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/CS/Program.cs#50)]
[!code-vb[System.Windows.Forms.ToolStrip.Misc#50](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.Misc/VB/Program.vb#50)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 System.Design、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 Visual Basic 或 Visual C# 生成命令行中的此示例的信息，请参阅[从命令行生成](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 也可以通过将代码粘贴到新的项目中生成此示例在 Visual Studio 中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.ToolStripItem>
- <xref:System.Windows.Forms.ToolStripMenuItem>
- [ToolStrip 控件](toolstrip-control-windows-forms.md)
