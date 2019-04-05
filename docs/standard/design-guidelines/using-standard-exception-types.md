---
title: 使用标准异常类型
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- throwing exceptions, standard types
- catching exceptions
- exceptions, catching
- exceptions, throwing
ms.assetid: ab22ce03-78f9-4dca-8824-c7ed3bdccc27
author: KrzysztofCwalina
ms.openlocfilehash: b947c7cce057c060b1ab5054d1227f5703ccbf89
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54543901"
---
# <a name="using-standard-exception-types"></a>使用标准异常类型
本部分介绍 Framework 提供的标准异常及其用法的详细信息。 该列表并非详尽无遗。 有关其他 Framework 异常类型的用法，请参阅 .NET Framework 参考文档。  
  
## <a name="exception-and-systemexception"></a>Exception 和 SystemException  
 **X DO NOT** 引发<xref:System.Exception?displayProperty=nameWithType>或<xref:System.SystemException?displayProperty=nameWithType>。  
  
 **X DO NOT** 捕获`System.Exception`或`System.SystemException`在 framework 代码中，除非您想要重新引发。  
  
 **X AVOID** 捕捉`System.Exception`或`System.SystemException`，除非在顶级异常处理程序。  
  
## <a name="applicationexception"></a>ApplicationException  
 **X DO NOT** 引发或从其派生<xref:System.ApplicationException>。  
  
## <a name="invalidoperationexception"></a>InvalidOperationException  
 **✓ DO** 引发<xref:System.InvalidOperationException>如果此对象处于不合适的状态。  
  
## <a name="argumentexception-argumentnullexception-and-argumentoutofrangeexception"></a>ArgumentException、ArgumentNullException 和 ArgumentOutOfRangeException  
 **✓ DO** 引发<xref:System.ArgumentException>或如果错误的自变量传递给成员及其子类型之一。 如果适用，倾向于使用的派生程度最高的异常类型。  
  
 **✓ DO** 设置`ParamName`属性时引发的子类之一`ArgumentException`。  
  
 此属性表示引发异常的参数的名称。 请注意，可以使用一个构造函数重载来设置该属性。  
  
 **✓ DO** 使用`value`属性 setter 的隐式值参数的名称。  
  
## <a name="nullreferenceexception-indexoutofrangeexception-and-accessviolationexception"></a>NullReferenceException、IndexOutOfRangeException 和 AccessViolationException  
 **X DO NOT** 允许公开可调用 Api 显式或隐式引发<xref:System.NullReferenceException>， <xref:System.AccessViolationException>，或<xref:System.IndexOutOfRangeException>。 这些例外情况是保留和引发的执行引擎和在大多数情况下指示 bug。  
  
 应检查参数以避免引发这些异常。 引发这些异常会暴露方法的实现细节，这些细节可能会随着时间而改变。  
  
## <a name="stackoverflowexception"></a>StackOverflowException  
 **X DO NOT** 显式引发<xref:System.StackOverflowException>。 应仅由 CLR 显式引发异常。  
  
 **X DO NOT** 捕获`StackOverflowException`。  
  
 在存在任意堆栈溢出的情况下编写保持一致的托管代码几乎是不可能的。 通过使用探测功能将堆栈溢出移动到明确定义的位置而不是从任意堆栈溢出中退出，CLR 的非托管部分可以保持一致。  
  
## <a name="outofmemoryexception"></a>OutOfMemoryException  
 **X DO NOT** 显式引发<xref:System.OutOfMemoryException>。 将仅由 CLR 基础结构引发此异常。  
  
## <a name="comexception-sehexception-and-executionengineexception"></a>ComException、SEHException 和 ExecutionEngineException  
 **X DO NOT** 显式引发<xref:System.Runtime.InteropServices.COMException>， <xref:System.ExecutionEngineException>，和<xref:System.Runtime.InteropServices.SEHException>。 这些异常将仅由 CLR 基础结构引发。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [异常的设计准则](../../../docs/standard/design-guidelines/exceptions.md)
