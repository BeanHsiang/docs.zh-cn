---
title: DataTables
ms.date: 03/30/2017
ms.assetid: 52ff0e32-3e5a-41de-9a3b-7b04ea52b83e
ms.openlocfilehash: f0f429d7f28360fd76dfff0e7d4a4eba019e5acf
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54653239"
---
# <a name="datatables"></a>DataTables
<xref:System.Data.DataSet> 由表、关系和约束的集合组成。 在 ADO.NET 中，<xref:System.Data.DataTable>对象用于表示中的表**数据集**。 一个**DataTable**表示的内存中关系数据; 一个表的数据是本地的。它驻留，但可以从数据源，例如 Microsoft SQL Server 使用填充的基于网络的应用程序**DataAdapter**有关详细信息，请参阅[填充数据集从 DataAdapter](../../../../../docs/framework/data/adonet/populating-a-dataset-from-a-dataadapter.md).  
  
 **DataTable**类是的成员**System.Data**中的.NET Framework 类库命名空间。 可以创建和使用**DataTable**单独或作为的成员**数据集**，并**DataTable**对象还可在与其他.NET Framework 对象，一起使用包括<xref:System.Data.DataView>。 访问的表中的集合**数据集**通过**表**属性**数据集**对象。  
  
 表的架构或结构由列和约束表示。 定义的架构**DataTable**使用<xref:System.Data.DataColumn>对象，以及<xref:System.Data.ForeignKeyConstraint>和<xref:System.Data.UniqueConstraint>对象。 表中的列可以映射到数据源中的列、包含从表达式计算所得的值、自动递增它们的值，或包含主键值。  
  
 架构，除了**DataTable**还必须具有要包含并对数据排序的行。 <xref:System.Data.DataRow> 类表示表中包含的实际数据。 您使用**DataRow**和其属性和方法用于检索、 计算和处理表中的数据。 在访问和更改的行的数据**DataRow**对象维护其当前和原始状态。  
  
 您可以使用表中的一个或多个相关的列来创建表与表之间的父子关系。 创建之间的关系**DataTable**对象使用<xref:System.Data.DataRelation>。 **DataRelation**对象然后可用于返回特定行的相关的子或父行。 有关详细信息，请参阅[添加 Datarelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [创建数据表](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-datatable.md)  
 说明如何创建**DataTable**并将其添加到**数据集**。  
  
 [数据表架构定义](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)  
 提供有关创建和使用信息**DataColumn**对象和约束。  
  
 [操作数据表中的数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)  
 说明如何添加、修改和删除表中的数据。 说明如何使用**DataTable**事件来检查对表中的数据的更改。  
  
 [处理数据表事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)  
 用于提供有关可用的事件信息**DataTable**，包括修改列值和添加或删除行时的事件。  
  
## <a name="related-sections"></a>相关章节  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)  
 描述 ADO.NET 结构和组件，并说明如何用来访问现有的数据源和管理应用程序数据。  
  
 [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 提供有关 ADO.NET 的信息**数据集**包括如何创建表之间的关系。  
  
 <xref:System.Data.Constraint>  
 有关提供的参考信息**约束**对象。  
  
 <xref:System.Data.DataColumn>  
 有关提供的参考信息**DataColumn**对象。  
  
 <xref:System.Data.DataSet>  
 有关提供的参考信息**数据集**对象。  
  
 <xref:System.Data.DataTable>  
 有关提供的参考信息**DataTable**对象。  
  
 [类库概述](../../../../../docs/standard/class-library-overview.md)  
 概述了.NET Framework 类库，包括**系统**命名空间以及第二个级别的命名空间**System.Data**。  
  
## <a name="see-also"></a>请参阅
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
