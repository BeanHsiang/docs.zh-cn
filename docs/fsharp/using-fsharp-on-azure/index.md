---
title: 在 Azure 上使用 F#
description: 使用 Azure 服务的指南F#
author: sylvanc
ms.date: 09/22/2016
ms.openlocfilehash: 8243c021b8bc3ea9b067b278a5d9c6e3619232b7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57371031"
---
# <a name="using-f-on-azure"></a>在 Azure 上使用 F#

F# 是一种出色的云编程语言，常用于编写 Web 应用程序、云服务、云托管微服务，也可用于可缩放数据处理。

在以下部分中，你将发现如何结合使用 F# 与一系列 Azure 服务的相关资源。

> [!NOTE]
> 如果某特定 Azure 服务不在此文档集中，请参阅适用于该服务的 Azure Functions 或 .NET 文档。 某些 Azure 服务独立于语言，不需要任何特定于语言的文档，未在此处列出。

## <a name="using-azure-virtual-machines-with-f"></a>使用 Azure 虚拟机和 F\#

Azure 支持各种不同的虚拟机 (VM) 配置，请参阅 [Linux 和 Azure 虚拟机](https://azure.microsoft.com/services/virtual-machines/)。

若要在虚拟机上安装 F# 用来执行、编译和/或编写脚本，请参阅[在 Linux 上使用 F#](https://fsharp.org/use/linux) 和[在 Windows 上使用 F#](https://fsharp.org/use/windows)。


## <a name="using-azure-functions-with-f"></a>使用 Azure Functions F\#

[Azure Functions](https://azure.microsoft.com/services/functions/) 是一个在云中轻松运行小代码段或“函数”的解决方案。 可针对手头的问题编写所需代码，无需担心用来运行该代码的完整应用程序或基础结构。 函数连接到 Azure 存储和其他云托管资源中的事件。 数据通过函数参数流入 F# 函数。 可以使用所选择的开发语言，信任 Azure 按需进行扩展。

Azure Functions 支持 F# 作为第一类语言，它执行 F# 代码时高效、反应迅速且可缩放。 请参阅 [Azure Functions F# 开发人员参考](/azure/azure-functions/functions-reference-fsharp)，了解如何将 F# 用于 Azure Functions 的相关参考文档。

结合使用 Azure Functions 和 F# 的其他资源：

* [Scale Up Azure Functions in F# Using Suave](https://blog.tamizhvendan.in/blog/2016/09/19/scale-up-azure-functions-in-f-number-using-suave/)（使用 Suave 以 F# 扩展 Azure Functions）
* [How to create Azure function in F#](https://mnie.github.io/2016-09-08-AzureFunctions/)（如何以 F# 创建 Azure Functions）
* [使用 Azure Functions 和 Azure 类型提供程序](https://compositional-it.com/blog/2017/08-30-using-the-azure-type-provider-with-azure-functions/index.html)

## <a name="using-azure-storage-with-f"></a>使用 Azure 存储与 F\#

Azure 存储是一种基层存储服务，用于依赖于持久性、可用性和可缩放性来满足其客户需求的现代应用程序。 F#程序可以直接与 Azure 存储服务，使用以下文章中所述的技术进行交互。

* [通过 F# 实现 Azure Blob 入门](blob-storage.md)
* [通过 F# 实现 Azure 文件存储入门](file-storage.md)
* [通过 F# 实现 Azure 队列存储入门](queue-storage.md)
* [通过 F# 实现 Azure 表格存储入门](table-storage.md)

Azure 存储还可以通过声明性配置（而非显式 API 调用）与 Azure Functions 结合使用。 请参阅 [Azure Functions triggers and bindings for Azure Storage](/azure/azure-functions/functions-bindings-storage)（用于 Azure 存储的 Azure Functions 触发器和绑定），其中包括 F# 示例。

## <a name="using-azure-app-service-with-f"></a>使用 Azure 应用服务与 F\#

[Azure 应用服务](https://azure.microsoft.com/services/app-service/)是一个用于构建功能强大的 Web 和移动应用的云平台，这些应用可连接到任何位置（云中或本地）的数据。

* [F# Azure Web API 示例](https://github.com/fsprojects/azure-webapi-example)
* [Hosting F# in a web application on Azure](https://github.com/isaacabraham/fsharp-demonstrator)（在 Azure 上的 Web 应用程序中托管 F#）

## <a name="using-apache-spark-with-f-with-azure-hdinsight"></a>通过 Azure HDInsight 结合使用 Apache Spark 与 F#

[Apache Spark for Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/) 是一个开放源代码处理框架，用于运行大型数据分析应用程序。 Azure 使 Apache Spark 的部署简单且经济实惠。 通过 [Mobius](https://github.com/Microsoft/Mobius)（适用于 Spark 的 .NET API）使用 F# 开发 Spark 应用程序。

* [Implementing Spark Apps in F# using Mobius](https://github.com/Microsoft/Mobius/blob/master/notes/spark-fsharp-mobius.md)（使用 Mobius 以 F# 形式实现 Spark 应用）
* [使用 Mobius 的示例 F# Spark 应用](https://github.com/Microsoft/Mobius/tree/master/examples/fsharp)

## <a name="using-azure-cosmos-db-with-f"></a>使用 Azure Cosmos DB 与 F\#

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db)是高度可用的全球分布式应用的 NoSQL 服务。

Azure Cosmos DB 可与F#通过两种方式：

1. 通过创建F#Azure Functions 响应或导致对 Azure Cosmos DB 集合的更改。 请参阅[Azure Functions 的 Azure Cosmos DB 绑定](/azure/azure-functions/functions-bindings-cosmosdb)，或
2. 通过使用[用于 SQL API 的 Azure Cosmos DB.NET SDK](/azure/cosmos-db/sql-api-sdk-dotnet)。 相关的示例采用 C# 编写。

## <a name="using-azure-event-hubs-with-f"></a>使用 Azure 事件中心与 F\#

[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)提供来自网站、应用和设备的云规模遥测引入。

可采用两种方式结合使用 Azure 事件中心与 F#：

1. 通过创建由事件触发的 F# Azure Functions。 请参阅 [Azure Function 事件中心触发器](/azure/azure-functions/functions-bindings-event-hubs)，或
2. 通过使用[适用于 Azure 的 .NET SDK](/azure/event-hubs/event-hubs-csharp-ephcs-getstarted)。 请注意，这些示例使用的是 C#。

## <a name="using-azure-notification-hubs-with-f"></a>使用 Azure 通知中心与 F\#

[Azure 通知中心](/azure/notification-hubs/)是多平台扩展式推送基础结构，可使用它从任何后端（云中或本地）向任何移动平台发送移动推送通知。

可采用两种方式结合使用 Azure 通知中心与 F#：

1. 通过创建向通知中心发送结果的 F# Azure Functions。 请参阅 [Azure Functions 通知中心输出触发器](/azure/azure-functions/functions-bindings-notification-hubs)，或
2. 通过使用[适用于 Azure 的 .NET SDK](https://blogs.msdn.microsoft.com/azuremobile/2014/04/08/push-notifications-using-notification-hub-and-net-backend/)。 请注意，这些示例使用的是 C#。


## <a name="implementing-webhooks-on-azure-with-f"></a>通过 F 在 Azure 上实现 Webhook\#

[Webhook](https://en.wikipedia.org/wiki/Webhook) 是通过 Web 请求触发的回调。 Webhook 由 GitHub 等站点使用，用以向事件发送信号。

Webhook 可采用 F# 实现，并通过 [Azure Function in F# with a Webhook Binding](/azure/azure-functions/functions-bindings-http-webhook)（具有 Web 绑定的 F# Azure Function）在 Azure 上进行托管。

## <a name="using-webjobs-with-f"></a>使用 Webjob 与 F\#

[Webjob](/azure/app-service-web/web-sites-create-web-jobs) 是可采用以下三种方式在应用服务 Web 应用中运行的程序：按需、连续或按计划。

[示例 F# Webjob](https://github.com/jrr/webjob-project-examples)

## <a name="implementing-timers-on-azure-with-f"></a>通过 F 在 Azure 上实现计时器\#

计时器触发器基于计划调用一次或重复调用函数。

计时器可采用 F# 实现，并通过 [Azure Function in F# with a Timer Trigger](/azure/azure-functions/functions-bindings-timer)（具有计时器触发器的 F# Azure Function）在 Azure 上进行托管。

## <a name="deploying-and-managing-azure-resources-with-f-scripts"></a>使用 F# 脚本部署和管理 Azure 资源

可使用 Microsoft.Azure.Management 包和 API，以编程方式通过 F# 脚本部署和管理 Azure VM。 有关示例，请参阅 [.NET 管理库入门](https://msdn.microsoft.com/library/dn722415.aspx)和[使用 Azure 资源管理器](/azure/azure-resource-manager/resource-manager-deployment-model)。

同样，其他 Azure 资源也可用相同的组件通过 F# 脚本进行部署和管理。 例如，创建存储帐户、 部署 Azure 云服务、 创建 Azure Cosmos DB 实例和管理 Azure 通知中心以编程方式从F#脚本。

通常，使用 F# 脚本来部署和管理资源并不必要。 例如，还可以直接从可参数化的 JSON 模板说明部署 Azure 资源。 请参阅 [Azure 资源管理器模板](/azure/azure-resource-manager/resource-manager-template-best-practices)，包括 [Azure 快速入门模板](https://azure.microsoft.com/resources/templates/)等示例。

## <a name="other-resources"></a>其他资源

* [有关所有 Azure 服务的完整文档](/azure/)
