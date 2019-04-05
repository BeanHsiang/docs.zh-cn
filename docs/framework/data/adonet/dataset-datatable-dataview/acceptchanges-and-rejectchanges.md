---
title: AcceptChange 和 RejectChange
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e2d1a6fe-31f9-4b83-9728-06c406a3394e
ms.openlocfilehash: 84381a9a71ae85baad618684ebf783039456854f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54538383"
---
# <a name="acceptchanges-and-rejectchanges"></a>AcceptChange 和 RejectChange
在验证中的数据所做的更改的准确性后<xref:System.Data.DataTable>，可以接受使用的更改<xref:System.Data.DataRow.AcceptChanges%2A>方法<xref:System.Data.DataRow>， <xref:System.Data.DataTable>，或<xref:System.Data.DataSet>，它将设置**当前**行值为**原始**值，并将设置**RowState**属性设置为**Unchanged**。 接受或拒绝更改会清除所有**RowError**信息和集**HasErrors**属性设置为**false**。 接受或拒绝更改还可以影响在数据源中更新数据。 有关详细信息，请参阅[使用 Dataadapter 更新数据源](../../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)。  
  
 如果外键约束上存在**DataTable**，接受或拒绝使用更改**AcceptChanges**并**RejectChanges**传播到子行的**DataRow**根据**就**。 有关详细信息，请参阅[数据表约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)。  
  
 以下示例检查有错误的行，如果可以会解决错误，拒绝无法解决错误的行。 请注意，对于已解决的错误， **RowError**值将重置为空字符串，从而导致**HasErrors**属性设置为**false**。 当已解决或拒绝，但出现错误的所有行**AcceptChanges**调用以接受所有的更改的整个**DataTable**。  
  
```vb  
If workTable.HasErrors Then  
  Dim errRow As DataRow  
  
  For Each errRow in workTable.GetErrors()  
  
    If errRow.RowError = "Total cannot exceed 1000." Then  
      errRow("Total") = 1000  
      errRow.RowError = ""    ' Clear the error.  
    Else  
      errRow.RejectChanges()  
    End If  
  Next  
End If  
  
workTable.AcceptChanges()  
```  
  
```csharp  
if (workTable.HasErrors)  
{  
  
  foreach (DataRow errRow in workTable.GetErrors())  
  {  
    if (errRow.RowError == "Total cannot exceed 1000.")  
    {  
      errRow["Total"] = 1000;  
      errRow.RowError = "";    // Clear the error.  
    }  
    else  
      errRow.RejectChanges();  
  }  
}  
  
workTable.AcceptChanges();  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Data.DataRow>
- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- [操作数据表中的数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
