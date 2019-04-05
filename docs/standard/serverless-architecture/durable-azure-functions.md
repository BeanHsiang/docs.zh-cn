---
title: 持久的 Azure 函数-无服务器应用
description: 持久的 Azure 函数来扩展 Azure Functions 运行时，若要启用在代码中的有状态工作流。
author: cecilphillip
ms.author: cephilli
ms.date: 06/26/2018
ms.openlocfilehash: 8ad354e1708eb88f016130f8235f534b967eb122
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53147300"
---
# <a name="durable-azure-functions"></a>持久的 Azure 函数

当使用 Azure Functions 创建无服务器应用程序，您的操作将通常设计为无状态方式运行。 选择此设计的原因是因为作为平台的刻度，则很难知道哪些服务器运行代码。 它还就会难以确定多少个实例处于活动状态，在任意给定时间。 但是，有需要为已知的进程的当前状态的应用程序的类。 请考虑提交到在线商店订单的过程。 签出操作可能是由多个操作，需要了解该过程的状态的工作流。 此类信息可能包括产品库存中，如果客户具有自己的帐户，以及处理信用卡的结果的任何信用额度。 这些操作轻松可能是其自己的内部工作流或甚至从第三方系统服务。

各种模式目前存在该帮助进行协调的内部和外部系统之间的应用程序状态。 它是通常会遇到依赖于集中式队列系统、 分布式的键-值存储或共享的数据库来管理该状态的解决方案。 但是，它们现在需要进行预配和管理的所有其他资源。 在无服务器环境中，你的代码会非常麻烦尝试手动协调这些资源。 Azure Functions 提供了用于创建调用 Durable Functions 的有状态函数的替代。

Durable Functions 是 Azure Functions 运行时，使您能够在代码中的有状态工作流定义的扩展。 通过将分解到活动的工作流，Durable Functions 扩展可管理状态、 创建进度检查点和跨服务器处理的函数调用的分布。 在后台，它使的 Azure 存储帐户中用于保存执行历史记录、 计划活动函数和检索响应。 在无服务器代码应永远不会与保持在该存储帐户中的信息和交互并通常不是开发人员需要与其进行交互。

## <a name="triggering-a-stateful-workflow"></a>触发有状态工作流

Durable Functions 中的有状态工作流可以分解为两个内部组件;业务流程和活动触发器。 触发器和绑定是使用 Azure functions，使无服务器函数开始，接收输入，并返回结果时要通知的核心组件。

### <a name="working-with-the-orchestration-client"></a>使用业务流程客户端

业务流程是在 Azure Functions 中触发操作的其他样式进行比较时唯一的。 Durable Functions 可实现函数可能需要数小时甚至数天才能完成的执行。 与需要的应用，可以检查正在运行的业务流程的状态，提前终止，或者将外部事件的通知发送对提供该类型的行为。

对于这种情况下，Durable Functions 扩展提供了`DurableOrchestrationClient`，可与之交互的类对函数进行安排。 通过获取对业务流程客户端访问`OrchestrationClientAttribute`绑定。 通常情况下，应包括此属性与另一种触发器类型，如`HttpTrigger`或`ServiceBusTrigger`。 一旦源函数已被触发，业务流程客户端可以用于启动业务流程协调程序函数。

```csharp
[FunctionName("KickOff")]
public static async Task<HttpResponseMessage> Run(
    [HttpTrigger(AuthorizationLevel.Function, "POST")]HttpRequestMessage req,
    [OrchestrationClient ] DurableOrchestrationClient<orchestrationClient>)
{
    OrderRequestData data = await req.Content.ReadAsAsync<OrderRequestData>();

    string instanceId = await orchestrationClient.StartNewAsync("PlaceOrder", data);

    return orchestrationClient.CreateCheckStatusResponse(req, instanceId);
}
```

### <a name="the-orchestrator-function"></a>业务流程协调程序函数

作为业务流程协调程序函数批注与 Azure Functions 将 OrchestrationTriggerAttribute 函数的函数。 它负责管理构成了在有状态工作流的各种活动。

业务流程协调程序函数不能使 OrchestrationTriggerAttribute 以外的绑定的使用。 此属性仅用于 DurableOrchestrationContext 的参数类型。 可以不使用任何其他输入，因为反序列化在函数签名中的输入不受支持。 若要获取有关提供的业务流程客户端，GetInput\<T\>必须使用方法。

此外，业务流程函数的返回类型必须为 void、 Task 或 JSON 可序列化值。

> *为简便起见，已被错误处理代码省略，*

```csharp
[FunctionName("PlaceOrder")]
public static async Task<string> PlaceOrder([OrchestrationTrigger] DurableOrchestrationContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    await context.CallActivityAsync<bool>("CheckAndReserveInventory", orderData);
    await context.CallActivityAsync<string>("ProcessPayment", orderData);

    string trackingNumber = await context.CallActivityAsync<string>("ScheduleShipping", orderData);
    await context.CallActivityAsync<string>("EmailCustomer", trackingNumber);

    return trackingNumber;
}
```

业务流程的多个实例可以在同一时间是启动并正在运行。 调用`StartNewAsync`方法`DurableOrchestrationClient`启动业务流程的新实例。 该方法将返回`Task<string>`完成业务流程已启动时将完成。 类型的异常`TimeoutException`获取如果在 30 秒内启动该业务流程尚未引发。

已完成`Task<string>`从`StartNewAsync`应包含业务流程实例的唯一 ID。 可以使用此实例 ID 来调用该特定业务流程上的操作。 业务流程可查询状态或发送事件通知。

### <a name="the-activity-functions"></a>活动函数

活动函数无非是获取组合在一起的业务流程函数来创建工作流中的离散操作。 下面是会执行大部分实际工作。 它们表示业务逻辑，长时间运行的进程和到更大的解决方案的填数游戏块。

`ActivityTriggerAttribute`用于进行批注类型的函数参数`DurableActivityContext`。 使用批注通知运行时函数旨在用作活动函数。 使用检索到活动函数的输入的值`GetInput<T>`方法的`DurableActivityContext`参数。

与业务流程函数相似，活动函数的返回类型必须为 void、 Task 或 JSON 可序列化值。

获取活动函数中引发的任何未处理的异常会获取向上发送到调用的业务流程协调程序函数，其中显示为`TaskFailedException`。 此时，可以捕获和记录在业务流程协调程序，该错误，该活动可以重试。

```csharp
[FunctionName("CheckAndReserveInventory")]
public static bool CheckAndReserveInventory([ActivityTrigger] DurableActivityContext context)
{
    OrderRequestData orderData = context.GetInput<OrderRequestData>();

    // Connect to inventory system and try to reserve items
    return true;
}
```

## <a name="recommended-resources"></a>推荐的资源

* [Durable Functions](https://docs.microsoft.com/azure/azure-functions/durable-functions-overview)
* [Durable Functions 的绑定](https://docs.microsoft.com/azure/azure-functions/durable-functions-bindings)
* [在 Durable Functions 中管理实例](https://docs.microsoft.com/azure/azure-functions/durable-functions-instance-management)

>[!div class="step-by-step"]
>[上一页](event-grid.md)
>[下一页](orchestration-patterns.md)