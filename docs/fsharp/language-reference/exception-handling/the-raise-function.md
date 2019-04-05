---
title: 异常：raise 函数
description: 了解如何F#raise 函数用来指示已发生的错误或异常情况。
ms.date: 05/16/2016
ms.openlocfilehash: 87773ead7773c62a325c7e7ff105c729e10dd69c
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610146"
---
# <a name="exceptions-the-raise-function"></a>异常：raise 函数

`raise`函数用来指示已发生的错误或异常情况。 异常对象中捕获有关错误的信息。

## <a name="syntax"></a>语法

```fsharp
raise (expression)
```

## <a name="remarks"></a>备注

`raise`函数生成的异常对象，并启动堆栈展开过程。 在堆栈展开过程由公共语言运行时 (CLR) 管理，因此与任何其他.NET 语言在此过程的行为都将是相同。 在堆栈展开过程是一个搜索匹配生成的异常的异常处理程序。 在当前开始搜索`try...with`表达式，如果有的话。 在每个模式`with`按顺序块检查。 当找到匹配的异常处理程序时，异常将被视为已处理。否则，堆栈的展开和`with`直到找到匹配的处理程序，则检查调用链的块。 任何`finally`当堆栈展开，按顺序还执行调用链中遇到的块。

`raise`函数等同于`throw`C# 或 c + +。 使用`reraise`传播调用链相同的异常的 catch 处理程序中。

下面的代码示例说明如何使用`raise`函数生成异常。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5801.fs)]

`raise`函数还可用来引发.NET 异常，如下面的示例中所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5802.fs)]

## <a name="see-also"></a>请参阅

- [异常处理](index.md)
- [异常类型](exception-types.md)
- [异常：`try...with`表达式](the-try-with-expression.md)
- [异常：`try...finally`表达式](the-try-finally-expression.md)
- [异常：`failwith`函数](the-failwith-function.md)
- [异常：`invalidArg`函数](the-invalidArg-function.md)