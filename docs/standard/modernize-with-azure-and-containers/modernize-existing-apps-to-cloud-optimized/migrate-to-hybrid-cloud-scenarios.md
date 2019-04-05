---
title: 将迁移到混合云方案
description: 更新现有.NET 应用程序与 Azure 云和 Windows 容器 |将迁移到混合云方案
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/30/2018
ms.openlocfilehash: 3d6fc272854654d890559d5db032b05667627d94
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53147328"
---
# <a name="migrate-to-hybrid-cloud-scenarios"></a>将迁移到混合云方案

某些组织和企业不能将其某些应用程序到 Microsoft Azure 等公有云或由于法规或他们自己的策略的任何其他公有云迁移。 但是，可能是任何组织可能具有一些在公有云与其他应用程序的本地应用程序受益。 但在环境中由于不同的平台和技术在公有云与本地环境中使用过多的复杂性可能会导致混合的环境。

Microsoft 提供了最佳的混合云解决方案，其中一个可以在其中优化现有资产的本地和公有云中，确保 Azure 混合云的一致性。 你可以最大程度提高现有技能，并获取一种灵活、 统一的方法，来生成可在云中或本地，得益于 Azure Stack （内部） 和 Azure （公有云） 中运行的应用。

谈到安全性，您可以跨混合云来集中管理和安全。 你可以通过单一登录方式登录到在本地提供从数据中心到云，获取对所有资产的控制和云应用。 通过将 Active Directory 扩展到混合云，并使用标识管理实现此目的。

最后，可以将分发和无缝地分析数据、 对在本地和云资产，使用相同的查询语言和应用分析和深度学习来丰富您的数据，而不考虑其源。

## <a name="azure-stack"></a>Azure Stack

Azure Stack 是一种混合云平台，可从组织的数据中心交付 Azure 服务。 Azure Stack 旨在支持现代应用程序中关键方案，如边缘和未连接的环境中或满足特定安全性和符合性要求的新选项。

图 4-13 显示了 Microsoft 提供的真正的混合云平台的概述。

![使用 Azure Stack 和 Azure 的 Microsoft 混合云平台](./media/image13.jpg)

> **图 4 月 13 日。** 使用 Azure Stack 和 Azure 的 Microsoft 混合云平台

Azure Stack 中两个部署选项，以满足你的需求提供：

-   Azure Stack 集成系统

-   Azure Stack 开发工具包

### <a name="azure-stack-integrated-systems"></a>Azure Stack 集成系统

Azure Stack 集成系统将通过 Microsoft 和硬件合作伙伴提供的合作关系提供。 合作关系创建一个解决方案，提供了与管理的简化保持平衡的兼顾云时代的创新。 由于 Azure Stack 作为集成系统的硬件和软件提供，您将获取适量的灵活性和控制，时仍采用云环境带来的创新。 Azure Stack 集成系统范围的大小从 4 到 12 个节点，由硬件合作伙伴和 Microsoft 共同提供支持。 使用 Azure Stack 集成系统来实现生产工作负荷的新方案。

### <a name="azure-stack-development-kit"></a>Azure Stack 开发工具包

Microsoft Azure Stack 开发工具包是单节点部署的 Azure Stack，可用于评估和了解 Azure Stack。 作为开发人员环境，其中您可以使用 Api 进行开发和工具，是与 Azure 一致，您还可以使用 Azure Stack 开发工具包。 Azure Stack 开发工具包不能用作生产环境。

### <a name="additional-resources"></a>其他资源

-   **Azure 混合云**

    [https://www.microsoft.com/cloud-platform/hybrid-cloud](https://www.microsoft.com/cloud-platform/hybrid-cloud)

-   **Azure Stack**

    [https://azure.microsoft.com/overview/azure-stack/](https://azure.microsoft.com/overview/azure-stack/)

-   **Active Directory 服务帐户用于 Windows 容器**

    [https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts)

-   **创建具有 Active Directory 支持的容器**

    [https://blogs.msdn.microsoft.com/containerstuff/2017/01/30/create-a-container-with-active-directory-support/](https://blogs.msdn.microsoft.com/containerstuff/2017/01/30/create-a-container-with-active-directory-support/)

-   **Azure 混合权益许可**

    [https://azure.microsoft.com/pricing/hybrid-use-benefit/](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

>[!div class="step-by-step"]
>[上一页](modernize-your-apps-lifecycle-with-ci-cd-pipelines-and-devops-tools-in-the-cloud.md)
>[下一页](../walkthroughs-technical-get-started-overview.md)