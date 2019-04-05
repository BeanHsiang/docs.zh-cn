---
title: 将 keyref XML 架构 (XSD) 约束映射到数据集约束
ms.date: 03/30/2017
ms.assetid: 5b634fea-cc1e-4f6b-9454-10858105b1c8
ms.openlocfilehash: bc3863bbe6fd7c290c25056e2420107ed2d8bff3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54732799"
---
# <a name="map-keyref-xml-schema-xsd-constraints-to-dataset-constraints"></a>将 keyref XML 架构 (XSD) 约束映射到数据集约束
**Keyref**元素可用于在文档内的元素之间建立链接。 它类似于关系数据库中的外键关系。 如果指定了架构**keyref**元素，元素转换到的表中的列上的相应外键约束在架构映射过程<xref:System.Data.DataSet>。 默认情况下**keyref**元素还会生成关系，使用**ParentTable**， **ChildTable**， **ParentColumn**，和**ChildColumn**对关系指定的属性。  
  
 下表概括**msdata**您可以在指定的属性**keyref**元素。  
  
|特性名|描述|  
|--------------------|-----------------|  
|**msdata:ConstraintOnly**|如果**ConstraintOnly ="true"** 上指定**keyref**架构中的元素，创建一个约束，但不创建任何关系。 如果未指定此属性 (或将设置为**False**)，在创建约束和关系**数据集**。|  
|**msdata:ConstraintName**|如果**ConstraintName**指定属性，其值将用作约束的名称。 否则为**名称**的属性**keyref**架构中的元素提供中的约束名称**数据集**。|  
|**msdata:UpdateRule**|如果**UpdateRule**中指定特性**keyref**架构中的元素，其值分配给**UpdateRule**约束属性中的**数据集**。 否则为**UpdateRule**属性设置为**Cascade**。|  
|**msdata:DeleteRule**|如果**DeleteRule**中指定特性**keyref**架构中的元素，其值分配给**DeleteRule**约束属性中的**数据集**。 否则为**DeleteRule**属性设置为**Cascade**。|  
|**msdata:AcceptRejectRule**|如果**AcceptRejectRule**中指定特性**keyref**架构中的元素，其值分配给**AcceptRejectRule** 中的约束属性**数据集**。 否则为**AcceptRejectRule**属性设置为**None**。|  
  
 下面的示例包含一个架构，指定**键**并**keyref**之间的关系**OrderNumber**的子元素**顺序**元素和**OrderNo**的子元素**OrderDetail**元素。  
  
 在示例中， **OrderNumber**的子元素**OrderDetail**元素是指**OrderNo**键子元素**顺序**元素。  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 XML 架构定义语言 (XSD) 架构映射过程会生成以下**数据集**这两个表：  
  
```  
OrderDetail(OrderNo, ItemNo) and  
Order(OrderNumber, EmpNumber)  
```  
  
 此外，**数据集**定义以下约束：  
  
-   Unique 约束**顺序**表。  
  
    ```  
              Table: Order  
    Columns: OrderNumber   
    ConstraintName: OrderNumberKey  
    Type: UniqueConstraint  
    IsPrimaryKey: False  
    ```  
  
-   之间的关系**顺序**并**OrderDetail**表。 **嵌套**属性设置为**False**因为两个元素未嵌套在架构中。  
  
    ```  
              ParentTable: Order  
    ParentColumns: OrderNumber   
    ChildTable: OrderDetail  
    ChildColumns: OrderNo   
    ParentKeyConstraint: OrderNumberKey  
    ChildKeyConstraint: OrderNoRef  
    RelationName: OrderNoRef  
    Nested: False  
    ```  
  
-   上的外键约束**OrderDetail**表。  
  
    ```  
              ConstraintName: OrderNoRef  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: OrderNo   
    RelatedTable: Order  
    RelatedColumns: OrderNumber   
    ```  
  
## <a name="see-also"></a>请参阅
- [将 XML 架构 (XSD) 约束映射到数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [从 XML 架构生成数据集关系 (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
