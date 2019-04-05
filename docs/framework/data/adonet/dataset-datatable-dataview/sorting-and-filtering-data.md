---
title: 对数据进行排序和筛选
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fdd9c753-39df-48cd-9822-2781afe76200
ms.openlocfilehash: 8733a9552787f7286ae76c77091b9833804478d8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54661212"
---
# <a name="sorting-and-filtering-data"></a>对数据进行排序和筛选
<xref:System.Data.DataView> 为在 <xref:System.Data.DataTable> 中对数据排序和筛选提供了多种方法：  
  
-   可以使用 <xref:System.Data.DataView.Sort%2A> 属性指定单个或多个列排序顺序并包含 ASC（升序）和 DESC（降序）参数。  
  
-   可以使用 <xref:System.Data.DataView.ApplyDefaultSort%2A> 属性自动以升序创建基于表的一个或多个主键列的排序顺序。 <xref:System.Data.DataView.ApplyDefaultSort%2A> 时，才适用**排序**属性为 null 引用或空字符串，并且表已定义主键时。  
  
-   可以使用 <xref:System.Data.DataView.RowFilter%2A> 属性根据行的列值来指定行的子集。 有关有效表达式的详细信息**RowFilter**属性，请参阅的参考信息<xref:System.Data.DataColumn.Expression%2A>属性的<xref:System.Data.DataColumn>类。  
  
     如果你想要返回的数据，而不是提供数据的子集的动态视图的特定查询的结果，请使用<xref:System.Data.DataView.Find%2A>或<xref:System.Data.DataView.FindRows%2A>方法的**DataView**以获得最佳性能而不是设置**RowFilter**属性。 设置**RowFilter**属性会重新生成索引的数据，将添加到你的应用程序的开销并降低性能。 **RowFilter**属性最适合用于数据绑定应用程序中其中绑定的控件显示筛选的结果。 **查找**并**FindRows**方法利用当前的索引而无需重新生成索引。 有关详细信息**查找**并**FindRows**方法，请参阅[查找行](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md)。  
  
-   可以使用 <xref:System.Data.DataView.RowStateFilter%2A> 属性指定要查看的行版本。 **DataView**隐式地管理要公开具体取决于哪个行版本**RowState**基础行。 例如，如果**RowStateFilter**设置为**DataViewRowState.Deleted**，则**DataView**公开**原始**行版本所有**Deleted**行，因为没有任何**当前**行版本。 您可以确定某行的行版本通过使用公开**RowVersion**的属性**DataRowView**。  
  
     下表显示的选项**DataViewRowState**。  
  
    |DataViewRowState 选项|描述|  
    |------------------------------|-----------------|  
    |**CurrentRows**|**当前**行版本的所有**Unchanged**， **Added**，并**Modified**行。 这是默认设置。|  
    |**添加**|**当前**行版本的所有**Added**行。|  
    |**已删除**|**原始**行版本的所有**Deleted**行。|  
    |**ModifiedCurrent**|**当前**行版本的所有**Modified**行。|  
    |**ModifiedOriginal**|**原始**行版本的所有**Modified**行。|  
    |**无**|没有行。|  
    |**OriginalRows**|**原始**行版本的所有**Unchanged**， **Modified**，以及**已删除**行。|  
    |**保持不变**|**当前**行版本的所有**Unchanged**行。|  
  
 有关行状态和行版本的详细信息，请参阅[行状态和行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  
  
 以下代码示例创建一个视图，该视图显示所有库存量小于或等于再订购量的产品，这些产品首先按供应商 ID 排序，然后按产品名称排序。  
  
```vb  
Dim prodView As DataView = New DataView(prodDS.Tables("Products"), _  
   "UnitsInStock <= ReorderLevel", _  
   "SupplierID, ProductName", _  
   DataViewRowState.CurrentRows)  
```  
  
```csharp  
DataView prodView = new DataView(prodDS.Tables["Products"],  
   "UnitsInStock <= ReorderLevel",  
   "SupplierID, ProductName",  
   DataViewRowState.CurrentRows);  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Data.DataViewRowState>
- <xref:System.Data.DataColumn.Expression%2A?displayProperty=nameWithType>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
