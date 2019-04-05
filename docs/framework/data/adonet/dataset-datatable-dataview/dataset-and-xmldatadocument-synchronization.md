---
title: 数据集和 XmlDataDocument 同步
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0ce3793d-54b2-47e4-8cf7-b0591cc4dd21
ms.openlocfilehash: 5360a7bce1b5470271bc6b512484964ebb9fd8d1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54587773"
---
# <a name="dataset-and-xmldatadocument-synchronization"></a>数据集和 XmlDataDocument 同步
ADO.NET <xref:System.Data.DataSet> 为您提供了数据的关系表示形式。 若要实现分层数据访问，可以使用 .NET Framework 中的可用 XML 类。 以前，数据的这两种表示形式是单独使用的。 但是，.NET Framework 可以实时、 同步访问通过对数据的关系和层次结构表示**数据集**对象和<xref:System.Xml.XmlDataDocument>对象，分别。  
  
 当**数据集**与同步**XmlDataDocument**，这两个对象都使用一组数据。 这意味着，如果对更改**数据集**，更改将反映在**XmlDataDocument**，反之亦然。 之间的关系**数据集**并**XmlDataDocument**创建单个应用程序，使用一组数据，若要访问生成的服务的完整套件，从而极大的灵活性围绕**数据集**（如 Web 窗体和 Windows 窗体控件和 Visual Studio.NET 设计器），以及包含可扩展样式表语言 (XSL)、 XSL 转换 (XSLT) 和 XML 路径的 XML 服务套件语言 (XPath)。 您不必选择使应用程序以哪一组服务为目标，这两组服务都可用。  
  
 有几种方法可以同步**数据集**与**XmlDataDocument**。 你可以：  
  
-   填充**数据集**使用架构 （即关系结构） 和数据，然后将其同步与新**XmlDataDocument**。 这将提供现有关系数据的分层视图。 例如：  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema and data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema and data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    ```  
  
-   填充**数据集**仅具有架构 (如强类型化**数据集**)，使其与同步**XmlDataDocument**，然后加载**XmlDataDocument**从 XML 文档。 这将提供现有分层数据的关系视图。 表名和列名中的您**数据集**架构必须匹配要与其同步的 XML 元素的名称。 该匹配区分大小写。  
  
     请注意的架构**数据集**只需匹配要在关系视图中公开的 XML 元素。 这样，就可以具有非常大的 XML 文档，而该文档上可以有非常小的关系“窗口”。 **XmlDataDocument**即使保留整个 XML 文档**数据集**仅公开一小部分。 (此详细示例，请参阅[将数据集和 XmlDataDocument 同步](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/synchronizing-a-dataset-with-an-xmldatadocument.md)。)  
  
     下面的代码示例演示了创建的步骤**数据集**并填充其架构，然后同步其与**XmlDataDocument**。 请注意，**数据集**架构只需匹配的元素**XmlDataDocument**你想要公开使用**数据集**。  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema, but not data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema, but not data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
     无法加载**XmlDataDocument**如果与同步**数据集**，其中包含数据。 否则会引发异常。  
  
-   创建一个新**XmlDataDocument**并将其加载 XML 文档中，然后访问数据使用的关系视图**数据集**属性**XmlDataDocument**。 您需要设置的架构**数据集**才能查看中的数据的任何**XmlDataDocument**使用**数据集**。 中的表名称和列的名称，你**数据集**架构必须匹配要与其同步的 XML 元素的名称。 该匹配区分大小写。  
  
     下面的代码示例演示如何访问中的数据的关系视图**XmlDataDocument**。  
  
    ```vb  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument  
    Dim dataSet As DataSet = xmlDoc.DataSet  
  
    ' Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    XmlDataDocument xmlDoc = new XmlDataDocument();  
    DataSet dataSet = xmlDoc.DataSet;  
  
    // Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
 同步的另一个优点**XmlDataDocument**与**数据集**是保留的 XML 文档保真度。 如果**数据集**从 XML 文档中使用填充**ReadXml**，当将数据写回与 XML 文档使用**WriteXml**明显可能不同于原始 XML 文档。 这是因为**数据集**不维护格式设置，例如空格或层次结构的信息，如元素顺序，从 XML 文档。 **数据集**也不包含 XML 文档中的已忽略，因为它们不匹配的架构元素**数据集**。 同步**XmlDataDocument**与**数据集**允许要在中维护的原始 XML 文档的格式设置和分层元素结构**XmlDataDocument**，而**数据集**包含唯一的数据和架构信息适用于**数据集**。  
  
 同步时**数据集**与**XmlDataDocument**，结果可能会有具体取决于是否您<xref:System.Data.DataRelation>嵌套对象。 有关详细信息，请参阅[嵌套 Datarelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [将数据集与 XmlDataDocument 同步](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/synchronizing-a-dataset-with-an-xmldatadocument.md)  
 演示同步强类型化**数据集**，最小架构后，使用**XmlDataDocument**。  
  
 [对数据集执行 XPath 查询](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/performing-an-xpath-query-on-a-dataset.md)  
 演示的内容执行 XPath 查询**数据集**。  
  
 [将 XSLT 转换应用于 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/applying-an-xslt-transform-to-a-dataset.md)  
 演示如何将 XSLT 转换应用到的内容**数据集**。  
  
## <a name="related-sections"></a>相关章节  
 [在数据集中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 介绍如何**数据集**作为数据源，包括加载和保持的内容与 XML 进行交互**数据集**作为 XML 数据。  
  
 [嵌套 DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)  
 讨论的重要性嵌套**DataRelation**对象表示的内容时**数据集**为 XML 数据，并介绍了如何创建这些关系。  
  
 [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 介绍**数据集**以及如何使用它来管理应用程序数据并与数据源包括关系数据库和 XML 进行交互。  
  
 <xref:System.Xml.XmlDataDocument>  
 参考信息包含有关**XmlDataDocument**类。  
  
## <a name="see-also"></a>请参阅
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
