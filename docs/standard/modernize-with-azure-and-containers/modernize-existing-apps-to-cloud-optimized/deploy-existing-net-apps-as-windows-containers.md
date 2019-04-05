---
title: 将现有.NET 应用部署为 Windows 容器
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |将现有.NET 应用部署为 Windows 容器
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/29/2018
ms.openlocfilehash: 646acc6fd14c1ff85593dbf6074f0d03d86f04bd
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53143742"
---
# <a name="deploy-existing-net-apps-as-windows-containers"></a>将现有.NET 应用部署为 Windows 容器

基于 Windows 容器的部署都适用于云优化的应用程序和云本机应用程序。

但是，本指南中，尤其是在以下各节，它主要侧重于使用 Windows 容器*云计算得到优化*您无需重新构建您的应用程序的应用程序。

## <a name="what-are-containers-linux-or-windows"></a>什么是容器？ （Linux 或 Windows）

容器是一种方法来打包到其自己的独立包的应用程序。 在其容器中，应用程序不受应用程序或容器之外的进程。 所有内容应用程序依赖于以运行已成功为进程在容器内。 容器可能会移动任何位置，应用程序要求始终得到满足，方面直接依赖项，因为它与捆绑在一起运行 （库依赖项、 运行时，等） 所需的所有内容。

容器的主要特征是，它可在环境相同跨不同的部署因为容器本身附带了其所需的所有依赖项。 可以在计算机上调试应用程序并将其部署到另一台计算机具有相同的环境保证。

容器是容器映像的实例。 容器映像是一种方法来打包的应用或服务 （如 snapshot）)，然后将它部署可靠且可重现的方式。 可以说 Docker 不只一技术的 it 还的基本原理和过程。

每日容器变得越来越普遍，因为这些访客成为行业范围"单元的部署。

## <a name="benefits-of-containers-docker-engine-on-linux-or-windows"></a>容器 （在 Linux 或 Windows 上的 Docker 引擎） 的优点

使用容器，以生成应用程序也可能是中定义为轻量的构建基块产品/服务显著增加生成、 传送和任何基础结构之间运行任何应用程序的灵活性。

使用容器，您可以采取任何应用从开发到生产环境很少或没有的代码更改，得益于 Docker 集成跨 Microsoft 开发人员工具、 操作系统和云。

在部署于普通 Vm 时，您可能已经有适用于 ASP.NET 应用部署到 Vm 具有方法。 很可能，不过，您的方法涉及多个手动步骤或复杂的自动化的过程，使用 Puppet 等部署工具或类似的工具。 您可能需要执行任务，例如修改配置项目、 将应用程序内容，在服务器之间复制和运行基于.msi 安装后, 跟测试的交互式安装程序。 在部署中的所有这些步骤将添加到部署的时间和风险。 每当依赖项不存在于目标环境时，将出现故障。

在 Windows 容器中的应用程序打包过程完全自动化。 Windows 容器基于 Docker 平台，它提供了自动更新和回滚容器部署。 从使用 Docker 引擎获取的主要改进是及其所有依赖项创建映像，就像您的应用程序的快照，这些映像。 映像是 Docker 映像 （Windows 容器中的映像，这种情况下）。 映像运行的 ASP.NET 应用程序在容器中，无需返回到源代码。 容器快照将成为部署单元。

由于以下原因，许多组织都容器化现有单一式应用程序：

-   **版本通过改进的部署实现灵便性**。 容器提供开发和运营之间的一致的部署协定。 当使用容器时，您不会听到开发人员说，"适用于我的计算机，为什么不在生产环境中？" 他们可以说"它运行作为容器，因此它将在生产环境中运行。" 已包装的应用程序，及其所有依赖项，可以在任何受支持的基于容器的环境中执行。 它将运行其目的是在所有部署目标 （开发、 QA、 暂存、 生产） 中运行的方式。 容器消除大多数的摩擦，当它们从一个阶段移动到下一步，极大地提高了部署，并可以更快地交付。

-   **成本降低**。 容器会导致降低成本，通过合并和删除的现有硬件，或在每个硬件单位更高的密度运行的应用程序。

-   **可移植性**。 容器是模块化且可移植。 在任何服务器操作系统 （Linux 和 Windows） 中任何大型公共云 （Microsoft Azure、 Amazon AWS、 Google、 IBM），并在本地和专用或混合云环境上支持 docker 容器。

-   **控制**。 容器提供灵活可靠的环境，在容器级别控制。 容器可以保护、 隔离，并且甚至在容器上设置执行约束策略受限制。 如本节中有关 Windows 容器所述，Windows Server 2016 和 HYPER-V 容器提供额外的企业级支持选项。

使用容器开发和维护应用程序时，敏捷性、 可移植性和控制中的重大改进最终导致显著降低成本。

## <a name="what-is-docker"></a>什么是 Docker？

[Docker](https://www.docker.com/)是[开放源代码项目](https://github.com/docker/docker)用于自动部署应用程序作为可以在云或本地运行的便携式独立容器。 Docker 也是一家促进和发展这项技术的[公司](https://www.docker.com/)。 公司中与云，Linux 和 Windows 供应商，包括 Microsoft 协作工作原理。

![](./media/image6.png)

> **图 4-6。** Docker 在混合云的所有层部署容器

某个人可以使用熟悉的虚拟机，容器可能看起来非常类似。 容器运行的操作系统、 具有文件系统，并且可以通过网络，就像物理或虚拟计算机系统访问。 但是，技术和容器背后的概念是迥然不同的虚拟机。 从开发人员的角度来看，容器必须被更当作单个进程。 事实上，容器都有一个进程的单一入口点。

Docker 容器 (为简单起见，*容器*) 可以在 Linux 和 Windows 上本机运行。 仅在 Windows 主机 （主机服务器或 VM） 上运行时正则容器，可以运行 Windows 容器和 Linux 容器可以仅在 Linux 主机上运行。 但是，在最新版本的 Windows Server 和 HYPER-V 容器，Linux 容器也可以本机运行 Windows Server 上使用目前仅在 Windows Server 容器中可用的 HYPER-V 隔离技术。

在不久的将来，将 Linux 和 Windows 容器的混合的环境将是可能和常见。

## <a name="benefits-of-windows-containers-for-your-existing-net-applications"></a>Windows 容器的现有.NET 应用程序的优点

使用 Windows 容器的好处基本上是相同的好处一般情况下获取容器中。 使用 Windows 容器用于极大地提高灵活性、 可移植性和控制。

现有.NET 应用程序是指那些使用.NET Framework 创建的应用程序。 例如，它们可能是传统的 ASP.NET web 应用程序-不使用.NET Core，后者是较新，并运行跨平台在 Linux、 Windows 和 MacOS 上。

.NET Framework 中的主要依赖项是 Windows。 它还具有传统的 ASP.NET 中的次要依赖项，如 IIS 和 System.Web。

.NET Framework 应用程序必须在运行 Windows，时间段。 如果你想要化现有.NET Framework 应用程序并且你不能或不希望投资迁移到.NET Core （"如果它能正常工作，不将其迁移"），你有针对容器是唯一选择是使用 Windows 容器。

因此，Windows 容器的主要优势之一是，它们为您提供一种方法来更新现有.NET Framework 应用程序，Windows 通过集装箱化上运行。 从根本上讲，Windows 容器可帮助你正在寻找使用容器的灵活、 可移植性和更好地控制的好处。

## <a name="choose-an-os-to-target-with-net-based-containers"></a>选择目标时使用的操作系统。基于 NET 的容器

给定的操作系统支持 Docker，以及.NET Framework 和.NET Core 之间的差异的多样性，应针对特定操作系统和基于正在使用的 framework 的特定版本。

对于 Windows，可使用 Windows Server Core 或 Windows Nano Server。 这些 Windows 版本提供所需的.NET Framework 或.NET Core 应用程序的不同特征 （如 IIS 与 Kestrel 类似的自承载的 web 服务器)。

对于 Linux，正式的 .NET Docker 映像（如 Debian）中提供并支持多个发行版本。

图 4-7 显示了你可以针对，具体取决于应用的.NET Framework 版本的操作系统版本。

![](./media/image7.png)

> **图 4-7。** 基于.NET Framework 版本的目标操作系统

在基于.NET Framework 应用程序的现有或旧版应用程序的迁移方案，主要依赖项是 Windows 和 IIS 上。 您的唯一选择是使用基于 Windows Server Core 和.NET Framework 的 Docker 映像。

时映像名称添加到 Dockerfile 文件后，可以选择的操作系统和版本，使用标记，如基于.NET Framework 的 Windows 容器映像的以下示例所示：

> | **标记** | **系统和版本** |
> |---|---|
> | **microsoft/dotnet-framework:4.x-windowsservercore** | .NET framework 4.x Windows Server Core 上 |
> | **microsoft/aspnet:4.x-windowsservercore** | .NET framework 4.x 与其他 ASP.NET 自定义，在 Windows Server Core 上 |

为.NET Core （适用于 Linux 和 Windows 跨平台），标记将如下所示：

> | **标记** | **系统和版本**
> |---|---|
> | **microsoft/dotnet:2.0.0-runtime** | .NET Core 2.0 仅运行时在 Linux 上 |
> | **microsoft/dotnet:2.0.0-runtime-nanoserver** | .NET Core 2.0 仅运行时在 Windows Nano Server 上 |

### <a name="multi-arch-images"></a>多体系结构映像

从 2017 中旬开始，你还可以使用新功能在 Docker 调用中[多体系结构](https://github.com/moby/moby/issues/15866)映像。 .NET Core Docker 映像可以使用多 arch 标记。 Dockerfile 不再文件需定义你面向的操作系统。 使用多 arch 功能，用于跨多个计算机配置的单个标记。 例如，多体系结构，您可以使用一个通用的标签： **microsoft/dotnet:2.0.0-runtime**。 如果请求 Linux 容器环境中的使用该标记时，获取基于 Debian 的映像。 如果请求 Windows 容器环境中使用该标记时，获取基于 Nano Server 的映像。

对于.NET Framework 映像，因为传统的.NET Framework 支持仅 Windows，不能使用多体系结构的功能。

## <a name="windows-container-types"></a>Windows 容器类型

Linux 容器，如 Windows Server 容器通过 Docker 引擎管理。 与 Linux 容器不同 Windows 容器包括两种不同的容器类型，或运行时间 Windows Server 容器和 HYPER-V 隔离。

**Windows Server 容器**:提供应用程序通过进程和命名空间隔离技术隔离。 Windows Server 容器与容器主机和主机运行的所有容器共享内核。 这些容器不提供恶意安全边界，不应使用隔离不受信任的代码。 由于共享的内核空间，这些容器需要相同的内核版本和配置。

**HYPER-V 隔离**:提供由 Windows Server 容器通过在高度优化的 VM 上运行每个容器的隔离上扩展。 在此配置中，与同一主机上的其他容器不共享容器主机的内核。 这些容器旨在用于恶意多租户托管，与 VM 的相同的安全保证。 这些容器不与主机或主机上的其他容器共享内核，因为它们可以使用不同版本和配置 （具有支持的版本） 运行的内核。 例如，Windows 10 上的所有 Windows 容器都使用的 HYPER-V 隔离来利用 Windows Server 内核版本和配置。

在 Windows 上运行容器，带或不带 HYPER-V 隔离是运行时决定。 可以选择最初，创建具有 HYPER-V 隔离的容器，并在运行时，选择为 Windows Server 容器运行它。

### <a name="additional-resources"></a>其他资源

-   **Windows 容器文档**

    [https://docs.microsoft.com/virtualization/windowscontainers/](https://docs.microsoft.com/virtualization/windowscontainers/)

-   **Windows 容器基础知识**

    [https://docs.microsoft.com/virtualization/windowscontainers/about/](https://docs.microsoft.com/virtualization/windowscontainers/about/)

-   **信息图：Microsoft 和容器**

    [https://info.microsoft.com/rs/157-GQE-382/images/Container%20infographic%201.4.17.pdf](https://info.microsoft.com/rs/157-GQE-382/images/Container%20infographic%201.4.17.pdf)


## <a name="the-container-ecosystem-in-azure"></a>Azure 中的容器生态系统

在前面部分，它已经介绍了 Docker 容器的好处是什么以及.NET 应用程序的特定容器映像的详细信息。 所有这些泛型信息是为了开发或容器化应用程序的基础。
但是，当正在思考如何进行生产部署环境或甚至 QA 和开发/测试环境，Microsoft Azure 提供打开和广泛的各种选项，（下图中所示） 在云中的完整容器生态系统。 具体取决于特定应用程序的需求，应选择一个或另一个 Azure 产品。

![](./media/image7.5.png)

> **图 4-7.5。** Azure 中的容器生态系统

从容器生态系统，在 Azure 中，支持将被视为基础结构的容器的以下产品：
-   **Azure 容器实例 (ACI)**
-   **Azure 虚拟机**（与容器的支持）
-   **Azure 虚拟机规模集**（与容器的支持）

从这三个 ACI 提供了很大的收益，这是无需维护基础操作系统，你无需升级/修补程序等，但 ACI 仍在基础结构级别，以更好地进行解释这本书后面几节中放置的事实。

Azure 支持的容器在同一时间多置于 PaaS （平台即服务） 级别中的产品是：

-   **Azure 应用服务**
-   **Azure Kubernetes 服务 （AKS 和 ACS）**
-   **Azure Service Fabric** 
-   **Azure 批处理** 

然后，Azure 容器注册表是可以从所有以前的产品注册和部署你的自定义容器映像时使用的 Azure 中托管的高可缩放的容器注册表。

此外，从你的容器，可以使用其他托管的服务等 Azure SQL 数据库，Azure Redis 缓存，Azure Cosmos DB 等 Azure 中。 此外，第三方解决方案/平台中提供了如 Cloud Foundry 和 OpenShift 还可以使用 Azure 中的容器的 Azure Marketplace。 

在下一步部分中，你可以浏览 Microsoft 的有关何时使用这些 Azure 产品和解决方案的每个专门面向 Windows 容器时的建议。

>[!div class="step-by-step"]
>[上一页](what-about-cloud-native-applications.md)
>[下一页](when-not-to-deploy-to-windows-containers.md)