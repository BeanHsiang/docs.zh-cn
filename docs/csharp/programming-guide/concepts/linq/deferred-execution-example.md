---
title: 延迟执行示例 (C#)
ms.date: 07/20/2015
ms.assetid: 50f4fbac-81fe-4f26-aedf-506e21419b19
ms.openlocfilehash: 9697f3e4c120c7d8bc184181ad99df08634e791e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54598875"
---
# <a name="deferred-execution-example-c"></a>延迟执行示例 (C#)
本主题演示延迟执行和迟缓计算如何影响 LINQ to XML 查询的执行。  
  
## <a name="example"></a>示例  
 下面的示例演示使用采用延迟执行的扩展方法时的执行顺序。 此示例声明一个由三个字符串组成的数组。 然后，循环访问 `ConvertCollectionToUpperCase` 所返回的集合。  
  
```csharp  
public static class LocalExtensions  
{  
    public static IEnumerable<string>  
      ConvertCollectionToUpperCase(this IEnumerable<string> source)  
    {  
        foreach (string str in source)  
        {  
            Console.WriteLine("ToUpper: source {0}", str);  
            yield return str.ToUpper();  
        }  
    }  
}  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        string[] stringArray = { "abc", "def", "ghi" };  
  
        var q = from str in stringArray.ConvertCollectionToUpperCase()  
                select str;  
  
        foreach (string str in q)  
            Console.WriteLine("Main: str {0}", str);  
    }  
}  
```  
  
 该示例产生下面的输出：  
  
```  
ToUpper: source abc  
Main: str ABC  
ToUpper: source def  
Main: str DEF  
ToUpper: source ghi  
Main: str GHI  
```  
  
 请注意，在循环访问 `ConvertCollectionToUpperCase` 所返回的集合时，每一项都从源字符串数组检索，并且在源字符串数组中检索下一项之前，被转换为大写形式。  
  
 可以看到，在 `foreach` 的 `Main` 循环中处理所返回集合的每一项之后，字符串数组才会完全转换为大写形式。  
  
 本教程下一主题演示如何将查询链接到一起：  
  
-   [链接查询示例 (C#)](../../../../csharp/programming-guide/concepts/linq/chaining-queries-example.md)  
  
## <a name="see-also"></a>请参阅

- [教程：将查询链接在一起 (C#)](../../../../csharp/programming-guide/concepts/linq/tutorial-chaining-queries-together.md)
