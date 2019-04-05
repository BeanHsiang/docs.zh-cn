---
title: 写入数据集内容作为 XML 数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd15f8a5-3b4c-46d0-a561-4559ab2a4705
ms.openlocfilehash: 9e4ef54321acec508aac787329cb911e083317bd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54710399"
---
# <a name="writing-dataset-contents-as-xml-data"></a>写入数据集内容作为 XML 数据
在 ADO.NET 中可以编写 <xref:System.Data.DataSet> 的 XML 表示形式（包含或不包含其架构）。 如果架构信息以内联形式包含在 XML 表示形式中，则使用 XML 架构定义语言 (XSD) 来编写。 架构包含 <xref:System.Data.DataSet> 的表定义以及关系和约束定义。  
  
 当以 XML 数据形式编写 <xref:System.Data.DataSet> 时，<xref:System.Data.DataSet> 中的行将以它们的当前版本编写。 不过，也可以用 DiffGram 形式编写 <xref:System.Data.DataSet>，从而使行的当前值和原始值都将包含在内。  
  
 XML 表示形式<xref:System.Data.DataSet>可以写入到文件、 流， **XmlWriter**，或字符串。 这些选择在如何传输 <xref:System.Data.DataSet> 的 XML 表示形式方面提供了很大的灵活性。 若要获取的 XML 表示形式<xref:System.Data.DataSet>作为一个字符串，使用**GetXml**方法，如以下示例所示。  
  
```vb  
Dim xmlDS As String = custDS.GetXml()  
```  
  
```csharp  
string xmlDS = custDS.GetXml();  
```  
  
 **GetXml**返回的 XML 表示形式<xref:System.Data.DataSet>不包含架构信息。 若要从架构信息写入<xref:System.Data.DataSet>（作为 XML 架构） 到一个字符串，使用**GetXmlSchema**。  
  
 若要编写<xref:System.Data.DataSet>到一个文件流，或**XmlWriter**，使用**WriteXml**方法。 第一个参数传递给**WriteXml**目标的 XML 输出。 例如，传递包含文件名的字符串**System.IO.TextWriter**对象，依次类推。 可以传递另一个可选参数**XmlWriteMode**来指定要写入的 XML 输出的方式。  
  
 下表显示的选项**XmlWriteMode**。  
  
|XmlWriteMode 选项|描述|  
|-------------------------|-----------------|  
|**IgnoreSchema**|以 XML 数据形式编写 <xref:System.Data.DataSet> 的当前内容，不包含 XML 架构。 这是默认设置。|  
|**WriteSchema**|以 XML 数据形式编写 <xref:System.Data.DataSet> 的当前内容，以关系结构作为内联 XML 架构。|  
|**DiffGram**|以 DiffGram 形式编写整个 <xref:System.Data.DataSet>，包括原始值和当前值。 有关详细信息，请参阅[Diffgram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)。|  
  
 当编写的 XML 表示形式<xref:System.Data.DataSet>，其中包含**DataRelation**对象，您很可能希望生成的 XML 将每个关系嵌套在它们相关的父元素的子行。 若要完成此操作，设置**嵌套**的属性**DataRelation**到**true**添加时**DataRelation**到<xref:System.Data.DataSet>. 有关详细信息，请参阅[嵌套 Datarelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)。  
  
 下面是两个有关如何将 <xref:System.Data.DataSet> 的 XML 表示形式写入文件的示例。 第一个示例将生成的 XML 的文件名称的字符串作为传递**WriteXml**。 第二个示例传递**System.IO.StreamWriter**对象。  
  
```vb  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema)  
```  
  
```csharp  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema);  
```  
  
```vb  
Dim xmlSW As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xml")  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema)  
xmlSW.Close()  
```  
  
```csharp  
System.IO.StreamWriter xmlSW = new System.IO.StreamWriter("Customers.xml");  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema);  
xmlSW.Close();  
```  
  
## <a name="mapping-columns-to-xml-elements-attributes-and-text"></a>将列映射到 XML 元素、属性和文本  
 您可以指定如何在 XML 中表示表的列使用**ColumnMapping**的属性**DataColumn**对象。 下表显示了不同**MappingType**值为**ColumnMapping**的表列和生成的 XML 属性。  
  
|MappingType 值|描述|  
|-----------------------|-----------------|  
|**元素**|这是默认设置。 列以元素名称为 ColumnName 的 XML 元素形式编写，列的内容以元素文本形式编写。 例如：<br /><br /> `<ColumnName>Column Contents</ColumnName>`|  
|**特性**|对于属性名称为 ColumnName 的当前行，列以 XML 元素的 XML 属性形式编写，列的内容以属性值形式编写。 例如：<br /><br /> `<RowElement ColumnName="Column Contents" />`|  
|**SimpleContent**|列的内容以 XML 元素中当前行文本的形式编写。 例如：<br /><br /> `<RowElement>Column Contents</RowElement>`<br /><br /> 请注意， **SimpleContent**不能设置为具有表的列**元素**列或嵌套的关系。|  
|**Hidden**|不在 XML 输出中编写该列。|  
  
## <a name="see-also"></a>请参阅
- [在数据集中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)
- [DiffGrams](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)
- [嵌套 DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)
- [以 XSD 的形式写入数据集构架信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-schema-information-as-xsd.md)
- [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
