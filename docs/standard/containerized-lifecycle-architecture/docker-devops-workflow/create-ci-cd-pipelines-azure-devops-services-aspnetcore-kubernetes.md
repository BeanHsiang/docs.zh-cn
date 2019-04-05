---
title: Docker 应用程序的外部循环 DevOps 工作流中的步骤
description: 使用 Microsoft 平台和工具的容器化 Docker 应用程序的生命周期
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 2cd769ce9013a8521c53f36b44ea260ceccd48b7
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56834961"
---
# <a name="creating-cicd-pipelines-in-azure-devops-services-for-a-net-core-20-application-on-containers-and-deploying-to-a-kubernetes-cluster"></a>在 Azure DevOps 服务中为容器和部署到 Kubernetes 群集中的.NET Core 2.0 应用程序创建 CI/CD 管道

图 5-12 中可以看到的端到端 DevOps 方案中介绍的代码管理、 代码编译、 生成 Docker 映像、 Docker 映像推送到 Docker 注册表，最后部署到 Azure 中的 Kubernetes 群集。

![工作流：在开发计算机中启动。 推送到存储库开始生成/CI 任务使用的自定义映像，获取推送到 Docker 注册表，然后任务使用的 CD/部署，最后，将推送到 AKS。](media/docker-workflow-ci-cd-aks.png)

**图 5-12**。 CI/CD 方案创建 Docker 映像，部署到 Azure 中的 Kubernetes 群集

务必以突出显示的两个管道，生成/CI 和发布/CD，通过 Docker 注册表 （如 Docker 中心或 Azure 容器注册表） 中的连接。 Docker 注册表是相比传统的 CI/CD 过程不带 Docker 的主要区别之一。

如所示在图 5 月 13 日，第一阶段是生成/CI 管道。 在 Azure DevOps 服务可以创建生成/CD 管道将编译代码、 创建 Docker 映像，并将它们推送到 Docker 注册表，如 Docker 中心或 Azure 容器注册表。

![Azure DevOps，生成进程任务定义的浏览器视图。](media/build-ci-pipeline-azure-devops-push-to-docker-registry.png)

**图 5-13**。 生成/CI 管道中 Azure DevOps 生成 Docker 映像并将映像推送到 Docker 注册表

第二个阶段是创建部署/发布管道。 在 Azure DevOps 服务，可以轻松地创建适用于 Azure DevOps 服务，使用 Kubernetes 任务面向的 Kubernetes 群集中图 5-14 所示的部署管道。

![Azure DevOps 的浏览器视图将部署到 Kubernetes 任务定义。](media/release-cd-pipeline-azure-devops-deploy-to-kubernetes.png)

**图 5-14**。 Azure DevOps 服务部署到 Kubernetes 群集中的发布/CD 管道

> [!演练] 部署到 Kubernetes eShopModernized:
>
> 有关 Azure DevOps CI/CD 管道的详细演练部署到 Kubernetes 中，请参阅此文章: \
><https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

>[!div class="step-by-step"]
>[上一页](docker-application-outer-loop-devops-workflow.md)
>[下一页](../run-manage-monitor-docker-environments/index.md)
