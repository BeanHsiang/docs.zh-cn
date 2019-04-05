---
title: 异常:try...finally 表达式
description: 了解如何F#try...最后表达式使您可以执行清理代码，即使代码块将引发异常。
ms.date: 05/16/2016
ms.openlocfilehash: 24613185818c8ea30b27dcf639b22af320c4b401
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53611615"
---
# <a name="exceptions-the-tryfinally-expression"></a>异常:try...finally 表达式

`try...finally`表达式使您可以执行清理代码，即使代码块将引发异常。

## <a name="syntax"></a>语法

```fsharp
try
    expression1
finally
    expression2
```

## <a name="remarks"></a>备注

`try...finally`表达式可用于执行中的代码*expression2*在上述语法而不考虑是否在执行期间生成异常*expression1*。

类型*expression2*不计入整个表达式; 的值不会发生异常时返回的类型是中的最后一个值*expression1*。 当发生了异常时，不返回任何值和控制流将传输到下一步的匹配异常处理程序在调用堆栈上。 如果不找到任何异常处理程序，则该程序将终止。 执行匹配的处理程序中的代码或程序终止中的代码之前`finally`执行分支。

下面的代码演示如何使用`try...finally`表达式。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5701.fs)]

向控制台输出如下所示。

```
Closing stream
Exception handled.
```

您可以看到输出中，在流关闭之前处理外部异常，和文件`test.txt`包含的文本`test1`，指示已刷新缓冲区，并已将其写入到磁盘，即使该异常将传输控制对外部异常处理程序。

请注意，`try...with`构造是一个单独的构造，从`try...finally`构造。 因此，如果你的代码需要两`with`块和一个`finally`块中，您必须将嵌套的两个构造，如以下代码示例所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5702.fs)]

在上下文中计算表达式，包括序列表达式和异步工作流**try...最后**表达式可能具有的自定义实现。 有关详细信息，请参阅[计算表达式](../computation-expressions.md)。

## <a name="see-also"></a>请参阅

- [异常处理](index.md)
- [异常：`try...with`表达式](the-try-with-expression.md)