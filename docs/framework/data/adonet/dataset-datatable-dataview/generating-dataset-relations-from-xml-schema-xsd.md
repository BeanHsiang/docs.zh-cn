---
title: 从 XML 架构生成数据集关系 (XSD)
ms.date: 03/30/2017
ms.assetid: 1c9a1413-c0d2-4447-88ba-9a2b0cbc0aa8
ms.openlocfilehash: b74c992c4569512a8692b70663002fd609d3501e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54546131"
---
# <a name="generating-dataset-relations-from-xml-schema-xsd"></a>从 XML 架构生成数据集关系 (XSD)
在 <xref:System.Data.DataSet> 中，可通过创建父子关系来形成两个或更多个列之间的关联。 有三种方法来表示**数据集**XML 架构定义语言 (XSD) 架构中的关系：  
  
-   指定嵌套复杂类型。  
  
-   使用**msdata: relationship**批注。  
  
-   指定**xs: keyref**而无需**msdata:ConstraintOnly**批注。  
  
## <a name="nested-complex-types"></a>嵌套的复杂类型  
 架构中的嵌套复杂类型定义指示元素的父子关系。 下面的 XML 架构片断显示**OrderDetail**是子元素的**顺序**元素。  
  
```xml  
<xs:element name="Order">  
  <xs:complexType>  
     <xs:sequence>          
       <xs:element name="OrderDetail" />  
           <xs:complexType>               
           </xs:complexType>  
     </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 XML 架构映射过程中创建表**数据集**对应于架构中嵌套的复杂类型。 它还将创建其他列用作父**-** 所生成的表的子列。 请注意，这些**-** 子列指定的关系，这是不与指定主键/外键约束相同。  
  
## <a name="msdatarelationship-annotation"></a>msdata:Relationship 批注  
 **Msdata: relationship**批注可以显式指定不嵌套在架构中的元素之间的父-子关系。 下面的示例演示的结构**关系**元素。  
  
```xml  
<msdata:Relationship name="CustOrderRelationship"    
msdata:parent=""    
msdata:child=""    
msdata:parentkey=""    
msdata:childkey="" />  
```  
  
 特性**msdata: relationship**批注标识为父-子关系中所涉及的元素**parentkey**并**childkey**元素和关系所涉及的属性。 映射过程使用此信息来生成中的表**数据集**并创建这些表之间主键/外的键关系。  
  
 例如，以下架构片断指定**顺序**并**OrderDetail**同一级别的元素 （不嵌套）。 该架构指定**msdata: relationship**批注，指定这两个元素之间的父-子关系。 在这种情况下，显式关系必须指定使用**msdata: relationship**批注。  
  
```xml  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
        <xs:element name="OrderDetail">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
       <xs:element name="Order">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
    </xs:choice>  
  </xs:complexType>  
</xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrdDetailRelation"  
          msdata:parent="Order"  
          msdata:child="OrderDetail"   
          msdata:parentkey="OrderNumber"  
          msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
```  
  
 映射进程使用**关系**元素来创建之间的父-子关系**OrderNumber**中的列**顺序**表并**OrderNo**中的列**OrderDetail**表中**数据集**。 映射进程仅指定关系；与关系数据库中的主键/外键约束不同，它并不会自动为这些列中的值指定任何约束。  
  
### <a name="in-this-section"></a>本节内容  
 [映射嵌套架构元素之间的隐式关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-implicit-relations-between-nested-schema-elements.md)  
 描述的约束和关系中隐式创建**数据集**时在 XML 架构中遇到嵌套的元素。  
  
 [映射为嵌套元素指定的关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-relations-specified-for-nested-elements.md)  
 介绍如何在中显式设置关系**数据集**XML 架构中的嵌套元素。  
  
 [指定无嵌套元素之间的关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/specify-relations-between-elements-with-no-nesting.md)  
 介绍如何创建中的关系**数据集**不嵌套的 XML 架构元素之间。  
  
### <a name="related-sections"></a>相关章节  
 [从 XML 架构派生数据集关系结构 (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 描述的关系结构或架构**数据集**创建从 XML 架构定义语言 (XSD) 架构。  
  
 [将 XML 架构 (XSD) 约束映射到数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 描述用于创建唯一约束和外键约束中的 XML 架构元素**数据集**。  
  
## <a name="see-also"></a>请参阅
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
