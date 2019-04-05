---
title: 监视容器化应用程序服务
description: 了解监视容器体系结构的一些重要层面
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 925db543617deb28590cf6631ebbda3ee96836c4
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56975740"
---
# <a name="monitor-containerized-application-services"></a>监视容器化应用程序服务

很重要的拆分为多个容器和微服务的应用程序具有一种方法来监视和分析整个应用程序的行为。

## <a name="microsoft-application-insights"></a>Microsoft Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview)是一项可扩展分析服务，用于监视实时应用程序。 它可帮助你检测和诊断性能问题以及了解用户实际使用你的应用。 它专为开发人员的意图是为了帮助您不断提高的性能和可用性的服务或应用程序。 Application Insights 适用于 web/服务和独立上各种不同的平台，如.NET、 Java、 Node.js 和许多其他平台，托管在本地或云中的应用程序。

### <a name="analyzing-docker-apps-in-qa-environments-using-application-insights"></a>分析在 QA 环境中使用 Application Insights 的 Docker 应用

因为它涉及到 Docker，可以绘制生命周期事件和性能计数器从 Application Insights 上的 Docker 容器。 只需运行[应用程序见解 Docker 映像](https://hub.docker.com/r/microsoft/applicationinsights/)如的容器中你的主机，它将显示性能计数器的主机也与其他 Docker 映像。 此应用程序见解 Docker 映像 (图 6-1） 可帮助你通过将收集有关性能和活动的 Docker 主机 (即，在 Linux Vm)、 Docker 容器和运行的应用程序的遥测数据来监视容器化应用程序在其中。

![示例](./media/image1.png)

**图 6-1**. Application Insights 监视 Docker 主机和容器

在运行时[应用程序见解 Docker 映像](https://hub.docker.com/r/microsoft/applicationinsights/)Docker 主机上你利用以下：

- 有关在主机上运行的所有容器的遥测数据的生命周期-启动、 停止和其他操作。

- 所有容器的性能计数器：CPU、 内存、 网络使用情况和的详细信息。

- 如果还安装了[Application Insights SDK](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net)在容器中运行的应用，这些应用程序的所有遥测数据将具有识别容器和主机计算机的其他属性。 因此，例如，如果有多个主机中运行的应用的实例，您将轻松能够筛选由主机应用程序遥测数据。

### <a name="setting-up-application-insights-to-monitor-docker-applications-and-docker-hosts"></a>设置 Application Insights 监视 Docker 应用程序和 Docker 主机

若要创建 Application Insights 资源时，请遵循后面的列表中显示的文章中的说明。 Azure 门户将为您创建所需的脚本。

- **在 Application Insights 中监视 Docker 应用程序：** \
  <https://docs.microsoft.com/azure/application-insights/app-insights-docker>

- **在 Docker 中心和 GitHub 的应用程序见解 Docker 映像：** \
  <https://hub.docker.com/r/microsoft/applicationinsights/> 和 \
  <https://github.com/Microsoft/ApplicationInsights-Docker>

- **为 ASP.NET web 应用和 ASP.NET Core 设置 Application Insights:** \
  <https://docs.microsoft.com/azure/application-insights/app-insights-asp-net>

- **适用于网页的 application Insights:**  
  <https://docs.microsoft.com/azure/application-insights/app-insights-javascript>

## <a name="security-backup-and-monitoring-services"></a>安全、 备份和监视服务

有许多支持零碎工作具有大量你需要处理以确保你的应用程序和基础结构中前陷波条件，以支持业务需求的详细信息，这种情况变得更加复杂的微服务领域，因此您需要一种方法当您需要采取措施时具有高级别和详细视图。

Azure 提供的工具来管理并提供在云中和本地资源的四个关键方面的统一的视图：

- **安全**。 与[Azure 安全中心](https://azure.microsoft.com/services/security-center/)。
  - 获取完整的可见性和控制虚拟机、 应用和工作负荷的安全性。
  - 集中你的安全策略的管理，并集成现有流程和工具。
  - 检测到使用高级分析真正的威胁。

- **备份**。 与[Azure 备份](https://azure.microsoft.com/services/backup/)。
  - 避免成本高昂的业务中断，满足符合性目标，并保护数据免受勒索软件和人为错误。
  - 保留备份数据在传输过程中和静止加密。
  - 请确保访问基于多重身份验证，以防止未经授权的使用。

- **监视**。 与[Azure 监视](https://azure.microsoft.com/solutions/monitoring/)， [Log Analytics](https://azure.microsoft.com/services/log-analytics/)，并[Application Insights](https://azure.microsoft.com/services/application-insights/)。
  - 获取完整的可见性的运行状况和性能的 Azure 工作负荷、 应用和基础结构。
  - 从任何源收集数据，获取丰富见解的虚拟机、 容器和应用程序。
  - 查找您需要使用交互式查询和全文搜索的信息。 
  - 执行根本原因分析使用高级分析，包括机器学习算法。

- **本地资源**。 与[真正一致的混合云](https://azure.microsoft.com/resources/truly-consistent-hybrid-cloud-with-microsoft-azure/)。

>[!div class="step-by-step"]
>[上一页](manage-production-docker-environments.md)
>[下一页](../key-takeaways/index.md)
