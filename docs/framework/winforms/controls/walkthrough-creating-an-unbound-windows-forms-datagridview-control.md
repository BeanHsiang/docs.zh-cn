---
title: 演练：创建未绑定的 Windows 窗体 DataGridView 控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [Windows Forms], displaying without binding to data source
- DataGridView control [Windows Forms], unbound data
- DataGridView control [Windows Forms], displaying data without binding to a data source
- data [Windows Forms], unbound
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: 5a8d6afa-1b4b-4b24-8db8-501086ffdebe
ms.openlocfilehash: ebbfeaa2d6a7734aa0f2b214be65e64111d28ac0
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708102"
---
# <a name="walkthrough-creating-an-unbound-windows-forms-datagridview-control"></a>演练：创建未绑定的 Windows 窗体 DataGridView 控件
您可能经常想要显示不是从数据库的表格数据。 例如，你可能想要显示二维数组的字符串的内容。 <xref:System.Windows.Forms.DataGridView>类提供了简单且高度可自定义的方式来显示数据，而不绑定到数据源。 本演练演示如何填充<xref:System.Windows.Forms.DataGridView>控制和管理的添加和删除"取消绑定"模式中的行。 默认情况下，用户可以添加新行。 若要禁止添加行，将设置<xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A>属性是`false`。  
  
 要将本主题中的代码作为单个列表进行复制，请参阅[如何：创建未绑定的 Windows 窗体 DataGridView 控件](how-to-create-an-unbound-windows-forms-datagridview-control.md)。  
  
## <a name="creating-the-form"></a>创建窗体  
  
#### <a name="to-use-an-unbound-datagridview-control"></a>若要使用未绑定的 DataGridView 控件  
  
1.  创建派生的类<xref:System.Windows.Forms.Form>并且包含以下变量声明和`Main`方法。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#01](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#01](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#02](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#02](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#02)]  
  
2.  实现`SetupLayout`窗体的类定义以设置窗体的布局中的方法。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#20)]  
  
3.  创建`SetupDataGridView`方法以设置<xref:System.Windows.Forms.DataGridView>列和属性。  
  
     此方法首先将添加<xref:System.Windows.Forms.DataGridView>控件在窗体的<xref:System.Windows.Forms.Control.Controls%2A>集合。 接下来，使用设置要显示的列数<xref:System.Windows.Forms.DataGridView.ColumnCount%2A>属性。 通过设置来设置列标题的默认样式<xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A>， <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>，并<xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A>的属性<xref:System.Windows.Forms.DataGridViewCellStyle>返回<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>属性。  
  
     设置布局和外观属性，并且然后分配列名称。 当此方法退出时，<xref:System.Windows.Forms.DataGridView>控件已准备好进行填充。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#30)]  
  
4.  创建`PopulateDataGridView`方法以将行添加到<xref:System.Windows.Forms.DataGridView>控件。  
  
     每一行代表一首歌曲和其相关的信息。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#40](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#40)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#40](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#40)]  
  
5.  使用实用工具方法后，可以将附加事件处理程序。  
  
     将处理**添加**和**删除**按钮<xref:System.Windows.Forms.Control.Click>事件、 窗体的<xref:System.Windows.Forms.Form.Load>事件，以及<xref:System.Windows.Forms.DataGridView>控件的<xref:System.Windows.Forms.DataGridView.CellFormatting>事件。  
  
     当**外**按钮的<xref:System.Windows.Forms.Control.Click>引发事件时，新的、 空的行添加到<xref:System.Windows.Forms.DataGridView>。  
  
     当**删除**按钮的<xref:System.Windows.Forms.Control.Click>引发事件，删除所选的行，除非它是用于新记录，用户可以使用它的行中添加新行。 此行始终是中的最后一行<xref:System.Windows.Forms.DataGridView>控件。  
  
     当窗体的<xref:System.Windows.Forms.Form.Load>引发事件时， `SetupLayout`， `SetupDataGridView`，和`PopulateDataGridView`调用实用程序方法。  
  
     当<xref:System.Windows.Forms.DataGridView.CellFormatting>引发事件时，每个单元格中`Date`列的格式为长日期，除非该单元格的值不能分析。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#10)]  
  
## <a name="testing-the-application"></a>测试应用程序  
 现在可以测试窗体，以确保其行为符合预期。  
  
#### <a name="to-test-the-form"></a>若要测试窗体  
  
-   按 F5 运行该应用程序。  
  
     你将看到<xref:System.Windows.Forms.DataGridView>控件，用于显示中列出的歌曲`PopulateDataGridView`。 您可以添加新行与**添加行**按钮，并且您可以删除与所选的行**删除行**按钮。 未绑定<xref:System.Windows.Forms.DataGridView>控件的数据存储，并且其数据独立于任何外部源，如<xref:System.Data.DataSet>或数组。  
  
## <a name="next-steps"></a>后续步骤  
 此应用程序为您提供了一个基本的了解<xref:System.Windows.Forms.DataGridView>控件的功能。 你可以自定义外观和行为<xref:System.Windows.Forms.DataGridView>控制几种方式：  
  
-   更改边框和标头的样式。 有关详细信息，请参阅[如何：更改边框和网格线的样式中的 Windows 窗体 DataGridView 控件](change-the-border-and-gridline-styles-in-the-datagrid.md)。  
  
-   启用或限制的用户输入<xref:System.Windows.Forms.DataGridView>控件。 有关详细信息，请参阅[如何：防止行中添加和删除 Windows 窗体 DataGridView 控件](prevent-row-addition-and-deletion-datagridview.md)，和[如何：将列设为只读、 只在 Windows 窗体 DataGridView 控件](how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)。  
  
-   检查用户输入与数据库相关的错误。 有关详细信息，请参见[演练：在 Windows 中的数据输入时发生的错误处理窗体 DataGridView 控件](handling-errors-that-occur-during-data-entry-in-the-datagrid.md)。  
  
-   处理极大型数据集使用的虚拟模式。 有关详细信息，请参见[演练：在 Windows 中实现虚拟模式窗体 DataGridView 控件](implementing-virtual-mode-wf-datagridview-control.md)。  
  
-   自定义单元格的外观。 有关详细信息，请参阅[如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](customize-the-appearance-of-cells-in-the-datagrid.md)和[如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- [在 Windows 窗体 DataGridView 控件中显示数据](displaying-data-in-the-windows-forms-datagridview-control.md)
- [如何：创建未绑定的 Windows 窗体 DataGridView 控件](how-to-create-an-unbound-windows-forms-datagridview-control.md)
- [Windows 窗体 DataGridView 控件中的数据显示模式](data-display-modes-in-the-windows-forms-datagridview-control.md)
