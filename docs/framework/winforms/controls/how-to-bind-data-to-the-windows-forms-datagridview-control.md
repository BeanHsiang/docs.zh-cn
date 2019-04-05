---
title: 如何：将数据绑定到 Windows 窗体 DataGridView 控件
ms.date: 02/08/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [Windows Forms], grids
- data binding [Windows Forms], DataGridView control
- DataGridView control [Windows Forms], data binding
ms.assetid: 1660f69c-5711-45d2-abc1-e25bc6779124
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cbcc04625a14ebc23cacfb567951bf8f76f14985
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725098"
---
# <a name="how-to-bind-data-to-the-windows-forms-datagridview-control"></a>如何：将数据绑定到 Windows 窗体 DataGridView 控件

<xref:System.Windows.Forms.DataGridView>控件支持标准 Windows 窗体数据绑定模型，因此它可以绑定到各种数据源。 通常情况下，您将绑定到<xref:System.Windows.Forms.BindingSource>的管理与数据源的交互。 <xref:System.Windows.Forms.BindingSource>可以是任何 Windows 窗体数据源，这将使您能非常灵活地选择或修改数据的位置时。 有关数据源的详细信息<xref:System.Windows.Forms.DataGridView>控件支持，请参阅[DataGridView 控件概述](datagridview-control-overview-windows-forms.md)。  

Visual Studio 可以绑定到 DataGridView 控件的数据的广泛支持。 有关详细信息，请参阅[如何：将数据绑定到使用设计器在 Windows 窗体 DataGridView 控件](bind-data-to-the-datagrid-using-the-designer.md)。  

DataGridView 控件连接到数据：

1. 实现方法来处理检索数据的详细信息。 下面的代码示例实现`GetData`方法初始化<xref:System.Data.SqlClient.SqlDataAdapter>，并使用它来填充<xref:System.Data.DataTable>。 然后将绑定<xref:System.Data.DataTable>到<xref:System.Windows.Forms.BindingSource>。 

2. 在窗体的<xref:System.Windows.Forms.Form.Load>事件处理程序中，绑定<xref:System.Windows.Forms.DataGridView>控制对<xref:System.Windows.Forms.BindingSource>，并调用`GetData`方法来检索数据。  

## <a name="example"></a>示例

此完整的代码示例从数据库填充在 Windows 窗体 DataGridView 控件中检索数据。 窗体还提供按钮以重新加载数据并将更改提交到数据库。  

此示例需要： 

- 访问 Northwind SQL Server 示例数据库。 有关安装 Northwind 示例数据库的详细信息，请参阅[获取这些示例数据库的 ADO.NET 代码示例](../../data/adonet/sql/linq/downloading-sample-databases.md)。 

- 引用 System、 System.Windows.Forms、 System.Data 和 System.Xml 程序集。  

若要生成并运行此示例中，粘贴到代码*Form1*中新的 Windows 窗体项目代码文件。 有关从生成的信息C#或 Visual Basic 命令行，请参阅[命令行上使用 csc.exe 生成](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)或[中的命令行生成](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)。  
  
填充`connectionString`变量中的示例使用 Northwind SQL Server 示例数据库连接的值。 Windows 身份验证，也称为集成的安全性，是更安全的方式连接到比将密码存储在连接字符串中的数据库。 有关连接安全性的详细信息，请参阅[保护连接信息](../../data/adonet/protecting-connection-information.md)。  

[!code-csharp[System.Windows.Forms.DataGridViewBoundEditable](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewBoundEditable/CS/datagridviewboundeditable.cs)]
[!code-vb[System.Windows.Forms.DataGridViewBoundEditable](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewBoundEditable/VB/datagridviewboundeditable.vb)]  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.DataSource%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.BindingSource>
- [Windows 窗体 DataGridView 控件中显示数据](displaying-data-in-the-windows-forms-datagridview-control.md)
- [保护连接信息](../../data/adonet/protecting-connection-information.md)
