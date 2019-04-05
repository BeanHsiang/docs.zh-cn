---
title: 何时将 Windows 容器部署到 Azure 容器实例 (ACI)
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |何时将 Windows 容器部署到 Azure 容器实例 (ACI)
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/29/2018
ms.openlocfilehash: 03ee7c8b65e1a92dcc7fd40b44e9ba081f571487
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57674401"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-instances-aci"></a>何时将 Windows 容器部署到 Azure 容器实例 (ACI)

Azure 容器实例时的主要价值主张是可以立即将容器部署到它并不需要以维护该环境，您无需升级/修补基础操作系统或虚拟机，所有的是透明的并将其只需部署到随时可用的环境中的容器。

原因和方案时想要使用 ACI 是类似的主要方案基本上使用 Azure Vm 和容器时，使用 Azure 容器实例的主要方案是：

- **开发/测试方案**
- **任务自动化**
- **CI/CD 代理**
- **小型/规模批处理**
- **简单的 web 应用**

简单的 web 应用方案是公平的 ACI 方案，但请考虑在 ACI 中只能有一个容器实例，每个容器映像，因为您不具有高可用性，仅具有有限的可伸缩性。

但是，即使 ACI 被视为基础结构，因为它只提供单个容器实例，是一个巨大的优势，比使用 Windows Server 的常规 Azure Vm。 使用 ACI，只需将容器部署到自我维护环境和您只需支付这些容器。 因此，更好平台，你可能正在使用虚拟机与容器的大多数情况下，不需要维护/更新/修补 Vm。 使用 ACI 非常简单，只需部署一个容器，则无需创建虚拟机环境只需部署容器。

Azure 容器实例 (ACI) 的主要优点是：

- 而无需管理服务器运行容器
- 提高灵活性的按需的容器
- 将容器部署到具有速度和便捷性史无前例的云-使用单个命令。
- 使用虚拟机监控程序隔离安全的应用程序

简单地说，使用 ACI 可以快速而无需管理虚拟机或无需学习新的工具开发应用。 它是只是你的应用程序在云中运行的容器。

> [!div class="step-by-step"]
> [上一页](when-to-deploy-windows-containers-to-azure-vms-iaas-cloud.md)
> [下一页](when-to-deploy-windows-containers-to-service-fabric.md)
