---
title: 业务流程模式-无服务器应用
description: Azure Durable functions 拉取请求
author: cecilphillip
ms.author: cephilli
ms.date: 06/26/2018
ms.openlocfilehash: 8be499a24e2c5a94132ce07241e17f675e8a1274
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57843753"
---
# <a name="orchestration-patterns"></a>业务流程模式

Durable Functions，可以更轻松地创建有状态工作流的无服务器环境中的离散、 长时间运行的活动组成。 Durable Functions 可以跟踪的工作流和定期检查点的进度的执行历史记录，因为它有助于实现一些有趣的模式。

## <a name="function-chaining"></a>函数链

在典型的顺序过程中，需要执行一个接一个按特定顺序活动。 （可选） 接下来的活动可能需要一些来自上一个函数。 此依赖项上的活动顺序创建执行的函数链。

使用 Durable Functions 来实现此工作流模式的优点来自于其能够执行检查点。 如果服务器发生故障，网络超时或出现一些其他问题，Durable functions 可以从最后一个已知状态恢复并继续运行工作流，即使它位于另一台服务器上。

```csharp
[FunctionName("PlaceOrder")]
public static async Task<string> PlaceOrder([OrchestrationTrigger] DurableOrchestrationContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    await context.CallActivityAsync<bool>("CheckAndReserveInventory", orderData);
    await context.CallActivityAsync<bool>("ProcessPayment", orderData);

    string trackingNumber = await context.CallActivityAsync<string>("ScheduleShipping", orderData);
    await context.CallActivityAsync<string>("EmailCustomer", trackingNumber);

    return trackingNumber;
}
```

在前面的代码示例中，`CallActivityAsync`函数负责数据中心中的虚拟机上运行给定的活动。 Await 返回，并且基础任务完成后，执行将记录到历史记录表中。 使业务流程协调程序函数中的代码可以使用所有熟悉的构造的任务并行库和 async/await 关键字。

下面的代码是什么的简化的示例`ProcessPayment`方法可能如下所示：

```csharp
[FunctionName("ProcessPayment")]
public static bool ProcessPayment([ActivityTrigger] DurableActivityContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    ApplyCoupons(orderData);
    if(IssuePaymentRequest(orderData)) {
        return true;
    }

    return false;
}
```

## <a name="asynchronous-http-apis"></a>异步 HTTP Api

在某些情况下，工作流可能包含需要相当长一段时间才能完成的活动。 假设进程中用于启动媒体的备份到 blob 存储的文件。 根据大小和数量的媒体文件，此备份过程可能需要数小时才能完成。

在此方案中，`DurableOrchestrationClient`的能够检查正在运行的工作流的状态将会很有用。 使用时`HttpTrigger`以启动工作流`CreateCheckStatusResponse`方法可用于返回的一个实例`HttpResponseMessage`。 可用于检查正在运行的进程的状态的有效负载中的 URI 为客户端提供此响应。

```csharp
[FunctionName("OrderWorkflow")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "POST")]HttpRequestMessage req,
    [OrchestrationClient ] DurableOrchestrationClient orchestrationClient)
{
    OrderRequestData data = await req.Content.ReadAsAsync<OrderRequestData>();

    string instanceId = await orchestrationClient.StartNewAsync("PlaceOrder", data);

    return orchestrationClient.CreateCheckStatusResponse(req, instanceId);
}
```

下面的示例结果显示了响应有效负载的结构。

```json
{
    "id": "instanceId",
    "statusQueryGetUri": "http://host/statusUri",
    "sendEventPostUri": "http://host/eventUri",
    "terminatePostUri": "http://host/terminateUri"
}
```

使用您首选的 HTTP 客户端，GET 请求可以对 statusQueryGetUri 中的 URI 来检查正在运行的工作流的状态。 返回的状态响应应类似于下面的代码。

```json
{
    "runtimeStatus": "Running",
    "input": {
        "$type": "DurableFunctionsDemos.OrderRequestData, DurableFunctionsDemos"
    },
    "output": null,
    "createdTime": "2018-01-01T00:22:05Z",
    "lastUpdatedTime": "2018-01-01T00:22:09Z"
}
```

此过程将继续，因为状态响应将更改为**失败**或**Completed**。 成功完成后，**输出**有效负载中的属性将包含任何返回的数据。

## <a name="monitoring"></a>监视

Azure Functions 提供的简单定期任务`TimerTrigger`可以基于 CRON 表达式计划的。 计时器非常适用于简单的生存期较短的任务，但可能需要更灵活的计划的位置的方案。 当监视模式和 Durable Functions 可帮助时，此方案。

Durable Functions，灵活的计划间隔、 生存期管理和创建从单个业务流程函数的多个监视器进程。 此功能的一个用例可能创建满足特定的阈值，完成的股票价格更改的观察程序。

```csharp
[FunctionName("CheckStockPrice")]
public static async Task CheckStockPrice([OrchestrationTrigger] DurableOrchestrationContext context)
{
    StockWatcherInfo stockInfo = context.GetInput<StockWatcherInfo>();
    const int checkIntervalSeconds = 120;
    StockPrice initialStockPrice = null;

    DateTime fireAt;
    DateTime exitTime = context.CurrentUtcDateTime.Add(stockInfo.TimeLimit);

    while (context.CurrentUtcDateTime < exitTime)
    {
        StockPrice currentStockPrice = await context.CallActivityAsync<StockPrice>("GetStockPrice", stockInfo);

        if (initialStockPrice == null)
        {
            initialStockPrice = currentStockPrice;
            fireAt = context.CurrentUtcDateTime.AddSeconds(checkIntervalSeconds);
            await context.CreateTimer(fireAt, CancellationToken.None);
            continue;
        }

        decimal percentageChange = (initialStockPrice.Price - currentStockPrice.Price) /
                               ((initialStockPrice.Price + currentStockPrice.Price) / 2);

        if (Math.Abs(percentageChange) >= stockInfo.PercentageChange)
        {
            // Change threshold detected
            await context.CallActivityAsync("NotifyStockPercentageChange", currentStockPrice);
            break;
        }

        // Sleep til next polling interval
        fireAt = context.CurrentUtcDateTime.AddSeconds(checkIntervalSeconds);
        await context.CreateTimer(fireAt, CancellationToken.None);
    }
}
```

`DurableOrchestrationContext``CreateTimer`方法设置的计划循环的下一个调用以检查股票价格更改。 `DurableOrchestrationContext` 此外具有`CurrentUtcDateTime`属性在 UTC 中获取当前日期时间值。 最好使用此属性，而不是`DateTime.UtcNow`因为它采用不易模拟用于测试。

## <a name="recommended-resources"></a>推荐的资源

* [Azure Durable 函数](https://docs.microsoft.com/azure/azure-functions/durable-functions-overview)
* [.NET Core 和 .NET Standard 中的单元测试](../../core/testing/index.md)

>[!div class="step-by-step"]
>[上一页](durable-azure-functions.md)
>[下一页](serverless-business-scenarios.md)