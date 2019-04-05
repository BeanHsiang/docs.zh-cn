---
title: 选择基于容器的应用程序的 Azure 计算平台
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |选择基于容器的应用程序的 Azure 计算平台
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/04/2018
ms.openlocfilehash: f251aecfeaf2421a5cecf218577369963bc736fb
ms.sourcegitcommit: 462dc41a13942e467984e48f4018d1f79ae67346
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58186099"
---
# <a name="choosing-azure-compute-platforms-for-container-based-applications"></a>选择基于容器的应用程序的 Azure 计算平台

阅读前面的部分后，您已经注意到，Azure 是开放的云，提供多个选项。 可以根据需要使用最合适，但是，它还会呈现为容器化应用程序应使用何种产品/技术有关的问题。

作为*默认情况下*建议，下面是本指南中建议主要的准则：

- **单个整体式应用程序：** 选择 Azure 应用服务
- **N 层应用程序：** 如果你有一个或几个后端服务，请选择业务流程协调程序，如 Azure Kubernetes 服务 (AKS)、 Service Fabric (SF) 或应用服务
- **Linux 微服务：** 选择 AKS/Kubernetes
- **Windows 微服务：** 选择 Service Fabric
- **无服务器函数 （&) 事件处理程序：** 选择 Azure 函数
- **大规模批处理：** 选择 Azure Batch

但是，此建议应使用盐，片段执行如产品的选择将取决于特定应用程序的需求和特征。 即使最初它们可能看起来类似的类型，并非所有应用程序都是相同的。

在应用程序的需求的更深入地分析之后, 选择产品可能会有所不同。 但是，作为起点，最好能够从您可以开始评估的初步指导和测试基于针对特定的优先级。

在下一步图中，你可以分析多全局时详细的决策表。

![](./media/image8.5.png)

请注意如何基础 OS (Windows vs。某些业务流程协调程序以及更成熟上 Linux 容器和 Windows 容器上其他 Linux) 也可以决定因素。 例如，Linux 容器是在 Kubernetes (在 Azure 中的 AKS) 中非常成熟但 Service Fabric 上不够成熟。 另一方面，Windows 容器是在 Service Fabric （在 2017 年 5 月发布） 中更成熟和在 AKS 中不够成熟。

但是，在 OS 成熟度这些差异将在将来淡多个平台具有可比较 OS 成熟度和决策将布局基于您的应用程序可能需要或基于每个平台的生态系统的特定功能的首选项将详细介绍原因。

> [!div class="step-by-step"]
> [上一页](when-to-deploy-windows-containers-to-azure-container-service-kubernetes.md)
> [下一页](build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud.md)
