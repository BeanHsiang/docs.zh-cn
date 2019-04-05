---
title: 异步编程
description: 了解如何F#通过是易于使用和自然语言的语言级别编程模型实现异步编程。
ms.date: 06/20/2016
ms.openlocfilehash: 18ba4873cd3dba6d9548a07c4487306d96adab61
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56980082"
---
# <a name="async-programming-in-f"></a>F 中的异步编程\#

> [!NOTE]
> 在本文中发现了一些错误。  它是被重写。  请参阅[问题 #666](https://github.com/dotnet/docs/issues/666)若要了解有关所做的更改。

异步编程中F#可以通过设计为易于使用和自然语言的语言级别编程模型来完成。

异步编程中的核心F#是`Async<'T>`，表示形式可以触发以便在后台运行的工作位置`'T`通过特殊的返回类型`return`关键字或`unit`如果异步工作流具有要返回的结果。

若要了解的关键概念在于异步表达式的类型是`Async<'T>`，即只_规范_的异步上下文中完成的工作。 不执行直到它显式启动其中一个起始函数 (如`Async.RunSynchronously`)。 虽然这是以不同的方式考虑执行工作的但它最终实际上非常简单。

例如，假设你想要从 dotnetfoundation.org 下载 HTML，而不会阻止主线程。 您可以实现它像这样：

```fsharp
open System
open System.Net

let fetchHtmlAsync url = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()

        // Execution of fetchHtmlAsync won't continue until the result
        // of AsyncDownloadString is bound.
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

let html = "https://dotnetfoundation.org" |> fetchHtmlAsync |> Async.RunSynchronously
printfn "%s" html
```

就是这么简单！ 除了使用`async`， `let!`，并`return`，这是正常的只是F#代码。

有几个语法构造是值得一提：

*   `let!` 将一个异步表达式 （其在另一个上下文中运行） 的结果绑定。
*   `use!` 工作方式就类似于`let!`，但它超出范围时释放其绑定的资源。
*   `do!` 将 await 的异步工作流，这不会返回任何内容。
*   `return` 只需从异步表达式将返回结果。
*   `return!` 执行另一个异步工作流并返回其返回值作为结果。

此外，正常`let`， `use`，和`do`关键字可以用异步版本，就像在普通函数中。

## <a name="how-to-start-async-code-in-f"></a>如何在 F 中启动异步代码\#

前面曾提到，异步代码将是一种规范，需要对其显式启动另一个上下文中完成工作。 下面是两种主要方法来实现此目的：

1.  `Async.RunSynchronously` 将另一个线程上启动异步工作流，并等待其结果。

```fsharp
open System
open System.Net

let fetchHtmlAsync url = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

 // Execution will pause until fetchHtmlAsync finishes
 let html = "https://dotnetfoundation.org" |> fetchHtmlAsync |> Async.RunSynchronously

 // you actually have the result from fetchHtmlAsync now!
 printfn "%s" html
 ```

2.  `Async.Start` 将另一个线程上启动的异步工作流，并将**不**等待其结果。

```fsharp
open System
open System.Net
  
let uploadDataAsync url data = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        webClient.UploadStringAsync(uri, data)
    }

let workflow = uploadDataAsync "https://url-to-upload-to.com" "hello, world!"

// Execution will continue after calling this!
Async.Start(workflow)

printfn "%s" "uploadDataAsync is running in the background..."
 ```

还有其他方法来启动异步工作流可用于更多特定方案。 对其进行详细[异步参考中](https://msdn.microsoft.com/library/ee370232.aspx)。

### <a name="a-note-on-threads"></a>有关线程的说明

上述"在另一个线程"短语，但务必要知道**这并不意味着异步工作流是用于的外观的多线程处理**。 工作流实际"跳转"借用的少量时间来执行有用的工作线程之间。 时异步工作流有效地"等待"（例如，等待网络调用，以返回某些内容），在时，它借用了任何线程被释放到转执行有用的工作在别的事情上。 这允许异步工作流，以利用它们尽可能有效地运行的系统并使这些极强的大量 I/O 方案。

## <a name="how-to-add-parallelism-to-async-code"></a>如何将并行处理添加到异步代码

有时您可能需要并行执行多个异步作业收集其结果，并以某种方式进行解释。 `Async.Parallel` 允许您执行此操作而无需使用任务并行库，这会涉及无需强制转换`Task<'T>`和`Async<'T>`类型。

下面的示例将使用`Async.Parallel`从并行的四个常用网站下载 HTML，等待这些任务完成，然后输出已下载的 HTML。

```fsharp
open System
open System.Net

let urlList = 
    [ "https://www.microsoft.com"
      "https://www.google.com"
      "https://www.amazon.com"
      "https://www.facebook.com" ]

let fetchHtmlAsync url = 
    async {
        let uri = Uri(url)
        use webClient = new WebClient()
        let! html = webClient.AsyncDownloadString(uri)
        return html
    }

let getHtmlList urls =
    urls
    |> Seq.map fetchHtmlAsync   // Build an Async<'T> for each site
    |> Async.Parallel           // Returns an Async<'T []>
    |> Async.RunSynchronously   // Wait for the result of the parallel work

let htmlList = getHtmlList urlList

// We now have the downloaded HTML for each site!
for html in htmlList do
    printfn "%s" html
```

## <a name="important-info-and-advice"></a>重要信息和建议

*   将"Async"追加到末尾将使用的任何函数

 虽然这是命名约定，但它确实使 API 可发现性等内容更容易。 尤其是例程的当有相同的同步和异步版本，它是例程的显式声明为异步通过名称的一个好办法。

*   侦听编译器 ！

 F#编译器是非常严格，因此几乎不可能执行一些麻烦的问题等操作以同步方式运行"async"代码。 如果您遇到一条警告，则代码不会执行认为它将如何登录。 如果编译器可以为取悦，按预期方式将很可能执行代码。

## <a name="for-the-cvb-programmer-looking-into-f"></a>有关C#/VB 程序员研究 F\#

本部分假定您熟悉使用中的异步模型C#/VB. 如果你不可以，[中的异步编程C#](../../../csharp/async.md)是一个起始点。

没有本质上之间的区别C#/VB 异步模型和F#异步模型。

当调用一个函数，它返回`Task`或`Task<'T>`，该作业已开始执行。 返回的句柄表示已在运行异步作业。 与此相反，当您调用异步函数F#，则`Async<'a>`返回表示一个作业，它将是**生成**在某个时间点。 了解此模型非常强大，因为它允许在异步作业F#链接起来变得更容易，有条件地执行和入门的更细粒度的控制。

有几个其他的相似之处和值得注意的区别。

### <a name="similarities"></a>相似之处

*   `let!``use!`，并`do!`类似于`await`内调用的异步作业时`async{ }`块。

 只能在使用三个关键字`async { }`块中，类似于如何`await`只能在调用`async`方法。 简单地说，`let!`适用于你想要捕获和使用结果`use!`是相同，但某些内容在使用后，应会清理其资源和`do!`适用于你想要等待的异步工作流完成不返回值再继续。

*   F#类似的方式支持数据并行。

 尽管它以非常不同的方式，运行`Async.Parallel`对应于`Task.WhenAll`想的一组异步作业结果，它们全部完成时的方案。

### <a name="differences"></a>差异

*   嵌套`let!`不允许，与不同嵌套 `await`

 与不同`await`，可以嵌套无限期`let!`能并且必须包含另一个内部使用它之前绑定其结果`let!`， `do!`，或`use!`。

*   取消支持是在F#比C#/VB.

 支持的任务在执行中途取消C#/VB 需要检查`IsCancellationRequested`属性或调用`ThrowIfCancellationRequested()`上`CancellationToken`传递到异步方法的对象。

与此相反，F#异步工作流是更自然可取消。 取消是一个简单的三步骤过程。

1.  创建一个新的 `CancellationTokenSource`。
2.  将它传递到起始函数。
3.  调用`Cancel`的令牌。

示例:

```fsharp
open System.Threading

// Create a workflow which will loop forever.
let workflow =
    async {
        while true do
            printfn "Working..."
            do! Async.Sleep 1000
    }
    
let tokenSource = new CancellationTokenSource()

// Start the workflow in the background
Async.Start (workflow, tokenSource.Token)

// Executing the next line will stop the workflow
tokenSource.Cancel()
```

就是这么简单！

## <a name="further-resources"></a>其他资源：

*   [MSDN 上的异步工作流](https://msdn.microsoft.com/library/dd233250.aspx)
*   [异步序列 F#](https://fsprojects.github.io/FSharp.Control.AsyncSeq/library/AsyncSeq.html)
*   [F# HTTP 数据实用程序](https://fsharp.github.io/FSharp.Data/library/Http.html)