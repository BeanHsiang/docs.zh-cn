---
title: 链接的查询的性能 (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: b2f1d715-8946-4dc0-8d56-fb3d1bba54a6
ms.openlocfilehash: e099d4d725a0603df61f5e308ce9897feec0af29
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54677312"
---
# <a name="performance-of-chained-queries-linq-to-xml-c"></a>链接的查询的性能 (LINQ to XML) (C#)
LINQ（以及 LINQ to XML）的一个最重要优点是，链接查询的执行性能与单个更大更复杂的查询一样好。  
  
 链接查询是一种将另一个查询作为其源的查询。 例如，在下面的简单代码中，`query2` 使用 `query1` 作为其源：  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child", 1),  
    new XElement("Child", 2),  
    new XElement("Child", 3),  
    new XElement("Child", 4)  
);  
  
var query1 = from x in root.Elements("Child")  
             where (int)x >= 3  
             select x;  
  
var query2 = from e in query1  
             where (int)e % 2 == 0  
             select e;  
  
foreach (var i in query2)  
    Console.WriteLine("{0}", (int)i);  
```  
  
 该示例产生下面的输出：  
  
```  
4  
```  
  
 此链接查询提供与循环访问链接列表相同的性能配置文件。  
  
-   <xref:System.Xml.Linq.XContainer.Elements%2A> 轴具有与循环访问链接列表基本相同的性能。 <xref:System.Xml.Linq.XContainer.Elements%2A> 作为具有延迟执行功能的迭代器实现。 这意味着它除了循环访问链接列表外还执行一些操作，例如分配迭代器对象和跟踪执行状态。 此项工作可以分为两类：设置迭代器时完成的工作和每次迭代过程中完成的工作。 设置工作是固定的少量工作，而每次迭代过程中完成的工作与源集合中的项数成正比。  
  
-   在 `query1` 中，`where` 子句将使查询调用 <xref:System.Linq.Enumerable.Where%2A> 方法。 此方法也作为迭代器实现。 设置工作包括实例化将引用 lambda 表达式的委托和对迭代器的常规设置。 每次迭代时，都将调用该委托以执行谓词。 设置工作和每次迭代过程中完成的工作类似于循环访问轴期间完成的工作。  
  
-   在 `query1` 中，select 子句将使查询调用 <xref:System.Linq.Enumerable.Select%2A> 方法。 此方法与 <xref:System.Linq.Enumerable.Where%2A> 方法具有相同的性能配置文件。  
  
-   `query2` 中的 `where` 子句和 `select` 子句与 `query1` 中的相应语句具有相同的性能配置文件。  
  
 因此，通过 `query2` 执行的迭代与第一个查询源中的项数（即，线形时间）成正比。 相应的 Visual Basic 示例将具有相同的性能配置文件。  
  
 有关迭代器的详细信息，请参阅 [yield](../../../../csharp/language-reference/keywords/yield.md)。  
  
 有关将查询链接在一起的更详细教程，请参阅[教程：将查询链接在一起](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)。  
  
## <a name="see-also"></a>请参阅

- [性能 (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/performance-linq-to-xml.md)
