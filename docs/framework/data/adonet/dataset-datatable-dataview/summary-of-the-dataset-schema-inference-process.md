---
title: 数据集架构接口过程摘要
ms.date: 03/30/2017
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
ms.openlocfilehash: 1eb12fd9c983bc0013b5dc528e0b3389250bdbe2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54527648"
---
# <a name="summary-of-the-dataset-schema-inference-process"></a>数据集架构接口过程摘要
推断过程首先从 XML 文档中确定将哪些元素推断为表。 从剩余的 XML 中，推断过程确定这些表的列。 对于嵌套表，推断过程会生成嵌套的 <xref:System.Data.DataRelation> 和 <xref:System.Data.ForeignKeyConstraint> 对象。  
  
 下面是推断规则的简要概述：  
  
-   具有属性的元素会被推断为表。  
  
-   具有子元素的元素会被推断为表。  
  
-   重复的元素会被推断为单个表。  
  
-   如果文档元素（即根元素）不具有属性和将被推断为列的子元素，则将被推断为 <xref:System.Data.DataSet>。 否则，文档元素会被推断为表。  
  
-   属性会被推断为列。  
  
-   不具有属性或子元素且不重复的元素会被推断为列。  
  
-   元素被推断为嵌套表中其他元素，同样被推断为表，嵌套**DataRelation**在两个表之间创建。 名为的新的主要密钥列**TableName_Id**添加到这两个表并使用**DataRelation**。 一个**ForeignKeyConstraint**使用在两个表之间创建**TableName_Id**列。  
  
-   对于被推断为表和包含文本但没有子元素的元素，新列命名为**TableName_Text**创建的每个元素的文本。 如果元素被推断为表并包含文本和子元素，则将忽略文本。  
  
## <a name="see-also"></a>请参阅
- [从 XML 推断数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)
- [从 XML 加载数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)
- [从 XML 加载数据集构架信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)
- [在数据集中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)
- [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
