---
title: Docker 应用程序中的状态和数据
description: 了解可用的选项以在容器化应用程序中保存状态。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 30dde3ce44aa61fff3fad1841ae4a8b941573877
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57678072"
---
# <a name="state-and-data-in-docker-applications"></a>Docker 应用程序中的状态和数据

在大多数情况下，可以将容器视为进程的实例。 进程不维护持久状态。 虽然容器可以写入其本地存储，假定实例将无限期围绕就像假设内存中的单个位置将持久。 应假设容器映像，与进程一样，有多个实例，并且它们最终将会终止;如果使用容器 orchestrator 管理它们，那么应该假定，它们可能会获取从一个节点或 VM 之间移动。

以下解决方案用于管理 Docker 应用程序中的持久性数据：

从 Docker 主机，作为 [Docker 卷](https://docs.docker.com/engine/admin/volumes/)：

- **卷**存储在由 Docker 管理的主机文件系统区域中。

- **将绑定装载**可以映射到主机文件系统中任何文件夹中，因此不能从 Docker 进程控制访问，并可带来安全风险，因为容器可以访问敏感的操作系统文件夹。

- **tmpfs 装载**类似仅存在于主机内存中的虚拟文件夹，并且绝不会写入文件系统。

从远程存储：

- [Azure 存储](https://azure.microsoft.com/documentation/services/storage/)提供可异地分发存储，为容器提供良好的持久性解决方案。

- 远程关系数据库喜欢[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)，等 NoSQL 数据库[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)，或缓存服务，如[Redis](https://redis.io/)。

从 Docker 容器：

- Docker 提供一个名为“覆盖文件系统”的功能。 此功能实现了写入时复制任务存储到的容器的根文件系统更新信息。 该信息"介绍了在最前面的"容器所基于的原始图像。 如果从系统中删除容器，则这些更改将丢失。 因此，虽然可能保存在其本地存储的容器的状态，但设计基于此功能的系统容器设计，它默认情况下是无状态的前提相冲突。

- 但是，Docker 卷现在是首选的方法来处理在 Docker 中的本地数据。 如果需要有关在容器中存储的详细信息，则检查[Docker 存储驱动程序](https://docs.docker.com/engine/userguide/storagedriver/)并[有关映像、 容器和存储驱动程序](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/)。

下面提供了有关这些选项的其他详细信息。

**卷**是从主机 OS 映射到容器目录的目录。 当容器中的代码访问该目录时，该访问实际上是对主机操作系统上的一个目录的访问。 此目录不与容器自身的生存期绑定，且该目录由 Docker 管理并独立于主机计算机的核心功能。 因此，数据卷用于将独立于容器的生命周期的数据持久保存。 如果从 Docker 主机中删除容器或图像，不会删除数据卷中保留的数据。

可以命名卷，也可以让卷保持匿名（默认设置）。 命名卷是**数据卷容器**的演变，它使得在不同容器之间共享数据变得容易。 卷还支持卷驱动程序，可用于将数据存储在远程主机，以及其他选项。

**将绑定装载**已经面世了很长时间，并允许将映射到容器中的装入点的任何文件夹。 绑定挂载的限制比卷的限制多，并存在一些重要安全问题，因此，卷是建议选项。

**`tmpfs` 装载**是虚拟文件夹，仅在主机的内存中保留，所以永远不会写入到文件系统。 它们快速且安全，但使用内存且仅适用于非持久性数据。

如图 4-5 所示，常规 Docker 卷可以存储在容器本身之外，但是在主机服务器或 VM 的物理边界内。 但是，Docker 容器不能从一个主机服务器或 VM 访问另一个主机服务器或 VM 的卷。 换而言之，如果使用这些卷，那么不能管理在不同 Docker 主机上运行的容器之间共享的数据，尽管可通过支持远程主机的卷驱动程序来实现这一功能。

![卷可在容器之间共享，但仅限于同一台主机，除非使用支持远程主机的远程驱动程序。 ](./media/image5.png)

**图 4-5**。 基于容器的应用程序的卷和外部数据源

此外，当 Docker 容器由业务流程协调程序管理时，容器可能会在主机之间“移动”，这取决于群集所执行的优化。 因此，不建议将数据卷用于业务数据。 但它们是一个良好的机制，可以使用跟踪文件、 临时文件，或类似，不会影响业务数据一致性。

远程数据源和缓存工具（如 Azure SQL 数据库、Azure Cosmos DB）或远程缓存（如 Redis）可以在容器化应用程序中使用，与开发时没有容器的使用方式相同。 这是存储业务应用程序数据的一种行之有效的方法。

Azure 存储。 业务数据通常需要放在外部资源或数据库，如 Azure 存储中。 Azure 存储提供在云中的以下服务：

- Blob 存储存储非结构化的对象数据。 Blob 可以是任何类型的文本或二进制数据，如文档或媒体文件（图像、音频和视频文件）。 Blob 存储也称为对象存储。

- 文件存储提供共享的存储使用标准 SMB 协议的旧版应用程序。 Azure 虚拟机和云服务可以通过装载的共享在应用程序组件之间共享文件数据。 在本地应用程序可以访问通过文件服务 REST API 的共享中的文件数据。

- 表存储存储结构化数据集。 表存储是 NoSQL 键属性数据存储，它允许快速开发和快速访问大量数据。

关系数据库和 NoSQL 数据库。 外部数据库有很多选择，包括关系数据库（如 SQL Server、PostgreSQL、Oracle）或 NoSQL 数据库（如 Azure Cosmos DB、MongoDB）等。这些数据库不会加以解释本指南的一部分，因为它们完全是不同的主题。

>[!div class="step-by-step"]
>[上一页](monolithic-applications.md)
>[下一页](soa-applications.md)
