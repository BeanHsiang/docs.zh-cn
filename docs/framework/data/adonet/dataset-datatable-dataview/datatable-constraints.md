---
title: 数据表约束
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 27c9f2fd-f64d-4b4e-bbf6-1d24f47067cb
ms.openlocfilehash: d0b3bd649da301c563a19450d7d9b42e9d0b29e9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54611756"
---
# <a name="datatable-constraints"></a>数据表约束
为了维护数据的完整性，可以使用约束来对 <xref:System.Data.DataTable> 中的数据施加限制。 约束是应用于某列或相关各列的自动规则，它决定了某行的值以某种方式更改时的操作过程。 强制执行约束时`System.Data.DataSet.EnforceConstraints`的属性<xref:System.Data.DataSet>是**true**。 有关显示如何设置 `EnforceConstraints` 属性的代码示例，请参见 <xref:System.Data.DataSet.EnforceConstraints%2A> 参考主题。  
  
 ADO.NET 中有两种约束：<xref:System.Data.ForeignKeyConstraint> 和 <xref:System.Data.UniqueConstraint>。 默认情况下，这两种约束都会自动创建时创建通过添加两个或多个表之间的关系<xref:System.Data.DataRelation>到**数据集**。 但是，可以通过指定禁用此行为**createConstraints** = **false**创建关系时。  
  
## <a name="foreignkeyconstraint"></a>ForeignKeyConstraint  
 一个**ForeignKeyConstraint**强制实施有关如何传播更新和删除对相关表的规则。 例如，如果更新或删除一个表中的行中的值和相同的值还可在一个或多个相关表， **ForeignKeyConstraint**确定相关表中会发生什么情况。  
  
 <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A>并<xref:System.Data.ForeignKeyConstraint.UpdateRule%2A>的属性**ForeignKeyConstraint**定义当用户尝试删除或更新相关表中的行时采取的操作。 下表描述了可用于不同的设置**DeleteRule**并**UpdateRule**的属性**ForeignKeyConstraint**。  
  
|规则设置|描述|  
|------------------|-----------------|  
|**Cascade**|删除或更新相关的行。|  
|**SetNull**|在相关的行中设置值**DBNull**。|  
|**SetDefault**|将相关行中的值设置为默认值。|  
|**无**|对相关行不执行任何操作。 这是默认设置。|  
  
 一个**ForeignKeyConstraint**可以限制，并传播到更改相关列。 具体取决于对设置的属性**ForeignKeyConstraint**的列，如果**EnforceConstraints**属性**数据集**是**true**，执行对父行的某些操作将导致异常。 例如，如果**DeleteRule**的属性**ForeignKeyConstraint**是**None**，如果有子行不能删除父行。  
  
 可以创建一组使用的列之间或单个列之间的外键约束**ForeignKeyConstraint**构造函数。 传递得到**ForeignKeyConstraint**对象传递给**添加**表的方法**约束**属性，它是**ConstraintCollection**. 此外可以将构造函数自变量传递给的几个重载**外**方法**ConstraintCollection**创建**ForeignKeyConstraint**。  
  
 创建时**ForeignKeyConstraint**，可以将传递**DeleteRule**并**UpdateRule**值构造函数作为自变量，也可以将它们设置为作为中的属性以下示例 (其中**DeleteRule**值设置为**None**)。  
  
```vb  
Dim custOrderFK As ForeignKeyConstraint = New ForeignKeyConstraint("CustOrderFK", _  
  custDS.Tables("CustTable").Columns("CustomerID"), _  
  custDS.Tables("OrdersTable").Columns("CustomerID"))  
custOrderFK.DeleteRule = Rule.None    
' Cannot delete a customer value that has associated existing orders.  
custDS.Tables("OrdersTable").Constraints.Add(custOrderFK)  
```  
  
```csharp  
ForeignKeyConstraint custOrderFK = new ForeignKeyConstraint("CustOrderFK",  
  custDS.Tables["CustTable"].Columns["CustomerID"],   
  custDS.Tables["OrdersTable"].Columns["CustomerID"]);  
custOrderFK.DeleteRule = Rule.None;    
// Cannot delete a customer value that has associated existing orders.  
custDS.Tables["OrdersTable"].Constraints.Add(custOrderFK);  
```  
  
### <a name="acceptrejectrule"></a>AcceptRejectRule  
 可以使用接受对行的更改**AcceptChanges**方法或已取消使用**RejectChanges**方法**数据集**， **DataTable**，或**DataRow**。 当**数据集**包含**ForeignKeyConstraints**，则调用**AcceptChanges**或者**RejectChanges**方法会强制**AcceptRejectRule**。 **AcceptRejectRule**的属性**ForeignKeyConstraint**确定将采取的操作在子活动时行**AcceptChanges**或**RejectChanges**对父行调用。  
  
 下表列出的可用设置**AcceptRejectRule**。  
  
|规则设置|描述|  
|------------------|-----------------|  
|**Cascade**|接受或拒绝对子行的更改。|  
|**无**|对子行不执行任何操作。 这是默认设置。|  
  
### <a name="example"></a>示例  
 下面的示例创建一个 <xref:System.Data.ForeignKeyConstraint>，设置它的一些属性（包括 <xref:System.Data.ForeignKeyConstraint.AcceptRejectRule%2A>），并将它添加到 <xref:System.Data.ConstraintCollection> 对象的 <xref:System.Data.DataTable>。  
  
 [!code-csharp[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/CS/source.cs#1)]
 [!code-vb[DataWorks Data.AcceptRejectRule#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.AcceptRejectRule/VB/source.vb#1)]  
  
## <a name="uniqueconstraint"></a>UniqueConstraint  
 **UniqueConstraint**对象，它可以分配到单个列或列中的数组**DataTable**，确保指定的列或列中的所有数据都是唯一每个行。 可以通过创建唯一约束列或一组列**UniqueConstraint**构造函数。 传递得到**UniqueConstraint**对象传递给**添加**表的方法**约束**属性，它是**ConstraintCollection**. 此外可以将构造函数自变量传递给的几个重载**外**方法**ConstraintCollection**创建**UniqueConstraint**。 创建时**UniqueConstraint**对于某一列或列，您可以选择指定的列是否为主键。  
  
 此外可以通过设置创建唯一约束的列**Unique**属性的列**true**。 或者，设置**Unique**到单个列的属性**false**删除可能存在的任何唯一约束。 如果将一列或多列定义为表的主键，会自动为一个或多个指定的列创建唯一的约束。 如果您删除某列从**PrimaryKey**的属性**DataTable**，则**UniqueConstraint**中删除。  
  
 下面的示例创建**UniqueConstraint**的两列**DataTable**。  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custUnique As UniqueConstraint = _  
    New UniqueConstraint(New DataColumn()   {custTable.Columns("CustomerID"), _  
    custTable.Columns("CompanyName")})  
custDS.Tables("Customers").Constraints.Add(custUnique)  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
UniqueConstraint custUnique = new UniqueConstraint(new DataColumn[]   
    {custTable.Columns["CustomerID"],   
    custTable.Columns["CompanyName"]});  
custDS.Tables["Customers"].Constraints.Add(custUnique);  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Data.DataRelation>
- <xref:System.Data.DataTable>
- <xref:System.Data.ForeignKeyConstraint>
- <xref:System.Data.UniqueConstraint>
- [数据表架构定义](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)
- [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
