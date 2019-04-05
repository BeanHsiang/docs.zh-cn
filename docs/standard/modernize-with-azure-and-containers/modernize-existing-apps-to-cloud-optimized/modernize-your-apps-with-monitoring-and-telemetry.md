---
title: 通过监视和遥测对应用进行现代化
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |通过监视和遥测对应用进行现代化
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/30/2018
ms.openlocfilehash: 7776edd91f73aa6ca74b82ae4d144635bb6c36a4
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53147471"
---
# <a name="modernize-your-apps-with-monitoring-and-telemetry"></a>通过监视和遥测对应用进行现代化

在生产环境中运行应用程序时，很重要，必须了解你的应用程序的执行有关的见解。 它执行在高级别？ 用户收到错误，或是稳定和可靠的应用程序？ 需要丰富的性能监视、 功能强大警报和仪表板，帮助确保你的应用程序可用并且按预期执行。 此外需要能够快速查看是否有问题，确定多少客户会受到影响，并执行根本原因分析，以查找并修复该问题。

## <a name="monitor-your-application-with-application-insights"></a>监视应用程序使用 Application Insights

Application Insights 是面向 web 开发人员可以在多个平台上的可扩展应用程序性能管理 (APM) 服务。 使用它监视实时 web 应用程序。 Application Insights 会自动检测性能异常。 它包括强大的分析工具来帮助你诊断问题，并帮助你了解用户实际使用你的应用。 Application Insights 旨在帮助持续提高性能和可用性。 它在各种平台，包括.NET、 Node.js 和 J2EE，是否适用于应用托管在本地或云中。 Application Insights 集成，与您的 DevOps 流程，并具有与各种开发工具的连接点。

图 4-10 演示了如何 Application Insights 监视你的应用程序和它如何到仪表板中显示这些见解的示例。

![Application Insights 监视仪表板](./media/image10.png)

> **图 4-10。** Application Insights 监视仪表板

## <a name="monitor-your-docker-infrastructure-with-log-analytics-and-its-container-monitoring-solution"></a>监视 Docker 基础结构与 Log Analytics 和其容器监视解决方案

[Azure Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)属于[Microsoft Azure 总体监视解决方案](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)。 它也是服务[Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)。 Log Analytics 监视云并在本地环境 (在内部部署的 OMS) 可帮助维护可用性和性能。 它可以收集资源和其他监视工具来跨多个源提供分析云和本地环境中生成的数据。

相对于 Azure 基础结构日志，Log Analytics 作为 Azure 服务，引入日志和指标数据从其他 Azure 服务 (通过[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor))，Azure Vm、 Docker 容器，并在本地或其他云基础结构。 Log Analytics 提供灵活的日志搜索和现成的-分析此数据的基础。 它提供了丰富的工具，可用于跨源分析数据，这样复杂的查询将针对所有日志，并可以主动发出警报根据指定的条件。 甚至可以收集自定义数据中心 Log Analytics 存储库中，您可以在其中查询和可视化这些数据。 您还可以充分利用 Log Analytics 内置解决方案，以立即深入了解安全性和基础结构的功能。

可以通过 OMS 门户中或在任何浏览器中运行，在 Azure 门户访问 Log Analytics，并提供可以访问配置设置和多个工具来分析和处理收集的数据。

[容器监视解决方案](https://docs.microsoft.com/azure/log-analytics/log-analytics-containers)中 Log Analytics 可帮助您查看和管理 Docker 和 Windows 容器主机在一个位置。 此解决方案显示哪些容器正在运行，哪些容器映像运行它们，以及运行容器。 可以查看详细的审核信息，包括与容器一起使用的命令。 此外可以通过查看和搜索集中式的日志，而无需远程查看 Docker 或 Windows 的主机来排查容器。 您可以找到可能会干扰并花费较长的主机上的过多资源的容器。 此外，您可以查看集中式的 CPU、 内存、 存储和网络使用情况和性能信息，为容器。 在运行 Windows 的计算机，您可以集中并比较日志从 Windows Server HYPER-V 和 Docker 容器。 该解决方案支持以下容器业务流程协调程序：

-   Docker Swarm

-   DC/OS

-   Kubernetes

-   Service Fabric

-   Red Hat OpenShift

图 4-11 显示了各种容器主机和代理和 OMS 之间的关系。

![Log Analytics 容器监视解决方案](./media/image11.png)

> **图 4-11。** Log Analytics 容器监视解决方案

可以使用的 Log Analytics 容器监视解决方案：

-   请参阅有关在单个位置所有容器主机的信息。

-   知道哪些容器正在运行，哪些映像运行它们，并运行位置。

-   请参阅在容器上的操作的审核线索。

-   通过查看和搜索而无需远程登录到 Docker 主机的集中化的日志进行故障排除。

-   查找可能是"噪声邻居，"并在消耗过多资源的主机上的容器。

-   查看集中式的 CPU、 内存、 存储和网络使用情况和性能信息，为容器。

### <a name="additional-resources"></a>其他资源

-   **Microsoft Azure 中的监视概述**

[https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

-   **什么是 Application Insights？**

[https://docs.microsoft.com/azure/application-insights/app-insights-overview](https://docs.microsoft.com/azure/application-insights/app-insights-overview)

-   **什么是 Log Analytics？**

[https://docs.microsoft.com/azure/log-analytics/log-analytics-overview](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

-   **在 Log Analytics 中的容器监视解决方案**

[https://docs.microsoft.com/azure/log-analytics/log-analytics-containers](https://docs.microsoft.com/azure/log-analytics/log-analytics-containers)

-   **Azure Monitor 概述**

[https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor)

-   **什么是 Operations Management Suite (OMS)？**

[https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

-   **监视 Service Fabric 和 OMS 中的 Windows Server 容器**

[https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-containers-windowsserver](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-containers-windowsserver)

>[!div class="step-by-step"]
>[上一页](build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud.md)
>[下一页](modernize-your-apps-lifecycle-with-ci-cd-pipelines-and-devops-tools-in-the-cloud.md)