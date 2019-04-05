---
title: 何时将 Windows 容器部署到 Service Fabric
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |何时将 Windows 容器部署到 Service Fabric
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/30/2018
ms.openlocfilehash: 01d76f325480c7cf09fef36b02589a602e3ee11e
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53129501"
---
# <a name="when-to-deploy-windows-containers-to-service-fabric"></a>何时将 Windows 容器部署到 Service Fabric

基于 Windows 容器的应用程序需要快速使用从 IaaS Vm 即可移动更进一步的平台。 此内容用于改进自动的可伸缩性和高可伸缩性，并获得全面的管理体验对于部署中的重大改进会升级，版本控制、 回滚、 和运行状况监视。 可以使用业务流程协调程序 Azure Service Fabric，可以在 Microsoft Azure 云，但还在本地，或甚至另一个云来实现这些目标。

许多组织是提升并转移到容器的现有单一式应用程序有两个原因：

-   成本的降低，或者由于合并和删除的现有硬件，或在更高的密度运行的应用程序。

-   开发和运营之间一致的部署协定。

追求降低成本是可以理解，并可能所有组织都跟踪这一目标。 一致的部署是更难以评估，但同样重要。 一致的部署协定说开发人员可自由选择使用适时，技术和运营团队获取一种方法来部署和管理应用程序。 本协议缓解了具有处理许多不同的技术，复杂的操作也不会强迫开发人员可以仅使用特定技术的麻烦。 从根本上来说，每个应用程序是适用于容器化的独立的部署映像中。

某些组织将继续通过添加微服务 （云原生应用程序） 实现现代化，但其他许多组织将就此打住 （云计算得到优化的应用程序）。 如所示图 4-8，这些组织不会移动到微服务体系结构，因为它们可能不需要。 在任何情况下，它们已经获得优势，使用容器以及 Service Fabric 提供了一个完整管理体验，包括部署、 升级、 版本控制、 回滚、 和运行状况监视。

> ![提升和迁移到 Service Fabric 应用程序](./media/image8.png)
>
> **图 4-8。** 提升和迁移到 Service Fabric 应用程序

Service Fabric 的关键方法是重复使用现有代码和提升和转移。 因此，可以通过使用 Windows 容器迁移当前.NET Framework 应用程序，并将其部署到 Service Fabric。 它将更容易地将会更新，最后，通过添加新的微服务。

将 Service Fabric 与其他业务流程协调程序进行比较，时，一定要突出显示 Service Fabric 是在运行基于 Windows 的应用程序和服务的成熟。 Service Fabric 运行基于 Windows 的服务和应用程序，包括年第 1 层、 关键来自 Microsoft 的产品。 这是用于 Windows 容器具有正式发布第一个业务流程协调程序。 其他容器，如 Kubernetes、 DC/OS 和 Docker Swarm，是在 Linux 中，但比基于 Service Fabric 的 Windows 的应用程序和 Windows 容器不够成熟更成熟。

Service Fabric 的最终目标是减少使用微服务方法构建应用程序的复杂性。 某些类型的应用程序以避免成本高昂的重新设计最终想使用微服务。 可以从小规模开始、 缩放时需要、 不推荐使用的服务、 添加新服务，并改进客户使用应用程序。 有许多其他尚待解决为进行大多数开发人员更方便地使用微服务的问题。 如果你当前是只需提升并转移使用 Windows 容器的应用程序，但你正在考虑添加将来基于容器的微服务，这是 Service Fabric 最擅长的领域。

>[!div class="step-by-step"]
>[上一页](when-to-deploy-windows-containers-to-azure-vms-iaas-cloud.md)
>[下一页](when-to-deploy-windows-containers-to-azure-container-service-kubernetes.md)