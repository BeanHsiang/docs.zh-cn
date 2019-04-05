---
title: 使用 Azure Service Fabric
description: 了解除了只用于安排容器之外，可以使用哪些 Azure Service Fabric 应用程序模型。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/20/2018
ms.openlocfilehash: b29be05f5ab353ddfae0d23211efaf57979d0604
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53126960"
---
# <a name="using-azure-service-fabric"></a>使用 Azure Service Fabric

Azure Service Fabric 源于 Microsoft 从交付现成产品到交付各种服务的转换，前者通常为单片式产品。 Service Fabric 的出现是由于大规模构建和运营大型服务，例如 Azure SQL 数据库、Azure Cosmos DB、Azure 服务总线、Cortana 后端。 越来越多的服务采用了该平台，它随着时间不断演变。 Service Fabric 不仅需要在 Azure 上运行，还需在独立的 Windows Server 部署上运行，这一点十分重要。

Service Fabric 旨在解决如何构建和运行服务，并有效利用基础结构资源等难题，让团队能够使用微服务方法来解决业务问题。

Service Fabric 提供了两个宽广区域，可帮助构建使用微服务方法的应用程序：

- 提供各种系统服务的平台，可用于部署、缩放、升级、检测、重新启动失败的服务、发现服务位置、管理状态和监视健康状况。 实际上，这些服务具备了很多前面介绍的微服务的特征。

- 有助于将应用程序构建为微服务的编程 API 或框架：[Reliable Actors 和 Reliable Services](https://docs.microsoft.com/azure/service-fabric/service-fabric-choose-framework)。 开发人员可选择任何代码来构建微服务，但这些 API 可简化构建工作，且更深入地与平台集成。 这样开发人员就可获得运行状况信息和诊断信息，也可利用可靠的状态管理。

Service Fabric 未指定服务构建方式，开发人员可使用任何技术。 但它内置了编程 API，可简化微服务的构建。

如图 4-27 所示，开发人员可在 Service Fabric 中创建和运行微服务，既可作为简单进程也可作为 Docker 容器运行。 此外还可在同一 Service Fabric 群集中混合基于容器的微服务与基于进程的微服务。

![Azure service Fabric 群集的比较：微服务作为进程，其中每个节点为每个微服务运行一个进程；微服务作为容器，其中每个节点使用多个容器运行 Docker（每个微服务一个容器）。](./media/image30.png)

**图 4-27**。 在 Azure Service Fabric 中将微服务部署为进程或容器

基于 Linux 和 Windows 主机的 Service Fabric 群集可分别运行 Docker Linux 容器和 Windows 容器。

有关 Azure Service Fabric 中容器支持的最新信息，请参阅 [Service Fabric 和容器](https://docs.microsoft.com/azure/service-fabric/service-fabric-containers-overview)。

Service Fabric 充分展示了什么是一个好的平台，开发人员可在其中定义不同于物理实现（[逻辑体系结构与物理体系结构](logical-versus-physical-architecture.md)部分中有所介绍）的逻辑体系结构（业务微服务或边界上下文）。 例如，如果实现[有状态可靠服务](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction)（稍后将在[无状态微服务与有状态微服务](#stateless-versus-stateful-microservices)部分介绍），则会获得一个业务微服务概念和多个物理服务。

如图 4-28 所示，从逻辑/业务微服务角度考虑，实现 Service Fabric 有状态可靠服务时，通常需要实现两个层级的服务。 第一层是后端有状态可靠服务，用于处理多个分区（每个分区均为一项有状态服务）。 第二层是前端服务或网关服务，负责跨多个分区或有状态服务实例进行路由，聚合数据。 该网关服务还处理访问后端服务的客户端通信，通信带有重试循环。 如果实现自定义服务，则其称为网关服务；或者，还可使用现成的 Service Fabric [反向代理](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy)。

![](./media/image31.png)

**图 4-28**。 具有多个有状态服务实例和一个自定义网关前端的业务微服务

在任何情况下，使用 Service Fabric 有状态可靠服务时，都伴有逻辑或业务微服务（边界上下文），二者通常由多个物理服务组成。 这两项服务，以及网关服务和分区服务都可作为 ASP.NET Web API 服务实现，如图 4-28 所示。

在 Service Fabric 中，可对成组服务进行分组，并将其部署为 [Service Fabric 应用程序](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-model)，即业务流程协调程序或群集的打包和部署单元。 因此，Service Fabric 应用程序同样可映射到该自治业务和逻辑微服务边界或边界上下文，这样开发人员就可以自主部署这些服务。

## <a name="service-fabric-and-containers"></a>Service Fabric 和容器

对于 Service Fabric 中的容器，开发人员也可在 Service Fabric 群集中的容器映像内部署服务。 如图 4-29 所示，大多数情况下，每个服务仅有一个容器。

![Service Fabric 应用程序可以运行访问外部数据库的多个容器，并且整个集会是业务微服务的逻辑边界](./media/image32.png)

**图 4-29**。 Service Fabric 中具有多个服务（容器）的业务微服务

但是，Service Fabric 中也可能有所谓的“sidecar”容器（两个容器必须一同部署为逻辑服务）。 重要的是，业务微服务是多个内聚元素的逻辑边界。 在许多情况下，它可能是具有单个数据模型的单个服务，但在其他一些情况下，也可能具有多个物理服务。

请注意，可在同一 Service Fabric 应用程序中混合进程中的服务和容器中的服务，如图 4-30 所示。

![在同一个节点中运行服务和容器的 Service Fabric 应用程序。](./media/image33.png)

**图 4-30**。 映射到含容器和有状态服务的 Service Fabric 应用程序的业务微服务

有关 Azure Service Fabric 中容器支持的详细信息，请参阅 [Service Fabric 和容器](https://docs.microsoft.com/azure/service-fabric/service-fabric-containers-overview)。

## <a name="stateless-versus-stateful-microservices"></a>无状态微服务与有状态微服务

如前所述，每个微服务（逻辑边界上下文）必须有其域模型（数据和逻辑）。 对于无状态微服务，数据库来自外部，采用 SQL Server 等关系选项，或 Azure Cosmos DB 或 MongoDB 等 NoSQL 选项。

但在 Service Fabric 中，服务本身可以是有状态的，也就是说数据驻留在微服务中。 此数据不仅能存在于同一服务器中，还可以存在于微服务进程中、内存中、硬盘驱动器中，并能复制到其他节点。 图 4-30 显示了不同的方法。

![在无状态服务中，状态（持久性、数据库）保留在微服务外部。 在有状态服务中，状态保留在微服务内部。](./media/image34.png)

**图 4-31**。 无状态微服务与有状态微服务

无状态方法是完全有效的，相比有状态微服务，它更易实现，因为这种方法类似于用户熟悉的传统模式。 但无状态微服务会在进程和数据源之间产生延迟。 若要试图增加缓存和队列来提高性能，该方法会涉及更多要移动的内容。 结果就是，最终会得到具有许多层级的复杂体系结构。

相反，[有状态微服务](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction#when-to-use-reliable-services-apis)采用的方案更高级，因为域逻辑和数据之间没有延迟。 有状态服务有利于处理繁重数据、游戏后端、数据库即服务和其他低延迟方案，因为它能启用本地状态，提高访问速度。

无状态服务和有状态服务相辅相成。 例如，如图 4-31 所示，在右边的图中，有状态服务可拆分为多个分区。 若要访问这些分区，可能需要无状态服务充当网关服务，该服务了解如何基于分区键处理每个分区。

有状态服务确实存在缺点。 该服务允许横向扩展，因而更复杂。完成跨有状态微服务和数据分区复制数据等任务时，必须解决通常由外部数据库系统实现的功能。 但这正是含[有状态可靠服务](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-introduction#when-to-use-reliable-services-apis)的 [Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-services-platform-architecture) 等业务流程协调程序可发挥重要作用的一方面，它可使用 [Reliable Services API](https://docs.microsoft.com/azure/service-fabric/service-fabric-work-with-reliable-collections) 和 [Reliable Actors](https://docs.microsoft.com/azure/service-fabric/service-fabric-reliable-actors-introduction) 简化有状态微服务的开发过程和生命周期。

其他允许有状态微服务，支持 Actor 模式，提高业务逻辑和数据之间的容错、缩短延迟的微服务框架有来自 Microsoft Research 的 Microsoft [Orleans](https://github.com/dotnet/orleans) 和 [Akka.NET](https://getakka.net/)。 这两个框架目前都在改善其对 Docker 的支持。

请注意，Docker 容器本身是无状态的。 若要实现有状态服务，需到前面提到的某个级别更高的规范框架。

## <a name="using-azure-service-fabric-mesh"></a>使用 Azure Service Fabric 网格 

Azure Service Fabric 网格是一个完全托管的服务，它使开发人员可以构建和部署任务关键型应用程序，而无需管理任何基础结构。 使用 Service Fabric 网格可构建并运行按需缩放的安全的分布式微服务应用程序。 

如图 4-32 所示，在 Service Fabric 网格上托管的应用程序进行运行和缩放时，无需考虑为它提供支持的基础结构。

![在 Docker 桌面中运行的多容器应用可以部署到 Azure Service Fabric 网格，而无需考虑基础结构。](media/image39.png)

**图 4-32**。 将微服务/容器应用程序部署到 Service Fabric 网格

事实上，Service Fabric 网格由包含数千台计算机的群集组成。 所有群集操作都向开发人员隐藏。 只需上传容器并指定所需资源、可用性要求和资源限制。 Service Fabric 网格会自动分配应用程序部署所请求的基础结构，还会处理基础结构故障，从而确保应用程序高度可用。 只需关心应用程序的运行状况和响应能力，而不是基础结构。

有关进一步信息，请参阅 [Service Fabric Mesh 文档](https://docs.microsoft.com/azure/service-fabric-mesh/)。

## <a name="choosing-orchestrators-in-azure"></a>在 Azure 中选择业务流程协调程序

下表提供有关根据工作负荷和 OS 焦点使用哪个业务流程协调程序的指南。

![Azure Kubernetes 服务在 Linux 中比在 Windows 中更成熟，主要用于部署基于容器的微服务。 Azure Service Fabric（群集和网格）在 Windows 中比在 Linux 中更成熟，通常用于基于容器的微服务、基于普通进程的微服务和有状态服务。](media/image40.png)

**图 4-33**。 Azure 指南中的业务流程协调程序选择

>[!div class="step-by-step"]
>[上一页](scalable-available-multi-container-microservice-applications.md)
>[下一页](../docker-application-development-process/index.md)