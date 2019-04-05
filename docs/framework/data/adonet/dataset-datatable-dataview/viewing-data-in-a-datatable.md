---
title: 查看数据表中的数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1d26e0fb-f6e0-4afa-9a9c-b8d55b8f20dc
ms.openlocfilehash: fa8749550e10256ee0623714cc95e03a838655c8
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364484"
---
# <a name="viewing-data-in-a-datatable"></a>查看数据表中的数据

可以访问的内容<xref:System.Data.DataTable>通过使用**行**并**列**集合**DataTable**。 此外可以使用<xref:System.Data.DataTable.Select%2A>方法来返回中的数据的子集**DataTable**根据包括搜索条件的条件，排序顺序和行状态。 此外，还可以使用<xref:System.Data.DataRowCollection.Find%2A>方法**DataRowCollection**搜索使用的主键值的特定行时。

**选择**方法**DataTable**对象返回的一组<xref:System.Data.DataRow>符合指定的条件的对象。 **选择**采用的筛选表达式、 排序表达式的可选参数和**DataViewRowState**。 筛选器表达式标识要返回基于的行**DataColumn**值，例如`LastName = 'Smith'`。 排序表达式遵循用于为列排序的标准 SQL 约定，例如 `LastName ASC, FirstName ASC`。 有关编写表达式的规则，请参阅<xref:System.Data.DataColumn.Expression%2A>的属性**DataColumn**类。

> [!TIP]
> 如果您正在执行对的调用次数**选择**方法**DataTable**，您可以提高性能，方法是首先创建<xref:System.Data.DataView>有关**DataTable**。 创建**DataView**表的行编制索引。 **选择**方法然后使用该索引，显著缩短生成查询结果的时间。 有关创建信息**DataView**有关**DataTable**，请参阅[Dataview](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)。

**选择**方法确定要查看或操作的行的版本根据<xref:System.Data.DataViewRowState>。 下表描述了可能**DataViewRowState**枚举值。

|DataViewRowState 值|描述|
|----------------------------|-----------------|
|**CurrentRows**|当前行，包括未更改的行、已添加的行和已修改的行。|
|**已删除**|已删除的行。|
|**ModifiedCurrent**|当前版本，它是原始数据的修改版本。 (请参阅**ModifiedOriginal**。)|
|**ModifiedOriginal**|所有已修改行的原始版本。 当前版本是可以使用**ModifiedCurrent**。|
|**添加**|新行。|
|**无**|无。|
|**OriginalRows**|原始行，包括未更改的行和已删除的行。|
|**保持不变**|未更改的行。|

在以下示例中，**数据集**对象进行筛选，以便仅使用行其**DataViewRowState**设置为**CurrentRows**。

```vb
Dim column As DataColumn
Dim row As DataRow

Dim currentRows() As DataRow = _
    workTable.Select(Nothing, Nothing, DataViewRowState.CurrentRows)

If (currentRows.Length < 1 ) Then
  Console.WriteLine("No Current Rows Found")
Else
  For Each column in workTable.Columns
    Console.Write(vbTab & column.ColumnName)
  Next

  Console.WriteLine(vbTab & "RowState")

  For Each row In currentRows
    For Each column In workTable.Columns
      Console.Write(vbTab & row(column).ToString())
    Next

    Dim rowState As String = _
        System.Enum.GetName(row.RowState.GetType(), row.RowState)
    Console.WriteLine(vbTab & rowState)
  Next
End If
```

```csharp
DataRow[] currentRows = workTable.Select(
    null, null, DataViewRowState.CurrentRows);

if (currentRows.Length < 1 )
  Console.WriteLine("No Current Rows Found");
else
{
  foreach (DataColumn column in workTable.Columns)
    Console.Write("\t{0}", column.ColumnName);

  Console.WriteLine("\tRowState");

  foreach (DataRow row in currentRows)
  {
    foreach (DataColumn column in workTable.Columns)
      Console.Write("\t{0}", row[column]);

    Console.WriteLine("\t" + row.RowState);
  }
}
```

**选择**方法可用于返回具有不同的行**RowState**值或字段值。 下面的示例返回**DataRow**引用已被删除，并返回另一个的所有行的数组**DataRow**按排序的数组，它都引用的所有行， **CustLName**，其中**CustID**列大于 5。 浪中的信息**已删除**行中，请参阅[行状态和行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。

```vb
' Retrieve all deleted rows.
Dim deletedRows() As DataRow = workTable.Select(Nothing, Nothing, DataViewRowState.Deleted)

' Retrieve rows where CustID > 5, and order by CustLName.
Dim custRows() As DataRow = workTable.Select( _
    "CustID > 5", "CustLName ASC")
```

```csharp
// Retrieve all deleted rows.
DataRow[] deletedRows = workTable.Select(
    null, null, DataViewRowState.Deleted);

// Retrieve rows where CustID > 5, and order by CustLName.
DataRow[] custRows = workTable.Select("CustID > 5", "CustLName ASC");
```

## <a name="see-also"></a>请参阅

- <xref:System.Data.DataRow>
- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataViewRowState>
- [操作数据表中的数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)
- [行状态和行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
