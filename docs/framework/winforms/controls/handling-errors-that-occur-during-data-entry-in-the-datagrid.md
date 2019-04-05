---
title: 演练：Windows 窗体 DataGridView 控件中的数据输入时发生的错误处理
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- error handling [Windows Forms], dataGridView control
- data grids [Windows Forms], error handling
- DataGridView control [Windows Forms], error handling
- data entry [Windows Forms], error handling
- error handling [Windows Forms], data entry
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: 30a68b85-d3af-4946-83c1-1e2d010d0511
ms.openlocfilehash: a8eb4584060924684eacc99d46b88408451f1c82
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708231"
---
# <a name="walkthrough-handling-errors-that-occur-during-data-entry-in-the-windows-forms-datagridview-control"></a>演练：Windows 窗体 DataGridView 控件中的数据输入时发生的错误处理
处理来自基础数据存储区的错误是数据输入应用程序的必需的功能。 Windows 窗体<xref:System.Windows.Forms.DataGridView>控件来实现轻松这公开<xref:System.Windows.Forms.DataGridView.DataError>事件，该数据存储区检测到违反了约束或违反的业务规则时引发事件。  
  
 在本演练中，您将检索中的行`Customers`Northwind 示例数据库中表，然后将它们显示在<xref:System.Windows.Forms.DataGridView>控件。 当重复`CustomerID`新行或编辑现有行中检测到值<xref:System.Windows.Forms.DataGridView.DataError>事件会发生，这将通过显示处理<xref:System.Windows.Forms.MessageBox>描述异常。  
  
 要将本主题中的代码作为单个列表进行复制，请参阅[如何：处理错误在 Windows 中的数据输入时发生的窗体 DataGridView 控件](handle-errors-that-occur-during-data-entry-in-the-datagrid.md)。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，你将需要：  
  
-   对具有 Northwind SQL Server 示例数据库的服务器的访问。  
  
## <a name="creating-the-form"></a>创建窗体  
  
#### <a name="to-handle-data-entry-errors-in-the-datagridview-control"></a>处理 DataGridView 控件中的数据输入错误  
  
1.  创建派生的类<xref:System.Windows.Forms.Form>并且包含<xref:System.Windows.Forms.DataGridView>控件和一个<xref:System.Windows.Forms.BindingSource>组件。  
  
     下面的代码示例提供了基本的初始化，并包括`Main`方法。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#01](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#01](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridView.DataError#02](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#02](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#02)]  
  
2.  用于处理连接到数据库的详细信息窗体的类定义中实现的方法。  
  
     此代码示例使用`GetData`方法，它返回已填充<xref:System.Data.DataTable>对象。 请确保您设置`connectionString`变量为适合于您的数据库的值。  
  
    > [!IMPORTANT]
    >  将敏感信息（如密码）存储在连接字符串中可能会影响应用程序的安全性。 若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。 有关详细信息，请参阅[保护连接信息](../../data/adonet/protecting-connection-information.md)。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#30)]  
  
3.  实现窗体的一个处理程序<xref:System.Windows.Forms.Form.Load>初始化的事件<xref:System.Windows.Forms.DataGridView>和<xref:System.Windows.Forms.BindingSource>和数据绑定设置。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#10)]  
  
4.  处理<xref:System.Windows.Forms.DataGridView.DataError>上的事件<xref:System.Windows.Forms.DataGridView>。  
  
     如果该错误的上下文，提交操作显示中的错误<xref:System.Windows.Forms.MessageBox>。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#20)]  
  
## <a name="testing-the-application"></a>测试应用程序  
 现在可以测试窗体，以确保其行为符合预期。  
  
#### <a name="to-test-the-form"></a>若要测试窗体  
  
-   按 F5 运行该应用程序。  
  
     你将看到<xref:System.Windows.Forms.DataGridView>控件填充使用客户表中的数据。 如果输入的重复值`CustomerID`和提交编辑、 单元格的值将自动恢复，你将看到<xref:System.Windows.Forms.MessageBox>显示数据输入错误。  
  
## <a name="next-steps"></a>后续步骤  
 此应用程序为您提供了一个基本的了解<xref:System.Windows.Forms.DataGridView>控件的功能。 你可以自定义外观和行为<xref:System.Windows.Forms.DataGridView>控制几种方式：  
  
-   更改边框和标头的样式。 有关详细信息，请参阅[如何：更改边框和网格线的样式中的 Windows 窗体 DataGridView 控件](change-the-border-and-gridline-styles-in-the-datagrid.md)。  
  
-   启用或限制的用户输入<xref:System.Windows.Forms.DataGridView>控件。 有关详细信息，请参阅[如何：防止行中添加和删除 Windows 窗体 DataGridView 控件](prevent-row-addition-and-deletion-datagridview.md)，和[如何：将列设为只读、 只在 Windows 窗体 DataGridView 控件](how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)。  
  
-   验证用户输入到<xref:System.Windows.Forms.DataGridView>控件。 有关详细信息，请参见[演练：验证 Windows 中的数据窗体 DataGridView 控件](walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)。  
  
-   处理极大型数据集使用的虚拟模式。 有关详细信息，请参见[演练：在 Windows 中实现虚拟模式窗体 DataGridView 控件](implementing-virtual-mode-wf-datagridview-control.md)。  
  
-   自定义单元格的外观。 有关详细信息，请参阅[如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](customize-the-appearance-of-cells-in-the-datagrid.md)和[如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [Windows 窗体 DataGridView 控件中的数据输入](data-entry-in-the-windows-forms-datagridview-control.md)
- [如何：处理 Windows 窗体 DataGridView 控件中的数据输入时发生的错误](handle-errors-that-occur-during-data-entry-in-the-datagrid.md)
- [演练：验证 Windows 窗体 DataGridView 控件中的数据](walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)
- [保护连接信息](../../data/adonet/protecting-connection-information.md)
