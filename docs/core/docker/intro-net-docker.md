---
title: Docker 简介
description: 本文简要概述 .NET Core 应用程序上下文中的 Docker。
ms.date: 11/06/2017
ms.custom: mvc, seodec18
ms.openlocfilehash: b2640a1cea4d77158b7d9ed6ec63cf36d9e1f9cd
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57676273"
---
# <a name="introduction-to-net-and-docker"></a>.NET 和 Docker 简介

本文提供了如何在 Docker 上使用 .NET 的简介和概念背景。

## <a name="docker-packaging-your-apps-to-deploy-and-run-anywhere"></a>Docker：打包应用以在任何位置部署和运行

[Docker](../../standard/microservices-architecture/container-docker-introduction/docker-defined.md) 是一个开放平台，使开发人员和管理员可以在称为[容器](https://www.docker.com/what-container)的松散隔离的环境中构建[映像](https://docs.docker.com/glossary/?term=image)、交付和运行分布式应用程序。 此方法可以在开发、QA 和生产环境之间进行高效的应用程序生命周期管理。
 
[Docker 平台](https://docs.docker.com/engine/docker-overview/#the-docker-platform)使用 [Docker 引擎](https://docs.docker.com/engine/docker-overview/#docker-engine)快速构建应用程序，并将其打包为使用以 [Dockerfile](https://docs.docker.com/glossary/?term=Dockerfile) 格式编写的文件创建的 [Docker 映像](https://docs.docker.com/glossary/?term=image)，然后在[分层容器](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/#container-and-layers)中部署和运行。

你可以创建自己的[分层映像](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/#images-and-layers)作为 dockerfiles，或使用[注册表](https://docs.docker.com/glossary/?term=registry)中的现有映像，例如 [Docker 中心](https://docs.docker.com/glossary/?term=Docker%20Hub)。

[Docker 容器、映像和注册表之间的关系](../../standard/microservices-architecture/container-docker-introduction/docker-containers-images-registries.md)是[构建和生成容器化应用程序或微服务](../../standard/microservices-architecture/architect-microservice-container-applications/index.md)时的一个重要概念。 此方法大大缩短了开发和部署之间的时间。

### <a name="further-reading-and-watching"></a>其他阅读材料（和视频）

* [基于 Windows 的容器：使用企业级控件的新式应用开发。](https://www.youtube.com/watch?v=Ryx3o0rD5lY&feature=youtu.be)
* [Docker 概述](https://docs.docker.com/engine/docker-overview/)
* [Windows 容器上的 Dockerfile](/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile)
* [编写 Dockerfile 的最佳做法](https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/)
* [为 .NET Core 应用程序生成 Docker 映像](../docker/building-net-docker-images.md)


### <a name="getting-net-docker-images"></a>获取 .NET Docker 映像

由 Microsoft 创建和优化官方 .NET Docker 映像。 这些映像在 Docker 中心的 Microsoft 存储库中公开提供。 每个存储库可以包含多个映像，具体取决于 .NET 和 OS 版本。 大多数映像存储库提供广泛的标记，以帮助选择特定的框架版本和 OS（Linux 发行版或 Windows 版本）。

## <a name="scenario-based-guidance"></a>基于方案的指南

Microsoft 对 .NET 存储库的打算是要有细化和集中存储库，表示特定方案或工作负载。

`microsoft/aspnetcore` 映像针对 Docker 上的 ASP.NET Core 应用进行了优化，因此容器可以更快启动。

.NET Core 映像 (`microsoft/dotnet`) 适用于基于 .NET Core 的控制台应用。 例如，批处理、Azure WebJobs 和其他控制台方案应该使用优化的 .NET Core 映像。

使用 Docker 和 .NET 应用程序最显而易见的水平方案是用于生产部署和托管。 事实证明，生产只是一种方案，其他方案同样有用。 这些方案不是特定于 .NET，但应该适用于大多数开发人员平台。

* **低摩擦安装** — 你可以尝试使用 .NET，无需本地安装。 只下载 Docker 映像，其中包含 .NET。

* **在容器中开发**你可以在一致的环境中开发，使开发和生产环境类似（可避免一些问题，例如开发人员计算机上的全局状态）。 通过 Visual Studio Tools for Docker，你甚至可以直接从 Visual Studio 启动容器。

* **容器中测试** — 你可以在容器中测试，减少由于环境配置不当或上次测试遗留的其他更改而导致的故障。

* **在容器中生成** — 你可以在容器中生成代码，消除为多个环境正确配置共享生成计算机的需要，而是转向“BYOC”（自带容器）方法。

* **在所有环境中部署** — 可以通过你的所有环境部署映像。 这种方法减少了配置差异导致的故障，通常通过外部配置（例如，注入的环境变量）改变映像行为。

[通用指南](../../standard/microservices-architecture/net-core-net-framework-containers/general-guidance.md)，确定是使用 .NET Core 还是 .NET Framework 进行 Docker 容器开发。

### <a name="common-docker-development-scenarios"></a>常见的 Docker 开发方案

#### <a name="net-core"></a>.NET Core

**.NET Core 资源**

 选择适合你感兴趣方案的 .NET Core 示例。 所有示例说明都介绍了如何从 Windows、Linux 或 macOS 主机定位 Windows 或 Linux Docker 映像。

这些示例使用 .NET Core 2.0。 它们会在适用时使用 Docker [多阶段生成](https://github.com/dotnet/announcements/issues/18)和[多拱形标记](https://github.com/dotnet/announcements/issues/14)。

* [DockerHub 上的 .NET Core 映像](https://hub.docker.com/r/microsoft/dotnet/)

* [使 .NET Core 应用程序 Docker 化](https://docs.docker.com/engine/examples/dotnetcore/)

* 此 .NET Core Docker 示例演示如何[在 .NET Core 开发过程中使用 Docker](https://github.com/dotnet/dotnet-docker-samples/tree/master/dotnetapp-dev)。 此示例适用于 Linux 和 Windows 容器。

* 此 .NET Core Docker 示例演示了[生成 .NET Core 应用程序的 Docker 映像以用于生产](https://github.com/dotnet/dotnet-docker-samples/tree/master/dotnetapp-prod)的最佳实践模式。 此示例适用于 Linux 和 Windows 容器。

* 此 [.NET Core Docker 示例](https://github.com/dotnet/dotnet-docker-samples/tree/master/dotnetapp-selfcontained)演示了生成[独立式 .NET Core 应用程序](../deploying/index.md)的 Docker 映像的最佳实践模式。 用于最小的生产容器，而不会受益于[在容器之间共享基础映像](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/)。 但是，可以共享较低的 Docker 层。

#### <a name="arm32--raspberry-pi"></a>ARM32/Raspberry Pi

* [.NET Core 运行时 ARM32 生成公告](https://github.com/dotnet/announcements/issues/29)

* [DockerHub 上的 ARM32/Raspberry Pi .NET Core 映像](https://hub.docker.com/r/microsoft/dotnet/)

* [GitHub 上的 ARM32/Raspberry Pi .NET Core Docker 示例](https://github.com/dotnet/dotnet-docker-samples#arm32--raspberry-pi)

#### <a name="net-framework"></a>.NET Framework

* [DockerHub 上的 .NET Framework 映像](https://hub.docker.com/r/microsoft/dotnet-framework/)

此存储库包含演示各种 .NET Framework Docker 配置的示例。 你可以将这些映像作为自己的 Docker 映像的基础。

**.NET Framework 4.7**

[dotnet-framework:4.7 示例](https://github.com/Microsoft/dotnet-framework-docker-samples/tree/master/dotnetapp-4.7)演示 [.NET Framework 4.7](../../framework/whats-new/index.md#v47) 的基本“hello world”用法。 它演示如何生成并部署依赖于 [.NET Framework 4.7 docker 映像](https://github.com/Microsoft/dotnet-framework-docker-samples/blob/master/dotnetapp-4.7/Dockerfile)的应用程序。

**.NET Framework 4.6.2**

[dotnet-framework:4.6.2 示例](https://github.com/Microsoft/dotnet-framework-docker-samples/tree/master/dotnetapp-4.6.2)演示 [.NET Framework 4.6.2](../../framework/whats-new/index.md#v462) 的基本“hello world”用法。 它演示如何生成并部署依赖于 [.NET Framework 4.6.2 docker 映像](https://github.com/Microsoft/dotnet-framework-docker-samples/blob/master/dotnetapp-4.6.2/Dockerfile)的应用程序。

**.NET Framework 3.5**

 [dotnet-framework:3.5 示例](https://github.com/Microsoft/dotnet-framework-docker-samples/tree/master/dotnetapp-3.5)演示 [.NET Framework 3.5](https://github.com/Microsoft/dotnet-framework-docker-samples/blob/master/dotnetapp-3.5/dotnetapp-3.5/Dockerfile) 的基本“hello world”用法。 它演示如何在 Docker 中生成并部署依赖于 .NET Framework 3.5 的项目。

#### <a name="aspnet-core"></a>ASP.NET Core

* [此 ASP.NET Core Docker 示例](https://github.com/dotnet/dotnet-docker-samples/tree/master/aspnetapp)演示了生成 ASP.NET Core 应用程序的 Docker 映像以用于生产的最佳实践模式。 此示例适用于 Linux 和 Windows 容器。

* [DockerHub 上的 ASP.NET Core 映像](https://hub.docker.com/r/microsoft/aspnetcore-build/)

* [GitHub 上的 ASP.NET Core 映像](https://github.com/aspnet/aspnet-docker)

#### <a name="aspnet-framework"></a>ASP.NET 框架

* [DockerHub 上的 ASP.NET 框架映像](https://hub.docker.com/r/microsoft/aspnet/)

* [.NET Framework 4.6.2 示例中的 ASP.NET Web 窗体应用](https://github.com/Microsoft/dotnet-framework-docker-samples/tree/master/aspnetapp)

#### <a name="windows-communication-framework-wcf"></a>Windows Communication Framework (WCF)

* [DockerHub 上的 Windows Communication Framework (WCF) 映像](https://hub.docker.com/r/microsoft/wcf/)

* [GitHub 上的 Windows Communication Framework (WCF) 映像](https://github.com/microsoft/wcf-docker)

* [使用 .NET Framework 4.6.2 的 Windows Communication Framework (WCF) Docker 示例](https://github.com/Microsoft/wcf-docker-samples)

#### <a name="internet-information-server-iis"></a>Internet Information Server (IIS)

* [DockerHub 上的 Internet Information Server (IIS) 映像](https://hub.docker.com/r/microsoft/iis/)

* [GitHub 上的 Internet Information Server (IIS) 映像](https://github.com/microsoft/iis-docker)

### <a name="interact-with-other-microsoft-stack-container-images"></a>与其他 Microsoft 堆栈容器映像进行交互

#### <a name="microsoft-sql-server"></a>Microsoft SQL Server

* [使用 Docker 快速入门运行 Microsoft SQL Server for Linux 2017 容器映像](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)

* [DockerHub 上的 Microsoft SQL Server for Linux 映像](https://hub.docker.com/r/microsoft/mssql-server-linux/)

* [DockerHub 上的用于 Windows 容器的 Microsoft SQL Server Express Edition 映像](https://hub.docker.com/r/microsoft/mssql-server-windows-express/)

* [DockerHub 上的用于 Windows 容器的 Microsoft SQL Server Developer Edition 映像](https://hub.docker.com/r/microsoft/mssql-server-windows-developer/)

#### <a name="azure-devops-services-agent"></a>Azure DevOps Services 代理

* [DockerHub 上的 Azure DevOps Services 代理映像](https://hub.docker.com/r/microsoft/vsts-agent/)

* [GitHub 上的 Azure DevOps Services 代理映像](https://github.com/Microsoft/vsts-agent-docker)

#### <a name="operations-management-suite-oms-linux-agent"></a>Operations Management Suite (OMS) Linux 代理

* [Operations Management Suite (OMS) Linux 代理概述](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Docker-Instructions.md)

* [DockerHub 上的 Operations Management Suite (OMS) 映像](https://hub.docker.com/r/microsoft/oms/)

* [GitHub 上的 Operations Management Suite (OMS) 映像](https://github.com/Microsoft/OMS-docker)

#### <a name="microsoft-azure-command-line-interface-cli"></a>Microsoft Azure 命令行接口 (CLI)

* [DockerHub 上的 Microsoft Azure 命令行接口 (CLI) 映像](https://hub.docker.com/r/microsoft/azure-cli/) 

* [GitHub 上的 Microsoft Azure 命令行接口 (CLI) 映像](https://github.com/Azure/azure-cli#Docker)

> [!NOTE]
> 如果你没有 Azure 订阅，请[立即注册](https://azure.microsoft.com/free/?b=16.48)获取一个免费的 30 天试用帐户和 200 美元的 Azure 信用额度，以便试用 Azure 服务的任意组合。

#### <a name="microsoft-azure-cosmos-db-emulator-windows-containers-only"></a>Microsoft Azure Cosmos DB 仿真器（仅限 Windows 容器）

* [DockerHub 上的 Microsoft Azure Cosmos DB 仿真器映像](https://hub.docker.com/r/microsoft/azure-cosmosdb-emulator) 

* [将 Azure Cosmos DB 仿真器用于本地开发和测试](/azure/cosmos-db/local-emulator#developing-with-the-emulator)

## <a name="exploring-the-rich-docker-development-ecosystem"></a>探索内容丰富的 Docker 开发生态系统

了解了 Docker 平台和不同的 Docker 映像后，下一步就是探索内容丰富的 Docker 生态系统。 以下链接展示了 Microsoft 工具对容器开发所做的补充。

* [将 .NET 与 Docker 一起使用](https://devblogs.microsoft.com/dotnet/using-net-and-docker-together/)
* [设计和开发基于微服务的多容器 .NET 应用程序](../../standard/microservices-architecture/multi-container-microservice-net-applications/index.md)
* [Visual Studio Code Docker 扩展](https://code.visualstudio.com/docs/languages/dockerfile)
* [了解如何使用 Azure Service Fabric](/azure/service-fabric/index)
* [Service Fabric 入门示例](https://azure.microsoft.com/resources/samples/service-fabric-dotnet-getting-started/)
* [Windows 容器的优点](/virtualization/windowscontainers/about/index#video-overview)
* [使用 Visual Studio Docker 工具](/aspnet/core/host-and-deploy/docker/visual-studio-tools-for-docker)
* [将 Azure 容器注册表中的 Docker 映像部署到 Azure 容器实例](https://blogs.msdn.microsoft.com/stevelasker/2017/07/28/deploying-docker-images-from-the-azure-container-registry-to-azure-container-instances/)
* [使用 Visual Studio Code 进行调试](https://code.visualstudio.com/docs/nodejs/debugging-recipes#_nodejs-typescript-docker-container)
* [在云中使用 Visual Studio for Mac、容器和无服务器代码](https://blogs.msdn.microsoft.com/visualstudio/2017/08/31/hands-on-with-visual-studio-for-mac-containers-serverless-code-in-the-cloud/#comments)
* [Docker 和 Visual Studio for Mac Lab 入门](https://github.com/Microsoft/vs4mac-labs/tree/master/Docker/Getting-Started)

## <a name="next-steps"></a>后续步骤

* [了解使用 .NET Core 的 Docker 的基本信息](docker-basics-dotnet-core.md)
* [生成 .NET Core Docker 映像](building-net-docker-images.md)
