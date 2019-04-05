---
title: 如何：访问对象绑定到 Windows 窗体 DataGridView 行
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- object binding [Windows Forms], accessing bound objects
- data grids [Windows Forms], accessing bound objects
- DataGridView control [Windows Forms], accessing objects bound to rows
ms.assetid: 0e05748f-4403-4eb8-8b2f-b098108181b5
ms.openlocfilehash: 5c66bc961d92a2ece1aea4986d0c23181c971b3e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720340"
---
# <a name="how-to-access-objects-bound-to-windows-forms-datagridview-rows"></a>如何：访问对象绑定到 Windows 窗体 DataGridView 行
有时，显示业务对象集合中存储的信息表很有用。 将 <xref:System.Windows.Forms.DataGridView> 控件绑定到此类集合时，每个公共属性都将在它自己的列中显示，除非该属性已用 <xref:System.ComponentModel.BrowsableAttribute> 标记为不可浏览。 例如，`Customer` 对象的集合包含“姓名”和“地址”等列。  
  
 如果这些对象包含你希望访问的附加信息和代码，则可以通过行对象来进行访问。 在下面的代码示例中，用户可以选择多行并单击一个按钮将发票发送给每个对应客户。  
  
### <a name="to-access-row-bound-objects"></a>访问行绑定对象  
  
-   使用 <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=nameWithType> 属性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#10)]  
  
## <a name="example"></a>示例  
 完整的代码示例包括一个简单的 `Customer` 实现，并将 <xref:System.Windows.Forms.DataGridView> 绑定到一个包含几个 `Customer` 对象的 <xref:System.Collections.ArrayList>。 因为在 <xref:System.Windows.Forms.Form.Load?displayProperty=nameWithType> 事件处理程序之外无法访问客户集合，所以 <xref:System.Windows.Forms.Button?displayProperty=nameWithType> 的 <xref:System.Windows.Forms.Control.Click> 事件处理程序必须通过行访问 `Customer` 对象。  
  
 [!code-csharp[System.Windows.Forms.DataGridViewObjectBinding#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/CS/datagridviewobjectbinding.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewObjectBinding#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewObjectBinding/VB/datagridviewobjectbinding.vb#00)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 System 和 System.Windows.Forms 程序集的引用。  
  
 Visual Basic 或 Visual C# 生成命令行中的此示例的信息，请参阅[从命令行生成](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 也可以通过将代码粘贴到新的项目中生成此示例在 Visual Studio 中。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewRow>
- <xref:System.Windows.Forms.DataGridViewRow.DataBoundItem%2A?displayProperty=nameWithType>
- [在 Windows 窗体 DataGridView 控件中显示数据](displaying-data-in-the-windows-forms-datagridview-control.md)
- [如何：将对象绑定到 Windows 窗体 DataGridView 控件](how-to-bind-objects-to-windows-forms-datagridview-controls.md)
