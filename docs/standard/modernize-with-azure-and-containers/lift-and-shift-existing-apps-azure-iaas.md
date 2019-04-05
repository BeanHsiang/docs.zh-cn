---
title: 提升并转移到 Azure IaaS （云基础结构的） 现有.NET 应用程序
description: 更新现有.NET 应用程序使用 Azure 云和 Windows 容器。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/28/2018
ms.openlocfilehash: 2b987d43f476f261bfdbd1b2af6ca7f792178cf8
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55266619"
---
# <a name="lift-and-shift-existing-net-apps-to-azure-iaas-cloud-infrastructure-ready"></a>提升并转移到 Azure IaaS （云基础结构的） 现有.NET 应用程序

> 设想：第一步中，若要减少你的本地投资回报和硬件和网络维护的总成本，只需重新托管云中你现有的应用程序。

在着手之前*如何*若要迁移到 Azure 基础结构即服务 (IaaS) 平台将现有应用程序，务必要分析的原因*为什么*你想要直接到 IaaS 迁移在 Azure 中。 在此更新成熟度级别方案实质上是开始在云中，而不是继续使用当前的本地基础结构中使用的 Vm。

若要分析的另一点是*为什么*可能想要迁移到纯 IaaS 云而不是仅仅增加了更高级的 Azure 中的托管的服务。 确定用例可能首先需要 IaaS。

图 2-1 现代化成熟度级别中定位云基础结构准备就绪的应用程序：

![定位云基础结构准备就绪的应用程序](./media/image2-1.png)

> **图 2-1.** 定位云基础结构准备就绪的应用程序

## <a name="why-migrate-existing-net-web-applications-to-azure-iaas"></a>为什么要迁移到 Azure IaaS 的现有.NET web 应用程序

若要将迁移到云中、 甚至是初始 IaaS 级别的主要原因是实现降低成本。 通过使用更多的托管基础结构服务，你的组织可以降低硬件维护、 服务器或 VM 预配和部署和基础结构管理其投资。

请将您的应用程序移动到云的决策后，让您决定选择 IaaS 而不是更多高级选项，如 PaaS 只需进行的 IaaS 环境的主要原因将更熟悉。 将移动到类似于你当前的环境，在本地环境提供了较低的学习曲线，这使得它到云的最快的途径。

但是，到云采用最快的路径并不意味着你将获得在云中运行应用程序从最大效益。 任何组织都将获得云迁移已引入的云优化和云本机成熟度级别从最大的好处。

也变得很明显，应用程序是更轻松地实现现代化，并在将来重构时它们已在云中、 甚至在 IaaS 中运行。 已实现应用程序数据迁移。 已还，获得在云中的工作所需的技能并对 shift"云区域性"。 在你的组织

## <a name="when-to-migrate-to-iaas-instead-of-to-paas"></a>何时迁移至而不是 IaaS 到 PaaS

接下来的部分讨论云优化的应用程序的主要基于 PaaS 平台和服务。 这些应用为您提供的大多数好处迁移到云。 

如果你的目标是只需移动到云的现有应用程序，首先要确定不需要修改大量，若要在 Azure 应用服务中运行的现有应用程序。 这些应用程序应该是第一个适合云计算得到优化。 

然后，应用，仍不能移动到 Windows 容器和 PaaS 如应用服务或 Azure Service Fabric 等业务流程协调程序迁移到简单的普通 Vm (IaaS)。 

但请记住，正确配置、 保护和维护 Vm 需要更多时间和 IT 专业知识相比于在 Azure 中使用 PaaS 服务。 如果你正在考虑 Azure 虚拟机，请确保所需修补、 更新和管理虚拟机环境的日常维护工作将其考虑到帐户。 Azure 虚拟机是 IaaS。

## <a name="use-azure-migrate-to-analyze-and-migrate-your-existing-applications-to-azure"></a>使用 Azure Migrate 来分析并迁移现有应用程序到 Azure

迁移到云并不一定要困难。 但是，许多组织不断努力，若要开始，以深入了解到的环境和应用程序、 工作负荷和数据之间的紧密相互依赖项。 了解不清，很难进行规划的未来发展途径。 没有什么已成功迁移所需的详细信息，不能在组织中具有适当的对话。 您不知道有足够的潜在成本效益，还是工作负荷可能只是提升和转移或需要大量的返工，若要成功迁移。 许多组织欢迎不奇怪。

[Azure Migrate](https://aka.ms/azuremigrate)是一种新的服务，提供指南、 见解和机制，以帮助你迁移到 Azure。 Azure Migrate 提供：

- 发现和评估本地虚拟机

- 多层应用程序的高置信度发现内置依赖关系映射

- 到 Azure 虚拟机的智能右大小调整

- 兼容性报告修正潜在的问题的指导原则

- 与 Azure 数据库管理服务集成以进行数据库发现和迁移

Azure Migrate 提供的工作负荷可以对业务影响最小迁移并按预期方式在 Azure 中运行的置信度。 使用合适的工具和指南，可以实现最大同时确保性能的关键投资回报和满足可靠性需求。

图 2-2 显示了由 Azure Migrate 执行的所有服务器和应用程序连接的内置依赖关系映射。

![定位云基础结构准备就绪的应用程序](./media/image2-2.png)

> **图 2-2。** 定位云基础结构准备就绪的应用程序

## <a name="use-azure-site-recovery-to-migrate-your-existing-vms-to-azure-vms"></a>使用 Azure Site Recovery 将现有 Vm 迁移到 Azure Vm

作为端到端的一部分[Azure Migrate](https://aka.ms/azuremigrate)， [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)是一个工具，可用于轻松地将你的 web 应用迁移到 Azure 中的 Vm。 您可以使用 Site Recovery 将本地 Vm 和物理服务器复制到 Azure，或将它们复制到辅助的本地位置。 甚至可以复制在本地上的受支持的 Azure VM 运行的工作负荷*HYPER-V* VM 上*VMware* VM，或在 Windows 或 Linux 的物理服务器上。 复制到 Azure 消除了成本和维护辅助数据中心的复杂性。

此外专门为混合环境的一部分进行站点恢复的本地和部分 on Azure。 Site Recovery 可帮助确保业务连续性使你在 Vm 运行的应用程序和本地物理服务器上可用如果在站点出现故障。 它将复制，以便它们仍然可用在辅助位置中，如果主站点不可用的 Vm 和物理服务器运行的工作负荷。 它会恢复到主站点时已启动并再次运行的工作负荷。

图 2-3 显示的多个 VM 迁移执行了使用 Azure Site Recovery。

![定位云基础结构准备就绪的应用程序](./media/image2-3.png)

> **图 2-3。** 定位云基础结构准备就绪的应用程序

### <a name="additional-resources"></a>其他资源

- **Azure Migrate Datasheet**

    [https://aka.ms/azuremigration\_datasheet](https://aka.ms/azuremigration\_datasheet)

- **Azure Migrate**

    [https://aka.ms/azuremigrate](https://aka.ms/azuremigrate)

- **Azure 迁移中心**

    [https://azure.microsoft.com/migration/](https://azure.microsoft.com/migration/)

- **使用 Site Recovery 迁移到 Azure**

    [https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-to-azure](https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-to-azure)

- **Azure Site Recovery 服务概述**

    [https://docs.microsoft.com/azure/site-recovery/site-recovery-overview](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)

- **将 Vm 迁移到 Azure Vm 的 AWS 中**

    [https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-aws-to-azure](https://docs.microsoft.com/azure/site-recovery/site-recovery-migrate-aws-to-azure)

>[!div class="step-by-step"]
>[上一页](index.md)
>[下一页](migrate-your-relational-databases-to-azure.md)
