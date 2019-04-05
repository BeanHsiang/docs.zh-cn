---
title: 在生产环境中运行组合和基于微服务的应用程序
description: 了解在生产环境中运行基于容器的应用程序的关键组件
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 52cf273194bff10192b06d236bda7c1cbea1abd8
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56835208"
---
# <a name="run-composed-and-microservices-based-applications-in-production-environments"></a>在生产环境中运行组合和基于微服务的应用程序

由多个微服务构成的应用程序需要将部署到业务流程协调程序群集为了简化部署的复杂性和使其可行从 IT 角度来看。 而无需与业务流程协调程序的群集，很难部署和横向扩展的复杂微服务应用程序。

## <a name="introduction-to-orchestrators-schedulers-and-container-clusters"></a>业务流程协调程序、 计划程序，以及容器群集简介

这本电子书，前面*群集*并*计划程序*讨论有关软件体系结构和开发的一部分引入。 Kubernetes 和 Service Fabric 是 Docker 群集的示例。 这两个这些业务流程协调程序可以运行提供 Microsoft Azure Kubernetes 服务的基础结构的一部分。

当应用程序是向外扩展跨多个主机系统时，管理每个主机系统和抽象出底层平台的复杂性的能力变得极具吸引力。 这就准确地说是业务流程协调程序和计划程序提供的内容。 看看简要此处所示：

- **计划程序**。 "计划"是指管理员能够加载到建立如何运行特定容器的主机系统上的服务文件的功能。 启动 Docker 群集中的容器通常被称为计划。 尽管计划是指特定操作的加载服务定义中的，在更多常规意义上，计划程序负责挂接到主机的 init 系统中任何所需的容量管理服务。

   群集计划程序具有多个目标： 高效使用群集的资源中，使用用户提供的放置约束，计划具有的应用程序快速以不将它们保留在挂起状态，在一定程度"的公平性，"正在可靠的错误，并始终为可用。

- **业务流程协调程序**。 平台扩展到的主机群集中部署复杂的多容器工作负荷的生命周期管理功能。 通过将抽象化的主机基础结构，业务流程工具为用户提供了一种方法将整个群集视为单个部署目标。

   业务流程的过程包括工具和一个平台，可以自动从初始放置或部署每个容器; 应用程序管理的所有方面将容器移动到不同的主机，具体取决于其主机的运行状况或性能;版本控制和滚动更新和运行状况监视功能的支持缩放和故障转移;及更多。

   业务流程是一个泛指的术语，指容器计划、 群集管理和可能的预配其他主机。

提供的业务流程协调程序和计划程序的功能比较复杂开发并从头开始创建，因此你通常想要使用由供应商提供的业务流程解决方案。

>[!div class="step-by-step"]
>[上一页](index.md)
>[下一页](manage-production-docker-environments.md)
