---
title: 管理 Docker 生产环境
description: 初步了解用于管理基于容器的生产环境的关键点。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: f3cf9bc281e94f342cecb1083d886daba03c019d
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56836612"
---
# <a name="manage-production-docker-environments"></a>管理 Docker 生产环境

群集管理和业务流程是控制的主机组的过程。 这可能涉及从添加和删除主机群集，获取有关主机和容器的当前状态的信息并开始和停止进程。 群集管理和业务流程与计划因为计划程序必须能够访问每个主机群集中以便计划服务密切相关。 出于此原因，同一个工具通常用于这两种用途。

## <a name="container-service-and-management-tools"></a>容器服务和管理工具

容器服务提供了快速部署流行的开源容器群集和业务流程解决方案。 它使用 Docker 映像以确保应用程序容器完全可移植。 通过使用容器服务，你可以部署 DC/OS （由 Mesosphere 和 Apache Mesos 提供支持） 和 Docker Swarm 群集使用 Azure 资源管理器模板或 Azure 门户，以确保你可以缩放到数千个这些应用程序 — 甚至数万个 — 的容器。

使用 Azure 虚拟机规模集，部署这些群集和群集充分利用 Azure 网络和存储产品/服务。 若要访问容器服务，你需要 Azure 订阅。 与容器服务中，可以同时仍维护应用程序可移植性，包括业务流程层充分利用 Azure 的企业级功能。

表 6-1 列出了其业务流程协调程序、 计划程序和聚类分析平台相关的常见管理工具。

**表 6-1**。 Docker 管理工具

| 管理工具 | 描述 | 相关业务流程协调程序 |
|------------------|-------------|-----------------------|
| [用于容器的 azure 监视器](https://docs.microsoft.com/azure/monitoring/monitoring-container-insights-overview) | 专用的 azure Kubernetes 管理工具 | Azure Kubernetes 服务 (AKS) |
| [Kubernetes Web UI （仪表板）](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) | Kubernetes 的管理工具，可以监视和管理本地 Kubernetes 群集 | Azure Kubernetes 服务 (AKS)<br/>本地 Kubernetes |
| [适用于 Service Fabric 的 azure 门户](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal)<br/>[Azure Service Fabric Explorer](https://docs.microsoft.com/azure/service-fabric/service-fabric-visualizing-your-cluster) | 用于管理 Service Fabric 群集，在 Azure 上、 在本地、 本地开发和其他云中的联机和桌面版本 | Azure Service Fabric |
| [容器监视 （日志分析）](https://docs.microsoft.com/azure/azure-monitor/insights/containers) | 常规容器监视解决方案管理 y。 可以管理通过 Kubernetes 群集[容器的 Azure Monitor](https://docs.microsoft.com/azure/monitoring/monitoring-container-insights-overview)。 | Azure Service Fabric<br/>Azure Kubernetes 服务 (AKS)<br/>Mesosphere DC/OS 和其他人。 |

## <a name="azure-service-fabric"></a>Azure Service Fabric

为群集部署和管理的另一个选项是 Azure Service Fabric。 [Service Fabric](https://azure.microsoft.com/services/service-fabric/)包括容器业务流程，以及开发人员的 Microsoft 微服务平台编程模型来构建高度可缩放的微服务应用程序。 Service Fabric 在 Linux 和 Windows 容器支持 Docker，可以在 Windows 和 Linux 服务器中运行。

以下是 Service Fabric 管理工具：

- [Azure 门户中的为 Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal)与群集相关的操作 （创建/更新/删除） 群集或配置其基础结构 (Vm、 负载均衡器、 网络等)

- [Azure Service Fabric Explorer](https://docs.microsoft.com/azure/service-fabric/service-fabric-visualizing-your-cluster)是一个专用 web UI 和桌面提供的见解和 Service Fabric 群集，从节点 /vm 的角度，并从应用程序和服务的角度上进行某些操作的多平台工具。

>[!div class="step-by-step"]
>[上一页](run-microservices-based-applications-in-production.md)
>[下一页](monitor-containerized-application-services.md)
