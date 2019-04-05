---
title: 数据表编辑
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f08008a9-042e-4de9-94f3-4f0e502b1eb5
ms.openlocfilehash: 473ea9963ce192f42e418bebc8e38971019350e3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54548555"
---
# <a name="datatable-edits"></a>数据表编辑
当您在 <xref:System.Data.DataRow> 中更改列值时，所做更改会立即置于行的当前状态中。 <xref:System.Data.DataRowState>然后将设置为**Modified**，和所做的更改来接受或拒绝使用<xref:System.Data.DataRow.AcceptChanges%2A>或<xref:System.Data.DataRow.RejectChanges%2A>方法**DataRow**。 **DataRow**还提供了可用于在编辑时挂起行状态的三种方法。 这三个方法是 <xref:System.Data.DataRow.BeginEdit%2A>、<xref:System.Data.DataRow.EndEdit%2A> 和 <xref:System.Data.DataRow.CancelEdit%2A>。  
  
 当修改列中的值**DataRow**直接**DataRow**管理使用的列的值**当前**，**默认**，和**原始**行版本。 除了这些行版本，之外**BeginEdit**， **EndEdit**，并**CancelEdit**方法使用第四个行版本：**建议**。 有关行版本的详细信息，请参阅[行状态和行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  
  
 **Proposed**编辑操作，首先会调用的过程中存在行版本**BeginEdit**结束通过使用**EndEdit**或**CancelEdit，** 或通过调用**AcceptChanges**或**RejectChanges**。  
  
 在编辑操作时，您可以将验证逻辑应用于单独的列通过评估**ProposedValue**中**ColumnChanged**的事件**DataTable**。 **ColumnChanged**事件保存**DataColumnChangeEventArgs**的保留的引用，到正在更改的列和**ProposedValue**。 计算了建议值后，可以对其进行修改或取消编辑。 在结束编辑后，将行移出**建议**状态。  
  
 可以通过调用来确认编辑**EndEdit**，或通过调用取消**CancelEdit**。 请注意，当**EndEdit**确实已确认编辑，**数据集**没有实际接受更改直至**AcceptChanges**调用。 另请注意，如果您调用**AcceptChanges**已结束编辑之前**EndEdit**或**CancelEdit**，编辑将会结束和**建议**行值接受两个**当前**并**原始**行版本。 以相同的方式调用**RejectChanges**结束编辑，并放弃**当前**并**建议**行版本。 调用**EndEdit**或**CancelEdit**后调用**AcceptChanges**或者**RejectChanges**不起任何作用，因为已经完成编辑已结束。  
  
 下面的示例演示如何使用**BeginEdit**与**EndEdit**并**CancelEdit**。 该示例还会检查**ProposedValue**中**ColumnChanged**事件并决定是否要取消编辑。  
  
```vb  
Dim workTable As DataTable = New DataTable  
workTable.Columns.Add("LastName", Type.GetType("System.String"))  
  
AddHandler workTable.ColumnChanged, _  
  New DataColumnChangeEventHandler(AddressOf OnColumnChanged)  
  
Dim workRow As DataRow = workTable.NewRow()  
workRow(0) = "Smith"  
workTable.Rows.Add(workRow)  
  
workRow.BeginEdit()  
' Causes the ColumnChanged event to write a message and cancel the edit.  
workRow(0) = ""       
workRow.EndEdit()  
  
' Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow(0), workRow.RowState)  
  
Private Shared Sub OnColumnChanged( _  
  sender As Object, args As DataColumnChangeEventArgs)  
  If args.Column.ColumnName = "LastName" Then  
    If args.ProposedValue.ToString() = "" Then  
      Console.WriteLine("Last Name cannot be blank.  Edit canceled.")  
      args.Row.CancelEdit()  
    End If  
  End If  
End Sub  
```  
  
```csharp  
DataTable workTable  = new DataTable();  
workTable.Columns.Add("LastName", typeof(String));  
  
workTable.ColumnChanged +=   
  new DataColumnChangeEventHandler(OnColumnChanged);  
  
DataRow workRow = workTable.NewRow();  
workRow[0] = "Smith";  
workTable.Rows.Add(workRow);  
  
workRow.BeginEdit();  
// Causes the ColumnChanged event to write a message and cancel the edit.  
workRow[0] = "";       
workRow.EndEdit();  
  
// Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow[0], workRow.RowState);    
  
protected static void OnColumnChanged(  
  Object sender, DataColumnChangeEventArgs args)  
{  
  if (args.Column.ColumnName == "LastName")  
    if (args.ProposedValue.ToString() == "")  
    {  
      Console.WriteLine("Last Name cannot be blank. Edit canceled.");  
      args.Row.CancelEdit();  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Data.DataRow>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataRowVersion>
- [操作数据表中的数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)
- [处理数据表事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
