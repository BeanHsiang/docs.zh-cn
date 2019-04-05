---
title: 映射嵌套架构元素之间的隐式关系
ms.date: 03/30/2017
ms.assetid: 6b25002a-352e-4d9b-bae3-15129458a355
ms.openlocfilehash: 3b17b7f76870c64a9c4332dd99a71fcd8ea6b6e1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54538279"
---
# <a name="map-implicit-relations-between-nested-schema-elements"></a>映射嵌套架构元素之间的隐式关系
XML 架构定义语言 (XSD) 架构可以具有相互嵌套的复杂类型。 在这种情况下，映射过程将应用默认映射并在 <xref:System.Data.DataSet> 中创建以下内容：  
  
-   为每个复杂类型（父和子）创建一个表。  
  
-   一个附加主键列每个表定义的父级上不存在任何唯一约束，如果名为*TableName*id （_i) 其中*TableName*是父表的名称。  
  
-   为主键将附加列标识父表上的主键约束 (通过设置**IsPrimaryKey**属性设置为**True**)。 该约束以 Constraint\# 的形式来命名，其中 \# 为 1、2、3。 例如，第一个约束的默认名称为 Constraint1。  
  
-   在子表上创建外键约束，该约束将附加列标识为引用父表主键的外键。 命名约束*ParentTable_ChildTable*其中*ParentTable*是父表的名称并*ChildTable*是子表的名称。  
  
-   在父表和子表之间创建数据关系。  
  
 下面的示例演示一个架构位置**OrderDetail**是子元素的**顺序**。  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
   <xs:complexType>  
     <xs:choice maxOccurs="unbounded">  
       <xs:element name="Order">  
         <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:string" />  
            <xs:element name="EmpNumber" type="xs:string" />  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:string" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
         </xs:complexType>  
       </xs:element>  
     </xs:choice>  
   </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
 XML 架构映射过程中创建以下**数据集**:  
  
-   **顺序**和一个**OrderDetail**表。  
  
    ```  
    Order(OrderNumber, EmpNumber, Order_Id)  
    OrderDetail(OrderNo, ItemNo, Order_Id)  
    ```  
  
-   Unique 约束**顺序**表。 请注意， **IsPrimaryKey**属性设置为**True**。  
  
    ```  
    ConstraintName: Constraint1  
    Type: UniqueConstraint  
    Table: Order  
    Columns: Order_Id   
    IsPrimaryKey: True  
    ```  
  
-   上的外键约束**OrderDetail**表。  
  
    ```  
    ConstraintName: Order_OrderDetail  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: Order_Id   
    RelatedTable: Order  
    RelatedColumns: Order_Id   
    ```  
  
-   之间的关系**顺序**并**OrderDetail**表。 **嵌套**为此关系的属性设置为**True**因为**顺序**并**OrderDetail**元素都嵌套在架构.  
  
    ```  
    ParentTable: Order  
    ParentColumns: Order_Id   
    ChildTable: OrderDetail  
    ChildColumns: Order_Id   
    ParentKeyConstraint: Constraint1  
    ChildKeyConstraint: Order_OrderDetail  
    RelationName: Order_OrderDetail  
    Nested: True  
    ```  
  
## <a name="see-also"></a>请参阅
- [从 XML 架构生成数据集关系 (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)
- [将 XML 架构 (XSD) 约束映射到数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
