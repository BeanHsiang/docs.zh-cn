---
title: 接口中的索引器 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
ms.openlocfilehash: c56369b28f8e1bab1ca8e8c13ebd9710c8f1d9fb
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57200099"
---
# <a name="indexers-in-interfaces-c-programming-guide"></a>接口中的索引器（C# 编程指南）
可以在[接口](../../../csharp/language-reference/keywords/interface.md)上声明索引器。 接口索引器的访问器与[类](../../../csharp/language-reference/keywords/class.md)索引器的访问器有所不同，差异如下：  
  
-   接口访问器不使用修饰符。  
  
-   接口访问器没有正文。  
  
 因此，访问器的用途是指示索引器为读写、只读还是只写。  
  
 下面是接口索引器访问器的示例：  
  
 [!code-csharp[csProgGuideIndexers#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#3)]  
  
 索引器的签名必须不同于同一接口中声明的所有其他索引器的签名。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现接口索引器。  
  
 [!code-csharp[csProgGuideIndexers#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#4)]  
  
 在前面的示例中，可通过使用接口成员的完全限定名来使用显示接口成员实现。 例如:  
  
```  
string ISomeInterface.this[int index]   
{   
}   
```  
  
 但仅当类采用相同的索引签名实现多个接口时，才需用到完全限定名称以避免歧义。 例如，如果 `Employee` 类正在实现接口 `ICitizen` 和接口 `IEmployee`，而这两个接口具有相同的索引签名，则需要用到显式接口成员实现。 即是说以下索引器声明：  
  
```  
string IEmployee.this[int index]   
{   
}   
```  
  
 在 `IEmployee` 接口中实现索引器，而以下声明：  
  
```  
string ICitizen.this[int index]
{   
}   
```  
  
 在 `ICitizen` 接口中实现索引器。  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [索引器](../../../csharp/programming-guide/indexers/index.md)
- [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)
- [接口](../../../csharp/programming-guide/interfaces/index.md)
