---
title: 何时将 Windows 容器部署到 Azure Vm （IaaS 云）
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |何时将 Windows 容器部署到 Azure Vm （IaaS 云）
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/28/2018
ms.openlocfilehash: 51217e2c94fd9727c8f7907e791cdebaec98f14f
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53152144"
---
# <a name="when-to-deploy-windows-containers-to-azure-vms-iaas-cloud"></a>何时将 Windows 容器部署到 Azure Vm （IaaS 云）

如果你的组织使用 Azure 虚拟机，即使您还在使用 Windows 容器，您依然是使用 IaaS 时的处理。 这意味着该处理基础结构操作、 VM OS 修补程序和基础结构的复杂性的高度可缩放的应用程序需要将部署到负载平衡基础结构中的多个 Vm。 在 Azure VM 中使用 Windows 容器的主要方案是：

-   **开发/测试环境**:云中的 VM 非常适合用于开发和测试在云中。 您可以快速创建或根据需要停止环境。

-   **小型和中型可伸缩性需要**:在其中为生产环境可能需要几个 Vm 的情况下，管理少量的虚拟机可能是经济实惠直到可以将它们移动到更高级的 PaaS 环境，如业务流程协调程序。

-   **生产环境中的现有部署工具**:您可能会将移动从您已经投资的工具来对虚拟机或裸机服务器 （如 Puppet 或类似工具） 进行复杂的部署在本地环境。 若要移动到云进行少量的更改到生产环境部署过程，您可能会继续使用这些工具来部署到 Azure Vm。 但是，你将想要使用 Windows 容器作为部署单元，以改善部署体验。

>[!div class="step-by-step"]
>[上一页](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)
>[下一页](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)