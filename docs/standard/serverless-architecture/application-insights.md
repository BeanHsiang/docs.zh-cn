---
title: Application Insights-无服务器应用
description: Application Insights 是一个无服务器诊断平台，使开发人员能够检测、 会审和诊断 web 应用、 移动应用、 桌面应用程序和微服务中的问题。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: b4884d483de07c1c2077f7280b6b77c6059572c0
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53154251"
---
# <a name="telemetry-with-application-insights"></a>使用 Application Insights 的遥测数据

[Application Insights](https://docs.microsoft.com/azure/application-insights)是一个无服务器诊断平台，使开发人员能够检测、 会审和诊断 web 应用、 移动应用、 桌面应用程序和微服务中的问题。 您可以启用 Application Insights 为函数应用只需通过在门户中扳动开关。 Application Insights 提供所有这些功能而无需配置服务器，或者设置您自己的数据库。 作为自动与您的应用程序集成的服务提供的所有 Application Insights 的功能。

![应用程序见解徽标](./media/application-insights-logo.png)

将 Application Insights 添加到现有应用程序非常简单，只需作为将检测密钥添加到应用程序的设置。 使用 Application Insights，你可以：

* 创建自定义图表和警报基于指标，如函数调用数，运行一个函数和异常所需的时间
* 分析故障和服务器异常
* 操作通过钻取到性能和度量值来调用第三方依赖项所花费的时间
* 监视托管函数应用的所有服务器上的 CPU 使用情况、 内存和费率
* 查看指标，包括请求计数和延迟为函数应用的实时流
* 使用[Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics)要搜索，请查询，并对函数数据创建自定义图表

![指标资源管理器](./media/metrics-explorer.png)

除了内置的遥测数据，还有可能生成自定义遥测数据。 下面的代码段将创建使用设置为函数应用的检测密钥的自定义遥测客户端：

```csharp
public static TelemetryClient telemetry = new TelemetryClient()
{
    InstrumentationKey = Environment.GetEnvironmentVariable("APPINSIGHTS_INSTRUMENTATIONKEY")
};
```

下面的代码度量值插入新行插入所需的时间长度[Azure 表存储](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)实例：

```csharp
var operation = TableOperation.Insert(entry);
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
await table.ExecuteAsync(operation);
telemetry.TrackDependency("AzureTableStorageInsert", "Insert", startTime, timer.Elapsed, true);
```

生成的性能图所示：

![自定义遥测](./media/custom-telemetry.png)

自定义遥测就会发现以插入新行的平均时间是 32.6 毫秒为单位。

Application Insights 提供强大而方便的方法来记录有关无服务器应用程序的详细遥测数据。 你可以完全控制的跟踪级别，提供的日志记录，它是。 你可以跟踪自定义统计信息，例如事件、 依赖项和页面视图。 最后，功能强大的分析，可以编写查询的重要提问并生成图表和高级的见解。

有关详细信息，请参阅[监视 Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-monitoring)。

>[!div class="step-by-step"]
>[上一页](azure-functions.md)
>[下一页](logic-apps.md)