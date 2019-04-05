---
title: 关于 ASP.NET Core Web 应用的 Azure 托管建议
description: 使用 ASP.NET Core 和 Azure 构建新式 Web 应用程序 | 关于 ASP.NET Web 应用的 Azure 托管建议
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: cda4c002c73e2dd0db1b2d5d1fa8bc76903c5c62
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55828379"
---
# <a name="azure-hosting-recommendations-for-aspnet-core-web-apps"></a>关于 ASP.NET Core Web 应用的 Azure 托管建议

> “全球各地的业务线领导绕过 IT 部门，从云获取应用程序（又称 SaaS）并支付使用费用，就像订阅杂志一样。 不再需要服务时，他们可取消订阅，不会出现设备闲置的情况。”  
> \-Gartner 分析师 Daryl Plummer

无论面对何种应用程序需要和体系结构，Microsoft Azure 均可提供支持。 托管需求可以非常简单（例如静态网站），也可以非常复杂（例如由多个服务组成的复杂的应用程序）。 对于 ASP.NET Core 整体 Web 应用程序和支持服务，推荐以下几种常见配置。 无论是完整应用程序、单个进程或数据，本文中的建议配置均按待托管资源的类型分组。

## <a name="web-applications"></a>Web 应用程序

可通过以下方式托管 Web 应用程序：

- 应用服务 Web 应用

- 容器

- Azure Service Fabric

- 虚拟机 (VM)

其中，对于大多数方案，推荐使用应用服务 Web 应用方法。 对于微服务体系结构，请考虑使用基于容器的方法或 Service Fabric。 如果需要更好地控制运行应用程序的计算机，请考虑使用 Azure 虚拟机。

### <a name="app-service-web-apps"></a>应用服务 Web 应用

应用服务 Web 应用提供的完全托管平台针对托管 Web 应用程序进行了优化。 它是一种平台即服务 (PaaS) 产品/服务，可使你专注于业务逻辑，而由 Azure 负责维护应用运行和缩放所需的基础结构。 应用服务 Web 应用的一些关键功能：

- DevOps 优化（持续集成和交付、多环境、A/B 测试和脚本支持）。

- 全球缩放和高可用性。

- 可连接至 SaaS 平台和本地数据。

- 安全性和符合性。

- Visual Studio 集成。

Azure 应用服务是适合大多数 Web 应用的最佳选择。 该平台集成部署与管理，站点可快速缩放以处理高流量负载，内置负载均衡和流量管理器提供高可用性。 可通过在线迁移工具将现有站点轻松移动到 Azure 应用服务、使用 Web 应用程序库中的开源应用或使用框架和你选择的工具创建新的站点。 通过 WebJobs 功能可将后台作业处理轻松添加到应用服务 Web 应用。

### <a name="azure-kubernetes-service"></a>Azure Kubernetes 服务

Azure Kubernetes 服务 (AKS) 管理托管的 Kubernetes 环境，即使没有容器业务流程专业知识，也可快速轻松地部署和管理容器化应用程序。 此外，它还通过预配、升级和按需缩放资源，消除了持续操作和维护的负担，而无需应用程序脱机。

通过将大量责任转移至 Azure，AKS 降低了管理 Kubernetes 群集的复杂性和运营开销。 作为一项托管的 Kubernetes 服务，Azure 将为你处理运行状况监视和维护等关键任务。 并且，你仅需支付群集中的代理节点，而无需支付主节点。 作为一项托管的 Kubernetes 服务，AKS 提供以下功能：

- 自动化的 Kubernetes 版本升级和修补。
- 轻松的群集缩放。
- 自我修复型托管控制平面（主节点）。
- 节省成本：仅支付运行的代理池节点。

由于 Azure 会负责管理 AKS 群集中的节点，因此，很多任务（例如群集升级）不再需要手动执行。 由于 Azure 会处理这些关键维护任务，因此，AKS 不提供对群集的直接访问（例如使用 SSH）。

### <a name="azure-service-fabric"></a>Azure Service Fabric

如果要创建新应用或重新编写现有应用以使用微服务体系结构，Service Fabric 是一个不错的选择。 在计算机共享池上运行的应用可能开始规模很小，然后逐渐规模扩大，根据需要可能具有成百上千台计算机。 通过有状态服务可一致而可靠地存储应用状态，并且 Service Fabric 会自动管理服务分区、缩放和可用性。 Service Fabric 还通过 Open Web Interface for .NET (OWIN) 和 ASP.NET Core 支持 WebAPI。 与应用服务相比，Service Fabric 还提供对底层基础结构的更多控制或直接访问。 可远程连接到服务器或配置服务器启动任务。

### <a name="azure-virtual-machines"></a>Azure 虚拟机

如果现有应用需要经过大量修改才可在应用服务或 Service Fabric 中运行，为简化迁移到云，可选择虚拟机。 然而，与 Azure 应用服务和 Service Fabric 相比，正确配置、保护和维护 VM 需要更多时间和 IT 专业知识。 如要使用 Azure 虚拟机，请务必考虑到 VM 环境的修补、更新和管理所需的持续性维护工作。 Azure 虚拟机属于基础结构即服务 (IaaS)，而应用服务和 Service Fabric 属于 PaaS。

#### <a name="feature-comparison"></a>功能比较

| 功能                                                                                    | 应用服务 | 容器 (AKS) | Service Fabric | 虚拟机 |
| ------------------------------------------------------------------------------------------ | ----------- | ---------------- | -------------- | --------------- |
| 近即时部署                                                                    | X           | X                | X              |                 |
| 无需重新部署即可扩展至较大的计算机                                               | X           | X                | X              |                 |
| 实例共享内容和配置；缩放时无需重新部署或重新配置 | X           | X                | X              |                 |
| 多部署环境（生产、暂存）                                     | X           | X                | X              |                 |
| 自动操作系统更新管理                                                             | X           | X                |                |                 |
| 32/64 位平台无缝切换                                             | X           | X                |                |                 |
| 使用 Git 和 FTP 部署代码                                                                  | X           | X                |                | X               |
| 使用 WebDeploy 部署代码                                                                 | X           | X                |                | X               |
| 使用 TFS 部署代码                                                                       | X           | X                | X              | X               |
| 托管多层体系结构的 Web 或 Web 服务层                                    | X           | X                | X              | X               |
| 访问服务总线、存储、SQL 数据库等 Azure 服务                              | X           | X                | X              | X               |
| 安装任何自定义 MSI                                                                     |             | X                | X              | X               |

## <a name="logical-processes"></a>逻辑进程

对于可从应用程序的剩余部分分离的单独逻辑进程，可以“无服务器”方式将其独立部署到 Azure Functions。 通过 Azure Functions 可编写解决特定问题所需的代码，无需担心运行它的应用程序或基础结构。 可选择各种编程语言，包括 C\#、F\#、Node.js、Python 和 PHP，以便你选择一种最高效语言来处理手头任务。 与多数基于云的解决方案一样，仅需为使用的时间量支付费用，而且 Azure Functions 按需扩展非常可靠。

## <a name="data"></a>数据

Azure 提供多种数据存储选择，以便应用程序可使用恰当的数据提供程序处理相关数据。

对于事务和关系数据，Azure SQL 数据库是最佳选择。 对于以读取为主的高性能数据，受 Azure SQL 数据库支持的 Redis 缓存是一个不错的解决方案。

可使用多种方式存储非结构化 JSON 数据，包括 SQL 数据库列、Blob、Azure 存储中的表以及 Cosmos DB。 其中，Cosmos DB 提供最佳查询功能，建议用于必须支持查询的大量基于 JSON 的文档。

暂时命令或者用于安排应用程序行为的基于事件的数据可使用 Azure 服务总线或 Azure 存储队列。 Azure 存储总线具有更强的灵活性，建议将该服务用于处理应用程序内和应用程序间的非普通消息传递。

## <a name="architecture-recommendations"></a>体系结构建议

应用程序要求应决定其体系结构。 有多种不同的 Azure 服务可供使用。 选择正确的服务是一项重要决定。 Microsoft 提供一系列参考体系结构，帮助用户确定针对常见方案优化的典型体系结构。 可找到一个与应用程序要求高度契合或至少提供一个出发点的参考体系结构。

图 11-2 显示了一个示例参考体系结构。 该图介绍了一个建议用于为市场营销而优化的 Sitecore 内容管理系统网站的体系结构方式。

![](./media/image11-2.png)

**Figure 11-1**。 Sitecore 市场营销网站参考体系结构。

**参考：Azure 托管建议**

- Azure解决方案体系结构\
  <https://azure.microsoft.com/solutions/architecture/>

- Azure 开发人员指南\
  <https://azure.microsoft.com/campaigns/developer-guide/>

- Web 应用概述\
  <https://docs.microsoft.com/azure/app-service/app-service-web-overview>

- Azure 应用服务、虚拟机、Service Fabric 和云服务的比较\
  <https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm>

- Azure Kubernetes 服务 (AKS) 简介\
  <https://docs.microsoft.com/azure/aks/intro-kubernetes>

>[!div class="step-by-step"]
>[上一篇](development-process-for-azure.md)