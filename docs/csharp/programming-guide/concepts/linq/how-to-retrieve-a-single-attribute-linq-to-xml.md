---
title: 如何：检索单个特性 (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: 1b6b07b9-933f-47e9-874e-e790cab49dc5
ms.openlocfilehash: 2bf42333d7a0b3e34cc0a636b68659b8c45d1d83
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54738178"
---
# <a name="how-to-retrieve-a-single-attribute-linq-to-xml-c"></a>如何：检索单个特性 (LINQ to XML) (C#)
本主题说明在给定属性名称的情况下，如何检索元素的单个属性。 这对于编写查询表达式查找具有特定属性的元素十分有用。  
  
 <xref:System.Xml.Linq.XElement.Attribute%2A> 类的 <xref:System.Xml.Linq.XElement> 方法返回具有指定名称的 <xref:System.Xml.Linq.XAttribute>。  
  
## <a name="example"></a>示例  
 下面的示例使用 <xref:System.Xml.Linq.XElement.Attribute%2A> 方法。  
  
```csharp  
XElement cust = new XElement("PhoneNumbers",  
    new XElement("Phone",  
        new XAttribute("type", "home"),  
        "555-555-5555"),  
    new XElement("Phone",  
        new XAttribute("type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =  
    from el in cust.Descendants("Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute("type"));  
```  
  
 本示例首先在名为 `Phone` 的树中查找所有后代，然后查找名为 `type` 的属性。  
  
 此代码生成以下输出：  
  
```  
home  
work  
```  
  
## <a name="example"></a>示例  
 如果希望检索属性的值，可以强制转换该值，就像使用 <xref:System.Xml.Linq.XElement> 对象时一样。 下面的示例演示这一操作。  
  
```csharp  
XElement cust = new XElement("PhoneNumbers",  
    new XElement("Phone",  
        new XAttribute("type", "home"),  
        "555-555-5555"),  
    new XElement("Phone",  
        new XAttribute("type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =   
    from el in cust.Descendants("Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute("type"));  
```  
  
 此代码生成以下输出：  
  
```  
home  
work  
```  
  
 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 为 <xref:System.Xml.Linq.XAttribute> 类提供了以下类型的显式强制转换运算符：`string`、`bool`、`bool?`、`int`、`int?`、`uint`、`uint?`、`long`、`long?`、`ulong`、`ulong?`、`float`、`float?`、`double`、`double?`、`decimal`、`decimal?`、`DateTime`、`DateTime?`、`TimeSpan`、`TimeSpan?`、`GUID` 和 `GUID?`。  
  
## <a name="example"></a>示例  
 下面的示例显式命名空间中的属性的相同代码。 有关详细信息，请参阅[使用 XML 命名空间 (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md)。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement cust = new XElement(aw + "PhoneNumbers",  
    new XElement(aw + "Phone",  
        new XAttribute(aw + "type", "home"),  
        "555-555-5555"),  
    new XElement(aw + "Phone",  
        new XAttribute(aw + "type", "work"),  
        "555-555-6666")  
);  
IEnumerable<XElement> elList =  
    from el in cust.Descendants(aw + "Phone")  
    select el;  
foreach (XElement el in elList)  
    Console.WriteLine((string)el.Attribute(aw + "type"));  
```  
  
 此代码生成以下输出：  
  
```  
home  
work  
```  
  
## <a name="see-also"></a>请参阅

- [LINQ to XML 轴 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)
