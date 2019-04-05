---
title: DiffGrams
ms.date: 03/30/2017
ms.assetid: 037f3991-7bbc-424b-b52e-8b03585d3e34
ms.openlocfilehash: 573da0b608b3f74b9cf789a27a10183f3320f908
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54513643"
---
# <a name="diffgrams"></a>DiffGrams
DiffGram 是用于标识数据元素的当前和原始版本的 XML 格式。 <xref:System.Data.DataSet> 使用 DiffGram 格式来加载和保持其内容，并将其内容序列化，以便通过网络连接来进行传输。 当<xref:System.Data.DataSet>编写为 DiffGram，若要精确地重新创建内容，但不架构的所有必要信息 DiffGram 填充它<xref:System.Data.DataSet>，包括从这两个列的值**原始**并**当前**行版本、 行错误信息以及行顺序。  
  
 当从 XML Web services 发送和检索 <xref:System.Data.DataSet> 时，将隐式地使用 DiffGram 格式。 此外，加载的内容时<xref:System.Data.DataSet>从 XML 使用**ReadXml**方法，或编写的内容时<xref:System.Data.DataSet>中使用 XML **WriteXml**方法，可以指定内容读取或写入作为 DiffGram。 有关详细信息，请参阅[从 XML 加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)并[写入数据集内容作为 XML 数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)。  
  
 虽然 DiffGram 格式主要由 .NET Framework 用作 <xref:System.Data.DataSet> 内容的序列化格式，但也可以使用 DiffGram 来修改 Microsoft SQL Server 数据库中表的数据。  
  
 通过写入到的所有表的内容生成 Diffgram  **\<diffgram >** 元素。  
  
### <a name="to-generate-a-diffgram"></a>生成 Diffgram  
  
1.  生成根表（即没有任何父级的表）的列表。  
  
2.  对于列表中每个表及其子代，在 Diffgram 的第一部分中写出所有行的当前版本。  
  
3.  对于每个表中<xref:System.Data.DataSet>，写出的所有行的原始版本，如果有，请在**\<之前 >** 在 diffgram 的部分。  
  
4.  对于有错误，行写入错误内容中**\<错误 >** 在 diffgram 的部分。  
  
 将按照从 XML 文件的开头到结尾的顺序处理 Diffgram。  
  
### <a name="to-process-a-diffgram"></a>处理 Diffgram  
  
1.  处理包含行当前版本的 Diffgram 的第一部分。  
  
2.  处理第二个或**\<之前 >** 节，其中包含原始行版本的修改和删除的行。  
  
    > [!NOTE]
    >  如果某行标记为已删除，则删除操作还可删除该行的子代，具体取决于当前 `Cascade` 的 <xref:System.Data.DataSet> 属性。  
  
3.  进程**\<错误 >** 部分。 为本部分中各项的指定行和列设置错误信息。  
  
> [!NOTE]
>  如果将 <xref:System.Data.XmlWriteMode> 设置为 Diffgram，则目标 <xref:System.Data.DataSet> 和原始 <xref:System.Data.DataSet> 的内容可能会不同。  
  
## <a name="diffgram-format"></a>DiffGram 格式  
 DiffGram 格式可分为三部分：当前数据、原始（或“before”）数据和错误部分，如下面的示例中所示。  
  
```xml  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  
   <DataInstance>  
   </DataInstance>  
  
  <diffgr:before>  
  </diffgr:before>  
  
  <diffgr:errors>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
 DiffGram 格式由以下数据块组成：  
  
 **\<**  ***DataInstance***  **>**  
 此元素的名称***DataInstance***，用于说明目的，本文档中。 一个***DataInstance***元素表示<xref:System.Data.DataSet>或行的<xref:System.Data.DataTable>。 而不是*DataInstance*，该元素所包含的名称<xref:System.Data.DataSet>或<xref:System.Data.DataTable>。 此 DiffGram 格式块包含当前数据（无论是否经过修改）。 使用标识的元素或已修改的行**diffgr: haschanges**批注。  
  
 **\<diffgr:before>**  
 此 DiffGram 格式块包含行的原始版本。 此块中的元素中的元素进行匹配***DataInstance***阻止使用**diffgr: id**批注。  
  
 **\<diffgr:errors>**  
 此 DiffGram 格式块包含中的特定行的错误信息***DataInstance***块。 此块中的元素中的元素进行匹配***DataInstance***阻止使用**diffgr: id**批注。  
  
## <a name="diffgram-annotations"></a>DiffGram 批注  
 DiffGram 使用一些批注来使来自不同 DiffGram 块的元素相关，这些块表示 <xref:System.Data.DataSet> 中的不同行版本或错误信息。  
  
 下表描述在 DiffGram 命名空间中定义的 DiffGram 批注**urn： 架构-microsoft-com:xml-diffgram-v1**。  
  
|批注|描述|  
|----------------|-----------------|  
|**id**|用于中的元素配对 **\<diffgr： 之前 >** 并 **\<diffgr:errors >** 块中的元素**\<*****DataInstance*** **>** 块。 使用值**diffgr: id**批注位于窗体 *[TableName] [RowIdentifier]*。 例如：`<Customers diffgr:id="Customers1">`。|  
|**parentId**|标识中的哪个元素**\<** ***DataInstance*** **>** 块是当前元素的父元素。 使用值**diffgr: parentid**批注位于窗体 *[TableName] [RowIdentifier]*。 例如：`<Orders diffgr:parentId="Customers1">`。|  
|**hasChanges**|中的行标识**\<** ***DataInstance*** **>** 阻止为已修改。 **HasChanges**批注可以具有以下两个值之一：<br /><br /> **inserted**<br /> 标识**Added**行。<br /><br /> **修改**<br /> 标识**Modified**包含行**原始**中的行版本 **\<diffgr： 之前 >** 块。 请注意， **Deleted**行将包含**原始**中的行版本 **\<diffgr： 之前 >** 块，但将存在中没有带批注的元素**\<**  ***DataInstance*** **>** 块。|  
|**hasErrors**|中的行标识**\<** ***DataInstance*** **>** 块**RowError**。 错误元素放置在 **\<diffgr:errors >** 块。|  
|**错误**|包含的文本**RowError**中的特定元素的 **\<diffgr:errors >** 块。|  
  
 当以 DiffGram 格式读写 <xref:System.Data.DataSet> 的内容时，还包含附加的批注。 下表描述了命名空间中定义这些其他批注**urn： 架构-microsoft-com:xml-msdata**。  
  
|批注|描述|  
|----------------|-----------------|  
|**RowOrder**|保留原始数据的行顺序并标识特定 <xref:System.Data.DataTable> 中行的索引。|  
|**Hidden**|标识为具有列**ColumnMapping**属性设置为**MappingType.Hidden**。 属性将写格式**msdata： 隐藏** *[ColumnName]*="*值*"。 例如：`<Customers diffgr:id="Customers1" msdata:hiddenContactTitle="Owner">`。<br /><br /> 请注意，只有当隐藏列包含数据时才以 DiffGram 属性的形式来编写隐藏列。 否则将忽略隐藏列。|  
  
## <a name="sample-diffgram"></a>DiffGram 示例  
 下面是 DiffGram 格式的示例。 该示例显示对表行的更新在提交更改之前的结果。 CustomerID 为“ALFKI”的行已被修改，但尚未更新。 因此，没有**当前**行**diffgr: id**为"Customers1"中**\<** ***DataInstance*** **>** 块中，和一个**原始**行**diffgr: id** "Customers1"的 **\<diffgr： 之前 >** 块。 Customerid 为"ANATR"的行包含**RowError**，因此它将批注`diffgr:hasErrors="true"`，并且没有一个相关的元素 **\<diffgr:errors >** 块。  
  
```xml  
<diffgr:diffgram xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
  <CustomerDataSet>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0" diffgr:hasChanges="modified">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>New Company</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers2" msdata:rowOrder="1" diffgram:hasErrors="true">  
      <CustomerID>ANATR</CustomerID>  
      <CompanyName>Ana Trujillo Emparedados y Helados</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers3" msdata:rowOrder="2">  
      <CustomerID>ANTON</CustomerID>  
      <CompanyName>Antonio Moreno Taquera</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers4" msdata:rowOrder="3">  
      <CustomerID>AROUT</CustomerID>  
      <CompanyName>Around the Horn</CompanyName>  
    </Customers>  
  </CustomerDataSet>  
  <diffgr:before>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>Alfreds Futterkiste</CompanyName>  
    </Customers>  
  </diffgr:before>  
  <diffgr:errors>  
    <Customers diffgr:id="Customers2" diffgr:Error="An optimistic concurrency violation has occurred for this row."/>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
## <a name="see-also"></a>请参阅
- [在数据集中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)
- [从 XML 加载数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)
- [以 XML 数据的形式编写数据集内容](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)
- [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
