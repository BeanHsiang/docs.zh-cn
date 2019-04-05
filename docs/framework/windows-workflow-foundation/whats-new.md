---
title: Windows Workflow Foundation 中的新增功能
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Workflow Foundation [WF], what's new
- WF [WF], what's new
ms.assetid: 11f96014-001e-41a0-bcc2-d0684a52fa43
ms.openlocfilehash: 5ab1419a29dd77ac276681bb49dc529fc05d5b15
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711819"
---
# <a name="whats-new-in-windows-workflow-foundation"></a>Windows Workflow Foundation 中的新增功能
中的 Windows Workflow Foundation (WF)[!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)]从以前的版本更改多个开发范例。 现在，工作流可以更方便地创建、执行、维护和实现许多新功能。 有关迁移.NET 3.0 和.NET 3.5 工作流应用程序以使用最新版本的详细信息，请参阅[迁移指南](migration-guidance.md)。  
  
## <a name="workflow-activity-model"></a>工作流活动模型  
 现在，活动是创建工作流的基本单元，它取代了使用的 <xref:System.Workflow.Activities.SequentialWorkflowActivity> 或 <xref:System.Workflow.Activities.StateMachineWorkflowActivity> 类。 <xref:System.Activities.Activity> 类提供工作流行为的抽象基类。 然后，活动作者可以实现基本自定义活动的 <xref:System.Activities.CodeActivity> 功能，或实现使用运行时范围的自定义活动功能的 <xref:System.Activities.NativeActivity>。 <xref:System.Activities.Activity> 是活动作者用于表示以声明方式在其他方面的新行为的类<xref:System.Activities.NativeActivity>， <xref:System.Activities.CodeActivity>， <xref:System.Activities.AsyncCodeActivity>，或<xref:System.Activities.DynamicActivity>对象，无论它们是自定义开发或包含在中[内置活动库](net-framework-4-5-built-in-activity-library.md)。  
  
## <a name="rich-composite-activity-options"></a>丰富的复合活动选项  
 <xref:System.Activities.Statements.Flowchart> 是一个功能强大的新控制流活动，作者可将其用于对任意循环和条件分支进行建模。 <xref:System.Activities.Statements.Flowchart> 提供了一个由事件驱动的编程模型，该模型以前只能通过 <xref:System.Workflow.Activities.StateMachineWorkflowActivity> 来实现。 程序工作流得益于对传统流控制结构进行建模的新增流控制活动，例如 <xref:System.Activities.Statements.TryCatch> 和 <xref:System.Activities.Statements.Switch%601>。  
  
## <a name="expanded-built-in-activity-library"></a>扩展的内置活动库  
 该活动库的新增功能包括：  
  
-   新增流控制活动，例如 <xref:System.Activities.Statements.DoWhile>、<xref:System.Activities.Statements.Pick>、<xref:System.Activities.Statements.TryCatch>、<xref:System.Activities.Statements.ForEach%601>、<xref:System.Activities.Statements.Switch%601> 和 <xref:System.Activities.Statements.ParallelForEach%601>。  
  
-   用于操作成员数据的活动，例如 <xref:System.Activities.Statements.Assign> 和集合活动（如 <xref:System.Activities.Statements.AddToCollection%601>）。  
  
-   用于控制事务的活动，例如 <xref:System.Activities.Statements.TransactionScope> 和 <xref:System.Activities.Statements.Compensate>。  
  
-   新增消息传递活动，例如 <xref:System.ServiceModel.Activities.SendContent> 和 <xref:System.ServiceModel.Activities.ReceiveReply>。  
  
## <a name="explicit-activity-data-model"></a>显式活动数据模型  
 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 包含用于存储或移动数据的新选项。 可以使用 <xref:System.Activities.Variable> 在活动中存储数据。 当在活动中移入和移出数据时，将使用专用参数类型来确定数据的移动方向。 这些类型包括 <xref:System.Activities.InArgument>、<xref:System.Activities.InOutArgument> 和 <xref:System.Activities.OutArgument>。 有关详细信息，请参阅[Windows Workflow Foundation 数据模型](data-model.md)。  
  
## <a name="enhanced-hosting-persistence-and-tracking-options"></a>增强的宿主、持久性和跟踪选项  
 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 包含如下持久性增强功能：  
  
-   提供了更多用于运行工作流的选项，其中包括 <xref:System.ServiceModel.Activities.WorkflowServiceHost>、<xref:System.Activities.WorkflowApplication> 和 <xref:System.Activities.WorkflowInvoker>。  
  
-   可以使用 <xref:System.Activities.Statements.Persist> 活动显式保存工作流状态数据。  
  
-   主机可以保存 <xref:System.Activities.ActivityInstance>，而不必卸载它。  
  
-   当使用无法保存的数据时，工作流可以指定非保存区域，以便推迟保存，直到退出非保存区域为止。  
  
-   可以使用 <xref:System.Activities.Statements.TransactionScope> 使事务流入到工作流中。  
  
-   使用 <xref:System.Activities.Tracking.TrackingParticipant> 可以更方便地完成跟踪。  
  
-   使用 <xref:System.Activities.Tracking.EtwTrackingParticipant> 可以提供对系统事件日志的跟踪。  
  
-   现在可以使用 <xref:System.Activities.Bookmark> 对象管理对挂起的工作流的恢复。  
  
## <a name="easier-ability-to-extend-wf-designer-experience"></a>简化的 WF 设计器扩展体验功能  
 新 WF 设计器内置上 Windows Presentation Foundation (WPF) 和提供更简单的模型时重新承载 WF 设计器在 Visual Studio 外部使用，还提供了用于创建自定义活动设计器的简单机制。 有关详细信息，请参阅[自定义工作流设计体验](customizing-the-workflow-design-experience.md)。
