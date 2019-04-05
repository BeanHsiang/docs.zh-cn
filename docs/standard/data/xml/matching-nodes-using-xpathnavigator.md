---
title: 使用 XPathNavigator 匹配节点
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: e6848c47-ee5d-401a-89a5-50b5eed40f30
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 525c8332d2884415ccf883dae03866776510f354
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54680399"
---
# <a name="matching-nodes-using-xpathnavigator"></a>使用 XPathNavigator 匹配节点
<xref:System.Xml.XPath.XPathNavigator> 类提供了 <xref:System.Xml.XPath.XPathNavigator.Matches%2A> 方法来确定节点是否与 XPath 表达式匹配。 <xref:System.Xml.XPath.XPathNavigator.Matches%2A> 方法使用 XPath 表达式作为输入并返回一个 <xref:System.Boolean>，指示当前节点是否与给定的 XPath 表达式或给定的已编译 <xref:System.Xml.XPath.XPathExpression> 对象匹配。  
  
## <a name="matching-nodes"></a>匹配节点  
 如果当前节点与指定的 XPath 表达式匹配，<xref:System.Xml.XPath.XPathNavigator.Matches%2A> 方法将返回 `true`。 例如，在以下代码示例中，如果当前节点为元素 <xref:System.Xml.XPath.XPathNavigator.Matches%2A>，并且元素 `true` 具有属性 `b`，`b` 方法将返回 `c`。  
  
> [!NOTE]
>  <xref:System.Xml.XPath.XPathNavigator.Matches%2A> 方法不会改变 <xref:System.Xml.XPath.XPathNavigator> 的状态。  
  
```vb  
Dim document as XPathDocument = New XPathDocument("input.xml")  
Dim navigator as XPathNavigator = document.CreateNavigator()  
  
navigator.Matches("b[@c]")  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
navigator.Matches("b[@c]");  
```  
  
## <a name="see-also"></a>请参阅

- <xref:System.Xml.XmlDocument>
- <xref:System.Xml.XPath.XPathDocument>
- <xref:System.Xml.XPath.XPathNavigator>
- [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)
- [使用 XPathNavigator 选择 XML 数据](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)
- [使用 XPathNavigator 计算 XPath 表达式](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)
- [XPath 查询识别的节点类型](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)
- [XPath 查询和命名空间](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)
- [已编译的 XPath 表达式](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
