---
title: 将关系数据库迁移到 azure
description: 更新现有.NET 应用程序使用 Azure 云和 Windows 容器 |将关系数据库迁移到 azure
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 04/28/2018
ms.openlocfilehash: 8cadfc99a4c3d32e24d4a44e8cf4ce17a2ba7a07
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57677547"
---
# <a name="migrate-your-relational-databases-to-azure"></a>将关系数据库迁移到 azure

设想：Azure 提供了最全面的数据库迁移。

在 Azure 中，你可以迁移您的数据库服务器直接到 IaaS Vm （纯提升与移动），或您可以将迁移到 Azure SQL 数据库，获取其他权益。 Azure SQL 数据库提供托管的实例和完整数据库作为-即服务 (DBaaS) 选项。 图 3-1 显示了多个关系数据库在 Azure 中可用的迁移路径。

![在 Azure 中的数据库迁移路径](./media/image3-1.png)

> **图 3-1。** 在 Azure 中的数据库迁移路径

## <a name="when-to-migrate-to-azure-sql-database-managed-instance"></a>何时迁移到 Azure SQL 数据库托管实例

在大多数情况下，Azure SQL 数据库托管实例将是您将数据迁移到 Azure 时要考虑的最佳选择。 如果你要迁移 SQL Server 数据库，并且需要几乎 100%保证，无需重新构建您的应用程序或对你的数据或数据访问代码进行更改，请选择 Azure SQL 数据库托管实例功能。

如果你有其他要求 SQL Server 实例级别的功能或超出标准的 Azure SQL 数据库 （单个数据库模型） 中提供的功能范围的隔离要求，azure SQL 数据库托管实例是最佳选择。 最后一项是最 PaaS 面向的选择，但它不提供与传统的 SQL server 的相同的功能。 迁移可能会出现的摩擦。

例如，在实例级别的 SQL Server 功能所做投资的组织将受益于迁移到 SQL 托管实例。 实例层级 SQL Server 功能的示例包括 SQL 公共语言运行时 (CLR) 集成，SQL Server 代理和跨数据库查询。 对这些功能的支持不可用标准的 Azure SQL 数据库 （单个数据库模型） 中。

组织，让其运行在高度管制行业中，且需要保持隔离出于安全目的，还可能会受益选择 SQL 托管实例模型。

在 Azure SQL 数据库托管的实例具有以下特征：

- 通过 Azure 虚拟网络的安全隔离

- 应用程序图面上与兼容性，这些功能：

  - SQL Server 代理和 SQL Server Profiler

  - 跨数据库引用和查询，SQL CLR、 复制、 变更数据捕获 (CDC) 和 Service Broker

- 数据库大小最多为 35 TB

- 使用这些功能最少的停机时间内迁移：

  - Azure 数据库迁移服务

  - 本机备份和还原，以及日志传送

使用这些功能，在现有应用程序数据库迁移到 Azure SQL 数据库托管实例模型提供了近 100%的 PaaS 的优势适用于 SQL Server。 托管的实例是继续使用实例级功能，而无需更改应用程序设计的 SQL Server 环境。

托管的实例可能是最适合企业的当前使用 SQL Server，并且需要灵活地在云中其网络安全。 它就像有有关 SQL 数据库的专用虚拟网络。

## <a name="when-to-migrate-to-azure-sql-database"></a>何时迁移到 Azure SQL 数据库

如前文所述，标准的 Azure SQL 数据库是完全托管的关系 DBaaS。 SQL 数据库当前 38 与世界各地的数据中心管理数以百万计的生产数据库。 它支持范围广泛的应用程序和工作负荷，从简单的事务数据，于促使需要在全球范围的高级的数据处理的最数据密集型、 任务关键型应用程序管理。

由于其完整的 PaaS 功能，更好地定价-，最终降低成本-您应该将移到标准 Azure SQL 数据库作为你的"默认情况下选择"如果您的应用程序，使用基本、 标准 SQL 数据库和任何其他实例功能。 在标准 Azure SQL 数据库中不支持 SQL Server 功能，如 SQL CLR 集成、 SQL Server 代理和跨数据库查询。 这些功能是仅在 Azure SQL 数据库托管实例模型中可用。

Azure SQL 数据库是为应用程序开发人员构建的仅智能云数据库服务。 它也是唯一的云数据库服务，缩放上动态，而无需停机时间，从而帮助你高效交付多租户应用。 从根本上讲，Azure SQL 数据库会使你更多时间进行创新，它并加速并加快推向市场。 可以构建安全应用程序并连接到 SQL 数据库使用的语言和您喜欢的平台。

Azure SQL 数据库提供以下优势：

- 学习和应用到您的应用程序的内置智能 （机器学习）

- 按需数据库预配

- 一系列产品/服务，适用于所有工作负荷

- 99.99%可用性 SLA，不需要维护

- 异地复制和还原服务的数据保护

- Azure SQL 数据库点还原功能

- 与 SQL Server 2016，包括混合和迁移的兼容性

标准的 Azure SQL Database 是更接近于 PaaS 比 Azure SQL 数据库托管实例。 选择标准的 Azure SQL 数据库，因为您将从托管的云有更多优势。 但是，Azure SQL 数据库有一些关键区别于常规和本地 SQL Server 实例。 根据现有应用程序的数据库要求和企业要求和策略，它可能规划在迁移到云时不是最佳选择。

## <a name="when-to-move-your-original-rdbms-to-a-vm-iaas"></a>何时将原始 RDBMS 移到 VM (IaaS)

迁移选项之一是继续在原始关系数据库管理系统 (RDBMS)，包括 Oracle、 IBM DB2、 MySQL、 PostgreSQL 或 SQL Server 到 Azure VM 运行的类似服务器。 如果必须在所有需要最快迁移到最小的更改或不做更改与云的现有应用程序，直接迁移到云中的 IaaS 可能是合理的选项。 它可能不会充分利用云的所有权益的最佳方法，但它可能是最快的初始路径。

目前，Microsoft Azure 支持最多[331 不同数据库服务器](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/databases?page=1&subcategories=databases-all)部署为 IaaS Vm。 其中包括 SQL Server、 Oracle、 MySQL、 PostgreSQL 和 IBM DB2 等常用 RDBMS 和 MongoDB、 Cassandra、 DataStax、 MariaDB 和 Cloudera 等许多其他 NoSQL 数据库。

> [!NOTE]
> 尽管移动到 Azure VM RDBMS 可能最快的方法 （因为它是 IaaS），将数据迁移到云，但这种方法需要投入大量的你的 IT 团队 （数据库管理员和 IT 专业人员）。 企业团队需要能够设置和管理高可用性、 灾难恢复和 SQL Server 修补的。 此上下文还需要具有完全管理权限的自定义的环境。

## <a name="when-to-migrate-to-sql-server-as-a-vm-iaas"></a>何时迁移到 SQL Server 作为虚拟机 (IaaS)

可能有几个情况下，仍需要迁移到常规 vm 的 SQL Server。 示例方案是如果您需要使用 SQL Server Reporting Services。 在大多数情况下，不过，Azure SQL 数据库托管实例可以提供将从迁移的本地 SQL 服务器，因此迁移到 SQL Server 虚拟机应尝试在最后一招所需的一切。

## <a name="use-azure-database-migration-service-to-migrate-your-relational-databases-to-azure"></a>Azure 数据库迁移服务用于将关系数据库迁移到 Azure 

可以使用 Azure 数据库迁移服务将 SQL Server、 Oracle 和 MySQL 等关系数据库迁移到 Azure，是否在目标数据库为 Azure SQL 数据库、 Azure SQL 数据库托管实例或在 Azure VM 上的 SQL Server。

自动化工作流，通过评估报告，可指导您完成您需要首先将数据库迁移进行的更改。 准备就绪后，该服务会将源数据库迁移到 Azure。

只要您更改原始 RDBMS，可能需要重新测试。 您可能还需要更改 SQL 句子或应用程序，具体取决于测试结果中的对象关系映射 (ORM) 代码。

如果有任何其他数据库 (例如，IBM DB2) 并选择使用直接方法，您可能想要继续使用这些数据库为 IaaS Vm 在 Azure 中，除非您是愿意执行更复杂的数据迁移。 更复杂的数据迁移将需要额外的努力，因为你将迁移到不同的数据库类型与新架构和不同的编程库。

若要了解如何使用 Azure 数据库迁移服务迁移数据库，请参阅[到 Azure SQL 数据库托管实例和 Azure 数据库迁移服务通过更快地在云中获取](https://channel9.msdn.com/Events/Build/2017/P4008)。

## <a name="additional-resources"></a>其他资源

- **选择云 SQL Server 选项：Azure SQL 数据库 (PaaS) 或 Azure VM (IaaS) 上的 SQL Server**

    [https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas)

- **转到 Azure SQL 数据库托管实例和数据库迁移服务通过更快地在云中**

    [https://channel9.msdn.com/Events/Build/2017/P4008](https://channel9.msdn.com/Events/Build/2017/P4008)

- **将 SQL Server 数据库迁移到云中的 SQL 数据库**

    [https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate)

- **Azure SQL 数据库**

    [https://azure.microsoft.com/services/sql-database/?v=16.50](https://azure.microsoft.com/services/sql-database/?v=16.50)

- **虚拟机上的 SQL Server**

    [https://azure.microsoft.com/services/virtual-machines/sql-server/](https://azure.microsoft.com/services/virtual-machines/sql-server/)

> [!div class="step-by-step"]
> [上一页](lift-and-shift-existing-apps-azure-iaas.md)
> [下一页](modernize-existing-apps-to-cloud-optimized/index.md)
