---
title: 内存中 XML 数据处理
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1bbb4d05-ead7-4bda-8ece-f86d35c57ad4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f1a4587838180896b52bb79d447ed7ede3e22d1a
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56836482"
---
# <a name="processing-xml-data-in-memory"></a>内存中 XML 数据处理
Microsoft .NET Framework 包括三种用于处理 XML 数据的模型：<xref:System.Xml.XmlDocument> 类、<xref:System.Xml.XPath.XPathDocument> 类，以及 [LINQ to XML (C#)](../../../csharp/programming-guide/concepts/linq/linq-to-xml.md) 和 [LINQ to XML (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)。  
  
 <xref:System.Xml.XmlDocument> 类实现 W3C 文档对象模型 (DOM) 级别 1 核心和 DOM 级别 2 核心建议。 DOM 是 XML 文档的内存中（缓存）树表示形式。 使用 <xref:System.Xml.XmlDocument> 及其相关的类，可以构造 XML 文档、加载和访问数据、修改数据以及保存更改。  
  
 <xref:System.Xml.XPath.XPathDocument> 类是基于 XPath 数据模型的只读的、内存中的数据存储区。 <xref:System.Xml.XPath.XPathNavigator> 类使用 XML 文档的游标模型提供多种编辑选项和浏览功能，该模型包含在只读的 <xref:System.Xml.XPath.XPathDocument> 类以及 <xref:System.Xml.XmlDocument> 类中。  
  
 [LINQ to XML](../../../csharp/programming-guide/concepts/linq/linq-to-xml.md) 是.NET Framework 3.5 版中引入的用于处理 XML 数据的模型。 这是利用[语言集成查询 (LINQ)](../../../csharp/programming-guide/concepts/linq/index.md) 的内存中模型。 LINQ 扩展 C# 和 Visual Basic 的语言语法以提供新的查询功能。  
  
## <a name="in-this-section"></a>本节内容  
 [使用 DOM 模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)  
 讨论如何使用 <xref:System.Xml.XmlDocument> 及其相关的类来处理 XML 数据。  
  
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
 讨论如何使用 <xref:System.Xml.XPath.XPathDocument>、<xref:System.Xml.XmlDocument> 和 <xref:System.Xml.XPath.XPathNavigator> 类来处理 XML 数据。  
  
 [使用 LINQ to XML 处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-linq-to-xml.md)  
 简要概述 LINQ to XML 并提供到 LINQ to XML 文档的链接。  
  
## <a name="related-sections"></a>相关章节  
 [XML 文档和数据](../../../../docs/standard/data/xml/index.md)
