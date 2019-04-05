---
title: 何时将 Windows 容器部署到 Azure 容器服务 (即 Kubernetes)
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |何时将 Windows 容器部署到 Azure 容器服务 (即 Kubernetes)
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/30/2018
ms.openlocfilehash: 0b803b104f905fddac7939d7b070c206aabffeda
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53144788"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-service-that-is-kubernetes"></a>何时将 Windows 容器部署到 Azure 容器服务 (即 Kubernetes)

Azure 容器服务优化了专门针对 Azure 的受欢迎的开源工具和技术配置。 获取打开的解决方案，可提供你的容器和应用程序配置的可移植性。 您选择的大小、 主机数和 orchestrator 工具。 Azure 容器服务为你处理的基础结构。

如果已在使用 Kubernetes、 Docker Swarm 或 DC/OS 等的开放源业务流程协调程序，不需要更改现有的管理措施以将容器工作负荷移动到云。 使用您已经熟悉的应用程序管理工具并通过标准 API 终结点连接的所选的业务流程协调程序。

如果你正在使用 Linux Docker 容器，但可能仅在 Windows 容器的预览状态，所有这些业务流程协调程序是成熟的环境。

例如，在 Kubernetes 中，对支持容器是本机 （一流成员），因此在 Kubernetes 上使用 Windows 容器也很有效 （在预览版在 ACS 中，从 2018 年初开始）。

重要说明：改进和"多个 PaaS"适用于 Kubernetes 的 ACS （Azure 容器服务） 的版本是 AKS （Azure Kubernetes 服务），但是，Windows 容器目前尚不支持从第 2 季度 2018 起，但将很快支持。

>[!div class="step-by-step"]
>[上一页](when-to-deploy-windows-containers-to-service-fabric.md)
>[下一页](choosing-azure-compute-options-for-container-based-applications.md)