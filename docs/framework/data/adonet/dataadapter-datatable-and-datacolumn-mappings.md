---
title: DataAdapter 数据表和 DataColumn 映射
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.openlocfilehash: 6aaaa126a0b19300abc2c10b88b0e4ff39a3ad66
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54530424"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>DataAdapter 数据表和 DataColumn 映射
一个**DataAdapter**包含零个或多集合<xref:System.Data.Common.DataTableMapping>中的对象及其**TableMappings**属性。 一个**DataTableMapping**提供了从对数据源，查询返回的数据之间的主映射和<xref:System.Data.DataTable>。 **DataTableMapping**可以将名称传递来代替**DataTable**到名称**填充**方法**DataAdapter**。 下面的示例创建**DataTableMapping**名为**AuthorsMapping**有关**作者**表。  
  
```vb  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors")  
```  
  
```csharp  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");  
```  
  
 一个**DataTableMapping**使您能够使用中的列名**DataTable**从数据库中的不同。 **DataAdapter**使用此映射来更新表时的列匹配。  
  
 如果未指定**TableName**或**DataTableMapping**时调用的名称**填充**或者**更新**方法**DataAdapter**，则**DataAdapter**寻找**DataTableMapping**名为"Table"。 如果该**DataTableMapping**不存在**TableName**的**DataTable**为"Table"。 可以指定默认值**DataTableMapping**通过创建**DataTableMapping** "Table"的名称。  
  
 下面的代码示例将创建**DataTableMapping** (从<xref:System.Data.Common>命名空间)，并使其指定的默认映射**DataAdapter**通过其命名为"Table"。 该示例然后将映射从查询结果中的第一个表的列 (**客户**表的**Northwind**数据库) 到一组更为用户友好名称中**Northwind 客户**表中<xref:System.Data.DataSet>。 对于未映射的列，将使用数据源中的列名称。  
  
```vb  
Dim mapping As DataTableMapping = _  
  adapter.TableMappings.Add("Table", "NorthwindCustomers")  
mapping.ColumnMappings.Add("CompanyName", "Company")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode")  
  
adapter.Fill(custDS)  
```  
  
```csharp  
DataTableMapping mapping =   
  adapter.TableMappings.Add("Table", "NorthwindCustomers");  
mapping.ColumnMappings.Add("CompanyName", "Company");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode");  
  
adapter.Fill(custDS);  
```  
  
 在更高级的情况下，你可能决定想相同**DataAdapter**以支持不同的映射不同的表加载。 若要执行此操作，只需添加附加**DataTableMapping**对象。  
  
 当**填充**方法传递的一个实例**数据集**和一个**DataTableMapping**名称，如果具有该名称的映射存在，则为; 否则为**DataTable**这使用名称。  
  
 以下示例创建两个**DataTableMapping**一个名为**客户**和一个**DataTable**的名称**BizTalkSchema**。 该示例然后将映射到 SELECT 语句返回的行**BizTalkSchema** **DataTable**。  
  
```vb  
Dim mapping As ITableMapping = _  
  adapter.TableMappings.Add("Customers", "BizTalkSchema")  
mapping.ColumnMappings.Add("CustomerID", "ClientID")  
mapping.ColumnMappings.Add("CompanyName", "ClientName")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIP")  
  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
ITableMapping mapping =   
  adapter.TableMappings.Add("Customers", "BizTalkSchema");  
mapping.ColumnMappings.Add("CustomerID", "ClientID");  
mapping.ColumnMappings.Add("CompanyName", "ClientName");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIP");  
  
adapter.Fill(custDS, "Customers");  
```  
  
> [!NOTE]
>  如果没有为列映射提供源列名称或者没有为表映射提供源表名称，则将自动生成默认名称。 如果为列映射提供没有源列，则列映射提供递增的默认名称的**SourceColumn** *N*开头**SourceColumn1**。 如果为表映射提供没有源表名称，则表映射提供递增的默认名称的**SourceTable** *N*，从开始**SourceTable1**。  
  
> [!NOTE]
>  我们建议你避免的命名约定**SourceColumn** *N*为列映射，或**SourceTable** *N*表映射，因为所提供的名称可能与中现有默认列映射名称冲突**ColumnMappingCollection**或表中的映射名称**DataTableMappingCollection**. 如果提供的名称已经存在，将引发异常。  
  
## <a name="handling-multiple-result-sets"></a>处理多个结果集  
 如果你**SelectCommand**返回多个表**填充**自动生成具有递增的值中的表的表名称**数据集**，从开始在窗体上指定表名和继续**TableName** *N*，从开始**TableName1**。 可以使用表映射自动生成的表名称映射到要为表中指定的名称**数据集**。 例如，对于**SelectCommand** ，它返回两个表**客户**并**订单**，发出以下调用到**填充**。  
  
```  
adapter.Fill(customersDataSet, "Customers")  
```  
  
 在中创建两个表**数据集**:**客户**并**Customers1**。 可以使用表映射以确保第二个表名为**订单**而不是**Customers1**。 若要执行此操作，将映射的源表**Customers1**到**数据集**表**订单**，如以下示例所示。  
  
```  
adapter.TableMappings.Add("Customers1", "Orders")  
adapter.Fill(customersDataSet, "Customers")  
```  
  
## <a name="see-also"></a>请参阅
- [DataAdapters 和 DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
