---
title: 向 XML 树添加元素、属性和节点 (C#)
ms.date: 07/20/2015
ms.assetid: db911e4f-40aa-499a-9500-a9763bb6df56
ms.openlocfilehash: 87b63df1011af9594ff44bed6385f9d82dee08a2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54585872"
---
# <a name="adding-elements-attributes-and-nodes-to-an-xml-tree-c"></a>向 XML 树添加元素、属性和节点 (C#)
可以向现有的 XML 树中添加内容（包括元素、属性、注释、处理指令、文本和 CDATA）。  
  
## <a name="methods-for-adding-content"></a>添加内容的方法  
 下面的方法将子内容添加到 <xref:System.Xml.Linq.XElement> 或 <xref:System.Xml.Linq.XDocument> 中：  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Add%2A>|在 <xref:System.Xml.Linq.XContainer> 的子内容的末尾添加内容。|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A>|在 <xref:System.Xml.Linq.XContainer> 的子内容的开头添加内容。|  
  
 下面的方法将内容添加为 <xref:System.Xml.Linq.XNode> 的同级节点。 向其中添加同级内容的最常见的节点是 <xref:System.Xml.Linq.XElement>，不过你也可以将有效的同级内容添加到其他类型的节点，例如 <xref:System.Xml.Linq.XText> 或 <xref:System.Xml.Linq.XComment>。  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|在 <xref:System.Xml.Linq.XNode> 后面添加内容。|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|在 <xref:System.Xml.Linq.XNode> 前面添加内容。|  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 下面的示例创建两个 XML 树，然后修改其中一个树。  
  
### <a name="code"></a>代码  
  
```csharp  
XElement srcTree = new XElement("Root",   
    new XElement("Element1", 1),  
    new XElement("Element2", 2),  
    new XElement("Element3", 3),  
    new XElement("Element4", 4),  
    new XElement("Element5", 5)  
);  
XElement xmlTree = new XElement("Root",  
    new XElement("Child1", 1),  
    new XElement("Child2", 2),  
    new XElement("Child3", 3),  
    new XElement("Child4", 4),  
    new XElement("Child5", 5)  
);  
xmlTree.Add(new XElement("NewChild", "new content"));  
xmlTree.Add(  
    from el in srcTree.Elements()  
    where (int)el > 3  
    select el  
);  
// Even though Child9 does not exist in srcTree, the following statement will not  
// throw an exception, and nothing will be added to xmlTree.  
xmlTree.Add(srcTree.Element("Child9"));  
Console.WriteLine(xmlTree);  
```  
  
### <a name="comments"></a>注释  
 此代码生成以下输出：  
  
```xml  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
  <Child4>4</Child4>  
  <Child5>5</Child5>  
  <NewChild>new content</NewChild>  
  <Element4>4</Element4>  
  <Element5>5</Element5>  
</Root>  
```  
  
## <a name="see-also"></a>请参阅

- [修改 XML 树 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
