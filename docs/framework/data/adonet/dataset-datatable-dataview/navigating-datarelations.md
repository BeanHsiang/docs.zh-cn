---
title: 导航 DataRelation
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
ms.openlocfilehash: 0f19e08aba36d2e93033fb944efe848d4e1125e8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54732773"
---
# <a name="navigating-datarelations"></a>导航 DataRelation
<xref:System.Data.DataRelation> 的一项主要功能就是在 <xref:System.Data.DataTable> 中从一个 <xref:System.Data.DataSet> 浏览到另一个。 这使您可以检索所有相关<xref:System.Data.DataRow>中一个对象**DataTable**如果给定的单个**DataRow**从相关**DataTable**。 例如，在建立**DataRelation**之间的客户表和 orders 的表，可以检索有关特定客户行使用的所有订单行**GetChildRows**。  
  
 下面的代码示例将创建**DataRelation**之间**客户**表和**订单**的表**数据集**，并返回每个客户的所有订单。  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 下一示例以上例为基础，将四个表关联在一起，并浏览这些关系。 如前面的示例中所示**CustomerID**相关**客户**表**订单**表。 对于中的每个客户**客户**表中的所有子行**订单**取决于都表，以便返回特定客户的订单数以及它们**OrderID**值。  
  
 扩展的示例还将返回的值从**OrderDetails**并**产品**表。 **订单**表与相关**OrderDetails**表可使用**OrderID**来确定每个客户订单的产品及数量进行排序。 因为**OrderDetails**表仅包含**ProductID**已订购产品， **OrderDetails**与相关**产品**使用**ProductID**为了返回**ProductName**。 在这一关系，**产品**表为父表和**订单详细信息**表为子表。 因此，当循环访问**OrderDetails**表中， **GetParentRow**调用以检索相关**ProductName**值。  
  
 请注意，当**DataRelation**为创建**客户**并**订单**表，为指定任何值**createConstraints**标志 (默认值是 **，则返回 true**)。 这假定所有中行**订单**表具有**CustomerID**存在的父代中的值**客户**表。 如果**CustomerID**存在于**订单**表中不存在**客户**表，<xref:System.Data.ForeignKeyConstraint>会导致引发异常。  
  
 当子列可能包含父列不包含的值时，设置**createConstraints**标记，用于**false**添加时**DataRelation**。 在示例中， **createConstraints**标志设置为**false**有关**DataRelation**之间**订单**表和**OrderDetails**表。 这使应用程序返回中的所有记录**OrderDetails**表，并仅从记录的子集**订单**表而不会生成运行时异常。 该扩展示例生成以下格式的输出。  
  
```  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 下面的代码示例是一个扩展的示例位置中的值**OrderDetails**并**产品**返回表，使用中的记录的一个子集**订单**返回的表。  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## <a name="see-also"></a>请参阅
- [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
