---
title: 序列化包含 XElement 对象的对象图 (C#)
ms.date: 07/20/2015
ms.assetid: fcbc3951-3cc4-4d0f-9259-e97549ed68f0
ms.openlocfilehash: db7354598fc84c6fa3f8ec4e5b53799030459387
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54569136"
---
# <a name="serializing-object-graphs-that-contain-xelement-objects-c"></a>序列化包含 XElement 对象的对象图 (C#)
本主题介绍序列化对象图的功能，其中对象图包含对类型为 <xref:System.Xml.Linq.XElement> 的对象的引用。 为便于执行这种类型的序列化，<xref:System.Xml.Linq.XElement> 实现了 <xref:System.Xml.Serialization.IXmlSerializable> 接口。  
  
 请注意，只有 <xref:System.Xml.Linq.XElement> 类才实现序列化。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|说明|  
|-----------|-----------------|  
|[如何：使用 XmlSerializer (C#) 进行序列化](../../../../csharp/programming-guide/concepts/linq/how-to-serialize-using-xmlserializer.md)|演示如何使用 <xref:System.Xml.Serialization.XmlSerializer> 进行序列化。|  
|[如何：使用 DataContractSerializer 进行序列化 (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-serialize-using-datacontractserializer.md)|演示如何使用 <xref:System.Runtime.Serialization.DataContractSerializer> 进行序列化。|  
  
## <a name="see-also"></a>请参阅

- [高级 LINQ to XML 编程 (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)
