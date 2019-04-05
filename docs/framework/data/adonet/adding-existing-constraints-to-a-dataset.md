---
title: 将现有约束添加到数据集
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.openlocfilehash: 39b1e9945a1cf6cd847fbe82c0b29e50f23bf785
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54714144"
---
# <a name="adding-existing-constraints-to-a-dataset"></a>将现有约束添加到数据集
**填充**方法**DataAdapter**填充<xref:System.Data.DataSet>只使用表中的列和行从数据源; 但是约束通常设置数据源，**填充**方法不会添加到此架构信息**数据集**默认情况下。 若要填充**数据集**与现有主键约束信息从数据源，可以通过调用**FillSchema**方法**DataAdapter**，或设置**MissingSchemaAction**的属性**DataAdapter**到**AddWithKey**之前调用**填充**。 这将确保该主键中的约束**数据集**反映数据源。 外键约束信息不包含在内，必须显式创建，如中所示[数据表约束](../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)。  
  
 添加到架构信息**数据集**用数据填充可确保主键约束所含之前<xref:System.Data.DataTable>中的对象**数据集**。 因此，当再次调用来填充**数据集**设为主要键列的信息用于匹配与当前行中每个数据源的新行**DataTable**，以及在当前数据使用数据源的数据覆盖表。 如果没有架构信息中，从数据源的新行追加到**数据集**，从而导致重复的行。  
  
> [!NOTE]
>  如果数据源中的列被标识为自动递增**FillSchema**方法，或**填充**方法替换**MissingSchemaAction**的**AddWithKey**，创建**DataColumn**与**AutoIncrement**属性设置为`true`。 但是，你将需要设置**AutoIncrementStep**并**AutoIncrementSeed**自己的值。 有关自动递增列的详细信息，请参阅[创建 AutoIncrement 列](../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-autoincrement-columns.md)。  
  
 使用**FillSchema**或设置**MissingSchemaAction**到**AddWithKey**需要额外的处理，在数据源来确定主键列信息。 这一额外的处理可能会降低性能。 如果主键信息在设计时已知，为了实现最佳性能，建议显式指定一个或多个主键列。 有关显式设置表的主键信息的信息，请参阅[定义主键](../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md)。  
  
 下面的代码示例演示如何将架构信息添加**数据集**使用**FillSchema**。  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers")  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers");  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
 下面的代码示例演示如何将架构信息添加**数据集**使用**MissingSchemaAction.AddWithKey**属性**填充**方法。  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
## <a name="handling-multiple-result-sets"></a>处理多个结果集  
 如果**DataAdapter**遇到多个结果集返回从**SelectCommand**，它将创建多个表中的**数据集**。 这些表提供的从零开始递增的默认名称**表** *N*，从开始**表**而不是"Table0"。 如果作为参数传递表名**FillSchema**方法，这些表将会提供的从零开始增量名称**TableName** *N*，从开始**TableName**而不是"TableName0"。  
  
> [!NOTE]
>  如果**FillSchema**方法**OleDbDataAdapter**返回多个结果集的命令调用对象时，所返回的架构信息将从第一个结果集。 当返回架构信息的多个结果集使用**OleDbDataAdapter**，，则建议您指定**MissingSchemaAction**的**AddWithKey**并获取架构信息时调用**填充**方法。  
  
## <a name="see-also"></a>请参阅
- [DataAdapters 和 DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [数据集、数据表和数据视图](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
