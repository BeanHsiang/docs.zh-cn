---
title: 生成可复原的准备好使用云服务。 包含在云中的暂时性故障
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |生成可复原的准备好使用云服务。 包含在云中的暂时性故障
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/30/2018
ms.openlocfilehash: 801d017457d1cdc3c8a495c8127b203380cb1d9e
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56971827"
---
# <a name="build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud"></a>生成可复原的准备好使用云服务：包含在云中的暂时性故障

恢复能力是指从故障中恢复并继续工作的能力。 复原能力不是有关避免故障发生，但接受这一事实，将出现故障，并可避免停机或数据丢失的方式对其然后作出响应。 恢复的目标是使应用程序在发生故障后回到完全正常运行的状态。

最小值，它实现了基于软件的模型的复原能力，而不是基于硬件的模型时，你的应用程序准备好使用云。 云应用程序必须接受必然会发生部分失败。 设计或部分重构应用程序以实现预期的部分故障的复原能力。 它应设计为处理部分故障，如暂时性网络中断和节点或在云中崩溃的 Vm。 甚至要移动到另一个节点的业务流程协调程序群集中的容器可能会导致应用程序中的间歇性短失败。

## <a name="handling-partial-failure"></a>处理部分失败错误

在基于云的应用程序，没有经常会出现部分失败错误。 例如，单个网站实例或容器可能会失败，也可能是不可用或在短时间无响应。 或者，单个 VM 或服务器可能会崩溃。

客户端和服务的单独进程，因为服务可能无法及时地响应客户端的请求。 可重载和响应速度慢的请求，服务也可能不是短时间内访问由于网络问题。

例如，考虑访问 Azure SQL 数据库中的数据库的整体化.NET 应用程序。 如果 Azure SQL 数据库或任何其他第三方服务为响应针对一条简短时间 （Azure SQL 数据库可能移动到另一个节点或服务器，并在几秒内无响应），当用户尝试执行任何操作，该应用程序可能会崩溃和显示w 异常在同一时间点。

中的应用程序使用 HTTP 的服务可能出现类似的方案。 网络或服务本身可能不能在云中较短的暂时性故障。

图 4-9 所示的可复原应用程序应实现技术，例如"重试使用指数退避算法"以便应用程序有机会处理资源中的暂时性故障。 此外应在应用程序中使用"断路器"。 断路器会停止应用程序尝试访问资源时实际上长期故障。 通过使用断路器，该应用程序可避免人深受启发拒绝到其自身的服务。

![通过使用指数退避算法的重试处理部分故障](./media/image9.png)

> **图 4-9。** 通过使用指数退避算法的重试处理部分故障

在 HTTP 资源和数据库资源，可以使用这些技术。 在图 4-9、 应用程序基于第 3 层体系结构，因此您需要在服务级别 (HTTP) 和数据层级别 (TCP) 这些技术。 在使用仅除了数据库 （任何其他服务或微服务） 的单个应用程序层的单一式应用程序，处理暂时性故障级别的数据库的连接可能已足够。 在这种情况下，只是特定的数据库连接的配置都需要。

实现访问数据库时，具体取决于使用的，.NET 版本的弹性通信时它可能比较简单 (例如， [Entity Framework 6 或更高版本](/ef/ef6/fundamentals/connection-resiliency/retry-logic)。 它是只需配置数据库连接。） 或者，可能需要使用其他库等[暂时性故障处理应用程序块](https://docs.microsoft.com/previous-versions/msp-n-p/hh680934(v=pandp.50))（适用于早期版本的.NET），或者甚至实现您自己的库。

实现 HTTP 重试次数和断路器时，.NET 的推荐方法是使用[Polly](https://github.com/App-vNext/Polly)库，后者面向.NET Framework 4.0、.NET Framework 4.5 和.NET Standard 1.1，包括.NET Core 的支持。

若要了解如何实现处理云中的部分失败的策略，请参阅以下参考资料。

### <a name="additional-resources"></a>其他资源

-   **实现弹性通信来处理部分失败错误**

    [https://docs.microsoft.com/dotnet/standard/microservices-architecture/implement-resilient-applications/partial-failure-strategies](../../microservices-architecture/implement-resilient-applications/partial-failure-strategies.md)

-   **实体框架连接复原和重试逻辑 （6 和更高版本）**

    [https://docs.microsoft.com/ef/ef6/fundamentals/connection-resiliency/retry-logic](/ef/ef6/fundamentals/connection-resiliency/retry-logic)

-   **暂时性故障处理应用程序块**

-   <https://docs.microsoft.com/previous-versions/msp-n-p/hh680934(v=pandp.50)>

-   **Polly 适用于弹性 HTTP 通信库**

    https://github.com/App-vNext/Polly

>[!div class="step-by-step"]
>[上一页](when-to-deploy-windows-containers-to-azure-container-service-kubernetes.md)
>[下一页](modernize-your-apps-with-monitoring-and-telemetry.md)
