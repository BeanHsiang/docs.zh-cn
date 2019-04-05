---
title: DataTableReader
ms.date: 03/30/2017
ms.assetid: 97546ae2-0e42-4d26-961d-e0b244d81ded
ms.openlocfilehash: 9984dc9c215a34ab35524560e4dcbcd6bd12596d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54602840"
---
# <a name="datatablereaders"></a>DataTableReader
<xref:System.Data.DataTableReader> 以一个或多个只读、只进结果集的形式提供 <xref:System.Data.DataTable> 或的 <xref:System.Data.DataSet> 的内容。  
  
 当您创建**DataTableReader**从**DataTable**，从而**DataTableReader**对象包含一个结果集具有相同的数据**DataTable**从创建它，但已标记为已删除任何行除外。 列的显示顺序与在原始**DataTable**。  
  
 一个**DataTableReader**可能包含多个结果集，如果它通过调用创建<xref:System.Data.DataSet.CreateDataReader%2A>。 结果采用的顺序相同**DataTables**中**数据集**对象的<xref:System.Data.DataSet.Tables%2A>集合。  
  
## <a name="in-this-section"></a>本节内容  
 [创建 DataReader](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-datareader.md)  
 讨论如何创建**DataTableReader**对象。  
  
 [导航数据表](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/navigating-datatables.md)  
 介绍如何使用**读**方法来移动的内容通过**DataTableReader**。  
  
## <a name="see-also"></a>请参阅
- [在 ADO.NET 中检索和修改数据](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
