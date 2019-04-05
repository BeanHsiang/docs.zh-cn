---
title: 将关键 XML 架构 (XSD) 约束映射到数据集约束
ms.date: 03/30/2017
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
ms.openlocfilehash: a68c43e9ab0a47c6a38bc794bac7d3ceb71391f6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54677623"
---
# <a name="map-key-xml-schema-xsd-constraints-to-dataset-constraints"></a>将关键 XML 架构 (XSD) 约束映射到数据集约束
在架构中，你可以指定在元素上的键约束或属性使用**密钥**元素。 对其指定键约束的元素或属性必须在任何架构实例中都具有唯一值，并且不能具有空值。  
  
 除了对其定义键约束的列不能具有空值之外，键约束与唯一约束类似。  
  
 下表概括**msdata**可以在指定的属性**密钥**元素。  
  
|特性名|描述|  
|--------------------|-----------------|  
|**msdata:ConstraintName**|如果指定了该属性，它的值将用作约束名。 否则为**名称**属性提供值的约束名称。|  
|**msdata:PrimaryKey**|如果`PrimaryKey="true"`存在，则**IsPrimaryKey**约束属性设置为**true**，从而使其主键。 **AllowDBNull**列属性设置为**false**，因为主键不能具有 null 值。|  
  
 在转换中的指定键约束的架构，映射过程将创建具有表的唯一约束**AllowDBNull**列属性设置为**false**中每一列约束。 **IsPrimaryKey**唯一约束的属性也设置为**false**除非有指定，否则`msdata:PrimaryKey="true"`上**密钥**元素。 它与 `PrimaryKey="true"` 的架构中的唯一约束相同。  
  
 在以下架构示例中，**键**元素上指定的键约束**CustomerID**元素。  
  
```xml  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>   
```  
  
 **键**元素指定的值**CustomerID**的子元素**客户**元素必须具有唯一值，并且不能具有 null 值。 在转换 XML 架构定义语言 (XSD) 架构时，映射过程将创建下表：  
  
```  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 XML 架构映射还会创建**UniqueConstraint**上**CustomerID**列，如下所示<xref:System.Data.DataSet>。 （为简便起见，只显示相关属性。）  
  
```  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID   
      IsPrimaryKey: True  
```  
  
 在中**数据集**生成， **IsPrimaryKey**属性**UniqueConstraint**设置为**true**因为架构指定`msdata:PrimaryKey="true"`中**密钥**元素。  
  
 值**ConstraintName**的属性**UniqueConstraint**中**数据集**的值**msdata:ConstraintName**中指定的属性**密钥**架构中的元素。  
  
## <a name="see-also"></a>请参阅
- [将 XML 架构 (XSD) 约束映射到数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [从 XML 架构生成数据集关系 (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
