---
title: 带 XML 声明的序列化 (C#)
ms.date: 07/20/2015
ms.assetid: c237fa4a-a042-40fd-886f-17b54c66bb75
ms.openlocfilehash: 4f5dd9a7e392acff30814db4a483b297494b68b1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54702400"
---
# <a name="serializing-with-an-xml-declaration-c"></a>带 XML 声明的序列化 (C#)
本主题说明如何控制序列化是否生成 XML 声明。  
  
## <a name="xml-declaration-generation"></a>XML 声明的生成  
 使用 <xref:System.IO.File> 方法或 <xref:System.IO.TextWriter> 方法序列化为 <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=nameWithType> 或 <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=nameWithType> 将生成 XML 声明。 在序列化为 <xref:System.Xml.XmlWriter> 时，编写器设置（在 <xref:System.Xml.XmlWriterSettings> 对象中指定）将确定是否生成 XML 声明。  
  
 如果要使用 `ToString` 方法序列化为字符串，则生成的 XML 不会包括 XML 声明。  
  
### <a name="serializing-with-an-xml-declaration"></a>使用 XML 声明进行序列化  
 下面的示例创建一个 <xref:System.Xml.Linq.XElement>，将文档保存到文件，然后将文件打印到控制台：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child", "child content")  
);  
root.Save("Root.xml");  
string str = File.ReadAllText("Root.xml");  
Console.WriteLine(str);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Child>child content</Child>  
</Root>  
```  
  
### <a name="serializing-without-an-xml-declaration"></a>不带 XML 声明的序列化  
 下面的示例演示如何将一个 <xref:System.Xml.Linq.XElement> 保存到一个 <xref:System.Xml.XmlWriter>。  
  
```csharp  
StringBuilder sb = new StringBuilder();  
XmlWriterSettings xws = new XmlWriterSettings();  
xws.OmitXmlDeclaration = true;  
  
using (XmlWriter xw = XmlWriter.Create(sb, xws)) {  
    XElement root = new XElement("Root",  
        new XElement("Child", "child content")  
    );  
    root.Save(xw);  
}  
Console.WriteLine(sb.ToString());  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root><Child>child content</Child></Root>  
```  
  
## <a name="see-also"></a>请参阅

- [序列化 XML 树 (C#)](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)
