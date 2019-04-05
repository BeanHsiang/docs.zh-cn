---
title: 演练和技术可帮助入门的概述
description: 更新现有.NET 应用程序使用 Azure 云和 Windows 容器 |演练和技术可帮助入门的概述
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/28/2018
ms.openlocfilehash: e89f1e79eec16919b2e70952392b6f640433156b
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57846254"
---
# <a name="walkthroughs-and-technical-get-started-overview"></a>演练和技术可帮助入门的概述

若要限制此电子书的大小，其他技术文档和完整的演练提供了在 GitHub 存储库中。 联机的此章中所述的演练一系列涵盖基于 Windows 容器和 Azure 上部署的多个环境的分步的设置。

以下部分介绍每个演练有关其目标和高级愿景是什么，并提供了所涉及的任务的图表。 可以获取自己的演练中*eShopModernizing*在应用 GitHub 存储库 wiki [ https://github.com/dotnet-architecture/eShopModernizing/wiki ](https://github.com/dotnet-architecture/eShopModernizing/wiki)。

## <a name="technical-walkthrough-list"></a>技术演练列表

下面的入门演练提供一致且全面的示例应用，你可以迁移使用容器，并在 Azure 中使用多个部署选项然后移动的技术指南。

每个以下演练使用的新示例 eShopLegacy 和 eShopModernizing 应用，可在 GitHub 上[ https://github.com/dotnet-architecture/eShopModernizing ](https://github.com/dotnet-architecture/eShopModernizing)。

- **EShop 旧版应用 （基线应用实现现代化） 的教程**

- **Windows 容器与容器化现有 ASP.NET web 应用 （WebForms 和 MVC）**

- **容器化现有 WCF 服务 （N 层应用程序） 与 Windows 容器**

- **将 Windows 基于容器的应用部署到 Azure Vm**

- **将 Windows 基于容器的应用部署到 Azure 容器服务中 Kubernetes**

- **部署到 Azure Service Fabric Windows 基于容器的应用程序**

## <a name="walkthrough-1-tour-of-eshop-legacy-apps"></a>演练 1:EShop 旧版应用的教程

### <a name="technical-walkthrough-availability"></a>技术演练可用性

全面的技术演练现已推出 eShopModernizing GitHub 存储库 wiki:

[eShopModernizing wiki 演练](https://github.com/dotnet-architecture/eShopModernizing/wiki)

### <a name="overview"></a>概述

在本演练中，可以浏览对旧版应用程序的三个示例的初始实现。 前两个示例 web 应用具有单一式体系结构，并使用传统的 ASP.NET 创建的。 一个应用程序基于 ASP.NET 4.x MVC;第二个应用程序基于 ASP.NET 4.x Web 窗体。
第三个应用程序是由客户端 WinForms 应用程序和服务器端的 3 层应用程序[Windows Communication Foundation (WCF)](../../framework/wcf/whats-wcf.md)服务。

所有这些应用程序目前[eShopModernizing GitHub 存储库](https://github.com/dotnet-architecture/eShopModernizing)。

### <a name="goals"></a>目标

本演练中的主要目标是只需熟悉这些应用程序，以及其代码和配置。 可以配置应用程序，使它们生成和使用模拟数据，而无需使用 SQL 数据库中，出于测试目的。 此可选配置基于依赖关系注入，方法中。

### <a name="scenario-1-aspnet-web-apps"></a>方案 1:ASP.NET Web 应用程序

下图显示了原始的旧版 ASP.NET web 应用程序的简单方案。

![简单的体系结构方案中的原始的旧版 ASP.NET web 应用程序](./media/image5-1.png)

从业务域的角度来看，这两个应用管理功能提供相同的目录。 EShop 企业团队的成员将使用该应用可以查看和编辑产品目录。

下图显示了初始应用程序的屏幕截图。

![ASP.NET MVC 和 ASP.NET Web 窗体应用程序 （现有/旧版技术）](./media/image5-2.png)

依赖关系在 ASP.NET 4.x 或更早版本 （不管是 MVC 或 Web 窗体） 意味着除非通过使用 ASP.NET Core MVC 完全重写代码，这些应用程序不会运行.NET Core 上。

### <a name="scenario-2-wcf-service-and-winforms-client-app-3-tier-app"></a>方案 2:WCF 服务和 WinForms 客户端应用程序 （第 3 层应用程序）

下图显示了原始的第 3 层旧应用程序的简单方案。

![简单的体系结构方案中的原始的旧版第 3 层应用程序与 WCF 服务和 WinForms 客户端应用程序](./media/image5-1.5.png)

### <a name="benefits"></a>优点

本演练的好处很简单：只需熟悉的代码和初始应用程序。

### <a name="next-steps"></a>后续步骤

浏览 GitHub wiki 上的更深入此内容：

- [教程基线 ASP.NET MVC 和 Web 窗体"传统"应用程序](https://github.com/dotnet-architecture/eShopModernizing/wiki/01.-Tour-on-the-ASP.NET-MVC-and-WebForms-apps-implementation-code)
- [基线 WCF 服务和 WinForms （3 层）"传统"应用程序的教程](https://github.com/dotnet-architecture/eShopModernizing/wiki/21.-Tour-on-the-WCF-service-and-WinForms-apps)

## <a name="walkthrough-2-containerize-your-existing-net-applications-with-windows-containers"></a>演练 2:容器化现有.NET 应用程序与 Windows 容器

### <a name="overview"></a>概述

使用 Windows 容器可提高现有.NET 应用程序，如基于 MVC、 Web 窗体或 WCF，向生产、 开发和测试环境的部署。

### <a name="goals"></a>目标

本演练的目的是说明用于容器化现有.NET Framework 应用程序的多个选项。 你可以：

- 通过使用容器化应用程序[Visual Studio 2017 Tools for Docker](/aspnet/core/host-and-deploy/docker/visual-studio-tools-for-docker) （Visual Studio 2017 或更高版本）。

- 通过手动添加容器化应用程序[Dockerfile](https://docs.docker.com/engine/reference/builder/)，然后使用[Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)。

- 通过使用容器化应用程序[Img2Docker](https://github.com/docker/communitytools-image2docker-win)工具 （Docker 的开放源代码工具）。

本演练重点介绍 Visual Studio 2017 Tools for Docker 方法，但其他两种方法是从使用 Dockerfile 非常相似。

### <a name="scenario-1-containerized-aspnet-web-apps"></a>方案 1:容器化的 ASP.NET web 应用

下图显示了容器化的 eShop 旧版 web 应用应用程序的方案。

![简化的体系结构关系图的适用于容器化 ASP.NET 应用程序在开发环境](./media/image5-3.png)

### <a name="scenario-2-containerized-wcf-service"></a>方案 2:容器化的 WCF 服务

下图显示了包含容器化的 WCF 服务的第 3 层应用程序的方案。

![简化的开发环境中的容器化 WCF 服务的体系结构关系图](./media/image5-3.5.png)

### <a name="benefits"></a>优点

有在容器中运行整体式应用程序的优点。 首先，创建用于应用程序的映像。 从该点开始，每个部署在同一环境中运行。 每个容器使用相同的 OS 版本，具有相同版本的安装的依赖项、 使用相同的.NET framework 版本，并使用相同的过程生成。 基本上，使用的 Docker 映像控制你的应用程序的依赖项。 部署容器时，依赖项与应用程序同步。

另一个好处是开发人员可以在由 Windows 容器提供一致的环境中运行应用程序。 可以立即发现仅某些版本出现的问题，而不是在过渡或生产环境中呈现。 在开发环境中的开发团队成员使用的差异不那么重要应用程序在容器中运行时。

容器化应用程序还具有 flatter 横向扩展曲线。 容器化应用程序，你有多个应用程序和服务实例 （基于容器） 中的 VM 或物理机到每台计算机的常规应用程序部署进行比较。 这会转换为更高的密度和更少所需的资源，尤其是当使用 Kubernetes 或 Service Fabric 等业务流程协调程序。

容器化，在理想情况下，不需要对应用程序代码进行任何更改 (C\#)。 在大多数情况下，你只需 Docker 部署元数据文件 （Dockerfile 和 Docker Compose 文件）。

### <a name="next-steps"></a>后续步骤

浏览 GitHub wiki 上的更深入此内容：

- [如何容器化.NET Framework web 应用程序使用 Windows 容器和 Docker](https://github.com/dotnet-architecture/eShopModernizing/wiki/02.-How-to-containerize-the-.NET-Framework-web-apps-with-Windows-Containers-and-Docker)
- [将 Docker 支持添加到 WCF 服务](https://github.com/dotnet-architecture/eShopModernizing/wiki/22.-Adding-Docker-Support)

## <a name="walkthrough-3-deploy-your-windows-containers-based-app-to-azure-vms"></a>演练 3:将 Windows 基于容器的应用部署到 Azure Vm

### <a name="technical-walkthrough-availability"></a>技术演练可用性

全面的技术演练现已推出 eShopModernizing GitHub 存储库 wiki: [https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD))

### <a name="overview"></a>概述

部署到 Docker 主机在 Windows Server 2016 虚拟机 (VM) 上 Azure 中，可让你快速设置开发/测试/暂存环境。 它还使您的测试人员或业务用户若要验证该应用程序的常见位置。 Vm 还可以作为有效的基础结构服务 (IaaS) 生产环境。

### <a name="goals"></a>目标

本演练的目的是说明将 Windows 容器部署到基于 Windows Server 2016 或更高版本的 Azure Vm 时，有多个备选方法。

### <a name="scenarios"></a>方案

在本演练涵盖了几个方案。

#### <a name="scenario-a-deploy-to-an-azure-vm-from-a-dev-pc-through-docker-engine-connection"></a>情况 a:从开发人员电脑通过 Docker 引擎连接部署到 Azure VM

![从开发人员电脑通过 Docker 引擎连接部署到 Azure VM](./media/image5-4.png)

**图 5-4**。 从开发人员电脑通过 Docker 引擎连接部署到 Azure VM

#### <a name="scenario-b-deploy-to-an-azure-vm-through-a-docker-registry"></a>方案 b:部署到 Azure VM 通过 Docker 注册表

![部署到 Azure VM 通过 Docker 注册表](./media/image5-5.png)

**图 5-5**。 部署到 Azure VM 通过 Docker 注册表

#### <a name="scenario-c-deploy-to-an-azure-vm-from-cicd-pipelines-in-azure-devops-services"></a>方案 c:从 Azure DevOps 服务中的 CI/CD 管道部署到 Azure VM

![从 Azure DevOps 服务中的 CI/CD 管道部署到 Azure VM](./media/image5-6.png)

**如 5-6**。 从 Azure DevOps 服务中的 CI/CD 管道部署到 Azure VM

### <a name="azure-vms-for-windows-containers"></a>用于 Windows 容器的 azure Vm

Windows 容器的 azure Vm 是基于 Windows Server 2016、 Windows 10 或更高版本的 Vm，它们都具有 Docker 引擎设置。 在大多数情况下，Windows Server 2016 Azure Vm 中使用。

Azure 当前提供了一个名为的虚拟机**Windows Server 2016 with Containers**。 可以使用此 VM 用于尝试新的 Windows Server 容器功能，与 Windows Server Core 或 Windows Nano Server。 安装容器操作系统映像，这样，VM 就可以使用 Docker。

### <a name="benefits"></a>优点

虽然 Windows 容器部署到 Azure 时，可以将它们部署到的本地 Windows Server 2016 Vm，可以轻松地开始使用随时可用的 Windows Server 容器 Vm。 您还了解常见的联机位置都能访问的测试人员和通过 Azure 虚拟机规模集自动可伸缩性。

### <a name="next-steps"></a>后续步骤

浏览 GitHub wiki 上的更深入此内容：

[https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/03.-How-to-deploy-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD))

## <a name="walkthrough-4-deploy-your-windows-containers-based-apps-to-azure-container-instances-aci"></a>演练 4:将 Windows 基于容器的应用部署到 Azure 容器实例 (ACI)

### <a name="technical-walkthrough-availability"></a>技术演练可用性

全面的技术演练现已推出 eShopModernizing GitHub 存储库 wiki:

[将应用部署到 ACI （Azure 容器实例）](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

### <a name="overview"></a>概述

[Azure 容器实例 (ACI)](https://docs.microsoft.com/azure/container-instances/)是具有可在其中部署容器的单个实例的容器开发/测试/暂存环境的最快方法。

### <a name="goals"></a>目标

本演练演示的主要方案时将 Windows 容器部署到 Azure 容器实例 (ACI) 和如何将 eShopModernizing 应用部署到 ACI。

### <a name="scenarios"></a>方案

可以将 eShopModernizing 应用部署到 ACI 部署只需一个或所有应用 （MVC 应用程序，WebForms 应用程序或 WCF 服务） 等有关的变体。 如下所示的以下方案中您可以为容器看到到 ACI （Azure 容器实例） 的 ASP.NET MVC 应用程序以及这两个部署的 SQL Server 容器。

![从开发环境部署到 ACI](./media/image5-3.5.6.png)

### <a name="benefits"></a>优点

Azure 容器实例轻松创建和管理 Docker 容器在 Azure 中，而无需预配虚拟机或采用更高级别的服务。 使用 ACI，可以直接部署在 Azure 中的 Windows 容器并将其公开给 internet 完全限定的域名 (FQDN) 与在几秒内 （前提是必须准备的 Windows 容器映像中的 Docker 注册表，如 Docker 中心或 Azure 容器注册表中）。

### <a name="considerations"></a>注意事项

使用任一完整的.NET Framework 的 Windows 容器部署 ASP.NET 或 SQL Server 到 Azure 容器实例 (ACI) 不是与部署到常规的 Docker 主机 （如 Windows Server 2016 与 Windows 容器)，因为 Docker 映像必须相当快 /每次下载 （拉入从 Docker 注册表） 和 SQL 容器映像 (15.1 GB) 和 ASP.NET 容器映像 (13.9 GB) 的大小会非常大，但是它更廉价比维护你自己的 docker 主机 （永久联机使用 Windows 容器在 Azure 中的 VM 的 Windows Server 2016) 更不必说一些，但是，对于生产部署的理想选择 Kubernetes 在 Azure (AKS/ACS) 或 Azure Service Fabric 等整个业务流程协调程序。

作为主结束时，使用 Azure 容器实例是一个非常引人注目的选项为开发/测试方案和 CI/CD 管道。

## <a name="next-steps"></a>后续步骤

浏览 GitHub wiki 上的更深入此内容：

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances)TBD)

## <a name="walkthrough-5-deploy-your-windows-containers-based-apps-to-kubernetes-in-azure-container-service"></a>演练 5:将 Windows 基于容器的应用部署到 Azure 容器服务中 Kubernetes

### <a name="technical-walkthrough-availability"></a>技术演练可用性

全面的技术演练现已推出 eShopModernizing GitHub 存储库 wiki:

[https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD))

### <a name="overview"></a>概述

基于 Windows 容器的应用程序需要快速使用从 IaaS Vm 即可移动更进一步的平台。 这需要能够轻松实现高可伸缩性和更好地自动可伸缩性，并得到显著提高自动执行部署和版本控制。 可以使用业务流程协调程序来实现这些目标[Kubernetes](https://kubernetes.io/)中的可用[Azure 容器服务](https://azure.microsoft.com/services/container-service/)。

### <a name="goals"></a>目标

本演练的目的是了解如何基于 Windows 容器应用程序部署到 Kubernetes (也称为*K8s*) 在 Azure 容器服务中。 从零开始部署到 Kubernetes 是一个两步过程：

1. 部署到 Azure 容器服务 Kubernetes 群集。

2. 将应用程序和相关的资源部署到 Kubernetes 群集。

### <a name="scenarios"></a>方案

#### <a name="scenario-a-deploy-directly-to-a-kubernetes-cluster-from-a-dev-environment"></a>情况 a:将直接部署到 Kubernetes 群集从开发环境

![将直接部署到 Kubernetes 群集从开发环境](./media/image5-7.png)

**图 5-7**。 将直接部署到 Kubernetes 群集从开发环境

#### <a name="scenario-b-deploy-to-a-kubernetes-cluster-from-cicd-pipelines-in-azure-devops-services"></a>方案 b:从 Azure DevOps 服务中的 CI/CD 管道部署到 Kubernetes 群集

![从 Azure DevOps 服务中的 CI/CD 管道部署到 Kubernetes 群集](./media/image5-8.png)

**图 5-8**。 从 Azure DevOps 服务中的 CI/CD 管道部署到 Kubernetes 群集

### <a name="benefits"></a>优点

有很多好处与部署到 Kubernetes 中的群集。 最大好处是，您将在其中可以扩大应用程序根据你想要使用 （内部的可伸缩性的现有节点中），并根据在群集 （节点或 Vm 的数量的容器实例数的生产就绪环境全局可伸缩性的群集）。

Azure 容器服务特别为 Azure 优化了常用的开源工具和技术。 获取打开的解决方案，提供可移植性，为你的容器和应用程序配置。 选择的大小，主机数和业务流程协调程序工具的容器服务可处理其他操作。

使用 Kubernetes，开发人员可以继续进行考虑物理机和虚拟机，从规划以容器为中心的基础结构，方便其他项中的以下功能：

- 基于多个容器的应用程序

- 复制容器实例和水平自动缩放

- 命名和发现 (例如，内部 DNS)

- 均衡负载

- 滚动更新

- 分发机密

- 应用程序运行状况检查

## <a name="next-steps"></a>后续步骤

浏览 GitHub wiki 上的更深入此内容： [https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-C-CD))

## <a name="walkthrough-6-deploy-your-windows-containers-based-apps-to-azure-service-fabric"></a>演练 6:部署到 Azure Service Fabric Windows 基于容器的应用程序

### <a name="technical-walkthrough-availability"></a>技术演练可用性

全面的技术演练现已推出 eShopModernizing GitHub 存储库 wiki:

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD))

### <a name="overview"></a>概述

基于 Windows 容器快速应用程序需要使用从 IaaS Vm 即可移动更进一步的平台。 这需要能够轻松实现高可伸缩性和更好地自动可伸缩性，并得到显著提高自动执行部署和版本控制。 通过使用业务流程协调程序 Azure Service Fabric 中，这是可在 Azure 云中，但也可使用在本地，或甚至在不同的公有云，可以实现这些目标。

### <a name="goals"></a>目标

本演练的目的是了解如何基于 Windows 容器应用程序部署到 Azure 中的 Service Fabric 群集。 从零开始部署到 Service Fabric 是一个两步过程：

1. 将 Service Fabric 群集部署到 Azure （或不同的环境）。

2. 将应用程序和相关的资源部署到 Service Fabric 群集。

### <a name="scenarios"></a>方案

#### <a name="scenario-a-deploy-directly-to-a-service-fabric-cluster-from-a-dev-environment"></a>情况 a:将直接部署到 Service Fabric 群集从开发环境

![将直接部署到 Service Fabric 群集从开发环境](./media/image5-9.png)

> **图 5-9**。 将直接部署到 Service Fabric 群集从开发环境

### <a name="scenario-b-deploy-to-a-service-fabric-cluster-from-cicd-pipelines-in-azure-devops-services"></a>方案 b:从 Azure DevOps 服务中的 CI/CD 管道部署到 Service Fabric 群集

![从 Azure DevOps 服务中的 CI/CD 管道部署到 Service Fabric 群集](./media/image5-10.png)

**图 5-10**。 从 Azure DevOps 服务中的 CI/CD 管道部署到 Service Fabric 群集

## <a name="benefits"></a>优点

将部署到 Service Fabric 中的群集的优点是类似于使用 Kubernetes 的好处。 一个区别，不过，是 Service Fabric 是更成熟的生产环境的 Windows 应用程序相比 Kubernetes，Kubernetes 1.9 版中的 Windows 容器的 beta 阶段中是 (2017 年 12 月)。 Kubernetes 是更成熟的环境，适用于 Linux。

使用 Azure Service Fabric 的主要优势是您获取在其中可以扩大应用程序根据你想要使用 （内部的可伸缩性的现有节点中），并根据的数量的容器实例数的生产就绪环境节点或群集 （群集的全局可伸缩性） 中的 Vm。

Azure Service Fabric 提供了容器和应用程序配置为可移植性。 您可以在 Azure 中，群集或安装在自己的数据中心中的本地 Service Fabric。 您甚至可以安装 Service Fabric 群集在另一个云，如[Amazon AWS](https://blogs.msdn.microsoft.com/azureservicefabric/2017/05/18/tutorial-how-to-create-a-service-fabric-standalone-cluster-with-aws-ec2-instances/)。

使用 Service Fabric，开发人员可以继续进行从思考物理机和虚拟机规划以容器为中心的基础结构，方便其他项中的以下功能：

- 基于多个容器的应用程序。

- 复制容器实例和水平自动缩放。

- 命名和发现 (例如，内部 DNS)。

- 平衡负载。

- 滚动更新。

- 分发机密。

- 应用程序运行状况检查。

以下功能是以独占方式 Service Fabric （与其他业务流程协调程序相比）：

- 有状态服务功能，通过 Reliable Services 应用程序模型。

- 执行组件模式，通过 Reliable Actors 应用程序模型。

- 部署精简进程，除了 Windows 或 Linux 容器。

- 高级滚动更新和运行状况检查。

### <a name="next-steps"></a>后续步骤

浏览 GitHub wiki 上的更深入此内容：

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-How-to-deploy-your-Windows-Containers-based-apps-into-Azure-Service-Fabric-(Including-CI-CD))

> [!div class="step-by-step"]
> [上一页](lift-and-shift-existing-apps-devops/migrate-to-hybrid-cloud-scenarios.md)
> [下一页](conclusions.md)
