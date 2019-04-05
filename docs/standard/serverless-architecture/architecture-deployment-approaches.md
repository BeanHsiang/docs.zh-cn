---
title: 体系结构部署方法-无服务器应用
description: 不同的方式企业体系结构的指南是已部署到云，IaaS、 PaaS、 容器之间的比较和无服务器。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 5477b8c4531780fdebf194e4f798564e59cd2953
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53152664"
---
# <a name="architecture-deployment-approaches"></a>体系结构部署方法

而不考虑体系结构方法用于设计业务应用程序、 实现中或这些应用程序的部署可能会有所不同。 企业上承载应用程序从物理硬件的所有内容对无服务器函数。

## <a name="n-tier-applications"></a>N 层应用程序

[N 层体系结构模式](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier)是成熟的体系结构，只需是指各逻辑层分为单独的物理层的应用程序。 N 层体系结构是 N 层体系结构的物理实现。 此体系结构的最常见的实现包括：

* 表示层，例如 web 应用。
* 将 API 或数据访问层，如 REST API。
* 数据层，例如 SQL 数据库。

![N 层体系结构](./media/n-tier-architecture.png)

N 层解决方案具有以下特征：

* 项目通常与层。
* 测试可能会接近以不同的方式按层级。
* 层提供的抽象层，例如表示层通常忽略数据层的实现细节。
* 通常情况下，层只能与相邻的层交互。
* 版本通常托管在该项目，并因此层级别。 简单的 API 更改可能要求整个的中间层的新版本。

这种方法提供了几个好处，包括：

* 隔离的数据库 （通常前端不能直接访问数据库后端）。
* 重复使用的 API （例如，移动、 桌面和 web 应用客户端可以所有重复使用相同的 Api）。
* 若要横向扩展层相互独立的功能。
* 重构隔离： 一层可能会重构而不会影响其他层。

## <a name="on-premises-and-infrastructure-as-a-service-iaas"></a>在本地和基础结构即服务 (IaaS)

托管应用程序的传统方法需要购买硬件和管理所有软件安装，包括操作系统。 最初，这涉及昂贵的数据中心和物理硬件。 附带了操作系统的物理硬件的挑战有很多，包括：

* 需要购买额外的"只是在用例"或峰值需求方案。
* 保护对硬件的物理访问。
* 硬件故障 （例如磁盘故障） 的职责。
* 冷却。
* 配置路由器和负载均衡器。
* 电源冗余。
* 保护软件的访问。

![IaaS 方法](./media/iaas-approach.png)

硬件，通过"虚拟机"的虚拟化使基础结构即服务 (IaaS)。 主机计算机有效地进行分区以分配为其自己的内存、 CPU 和存储提供的资源添加到实例。 团队设置必要的虚拟机以及如何配置关联的网络和存储的访问。

有关详细信息，请参阅[虚拟机 N 层参考体系结构](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/n-tier)。

尽管虚拟化和基础结构即服务 (IaaS) 解决许多问题，但仍在基础结构团队的手中由大的职责。 团队维护的操作系统版本、 应用安全修补程序，并在目标计算机上安装第三方依赖项。 应用程序通常在与测试环境相比的生产计算机上以不同方式行为。 由于不同的依赖项版本和/或 OS SKU 级别出现的问题。 尽管许多组织部署到这些目标的 N 层应用程序，许多公司都受益于如部署到多个云本机模型[平台即服务](#platform-as-a-service-paas)。 使用微服务体系结构都更具挑战性，因为横向扩展实现弹性和恢复能力的要求。

有关详细信息，请参阅[虚拟机](https://docs.microsoft.com/azure/virtual-machines/)。

## <a name="platform-as-a-service-paas"></a>平台即服务 (PaaS)

服务 (PaaS) 提供了平台配置开发人员可以直接插入到的解决方案。 PaaS 托管的宿主是另一个术语。 它无需管理基础操作系统，安全修补程序，并在许多情况下任何第三方依赖项。 平台的示例包括数据库的 web 应用程序和移动后端。

PaaS 解决普遍适用于 IaaS 的挑战。 PaaS 让开发人员将精力集中在代码或数据库架构而不是获取部署方式。 PaaS 的优点包括：

* 需要支付使用模型，消除了投资在空闲状态机中的开销。
* 直接部署并改进的 DevOps、 持续集成 (CI) 和持续交付 (CD) 管道。
* 自动升级、 更新和安全修补程序。
* 按钮式横向扩展和纵向扩展 （弹性缩放）。

PaaS 的主要缺点通常是供应商绑架。 例如，某些 PaaS 提供程序仅支持 ASP.NET、 Node.js 或其他特定语言和平台。 产品，如 Azure 应用服务已演变成面向多个平台和支持各种语言和框架，用于托管 web 应用。

![平台即服务体系结构](./media/paas-architecture.png)

## <a name="software-as-a-service-saas"></a>软件即服务 (SaaS)

软件即服务或 SaaS 是集中托管和可用而无需本地安装或预配。 SaaS 通常是基于 PaaS 作为托管平台，部署软件。 SaaS 提供服务运行并连接现有的软件。 SaaS 通常是垂直的特定于和行业。 SaaS 通常使用许可，通常会提供客户端/服务器模型。 大多数现代的 SaaS 产品/服务为客户端使用基于 web 的应用。 公司通常用作许可证产品/服务的业务解决方案所认为的 SaaS。 它通常不被实现作为可伸缩性和可维护性的应用程序的体系结构考虑事项。 实际上，大多数 SaaS 解决方案基于 IaaS、 PaaS，和/或无服务器的后端。

了解有关通过 SaaS[示例应用程序](https://docs.microsoft.com/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app)。

## <a name="containers-and-functions-as-a-service-faas"></a>容器和服务 (FaaS) 的功能

容器是有趣的解决方案，无需使用 IaaS 类似于 PaaS 的优势。 容器是实质上是包含空白的基本运行的唯一应用程序所需的运行时。 在主机之间共享的主机操作系统和存储等服务的内核或核心部分。 共享的内核使容器轻型的软件 （有些仅仅兆字节为单位的大小，典型的虚拟机的数千兆字节大小）。 与已在运行时主机，容器可以启动速度快，促进高可用性。 能够快速启动容器还提供了额外的复原能力的层。 Docker 是一个容器的更受欢迎的实现。

容器的优点包括：

* 轻型且可移植的
* 自包含因此无需安装依赖项
* 提供一致的环境，而不考虑主机 （运行在便携式计算机上的云服务器完全相同）
* 可以快速预配用于横向扩展
* 可以快速重启从失败中恢复

在容器主机 （这又可能运行裸机计算机或虚拟机上） 中运行容器。 多个容器或同一个容器的实例可能在一台主机上运行。 真正的故障转移并提高恢复能力，必须跨主机缩放容器。

有关 Docker 容器的详细信息，请参阅[什么是 Docker](../microservices-architecture/container-docker-introduction/docker-defined.md)？

通常跨主机管理容器需要如 Kubernetes 业务流程工具。 配置和管理业务流程解决方案如果可能，则可向项目添加额外的开销和复杂性。 幸运的是，许多云提供商提供通过 PaaS 解决方案，简化管理容器业务流程服务。

下图演示了示例的 Kubernetes 安装。 在安装中的节点地址向外扩展和故障转移。 它们运行 Docker 容器实例管理的主服务器。 *Kubelet*是中继到 Docker 命令在 Kubernetes 中的客户端。

![Kubernetes](./media/kubernetes-example.png)

有关业务流程的详细信息，请参阅[Azure 上的 Kubernetes](https://docs.microsoft.com/azure/aks/intro-kubernetes)。

函数即服务 (FaaS) 是一种类似于无服务器的专用的容器服务。 FaaS，名为的特定实现[OpenFaaS](https://github.com/openfaas/faas)，顶部容器来提供无服务器功能。 OpenFaaS 提供了打包所有容器的依赖项运行一段代码所需的模板。 使用模板可以简化部署为功能单元的代码的过程。 OpenFaaS 面向已包含容器和业务流程协调程序，因为它可以使用现有基础结构的体系结构。 尽管提供无服务器功能，它明确要求你使用 Docker 和业务流程协调程序。

## <a name="serverless"></a>无服务器

无服务器体系结构提供了明显不同的代码和其宿主环境。 实现中的代码*函数*由调用*触发器*。 该函数退出后，可能会释放所有所需的资源。 触发器可能手动、 定时的进程、 HTTP 请求或文件上传。 触发器的结果是执行代码。 无服务器平台会有所不同，但最提供访问预定义的 Api 和绑定来简化任务，例如写入到数据库或将排入队列的结果。

无服务器是很大程度抽象化要专注于代码的主机环境依赖体系结构。 它可以被看作*较少服务器*。

容器解决方案提供现有的开发人员构建脚本以将代码发布到无服务器已准备映像。 其他实现中使用现有的 PaaS 解决方案提供了可扩展体系结构。

抽象意味着 DevOps 团队无需预配或管理服务器，也不特定容器。 无服务器平台的主机代码，作为脚本或打包可执行文件使用相关的 SDK，构建并分配所需的资源的代码就能缩放。

下图的关系图四个无服务器组件。 HTTP 请求会导致签出 API 代码运行。 签出 API 将代码插入到数据库，并插入触发其他多项功能运行，以执行计算任务和履行订单等任务。

![无服务器实现](./media/serverless-implementation.png)

无服务器的优点包括：

* **高的密度。** 相同的无服务器代码的多个实例可以与容器或虚拟机相比在同一主机上运行。 跨多个主机向外扩展和复原能力实例小数位数。
* **Micro 计费**。 基于无服务器执行，在某些情况下节约大量成本最无服务器的提供程序清单。
* **即时扩展**。 无服务器可以缩减工作负荷自动和快速。
* **更快地投入**开发人员专注于代码并直接向无服务器平台部署。 组件可以互相独立地释放。

无服务器计算上下文中最常讨论，但还可以将应用于数据。 例如， [Azure SQL](https://docs.microsoft.com/azure/sql-database)并[Cosmos DB](https://docs.microsoft.com/azure/cosmos-db)两者都不是需要你配置的主机或群集的云数据库。 本书重点介绍无服务器计算。

## <a name="summary"></a>总结

没有范围广泛的体系结构，包括混合方法的可用选项。 方法、 管理和成本的代价是控件和可移植性的应用程序功能，可简化无服务器。 但是，许多的无服务器平台公开了配置，以帮助优化该解决方案。 对可移植性代码和更少无服务器平台锁中，还可能会导致最佳编程实践。 下表说明了体系结构方法并排显示。 选择无服务器根据规模需求、 你想要管理运行时，以及如何可以将工作负荷分为小组件。 您将学习如何使用无服务器解决方案的潜在挑战和下一章中的其他决策点。

|         |IaaS     |PaaS     |容器|无服务器|
|---------|---------|---------|---------|----------|
|缩放|VM       |实例 |应用      |函数  |
|**摘要**|硬件|平台|OS 主机|运行时   |
|**单元** |VM       |项目  |图像    |代码      |
|**生存期**|几个月|天到几个月|分钟到几天|毫秒到数分钟|
|**责任**|应用程序、 依赖项、 运行时和操作系统|应用程序和依赖项|应用程序、 依赖项和运行时|函数

* **缩放**用于缩放应用程序的单元是指
* **提取**指的由实现抽象的层
* **单元**指的是部署的内容的作用域
* **生存期**指的是典型的运行时的特定实例
* **责任**指的是生成、 部署和维护应用程序的开销

下一章将重点关注无服务器体系结构、 用例和设计模式。

## <a name="recommended-resources"></a>推荐的资源

* [Azure 应用程序体系结构指南](https://docs.microsoft.com/azure/architecture/guide/)
* [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db)
* [Azure SQL](https://docs.microsoft.com/azure/sql-database)
* [N 层体系结构模式](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier)
* [在 Azure 上的 Kubernetes](https://docs.microsoft.com/azure/aks/intro-kubernetes)
* [微服务](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)
* [虚拟机 N 层参考体系结构](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/n-tier)
* [虚拟机](https://docs.microsoft.com/azure/virtual-machines/)
* [什么是 Docker？](../microservices-architecture/container-docker-introduction/docker-defined.md)
* [Wingtip Tickets SaaS 应用程序](https://docs.microsoft.com/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app)

>[!div class="step-by-step"]
>[上一页](architecture-approaches.md)
>[下一页](serverless-architecture.md)