---
title: 云优化的应用程序中的 Microsoft 技术
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |云优化的应用程序中的 Microsoft 技术
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/28/2018
ms.openlocfilehash: 2f1d624365c168d14e98ed175d369f6aef18e42e
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53153873"
---
# <a name="microsoft-technologies-in-cloud-optimized-applications"></a>云优化的应用程序中的 Microsoft 技术

以下列表介绍工具、 技术和识别为云计算得到优化的应用程序要求的解决方案。 可以采用云计算得到优化的元素有选择地或逐步，具体取决于你的优先顺序。

-   **云基础结构**:提供的计算平台、 操作系统、 网络和存储的基础结构。 Microsoft Azure 位于此级别。

-   **运行时**:此层提供了用于运行应用程序的环境。 如果使用的容器，此层通常基于[Docker 引擎](https://docs.docker.com/engine/)，Linux 主机上或在 Windows 主机上运行。 ([Windows 容器](https://docs.microsoft.com/virtualization/windowscontainers/about/)从 Windows Server 2016 开始支持。 Windows 容器是在 Windows 运行的现有.NET Framework 应用程序的最佳选择。）

-   **托管云**:当您选择托管的云选项时，可以避免的花费和麻烦的管理和支持的基础的基础结构 Vm、 OS 修补程序，与网络配置。 如果您选择使用 IaaS 迁移，您是负责所有这些任务，以及关联的成本。 在托管的云选项中，你可以管理应用程序和服务开发的。 云服务提供商通常管理所有其他内容。 在 Azure 中托管的云服务的示例包括[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database)， [Azure Redis 缓存](https://azure.microsoft.com/services/cache/)， [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)， [Azure 存储](https://azure.microsoft.com/services/storage/)，[Azure Database for MySQL](https://azure.microsoft.com/services/mysql/)， [Azure Database for PostgreSQL](https://azure.microsoft.com/services/postgresql/)， [Azure Active Directory](https://azure.microsoft.com/services/active-directory/)，并托管计算服务，如[VM 规模设置](https://azure.microsoft.com/services/virtual-machine-scale-sets/)， [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)， [Azure 应用服务](https://azure.microsoft.com/services/app-service/)，并且[Azure Kubernetes 服务](https://azure.microsoft.com/services/container-service/)。

-   **应用程序开发**:您可以生成在容器中运行的应用程序时，从许多语言选择。 本指南重点[.NET](https://www.microsoft.com/net)，但您可以通过使用其他语言，如 Node.js、 Python、 Spring/Java，开发基于容器的应用或转。

-   **监视遥测，日志记录和审核**:对监视并审核应用程序和在云中运行的容器的能力是关键的任何云计算得到优化的应用程序。 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/)并[Microsoft Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite)是主要的 Microsoft 工具，为云优化的应用程序提供监视和审核。

-   **预配**:自动化工具可帮助你预配基础结构和应用程序部署到多个环境 （生产、 测试、 过渡）。 Chef 和 Puppet 等工具可用于管理应用程序的配置和环境。 此外可以通过使用简单、 更直接的方法实现这一层。 例如，您可以直接通过 Azure 命令行接口 (Azure CLI) 工具、 部署，然后使用连续部署和发布管理管道中的[Azure DevOps 服务](https://visualstudio.microsoft.com/team-services/)。

-   **应用程序生命周期**:[Azure DevOps 服务](https://visualstudio.microsoft.com/team-services/)和 Jenkins，等其他工具是帮助你的生成的自动化服务器实现 CI/CD 管道，其中包括发布管理。

本章节中和的相关的演练的下一步部分专门重点介绍有关运行时层 （Windows 容器） 的详细信息。 本指南介绍你可以部署 Windows Server 2016 （和更高版本） 上的 Windows 容器的 Vm 和 Azure 容器实例的方法。 它还介绍了更高级的 PaaS 平台，如 Azure 应用服务和业务流程协调程序类似于 Azure Service Fabric 和 Azure Kubernetes 服务。

## <a name="monolithic-applications-can-be-cloud-optimized"></a>单一式应用程序*可以*是云计算得到优化

务必要突出显示该单一式应用程序 （不基于微服务的应用程序）*可以*是云计算得到优化的应用程序。 您可以构建和运行整体式应用程序，充分利用云计算模型的容器、 持续交付和 DevOps 结合使用。 如果现有单一式应用程序是正确的业务目标，可以让其现代化并使其云计算得到优化。

同样，如果单一式应用程序可以将云优化的应用程序，可以还为云优化的应用程序优化其他、 更复杂的体系结构，如 N 层应用程序。

>[!div class="step-by-step"]
>[上一页](reasons-to-modernize-existing-net-apps-to-cloud-optimized-applications.md)
>[下一页](what-about-cloud-native-applications.md)