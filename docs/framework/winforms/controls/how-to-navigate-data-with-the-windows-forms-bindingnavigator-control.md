---
title: 如何：使用 Windows 窗体 BindingNavigator 控件导航数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BindingNavigator control [Windows Forms], navigating data
- data [Windows Forms], navigating
- data navigation
- examples [Windows Forms], BindingNavigator control
ms.assetid: 0e5d4f34-bc9b-47cf-9b8d-93acbb1f1dbb
ms.openlocfilehash: 5fd1caabbc876d5b71deae2d9b1b9cf232d17700
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723239"
---
# <a name="how-to-navigate-data-with-the-windows-forms-bindingnavigator-control"></a>如何：使用 Windows 窗体 BindingNavigator 控件导航数据
Windows 窗体提供 <xref:System.Windows.Forms.BindingNavigator> 控件，开发人员可通过该控件在他们创建的窗体上为最终用户提供简单的数据导航和用户界面操作。  
  
 <xref:System.Windows.Forms.BindingNavigator> 控件是一个 <xref:System.Windows.Forms.ToolStrip> 控件，该控件上带有预配置为导航到数据集中第一条、最后一条、下一条和上一条记录的按钮，而且还有用于添加和删除记录的按钮。 将按钮添加到 <xref:System.Windows.Forms.BindingNavigator> 控件非常简单，因为它是一个 <xref:System.Windows.Forms.ToolStrip> 控件。 相关示例，请参阅[如何：添加负载，保存和取消按钮，为 Windows 窗体 BindingNavigator 控件](load-save-and-cancel-bindingnavigator.md)。  
  
 对于 <xref:System.Windows.Forms.BindingNavigator> 控件上的每个按钮，都有一个对应的 <xref:System.Windows.Forms.BindingSource> 组件成员，以编程方式允许相同的功能。 例如，<xref:System.Windows.Forms.BindingNavigator.MoveFirstItem%2A> 按钮对应 <xref:System.Windows.Forms.BindingSource> 组件的 <xref:System.Windows.Forms.BindingSource.MoveFirst%2A> 方法，<xref:System.Windows.Forms.BindingNavigator.DeleteItem%2A> 按钮对应 <xref:System.Windows.Forms.BindingSource.RemoveCurrent%2A> 方法，依次类推。 这样，启用 <xref:System.Windows.Forms.BindingNavigator> 控件导航数据记录就如同在窗体上将其 <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> 属性设置为适当的 <xref:System.Windows.Forms.BindingSource> 组件一样简单。  
  
### <a name="to-set-up-the-bindingnavigator-control"></a>设置 BindingNavigator 控件  
  
1.  添加一个名为 `bindingSource1` 的 <xref:System.Windows.Forms.BindingSource> 组件和两个分别名为 `textBox1` 和 `textBox2` 的 <xref:System.Windows.Forms.TextBox> 控件。  
  
2.  将 `bindingSource1` 绑定到数据，并将文本框控件绑定到 `bindingSource1`。 若要执行此操作，请将下面的代码粘贴到窗体中，并从窗体的构造函数调用 `LoadData` 或调用 <xref:System.Windows.Forms.Form.Load> 事件处理方法中。  
  
     [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#2)]  
  
3.  将名为 `bindingNavigator1` 的 <xref:System.Windows.Forms.BindingNavigator> 控件添加到窗体。  
  
4.  将 `bindingNavigator1`的 <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> 属性设置为 `bindingSource1`。 可以使用设计器或用代码执行此操作。  
  
     [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#3)]  
  
## <a name="example"></a>示例  
 下面的代码示例是前面所列步骤的完整示例。  
  
 [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 System、System.Data、System.Drawing、System.Windows.Forms 和 System.Xml 程序集的引用。  
  
 Visual Basic 或 Visual C# 生成命令行中的此示例的信息，请参阅[从命令行生成](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 也可以通过将代码粘贴到新的项目中生成此示例在 Visual Studio 中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.BindingNavigator>
- [BindingNavigator 控件](bindingnavigator-control-windows-forms.md)
- [ToolStrip 控件](toolstrip-control-windows-forms.md)
