---
title: 异步工作流
description: 了解有关支持在F#编程语言以异步方式执行计算执行而不会阻止执行其他工作。
ms.date: 05/16/2016
ms.openlocfilehash: 7643a26469ee6a6cf15940f90611fd430beef42e
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610783"
---
# <a name="asynchronous-workflows"></a>异步工作流

> [!NOTE]
> API 参考链接将转至 MSDN。  Docs.microsoft.com API 参考尚未完成。

本主题介绍中的支持F#用于以异步方式执行计算，即，而不会阻止执行其他工作。 例如，可以使用异步计算编写应用程序，因为应用程序会执行其他工作仍能响应用户的 ui。

## <a name="syntax"></a>语法

```fsharp
async { expression }
```

## <a name="remarks"></a>备注

在上述语法中，由表示计算`expression`设置以异步方式运行，也就是说，而不会阻止当前计算线程执行异步睡眠操作、 I/O 和其他异步操作时。 通常在后台线程上启动异步计算，而当前线程上继续执行。 表达式的类型是`Async<'T>`，其中`'T`是由表达式返回的类型时`return`使用关键字。 此类表达式中的代码被称为*异步块*，或*异步块*。

有多种方法的异步编程，并[ `Async` ](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7)类提供了支持多个方案的方法。 常规方法是创建`Async`表示计算或你想要以异步方式运行的计算，并使用触发的函数之一，然后启动这些计算的对象。 各种触发函数提供不同的方法来运行异步计算，并使用哪一个取决于是否想要使用当前线程、 后台线程或.NET Framework 任务对象，以及是否有延续当在计算完成时应运行的函数。 例如，若要在当前线程上开始一个异步计算，可以使用[ `Async.StartImmediate` ](https://msdn.microsoft.com/library/2f71d1cc-187f-48cf-ac66-e7fda41c46e3)。 当您从 UI 线程启动一个异步计算时，不会阻止处理用户操作，例如击键和鼠标活动，因此应用程序保持响应能力的主要事件循环。

## <a name="asynchronous-binding-by-using-let"></a>异步绑定通过使用 let ！

在异步工作流中，某些表达式和操作是同步的而有些则更长的计算，可用于以异步方式返回结果。 当您调用的方法以异步方式，而不是普通`let`绑定，请使用`let!`。 效果`let!`是使正在执行计算时，继续在其他计算或线程上执行。 之后的右侧`let!`绑定返回时，异步工作流的剩余部分将继续执行。

下面的代码显示之间的差异`let`和`let!`。 使用的代码行`let`只需创建一个对象，您可以运行更高版本通过使用，例如，作为一个异步计算`Async.StartImmediate`或[ `Async.RunSynchronously` ](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b)。 使用的代码行`let!`开始计算，，然后挂起线程，直到结果可用，请在哪个点执行将继续。

```fsharp
// let just stores the result as an asynchronous operation.
let (result1 : Async<byte[]>) = stream.AsyncRead(bufferSize)
// let! completes the asynchronous operation and returns the data.
let! (result2 : byte[])  = stream.AsyncRead(bufferSize)
```

除了`let!`，可以使用`use!`执行异步绑定。 之间的差异`let!`并`use!`之间的区别相同`let`和`use`。 有关`use!`，在当前范围的结束位置释放的对象。 请注意，当前版本中的F#语言中，`use!`不允许使用值初始化为 null，即使`use`does。

## <a name="asynchronous-primitives"></a>异步基元

执行单个异步任务并返回结果的方法，称为*异步基元*，，它们专门用于专门设计`let!`。 多个异步基元中定义F#核心库。 该模块中定义的 Web 应用程序的两个此类方法[ `Microsoft.FSharp.Control.WebExtensions` ](https://msdn.microsoft.com/library/95ef17bc-ee3f-44ba-8a11-c90fcf4cf003): [ `WebRequest.AsyncGetResponse` ](https://msdn.microsoft.com/library/09a60c31-e6e2-4b5c-ad23-92a86e50060c)并[ `WebClient.AsyncDownloadString` ](https://msdn.microsoft.com/library/8a85a9b7-f712-4cac-a0ce-0a797f8ea32a)。 这两个基元从 Web 页上，给定的 URL 下载数据。 `AsyncGetResponse` 将生成`System.Net.WebResponse`对象，和`AsyncDownloadString`生成一个字符串，表示网页的 HTML。

中包含用于异步 I/O 操作的多个基元[ `Microsoft.FSharp.Control.CommonExtensions` ](https://msdn.microsoft.com/library/2edb67cb-6814-4a30-849f-b6dbdd042396)模块。 这些扩展方法`System.IO.Stream`类是[ `Stream.AsyncRead` ](https://msdn.microsoft.com/library/85698aaa-bdda-47e6-abed-3730f59fda5e)并[ `Stream.AsyncWrite` ](https://msdn.microsoft.com/library/1b0a2751-e42a-47e1-bd27-020224adc618)。

此外可以通过定义其完整的主体括在异步块中的函数来编写您自己的异步基元。

若要为与其他异步模型使用.NET Framework 中设计的异步方法F#异步编程模型，创建一个函数，返回F#`Async`对象。 F#库具有函数，这可以更轻松地执行操作。

使用异步工作流的一个示例是为了让;还有很多这样的方法的文档中[异步类](https://msdn.microsoft.com/library/03eb4d12-a01a-4565-a077-5e83f17cf6f7)。

此示例演示如何使用异步工作流来并行执行计算。

在下面的代码示例，一个函数`fetchAsync`获取来自于 Web 请求返回 HTML 文本。 `fetchAsync`函数包含代码的异步块。 当绑定对结果的异步基元，在这种情况下[ `AsyncDownloadString` ](https://msdn.microsoft.com/library/8a85a9b7-f712-4cac-a0ce-0a797f8ea32a)、 let ！ 而不是让使用。

使用函数[ `Async.RunSynchronously` ](https://msdn.microsoft.com/library/0a6663a9-50f2-4d38-8bf3-cefd1a51fd6b)来执行异步操作并等待其结果。 例如，您可以多个异步操作并行执行通过[ `Async.Parallel` ](https://msdn.microsoft.com/library/aa9b0355-2d55-4858-b943-cbe428de9dc4)函数一起使用`Async.RunSynchronously`函数。 `Async.Parallel`函数采用一系列`Async`对象，每个设置了代码`Async`任务对象以运行并行，并返回`Async`对象，表示并行计算。 只与单个操作中，您调用`Async.RunSynchronously`要开始执行。

`runAll`函数启动三个并行的异步工作流，并等待，直到它们全部完成。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet8003.fs)]

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [计算表达式](computation-expressions.md)
- [Control.Async 类](https://msdn.microsoft.com/visualfsharpdocs/conceptual/control.async-class-%5bfsharp%5d)