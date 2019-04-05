---
title: 资源管理：Use 关键字
description: 了解如何F#关键字 use 和 using 函数，可以控制的初始化和释放资源。
ms.date: 05/16/2016
ms.openlocfilehash: 127877a3823faade9bc3c6aefea655c86cc348e7
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613084"
---
# <a name="resource-management-the-use-keyword"></a>资源管理：Use 关键字

本主题介绍了关键字`use`和`using`函数，可以控制的初始化和释放资源。

## <a name="resources"></a>资源

术语*资源*以多种方式使用。 是的资源可以是应用程序使用，如字符串、 图形和类似的内容，但在此上下文中的数据*资源*指的是软件或操作系统资源，例如图形设备上下文、 文件句柄、 网络和数据库连接，如等待句柄等并发对象。 由应用程序的这些资源的使用涉及到操作系统或其他资源提供程序后, 跟资源的更高版本到池，以便它可以提供给另一个应用程序的资源的获取。 当应用程序不会释放资源恢复到公共池时，会出现问题。

## <a name="managing-resources"></a>管理资源

若要有效地和负责任地管理应用程序中的资源，你必须立即和可预测的方式释放资源。 .NET Framework 可帮助你执行此操作，从而`System.IDisposable`接口。 实现的类型`System.IDisposable`具有`System.IDisposable.Dispose`方法，可正确地释放资源。 编写良好的应用程序保证`System.IDisposable.Dispose`时不再需要保留有限的资源的任何对象，立即调用。 幸运的是，大多数.NET 语言提供支持，以简化此过程，并F#也不例外。 有两个有用的语言结构支持的释放模式：`use`绑定和`using`函数。

## <a name="use-binding"></a>使用绑定

`use`关键字具有类似的窗体`let`绑定：

使用*值* = *表达式*

它提供了相同的功能`let`绑定，但添加到调用`Dispose`值超出范围时的值。 请注意，编译器将插入 null 值，检查，因此，如果值为`null`，在调用`Dispose`未尝试。

下面的示例演示如何通过使用自动关闭文件`use`关键字。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6301.fs)]

> [!NOTE]
> 可以使用`use`在计算表达式中，在这种情况下的自定义的版本`use`使用表达式。 有关详细信息，请参阅[序列](sequences.md)，[异步工作流](asynchronous-workflows.md)，并[计算表达式](computation-expressions.md)。

## <a name="using-function"></a>使用函数

`using`函数具有以下形式：

`using` (*expression1*)*函数或 lambda*

在中`using`表达式中， *expression1*创建必须释放的对象。 结果*expression1* （必须释放的对象） 将成为自变量，*值*到*函数或 lambda*，它是需要将单个的任一函数剩余值相匹配的类型参数由*expression1*，或需要一个该类型的参数的 lambda 表达式。 在函数的执行结束时，运行时调用`Dispose`，并释放资源 (除非的值为`null`，在这种情况下不尝试对 Dispose 的调用)。

下面的示例演示`using`使用 lambda 表达式的表达式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6302.fs)]

下面的示例说明`using`的函数的表达式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6303.fs)]

请注意，该函数可以是具有已应用某些参数的函数。 下面的代码示例展示了此操作。 它将创建包含字符串的文件`XYZ`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6304.fs)]

`using`函数和`use`绑定是几乎等效方法来完成同样的操作。 `using`关键字提供了更好地控制何时`Dispose`调用。 当你使用`using`，`Dispose`在使用时调用的函数或 lambda 表达式，则末尾`use`关键字，`Dispose`包含代码块的结束时调用。 一般情况下，应优先使用`use`而不是`using`函数。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)