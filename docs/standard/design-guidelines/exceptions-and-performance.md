---
title: 异常和性能
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- tester-doer pattern
- TryParse pattern
- exceptions, throwing
- exceptions, performance
- throwing exceptions, performance
ms.assetid: 3ad6aad9-08e6-4232-b336-0e301f2493e6
author: KrzysztofCwalina
ms.openlocfilehash: f9fe3045d8bd8b4d625c5cd49bc18574ebb740de
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54707721"
---
# <a name="exceptions-and-performance"></a>异常和性能
一个常见的与异常相关的问题是，如果异常用于通常会失败的代码，则实现的性能将变得不可接受。 这确实是一个问题。 当成员引发异常时，其性能可能会慢几个数量级。 但是，在严格遵守禁止使用错误代码的异常准则的同时，仍可能实现良好的性能。 本部分中描述了两种建议的模式。  
  
 **X DO NOT** 由于异常可能会对性能产生负面影响的问题，因此使用错误代码。  
  
 为了提高性能，可以使用 Tester-Doer 模式或 Try-Parse 模式，如以下两部分所述。  
  
## <a name="tester-doer-pattern"></a>Tester-Doer 模式  
 有时，通过将成员分成两部分，可以改善异常引发成员的性能。 让我们来了解一下 <xref:System.Collections.Generic.ICollection%601> 接口的 <xref:System.Collections.Generic.ICollection%601.Add%2A> 方法。  
  
```  
ICollection<int> numbers = ...   
numbers.Add(1);  
```  
  
 如果集合是只读的，则 `Add` 方法会引发异常。 在通常预期方法调用会失败的情况下，这可能会导致性能问题。 优化此问题的方法之一是在尝试添加值之前测试集合是否可写。  
  
```  
ICollection<int> numbers = ...   
...  
if(!numbers.IsReadOnly){  
    numbers.Add(1);  
}  
```  
  
 用于测试条件的成员（在我们的示例中是属性 `IsReadOnly` ）被称为 tester。 用于执行潜在引发操作的成员（在我们的示例中为 `Add` 方法）称为doer。  
  
 **✓ CONSIDER** 可能会引发异常的成员 Tester-doer 模式在常见方案以避免性能问题与异常相关。  
  
## <a name="try-parse-pattern"></a>Try-Parse 模式  
 对于性能极其敏感的 API，应使用比上一部分中介绍的 Tester-Doer 模式更快的模式。 该模式要求调整成员名称，以使明确定义的测试用例成为成员语义的一部分。 例如，<xref:System.DateTime> 定义了一个 <xref:System.DateTime.Parse%2A> 方法，如果解析字符串失败，则该方法会引发异常。 它还定义了一个相应的尝试进行解析的 <xref:System.DateTime.TryParse%2A> 方法，如果解析不成功则返回 false，并使用 `out` 参数返回成功解析的结果。  
  
```  
public struct DateTime {  
    public static DateTime Parse(string dateTime){   
        ...   
    }  
    public static bool TryParse(string dateTime, out DateTime result){  
        ...  
    }  
}  
```  
  
 使用此模式时，务必要严格定义 try 功能。 如果在已妥善定义 try 的情况下，成员仍因某个原因失败，则该成员仍必须引发相应异常。  
  
 **✓ CONSIDER** 可能会引发异常的成员尝试分析模式在常见方案以避免性能问题与异常相关。  
  
 **✓ DO** 方法实现此模式中使用前缀"Try"和布尔值返回的类型。  
  
 **✓ DO** 每个成员使用 Try 分析模式提供的异常引发的成员。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [异常的设计准则](../../../docs/standard/design-guidelines/exceptions.md)
