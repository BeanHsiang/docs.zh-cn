---
title: Azure 事件网格的无服务器应用
description: Azure 事件网格是可靠事件交付和支付每个事件模型上大规模地路由的无服务器解决方案。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 4970130ede0c96c645129ee6c8c7d54cb1114042
ms.sourcegitcommit: 79066169e93d9d65203028b21983574ad9dcf6b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57212178"
---
# <a name="event-grid"></a>事件网格

[Azure 事件网格](/azure/event-grid/overview)为基于事件的应用程序提供无服务器基础结构。 可以从任何源发布到事件网格，并使用从任何平台的消息。 事件网格还提供来自 Azure 资源，以简化您的应用程序与集成的事件的内置支持。 例如，您可以订阅 blob 存储事件，以在文件上传时通知您的应用程序。 你的应用程序然后可以将发布供其他云或本地应用程序的自定义事件网格消息。 事件网格旨在可靠地处理很大的规模。 获取发布和订阅消息，而不必设置必要的基础结构的开销的优势。

![事件网格徽标](./media/event-grid-logo.png)

事件网格的主要功能包括：

* 完全托管的事件路由。
* 附近大规模实时事件交付。
* 内部和外部 Azure 广泛覆盖范围。

## <a name="scenarios"></a>方案

事件网格解决了几个不同的方案。 本部分介绍了三个最常见的。

### <a name="ops-automation"></a>运维自动化

![运维自动化](./media/ops-automation.png)

事件网格可以帮助速度自动化和简化策略执行通知[Azure 自动化](https://docs.microsoft.com/azure/automation)基础结构预配时。

### <a name="application-integration"></a>应用程序集成

![应用程序集成](./media/app-integration.png)

事件网格可用于将应用连接到其他服务。 使用标准 HTTP 协议，甚至旧版应用可以轻松地修改发布事件网格消息。 Web 挂钩是适用于其他服务和平台使用事件网格的消息。

### <a name="serverless-apps"></a>无服务器应用

![无服务器应用](./media/serverless-apps.png)

事件网格可以触发 Azure Functions、 逻辑应用或你自己的自定义代码。 使用事件网格的主要优点是，它使用*推送*事件发生时发送消息的机制。 推送体系结构会占用较少的资源和伸缩性优于*轮询*机制。 轮询必须检查固定时间间隔上的更新。

## <a name="event-grid-vs-other-azure-messaging-services"></a>事件网格与其他 Azure 消息传送服务

Azure 提供了多个消息传送服务，包括[事件中心](https://docs.microsoft.com/azure/event-hubs)并[服务总线](https://docs.microsoft.com/azure/service-bus-messaging)。 每个旨在解决一组特定的用例。 下图提供了在服务之间的差异的高级概述。

![Azure 消息传递的比较](./media/azure-messaging-services.png)

有关更深入比较，请参阅[比较消息服务](https://docs.microsoft.com/azure/event-grid/compare-messaging-services)。

## <a name="performance-targets"></a>性能目标

使用事件网格可以充分利用以下性能可保证：

* 次秒级的端到端延迟在第 99 个百分点值。
* 99.99%的可用性。
* 每个区域每秒 10 万个事件。
* 每个区域 100 万个订阅。
* 发布服务器 50 毫秒的延迟。
* 使用指数回退的 1 天的时间窗口中的有保证传递的 24 小时重试。
* 透明区域故障转移。

## <a name="event-grid-schema"></a>事件网格架构

事件网格使用的标准架构来包装自定义事件。 架构就像自定义数据元素进行包装的信封。 下面是示例事件网格消息：

```json
[{
    "id": "03e24f21-a955-43cc-8921-1f61a6081ce0",
    "eventType": "myCustomEvent",
    "subject": "foo/bar/12",
    "eventTime": "2018-09-22T10:36:01+00:00",
    "data": {
        "favoriteColor": "blue",
        "favoriteAnimal": "panther",
        "favoritePlanet": "Jupiter"
    },
    "dataVersion": "1.0"
}]
```

有关消息的所有内容都是除标准`data`属性。 可以检查消息，并使用`eventType`和`dataVersion`进行反序列化有效负载的自定义部分。

## <a name="azure-resources"></a>Azure 资源

使用事件网格的主要优点是由 Azure 生成的自动消息。 在 Azure 中，资源会自动将发布到*主题*，可以有多个事件订阅。 下表列出了资源类型、 消息类型和事件将自动应用。

| Azure 资源 | 事件类型 | 描述 |
| -------------- | ---------- | ----------- |
| Azure 订阅 | Microsoft.Resources.ResourceWriteSuccess | 引发时资源创建或更新操作成功。 |
| | Microsoft.Resources.ResourceWriteFailure | 在资源创建或更新操作失败时引发。 |
| | Microsoft.Resources.ResourceWriteCancel | 引发时资源创建或更新操作已取消。 |
|  | Microsoft.Resources.ResourceDeleteSuccess | 当资源删除操作成功时引发。 |
|  | Microsoft.Resources.ResourceDeleteFailure | 当资源删除操作失败时引发。 |
| | Microsoft.Resources.ResourceDeleteCancel | 取消资源删除操作时引发。 取消模板部署时会发生此事件。 |
| Blob 存储 | Microsoft.Storage.BlobCreated | 创建 blob 时引发。 |
| | Microsoft.Storage.BlobDeleted | 删除 blob 时引发。 |
| 事件中心 | Microsoft.EventHub.CaptureFileCreated | 创建捕获文件时引发。
| IoT 中心 | Microsoft.Devices.DeviceCreated | 发布到 IoT 中心注册设备。 |
| | Microsoft.Devices.DeviceDeleted | 当设备从 IoT 中心删除时发布。 |
| 资源组 | Microsoft.Resources.ResourceWriteSuccess | 引发时资源创建或更新操作成功。 |
| | Microsoft.Resources.ResourceWriteFailure | 在资源创建或更新操作失败时引发。 |
| | Microsoft.Resources.ResourceWriteCancel | 引发时资源创建或更新操作已取消。 |
| | Microsoft.Resources.ResourceDeleteSuccess | 当资源删除操作成功时引发。 |
| | Microsoft.Resources.ResourceDeleteFailure | 当资源删除操作失败时引发。 |
| | Microsoft.Resources.ResourceDeleteCancel | 取消资源删除操作时引发。 取消模板部署时会发生此事件。 |

有关详细信息，请参阅[Azure 事件网格事件架构](https://docs.microsoft.com/azure/event-grid/event-schema)。

可以从任何类型的应用程序，甚至是在本地运行的一个来访问事件网格。

## <a name="conclusion"></a>结束语

在这一章中您学习了有关 Azure 无服务器平台，其中包含 Azure Functions、 逻辑应用和事件网格。 您可以使用这些资源生成一个完全无服务器应用程序体系结构，或创建与其他云资源进行交互和本地服务器上的混合解决方案。 如结合无服务器的数据平台[Azure SQL](https://docs.microsoft.com/azure/sql-database)或[CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction)，可以生成完全托管的云本机应用程序。

## <a name="recommended-resources"></a>推荐的资源

* [应用服务计划](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)
* [Application Insights](https://docs.microsoft.com/azure/application-insights)
* [Application Insights 分析](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)
* [Azure:将应用迁移到使用无服务器 Azure Functions 在云中](https://channel9.msdn.com/events/Connect/2017/E102)
* [Azure 事件网格](https://docs.microsoft.com/azure/event-grid/overview)
* [Azure 事件网格事件架构](https://docs.microsoft.com/azure/event-grid/event-schema)
* [Azure 事件中心](https://docs.microsoft.com/azure/event-hubs)
* [Azure Functions 文档](https://docs.microsoft.com/azure/azure-functions)
* [Azure Functions 触发器和绑定概念](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)
* [Azure 逻辑应用](https://docs.microsoft.com/azure/logic-apps)
* [Azure 服务总线](https://docs.microsoft.com/azure/service-bus-messaging)
* [Azure 表存储](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)
* [比较函数 1.x 和 2.x](https://docs.microsoft.com/azure/azure-functions/functions-versions)
* [连接到使用 Azure 本地数据网关的本地数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway)
* [在 Azure 门户中创建第一个函数](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)
* [创建使用 Azure CLI 将第一个函数](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli)
* [创建第一个函数使用 Visual Studio](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio)
* [函数支持的语言](https://docs.microsoft.com/azure/azure-functions/supported-languages)
* [监视 Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring)
* [使用 Azure Functions 代理](https://docs.microsoft.com/azure/azure-functions/functions-proxies)

>[!div class="step-by-step"]
>[上一页](logic-apps.md)
>[下一页](durable-azure-functions.md)
