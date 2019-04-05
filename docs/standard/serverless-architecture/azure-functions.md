---
title: Azure Functions 的无服务器应用
description: Azure functions 提供无服务器功能跨多个语言 （C#、 JavaScript、 Java） 和平台提供事件驱动即时缩放代码。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 2d8729276a5797bd8b89c39d8fb03c6f20646ea0
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53145158"
---
# <a name="azure-functions"></a>Azure Functions

Azure functions 提供无服务器计算体验。 通过调用函数*触发器*（如访问 HTTP 终结点或计时器） 并执行代码或业务逻辑的块。 函数还支持专用*绑定*，连接到存储和队列等资源。

![Azure functions 徽标](./media/azure-functions-logo.png)

有两个版本的 Azure 功能框架。 旧的版本支持完整的.NET Framework 和新的运行时支持跨平台.NET Core 应用程序。 除了其他语言C#JavaScript 中，如F#，并支持 Java。 在门户中创建的函数提供了丰富的脚本语法。 可以使用完整的平台支持和功能部署作为独立项目创建的函数。

有关详细信息，请参阅[Azure Functions 文档](https://docs.microsoft.com/azure/azure-functions)。

## <a name="functions-v1-vs-v2"></a>函数 v1 与 v2

有两个版本的 Azure Functions 运行时：1.x 和 2.x。 版本 1.x 已正式推出 (GA)。 它支持从门户或 Windows 计算机的.NET 开发，并使用.NET Framework。 1.x 支持C#，JavaScript，和F#，使用 Python、 PHP、 TypeScript、 Batch、 Bash、 和 PowerShell 的实验性支持。

版本 2.x 处于预览状态。 它利用.NET Core，并支持 Windows、 macOS 和 Linux 计算机上的跨平台开发。 2.x 添加了适用于 Java 的一流支持，但尚不直接支持的任何实验性语言。 版本 2.x 使用新的绑定扩展性模型，从而使第三方扩展到平台独立的版本控制的绑定，并更简化的执行环境。

> **与 1.x 中没有的已知的问题[绑定重定向支持](https://github.com/Azure/azure-functions-host/issues/992)。** 问题是特定于.NET 开发。 依赖库的运行时中包括的库中的不同版本的项目会受到影响。 功能团队已致力于具体进度有关的问题。 它将进入正式发布之前，团队将解决在 2.x 中的绑定重定向。 此处提供了官方团队语句中使用的建议修补程序和解决方法：[在 Azure Functions 中的程序集解析](https://github.com/Azure/azure-functions-host/wiki/Assembly-Resolution-in-Azure-Functions)。

有关详细信息，请参阅[比较 1.x 和 2.x](https://docs.microsoft.com/azure/azure-functions/functions-versions)。

## <a name="programming-language-support"></a>编程语言支持

支持以下语言或者在一般情况下发布 (GA) 预览，或实验性。

|语言      |1.x         |2.x      |
|--------------|------------|---------|
|**C#**        |GA          |预览  |
|**JavaScript**|GA          |预览  |
|**F#**        |GA          |         |
|**Java**      |            |预览  |
|**Python**    |实验|         |
|**PHP**       |实验|         |
|**TypeScript**|实验|         |
|**Batch**     |实验|         |
|**Bash**      |实验|         |
|**PowerShell**|实验|         |

有关详细信息，请参阅[支持的语言](https://docs.microsoft.com/azure/azure-functions/supported-languages)。

## <a name="app-service-plans"></a>应用服务计划

受支持的函数*应用服务计划*。 该计划定义的函数应用使用的资源。 可以将计划分配到某个区域，确定的大小和数量的虚拟机将使用，并选择定价层。 为 true 的无服务器方案，可以使用函数应用**消耗**计划。 消耗计划后端根据负载自动缩放。

有关详细信息，请参阅[应用服务计划](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)。

## <a name="create-your-first-function"></a>创建第一个函数

有三种常见方法，您可以创建函数应用。

* 在门户中的脚本函数。
* 创建使用 Azure 命令行接口 (CLI) 所需的资源。
* 生成函数，使用你喜爱的 IDE 在本地，并将其发布到 Azure。

在门户中创建的脚本化的函数的详细信息，请参阅[Azure 门户中创建第一个函数](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function)。

若要从 Azure CLI 生成，请参阅[创建第一个函数使用 Azure CLI](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function-azure-cli)。

若要从 Visual Studio 创建一个函数，请参阅[创建第一个函数使用 Visual Studio](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio)。

## <a name="understand-triggers-and-bindings"></a>了解触发器和绑定

通过调用函数*触发器*和恰好有一个。 除了调用函数，某些触发器还充当绑定。 你还可以定义除了触发器的多个绑定。 *绑定*提供的声明性方式将数据连接到你的代码。 它们可以传入 （输入），或接收数据 （输出）。 触发器和绑定使函数更易使用。 绑定中删除手动创建数据库或文件系统连接的系统开销。 所有绑定所需的信息都包含在一个特殊*functions.json*脚本文件，或者使用代码中的属性声明。

一些常见的触发器包括：

* Blob 存储： 文件或文件夹上传或在存储中发生更改时调用您的函数。
* HTTP： 调用 REST API 等函数。
* 队列： 调用函数时队列中存在的项。
* 计时器： 调用上一般的步调函数。

绑定的示例包括：

* Cosmos Db： 轻松连接到要加载或保存文件的数据库。
* 表存储： 适用于从 function app 的键/值存储。
* 队列存储： 轻松地从队列中检索项，或将新项放入队列。

下面的示例*functions.json*文件定义一个触发器和绑定：

```json
{
  "bindings": [
    {
      "name": "myBlob",
      "type": "blobTrigger",
      "direction": "in",
      "path": "images/{name}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "$return",
      "type": "queue",
      "direction": "out",
      "queueName": "images",
      "connection": "AzureWebJobsStorage"
    }
  ],
  "disabled": false
}
```

在此示例中，该函数对 blob 存储中的更改触发`images`容器。 文件的信息传入，因此触发器还可作为一个绑定。 存在另一个绑定以将信息到名为的队列上放`images`。

以下是 C# 脚本函数：

```csharp
public static string Run(Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
    return name;
}
```

该示例是采用文件的名称的简单函数已修改或上传到 blob 存储，并将其放置于队列上供以后处理。

有关触发器和绑定的完整列表，请参阅[Azure Functions 触发器和绑定概念](https://docs.microsoft.com/azure/azure-functions/functions-triggers-bindings)。

## <a name="proxies"></a>代理

代理为你的应用程序提供重定向功能。 代理公开一个终结点，并将该终结点映射到另一个资源。 使用代理，你可以：

* 重新路由到其他终结点的传入请求。
* 传递此过程之前，请修改传入的请求。
* 修改或提供了一个响应。

使用代理的方案例如：

* 简化、 缩短，或更改 URL。
* 提供多个后端服务的一致 API 前缀。
* 模拟正在开发的终结点的响应。
* 提供的已知终结点的静态响应。
* 保持 API 终结点时移动或迁移后端一致。

代理存储为 JSON 定义。 下面是一个示例：

```json
{
  "$schema": "http://json.schemastore.org/proxies",
  "proxies": {
    "Domain Redirect": {
      "matchCondition": {
        "route": "/{shortUrl}"
      },
      "backendUri": "http://%WEBSITE_HOSTNAME%/api/UrlRedirect/{shortUrl}"
    },
    "Root": {
      "matchCondition": {
        "route": "/"
      },
      "responseOverrides": {
        "response.statusCode": "301",
        "response.statusReason": "Moved Permanently",
        "response.headers.location": "https://docs.microsoft.com/"
      }
    }
  }
}
```

`Domain Redirect`代理需要缩短的路由并将其映射到更长的函数资源。 转换如下所示：

`https://--shorturl--/123` -> `https://--longurl--.azurewebsites.net/api/UrlRedirect/123`

`Root`代理会发送到的根 URL 的任何内容 (`https://--shorturl--/`) 并将它重定向到文档站点。

使用代理的示例所示视频[Azure:将应用迁移到使用无服务器 Azure Functions 在云中](https://channel9.msdn.com/events/Connect/2017/E102)。 在真实时间中在本地 SQL Server 上运行的 ASP.NET Core 应用程序迁移到 Azure 云。 使用代理服务器来帮助重构传统的 Web API 项目以使用函数。

有关代理的详细信息，请参阅[使用 Azure Functions 代理](https://docs.microsoft.com/azure/azure-functions/functions-proxies)。

>[!div class="step-by-step"]
>[上一页](azure-serverless-platform.md)
>[下一页](application-insights.md)