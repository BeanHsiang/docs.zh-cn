---
title: DataRow 删除
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c34f531d-4b9b-4071-b2d7-342c402aa586
ms.openlocfilehash: 69bdf4d23463cc07259a2b1de6b9efaa78f0f0de
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54593753"
---
# <a name="datarow-deletion"></a>DataRow 删除
有两种方法可用于删除<xref:System.Data.DataRow>对象从<xref:System.Data.DataTable>对象：**删除**方法<xref:System.Data.DataRowCollection>对象，和<xref:System.Data.DataRow.Delete%2A>方法**DataRow**对象。 而<xref:System.Data.DataRowCollection.Remove%2A>方法删除**DataRow**从**DataRowCollection**，则<xref:System.Data.DataRow.Delete%2A>方法仅将标记为删除的行。 当应用程序调用时，会发生实际移除**AcceptChanges**方法。 通过使用 <xref:System.Data.DataRow.Delete%2A>，您可以在实际删除行之前，先以编程方式来检查哪些行已标记为删除。 如果将行标记为删除，则该行的 <xref:System.Data.DataRow.RowState%2A> 属性会设置为 <xref:System.Data.DataRow.Delete%2A>。  
  
 在 foreach 循环中，不会调用 <xref:System.Data.DataRow.Delete%2A> 和 <xref:System.Data.DataRowCollection.Remove%2A>，而是循环访问 <xref:System.Data.DataRowCollection> 对象。 <xref:System.Data.DataRow.Delete%2A> 和 <xref:System.Data.DataRowCollection.Remove%2A> 不会修改该集合的状态。  
  
 使用时<xref:System.Data.DataSet>或**DataTable**结合**DataAdapter**和关系数据源，使用**删除**方法的**DataRow**以删除的行。 **删除**方法将行标记为**Deleted**中**数据集**或者**DataTable**但不会删除它。 相反，当**DataAdapter**遇到标记为行**已删除**，它将执行其**DeleteCommand**方法来删除数据源处的行。 行随后便会永久删除使用**AcceptChanges**方法。 如果您使用**删除**若要删除的行，该行是完全从表中删除，但**DataAdapter**不会删除数据源处的行。  
  
 **删除**方法**DataRowCollection**采用**DataRow**作为自变量并将其从集合中，删除，如下面的示例中所示。  
  
```vb  
workTable.Rows.Remove(workRow)  
```  
  
```csharp  
workTable.Rows.Remove(workRow);  
```  
  
 与此相反，下面的示例演示如何调用**删除**方法**DataRow**若要更改其**RowState**到**Deleted**.  
  
```vb  
workRow.Delete  
```  
  
```csharp  
workRow.Delete();  
```  
  
 如果将行标记为待删除，并且调用**AcceptChanges**方法**DataTable**对象，从删除行**DataTable**。 相反，如果您调用**RejectChanges**，则**RowState**的行的将恢复为标记为前**Deleted**。  
  
> [!NOTE]
>  如果**RowState**的**DataRow**是**Added**，这意味着它只是已添加到表中，然后将其标记为**Deleted**，它是从表中删除。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Data.DataRow>
- <xref:System.Data.DataRowCollection>
- <xref:System.Data.DataTable>
- [操作数据表中的数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
