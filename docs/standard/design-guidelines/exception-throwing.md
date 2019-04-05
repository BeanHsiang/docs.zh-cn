---
title: 引发异常
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- exceptions, throwing
- explicitly throwing exceptions
- throwing exceptions, design guidelines
ms.assetid: 5388e02b-52f5-460e-a2b5-eeafe60eeebe
author: KrzysztofCwalina
ms.openlocfilehash: 74eee418a3c87b335cdf96557c4e17b95aff7b58
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54562877"
---
# <a name="exception-throwing"></a>引发异常
本部分介绍的异常引发准则要求对执行失败的含义进行明确定义。 只要成员无法执行其指定操作（成员名称所体现的含义），就会导致执行失败。 例如，如果 `OpenFile` 方法无法将打开的文件句柄返回给调用方，则视为执行失败。  
  
 大多数开发人员已经习惯使用异常来处理用法错误，例如除零或空引用。 在 Framework 中，异常用于所有错误条件，包括执行错误。  
  
 **X DO NOT** 返回错误代码。  
  
 异常是框架中报告错误的主要方式。  
  
 **✓ DO** 引发异常来报告执行失败数。  
  
 **✓ CONSIDER** 通过调用来终止进程`System.Environment.FailFast`（.NET Framework 2.0 功能） 而不是引发异常，如果你的代码遇到进一步执行不安全的情况。  
  
 **X DO NOT** 正常流控制，如有可能使用异常。  
  
 除系统故障和存在潜在争用条件的操作这两种情况外，框架设计者应设计 API，以便用户可以编写不会引发异常的代码。 例如，可以提供在调用成员之前检查前提条件的方法，以便用户可以编写不会引发异常的代码。  
  
 用于检查另一个成员的前提条件的成员通常被称为 tester（测试者），实际执行该工作的成员称为 doer（实施者）。  
  
 有些情况下，Tester-Doer 模式可能会产生不可接受的性能开销。 在这种情况下，应考虑使用所谓的 Try-Parse 模式（有关详细信息，请参阅[异常和性能](../../../docs/standard/design-guidelines/exceptions-and-performance.md)）。  
  
 **✓ CONSIDER** 引发异常的性能影响。 Throw 速率大于每秒 100 会显著影响大多数应用程序的性能。  
  
 **✓ DO** 由于的成员冲突而引发的公开可调用的成员的所有异常协定 （而不是系统故障），并将它们视为协定的一部分的文档。  
  
 作为协定一部分的异常在协定的不同版本中应保持一致（即，不应更改异常类型，并且不应添加新的异常）。  
  
 **X DO NOT** 具有或不会引发的公共成员根据某些选项。  
  
 **X DO NOT** 具有作为返回值返回异常的公共成员或`out`参数。  
  
 如果选择从公共 API 返回异常而不是引发它们，会丧失基于异常的错误报告的优势。  
  
 **✓ CONSIDER** 使用异常生成器方法。  
  
 从不同位置引发相同的异常是很常见的。 为避免代码膨胀，请使用可创建异常并初始化其属性的辅助方法。  
  
 此外，引发异常的成员不会被内联。 或可通过将引发语句移动到生成器内来实现成员内联。  
  
 **X DO NOT** 异常筛选器块中引发异常。  
  
 当异常筛选器引发异常时，CLR 会捕获该异常，筛选器会返回 false。 此行为与执行并显式返回 false 的过滤器行为无法区分，因此很难进行调试。  
  
 **X AVOID** 显式引发 finally 块中的异常。 隐式引发的异常导致的调用引发的方法是可接受的。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [异常的设计准则](../../../docs/standard/design-guidelines/exceptions.md)
