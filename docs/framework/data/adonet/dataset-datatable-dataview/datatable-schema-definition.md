---
title: 数据表架构定义
ms.date: 03/30/2017
ms.assetid: efbcdda4-f5a9-421d-8be2-4c194c74552f
ms.openlocfilehash: aa275e0a9cbd4f8fb3e851865b9de49eca327727
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54545379"
---
# <a name="datatable-schema-definition"></a>数据表架构定义
表的架构（即结构）由列和约束表示。 使用 <xref:System.Data.DataTable> 对象以及 <xref:System.Data.DataColumn> 和 <xref:System.Data.ForeignKeyConstraint> 对象定义 <xref:System.Data.UniqueConstraint> 的架构。 表中的列可以映射到数据源中的列、包含从表达式计算所得的值、自动递增它们的值，或包含主键值。  
  
 按名称引用表中的列、关系和约束是区分大小写的。 因此，一个表中可以存在两个或两个以上名称相同（但大小写不同）的列、关系或约束。 例如，你可以**Col1**并**col1**。 在这种情况下，按名称引用某一列就必须完全符合该列名的大小写，否则会引发异常。 例如，如果表**myTable**包含的列**Col1**并**col1**，将引用**Col1**按名称作为**myTable.Columns["Col1"]**，并**col1**作为**myTable.Columns["col1"]**。 正在尝试引用的列作为任一**myTable.Columns["COL1"]** 会生成异常。  
  
 如果某个特定名称只存在一个列、关系或约束，则不应用区分大小写规则。 也就是说，如果表中没有其他的列、关系或约束对象与该特定列、关系或约束对象的名称匹配，您就可以使用任意的大小写来按名称引用该对象，并且不会引发异常。 例如，如果表中只有**Col1**，您可以引用它使用**我。列"COL1"**。  
  
> [!NOTE]
>  <xref:System.Data.DataTable.CaseSensitive%2A>的属性**DataTable**不会影响此行为。 **CaseSensitive**属性适用于数据中的表和影响排序、 搜索、 筛选、 强制执行约束，以此类推，但不适用于对列、 关系和约束的引用。  
  
## <a name="in-this-section"></a>本节内容  
 [向数据表添加列](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-columns-to-a-datatable.md)  
 介绍如何定义表使用的列**DataColumn**对象。  
  
 [创建表达式列](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-expression-columns.md)  
 介绍如何**表达式**列属性可用于计算值的行中其他列中的值。  
  
 [创建 AutoIncrement 列](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-autoincrement-columns.md)  
 说明如何将列设置为自动递增数值，以确保每行都有唯一的列值。  
  
 [定义主键](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md)  
 介绍如何指定从一个或多个表的主键**DataColumn**对象。  
  
 [数据表约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)  
 说明如何为表中的列定义外键和唯一约束。  
  
## <a name="see-also"></a>请参阅
- [数据表](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
