---
title: 加载方法
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: e22e5812-89c6-41f0-9302-bb899a46dbff
ms.openlocfilehash: 06666e069f20bc06f303c4e829d1c69c185a8a84
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54602476"
---
# <a name="the-load-method"></a>加载方法
可以使用 <xref:System.Data.DataTable.Load%2A> 方法为 <xref:System.Data.DataTable> 加载数据源中行。 这是重载的方法，在最简单的形式接受一个参数， **DataReader**。 在此窗体，它只需加载**DataTable**行。 或者，您可以指定**LoadOption**参数来控制如何将数据添加到**DataTable**。  
  
 **LoadOption**参数是特别有用的其中**DataTable**已包含的数据行，因为它说明了从数据源如何传入的数据将合并的数据已在表中。 例如， **PreserveCurrentValues** （默认值） 指定在其中将行标记为的情况下**Added**中**DataTable**，则**原始**值或每个列设置为匹配的行的内容从数据源。 **当前**值将保留在时添加行，分配的值和**RowState**的行的将设置为**Changed**。  
  
 下表给出了对 <xref:System.Data.LoadOption> 枚举值的简要说明。  
  
|LoadOption 值|描述|  
|----------------------|-----------------|  
|**OverwriteRow**|如果传入行具有相同**PrimaryKey**值作为行中已**DataTable**，则**原始**并**当前**每个值列将替换为传入行中的值和**RowState**属性设置为**Unchanged**。<br /><br /> 中不存在的数据源中的行**DataTable**与添加**RowState**的值**Unchanged**。<br /><br /> 此选项的作用是刷新的内容**DataTable** ，使其匹配数据源的内容。|  
|**PreserveCurrentValues （默认值）**|如果传入行具有相同**PrimaryKey**值作为行中已**DataTable**，则**原始**值设置为的内容的传入行，以及**当前**值未发生更改。<br /><br /> 如果**RowState**是**Added**或**Modified**，将其设置为**Modified**。<br /><br /> 如果**RowState**已**Deleted**，它将保持**Deleted**。<br /><br /> 中不存在的数据源中的行**DataTable**添加，并且**RowState**设置为**Unchanged**。|  
|**UpdateCurrentValues**|如果传入行具有相同**PrimaryKey**值作为行中已**DataTable**，则**当前**值复制到**原始**值，并**当前**值然后将设置为传入行的内容。<br /><br /> 如果**RowState**中**DataTable**已**Added**，则**RowState**保持**Added**。 行标记为**Modified**或**Deleted**，则**RowState**是**Modified**。<br /><br /> 中不存在的数据源中的行**DataTable**添加，并且**RowState**设置为**Added**。|  
  
 下面的示例使用**负载**方法来显示中的员工的生日列表**Northwind**数据库。  
  
```vb  
Private Sub LoadBirthdays(ByVal connectionString As String)  
    ' Assumes that connectionString is a valid connection string  
    ' to the Northwind database on SQL Server.  
    Dim queryString As String = _  
    "SELECT LastName, FirstName, BirthDate " & _  
      " FROM dbo.Employees " & _  
      "ORDER BY BirthDate, LastName, FirstName"  
  
    ' Open and fill a DataSet.   
    Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
        queryString, connectionString)  
    Dim employees As New DataSet  
    adapter.Fill(employees, "Employees")  
  
    ' Create a SqlDataReader for use with the Load Method.  
    Dim reader As DataTableReader = employees.GetDataReader()  
  
    ' Create an instance of DataTable and assign the first  
    ' DataTable in the DataSet.Tables collection to it.  
    Dim dataTableEmp As DataTable = employees.Tables(0)  
  
    ' Fill the DataTable with data by calling Load and  
    ' passing the SqlDataReader.  
    dataTableEmp.Load(reader, LoadOption.OverwriteRow)  
  
    ' Loop through the rows collection and display the values  
    ' in the console window.  
    Dim employeeRow As DataRow  
    For Each employeeRow In dataTableEmp.Rows  
        Console.WriteLine("{0:MM\\dd\\yyyy}" & ControlChars.Tab & _  
          "{1}, {2}", _  
          employeeRow("BirthDate"), _  
          employeeRow("LastName"), _  
          employeeRow("FirstName"))  
    Next employeeRow  
  
    ' Keep the window opened to view the contents.  
    Console.ReadLine()  
End Sub  
```  
  
## <a name="see-also"></a>请参阅
- [操作数据表中的数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
