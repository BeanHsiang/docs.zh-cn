---
title: 实例激活
ms.date: 03/30/2017
ms.assetid: 134c3f70-5d4e-46d0-9d49-469a6643edd8
ms.openlocfilehash: 41dfc076bdee72c2f4d0c781c6588caa927c740e
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703391"
---
# <a name="instance-activation"></a>实例激活
SQL 工作流实例存储运行一个内部任务，该任务将定期唤醒并检测持久性数据库中是否有可运行或可激活的工作流实例。 如果找到可运行的工作流实例，SQL 工作流实例存储将通知能够激活该实例的工作流主机。 如果实例存储找到可激活的工作流实例，它将通知用于激活工作流主机的泛型主机，而泛型主机将运行此工作流实例。 本主题的以下各节详细说明了实例激活过程。  
  
## <a name="RunnableSection"></a> 检测和激活可运行工作流实例  
 SQL 工作流实例存储将工作流实例视为*可运行*如果实例未处于挂起的状态或已完成的状态并且满足以下条件：  
  
-   实例处于解除锁定状态，并且具有已过期的挂起计时器。  
  
-   实例上的锁已过期。  
  
-   对实例进行解锁且其状态为**Executing**。  
  
 当 SQL 工作流实例存储找到可运行的实例时，将引发 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent>。 此后，SqlWorkflowInstanceStore 将停止监视，直到在该存储上调用一次 <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>。  
  
 已订阅 <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> 且能够加载该实例的工作流主机将针对实例存储执行 <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>，以将该实例加载到内存中。 工作流主机被视为能够加载工作流实例，如果主机和实例元数据属性**WorkflowServiceType**设置为相同值。  
  
## <a name="detecting-and-activating-activatable-workflow-instances"></a>检测和激活可激活的工作流实例  
 工作流实例被视为*可激活*没有能够加载该实例的工作流主机是否可运行，并且没有正在运行的计算机上。 有关可运行的工作流实例的定义，请参见上面的“检测和激活可运行的工作流实例”。  
  
 当 SQL 工作流实例存储在数据库中找到可激活的工作流实例时，将引发 <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent>。 此后，SqlWorkflowInstanceStore 将停止监视，直到在该存储上调用一次 <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand>。  
  
 当已订阅 <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent> 的泛型主机接收到此事件时，它将针对实例存储执行 <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand> 以获取创建工作流主机所需的激活参数。 泛型主机使用这些激活参数来创建工作流主机，后者又依次加载并运行可运行的服务实例。  
  
## <a name="generic-hosts"></a>泛型主机  
 泛型主机是元数据属性的值与主机**WorkflowServiceType**对于泛型主机将设置为**WorkflowServiceType.Any**以指示它可以处理任何工作流类型。 泛型主机采用名为的 XName 参数**ActivationType**。  
  
 目前，SQL 工作流实例存储支持 ActivationType 参数设置为值的泛型主机**WAS**。 如果未将 ActivationType 设置为 WAS，SQL 工作流实例存储将引发 <xref:System.Runtime.DurableInstancing.InstancePersistenceException>。 Workflow Management Service 附带[!INCLUDE[dublin](../../../includes/dublin-md.md)]是设置为将激活类型的泛型主机**WAS**。  
  
 为了实现 WAS 激活，泛型主机需要一组激活参数来派生激活新主机所在的终结点地址。 用于 WAS 激活的激活参数包括：站点名称、应用程序路径（相对于站点）和服务路径（相对于应用程序）。 SQL 工作流实例存储在执行 <xref:System.Activities.DurableInstancing.SaveWorkflowCommand> 期间存储这些激活参数。  
  
## <a name="runnable-instances-detection-period"></a>可运行实例的检测周期  
 **可运行实例的检测周期**SQL 工作流实例存储的属性指定的时间段后将 SQL 工作流实例存储运行一个检测任务，以检测任何可运行或可激活的工作流上一检测周期后持久性数据库中的实例。 请参阅[可运行实例的检测周期](runnable-instances-detection-period.md)有关此属性的详细信息。
