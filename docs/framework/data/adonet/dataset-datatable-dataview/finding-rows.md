---
title: 查找行
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5da300e2-74c0-4d13-9202-fc20ed8212d8
ms.openlocfilehash: e5a48c5caf9239e0e7b7f2e7a3ad8ab5df168ba1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54684185"
---
# <a name="finding-rows"></a>查找行
可以使用 <xref:System.Data.DataView.Find%2A> 的 <xref:System.Data.DataView.FindRows%2A> 和 <xref:System.Data.DataView> 方法，根据排序关键字值搜索行。 中的值以搜索是否区分大小写**查找**并**FindRows**方法由**CaseSensitive**属性的基础<xref:System.Data.DataTable>。 搜索值必须完全匹配现有排序关键字值才能返回结果。  
  
 **查找**方法返回一个整数，其索引的<xref:System.Data.DataRowView>与搜索条件匹配的。 如果多个行匹配搜索条件，仅第一个匹配的索引**DataRowView**返回。 如果不找到任何匹配项，**查找**返回-1。  
  
 若要返回的多个行匹配的搜索结果，请使用**FindRows**方法。 **FindRows**工作方式就类似于**查找**方法，前者返回**DataRowView**引用中的所有匹配行的数组**DataView**。 如果不找到任何匹配项， **DataRowView**数组将为空。  
  
 若要使用**查找**或**FindRows**方法必须指定排序顺序设置**ApplyDefaultSort**到**true**或通过使用**排序**属性。 如果未指定排序顺序，则将引发异常。  
  
 **查找**并**FindRows**方法采用一个值数组作为其长度与排序顺序中的列数相匹配的输入。 在对单个列进行排序的情况下，可以传递单个值。 对于包含多个列的排序顺序，可传递一个对象数组。 请注意，对多个列上进行排序，对象数组中的值必须匹配中指定的列的顺序**排序**的属性**DataView**。  
  
 下面的代码示例演示**查找**方法调用针对**DataView**使用单个列的排序顺序。  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName", DataViewRowState.CurrentRows)  
  
Dim rowIndex As Integer = custView.Find("The Cracker Box")  
  
If rowIndex = -1 Then  
  Console.WriteLine("No match found.")  
Else  
  Console.WriteLine("{0}, {1}", _  
    custView(rowIndex)("CustomerID").ToString(), _  
    custView(rowIndex)("CompanyName").ToString())  
End If  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",   
  "CompanyName", DataViewRowState.CurrentRows);  
  
int rowIndex = custView.Find("The Cracker Box");  
  
if (rowIndex == -1)  
  Console.WriteLine("No match found.");  
else  
  Console.WriteLine("{0}, {1}",  
    custView[rowIndex]["CustomerID"].ToString(),  
    custView[rowIndex]["CompanyName"].ToString());  
```  
  
 如果你**排序**属性指定多个列，则必须按指定顺序通过包含每个列的搜索值的对象数组**排序**属性，如以下代码示例所示。  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName, ContactName", _  
  DataViewRowState.CurrentRows)  
  
Dim foundRows() As DataRowView = _  
  custView.FindRows(New object() {"The Cracker Box", "Liu Wong"})  
  
If foundRows.Length = 0 Then  
  Console.WriteLine("No match found.")  
Else  
  Dim myDRV As DataRowView  
  For Each myDRV In foundRows  
    Console.WriteLine("{0}, {1}", _  
      myDRV("CompanyName").ToString(), myDRV("ContactName").ToString())  
  Next  
End If  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",  
  "CompanyName, ContactName",  
  DataViewRowState.CurrentRows);  
  
DataRowView[] foundRows =   
  custView.FindRows(new object[] {"The Cracker Box", "Liu Wong"});  
  
if (foundRows.Length == 0)  
  Console.WriteLine("No match found.");  
else  
  foreach (DataRowView myDRV in foundRows)  
    Console.WriteLine("{0}, {1}", myDRV["CompanyName"].ToString(),   
      myDRV["ContactName"].ToString());  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
