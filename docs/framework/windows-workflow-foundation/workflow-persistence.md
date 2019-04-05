---
title: 工作流持久性
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], persistence
ms.assetid: 39e69d1f-b771-4c16-9e18-696fa43b65b2
ms.openlocfilehash: db0e4acc76f758004948857fc0b23a9cbc62f244
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715537"
---
# <a name="workflow-persistence"></a>工作流持久性
工作流持久性是指独立于进程或计算机信息持续捕获工作流实例的状态。 其目的在于：在发生系统故障时为工作流实例提供一个已知恢复点，通过卸载当前未主动执行工作的工作流实例来节省内存，或者将工作流实例状态从服务器场中的一个节点移至另一个节点。  
  
 持久性支持进程灵活性、可扩展性、故障恢复以及更有效地管理内存的功能。 持久性进程包括标识持久点、收集要保存的数据以及将数据实际存储最终委托给持久性提供程序。  
  
 若要启用工作流的持久性，您需要将实例存储与相关联**WorkflowApplication**或**WorkflowServiceHost**中所述[如何：为工作流和工作流服务启用持久性](how-to-enable-persistence-for-workflows-and-workflow-services.md)。 **WorkflowApplication**并**WorkflowServiceHost**使用与其关联的实例存储到持久性存储区中，并加载到工作流实例将工作流实例基于存储在持久性存储区中的工作流实例数据的内存。  
  
 [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]附带**SqlWorkflowInstanceStore**类，该类允许的数据和有关在 SQL Server 2005 或 SQL Server 2008 数据库的工作流实例的元数据持久性。 请参阅[SQL 工作流实例存储](sql-workflow-instance-store.md)的更多详细信息。  
  
 若要存储和加载应用程序特定数据以及与工作流实例相关的信息，您可以创建用于扩展 <xref:System.Activities.Persistence.PersistenceParticipant> 类的持久性参与者。 持久性参与者参与持久性进程的目的是：将可序列化的自定义数据保存到持久性存储中，将实例存储中的数据加载到内存中，以及在持久性事务下执行任何其他逻辑。 有关详细信息，请参阅[持久性参与者](persistence-participants.md)。  
  
 Windows Server App Fabric 大大简化了配置持久性的过程。 有关详细信息，请参阅[Windows Server App Fabric 的持久性概念](https://go.microsoft.com/fwlink/?LinkId=201200)  
  
## <a name="implicit-persistence-points"></a>隐式持久点  
 以下列表包含当实例存储与工作流关联时持久化工作流所依据的条件的示例。  
  
-   当**TransactionScope**活动完成或**TransactedReceiveScope**活动完成。  
  
-   当工作流实例变为空闲状态并**WorkflowIdleBehavior**对工作流主机设置。 发生这种情况，例如，当使用消息传递活动或**延迟**活动。  
  
-   当 WorkflowApplication 变为空闲状态并**PersistableIdle**应用程序的属性设置为**PersistableIdleAction.Persist**。  
  
-   当指示主机应用程序保存或卸载工作流实例时。  
  
-   当中止工作流实例或工作流实例结束时。  
  
-   当**Persist**活动执行。  
  
-   当使用 Windows Workflow Foundation 的早期版本开发的工作流实例在可互操作执行过程中遇到持久点时。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [SQL 工作流实例存储](sql-workflow-instance-store.md)  
  
-   [实例存储](instance-stores.md)  
  
-   [暂留参与者](persistence-participants.md)  
  
-   [暂留最佳做法](persistence-best-practices.md)  
  
-   [非暂留工作流实例](non-persisted-workflow-instances.md)  
  
-   [暂停和继续工作流](pausing-and-resuming-a-workflow.md)
