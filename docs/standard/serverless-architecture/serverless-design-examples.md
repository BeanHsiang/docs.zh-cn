---
title: 无服务器设计示例-无服务器应用
description: 了解各种支持的无服务器体系结构，从计划和基于事件的处理到文件触发器和流处理方案。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: d165746ff2f03b0edc59a9284052323a0c1fd05b
ms.sourcegitcommit: 4ac80713f6faa220e5a119d5165308a58f7ccdc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54149672"
---
# <a name="serverless-design-examples"></a>无服务器设计示例

有多的设计模式存在的无服务器。 此部分捕获使用无服务器的一些常见方案。 内容的所有示例都有共同点是基本事件触发器和业务逻辑的组合。

## <a name="scheduling"></a>计划

计划任务是一个常见的函数。 下图显示了旧的数据库不具有适当的完整性检查。 必须定期清理数据库。 无服务器函数找到无效的数据，并清除它。 触发器是计时器按计划运行的代码。

![无服务器计划](./media/serverless-scheduling.png)

## <a name="command-and-query-responsibility-segregation-cqrs"></a>命令和查询责任分离 (CQRS)

命令查询职责分离 (CQRS) 是提供了不同的接口，以进行读取 （或查询） 数据和修改数据的操作的模式。 它解决了几个常见的问题。 在传统创建读取更新删除 (CRUD) 基于系统中，可能会发生冲突从大量的读取和写入到相同的数据存储。 锁定可能经常发生，并显著降低读取。 通常情况下，数据显示为多个域对象和读取的操作的组合必须合并来自不同的实体的数据。

使用 CQRS，读取可能涉及一个特殊的"平展"实体的模型数据的方式使用它。 读取的处理方式不同于存储方式。 例如，尽管数据库可能具有子地址记录的标头记录作为存储联系人，读取可能涉及具有标头和地址属性的实体。 有多种方法创建读取的模型。 它可能会具体化视图中。 更新操作可以封装为独立的事件，然后触发两个不同的模型内容的最新更新。 用于读取和写入存在单独的模型。

![CQRS 示例](./media/cqrs-example.png)

通过提供分离终结点，无服务器可以适应 CQRS 模式。 查询或读取，还包含一个无服务器函数，不同的无服务器函数或一组函数将处理更新操作。 无服务器函数也可能是负责使读取的模型保持最新，并可触发的数据库的[更改源](https://docs.microsoft.com/azure/cosmos-db/change-feed)。 前端开发简化为连接到必要的终结点。 在后端处理事件的处理。 此外，因为不同的团队可能在不同的操作上运行，适合大型项目还可以扩展此模型。

## <a name="event-based-processing"></a>基于事件的处理

在基于消息的系统中，通常在队列或发布服务器/订阅主题有待处理中收集事件。 这些事件可以触发无服务器函数来执行业务逻辑的组成部分。 基于事件的一个示例是处理的事件源系统。 引发"事件"以将标记为已完成的任务。 由事件触发的无服务器函数更新相应的数据库文档。 第二个无服务器函数可能会使用事件来更新系统的读取的模型。 [Azure 事件网格](https://docs.microsoft.com/azure/event-grid/overview)使您能够将事件与订阅服务器的功能相集成。

> 事件是信息性消息。 有关详细信息，请参阅[事件溯源模式](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing)。

## <a name="file-triggers-and-transformations"></a>文件触发器和转换

提取、 转换和加载 (ETL) 是一个常见的业务函数。 无服务器是很好的解决方案 etl 因为它允许代码触发管道的一部分。 单个代码组件可以处理各个方面。 一个无服务器函数可能会下载文件、 另一个应用转换，以及另一个加载数据。 可以测试代码，并将其独立部署，使它更易于维护和扩展在需要时。

![无服务器文件触发器和转换](./media/serverless-file-triggers.png)

在图中，"冷存储"提供数据中分析[Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics)。 在数据流中遇到任何问题触发 Azure 函数来解决异常情况。

## <a name="asynchronous-background-processing-and-messaging"></a>异步后台处理和消息传送

异步消息传送和后台处理允许应用程序而无需等待启动进程。 异步处理的一个示例是 OCR 应用。 提交图像并将其排队等待处理。 扫描要提取文本的图像可能需要时间，并发送它完成后通知。 调用和结果在此方案中，可以处理无服务器。

## <a name="web-apps-and-apis"></a>Web 应用和 Api

一种常用方案的无服务器是 N 层应用程序，最常用的 UI 层所在的 web 应用。 具有最近拉响广受欢迎的单页面应用程序 (SPA)。 SPA 应用程序呈现单个页面，然后依赖于 API 调用和返回的数据动态而无需重新加载完整页面中呈现新的用户界面。 客户端呈现提供了对最终用户更快、 更快地响应应用程序。

触发的 HTTP 调用的无服务器终结点可以用于处理 API 请求。 例如，ad 服务公司可以调用具有用户配置文件信息来请求自定义广告的无服务器函数。 无服务器函数将返回自定义 ad 并网页上呈现报表。

![无服务器 web API](./media/serverless-web-api.png)

## <a name="data-pipeline"></a>数据管道

可以使用无服务器函数，以便数据管道。 在此示例中，文件会触发一个函数来转换到表中的数据行的 CSV 文件中的数据。 组织的表允许 Power BI 仪表板以向最终用户提供分析。

![无服务器的数据管道](./media/serverless-data-pipeline.png)

## <a name="stream-processing"></a>Stream 处理

设备和传感器通常实时生成必须处理的数据的数据流。 有许多可以捕获消息和从流的技术[事件中心](https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs)并[IoT 中心](https://docs.microsoft.com/azure/iot-hub)到[Service Bus](https://docs.microsoft.com/azure/service-bus)。 传输，无论无服务器是一种理想机制来处理传入消息和数据的数据流。 无服务器可以快速缩放以满足数据量很大的需求。 无服务器代码可以应用业务逻辑以分析数据和输出的操作和分析结构化格式。

![无服务器的流处理](./media/serverless-stream-processing.png)

## <a name="api-gateway"></a>API 网关

API 网关为客户端提供单一入口点，然后以智能方式将请求路由到后端服务。 它可用于管理大型的服务集。 它可以处理版本控制，并通过轻松地将客户端连接到不同的环境，简化开发。 无服务器可以处理演示通过 API 网关的单个前端时各个微服务的缩放比例的后端。

![无服务器 API 网关](./media/serverless-api-gateway.png)

## <a name="recommended-resources"></a>推荐的资源

* [Azure 事件网格](https://docs.microsoft.com/azure/event-grid/overview)
* [Azure IoT 中心](https://docs.microsoft.com/azure/iot-hub)
* [分布式数据管理挑战和解决方案](../microservices-architecture/architect-microservice-container-applications/distributed-data-management.md)
* [设计微服务： 标识微服务边界](https://docs.microsoft.com/azure/architecture/microservices/microservice-boundaries)
* [事件中心](https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs)
* [事件溯源模式](https://docs.microsoft.com/azure/architecture/patterns/event-sourcing)
* [实现断路器模式](../microservices-architecture/implement-resilient-applications/implement-circuit-breaker-pattern.md)
* [IoT 中心](https://docs.microsoft.com/azure/iot-hub)
* [服务总线](https://docs.microsoft.com/azure/service-bus)
* [使用 Azure Cosmos DB 中源支持的更改](https://docs.microsoft.com/azure/cosmos-db/change-feed)

>[!div class="step-by-step"]
>[上一页](serverless-architecture-considerations.md)
>[下一页](azure-serverless-platform.md)
