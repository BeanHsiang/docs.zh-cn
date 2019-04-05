---
title: 状态机工作流
ms.date: 03/30/2017
ms.assetid: 344caacd-bf3b-4716-bd5a-eca74fc5a61d
ms.openlocfilehash: 78ce1124137e3b97978f3522a59ad1febd23135d
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724955"
---
# <a name="state-machine-workflows"></a>状态机工作流
状态机是用于开发程序的已知范例。 <xref:System.Activities.Statements.StateMachine> 活动与 <xref:System.Activities.Statements.State>、<xref:System.Activities.Statements.Transition> 以及其他活动一起可用于生成状态机工作流程序。 本主题概述如何创建状态机工作流。  
  
## <a name="state-machine-workflow-overview"></a>状态机工作流概述  
 状态机工作流提供建模样式，使用该样式可以通过事件驱动方式对您的工作流进行建模。 <xref:System.Activities.Statements.StateMachine> 活动包含状态和转换，它们构成了状态机的逻辑，并且可以在能够使用活动的任何地方使用。 状态机运行时有若干类：  
  
-   <xref:System.Activities.Statements.StateMachine>  
  
-   <xref:System.Activities.Statements.State>  
  
-   <xref:System.Activities.Statements.Transition>  
  
 为了创建状态机工作流，需要将状态将添加到 <xref:System.Activities.Statements.StateMachine> 活动中，并且使用转换控制各状态之间的流。 以下屏幕截图中，从[入门教程](getting-started-tutorial.md)步骤[如何：创建状态机工作流](how-to-create-a-state-machine-workflow.md)，显示了三种状态和三个转换的状态机工作流。 **初始化目标**是初始状态，表示工作流中的第一个状态。 这指定的行，从而导致它从**启动**节点。 名为工作流中的最终状态**FinalState**，并表示在其中完成工作流的点。  
  
 ![完整的状态机工作流](./media/wfstatemachinegettingstartedtutorialcomplete.JPG "WFStateMachineGettingStartedTutorialComplete")  
  
 状态机工作流必须有且只有一个初始状态，并且至少有一个最终状态。 不属于最终状态的每个状态都必须具有至少一个转换。 下面的几节将介绍如何创建和配置状态和转换。  
  
## <a name="creating-and-configuring-states"></a>创建和配置状态  
 <xref:System.Activities.Statements.State> 表示状态机可具有的状态。 若要添加<xref:System.Activities.Statements.State>到工作流，拖动**状态**活动设计器从**状态机**一部分**工具箱**放到<xref:System.Activities.Statements.StateMachine>上的活动[!INCLUDE[wfd1](../../../includes/wfd1-md.md)]图面。  
  
 ![WF4 状态机活动](./media/netframework4platformupdate1statemachineactivities.jpg "NETFramework4PlatformUpdate1StateMachineActivities")  
  
 若要配置状态作为**初始状态**，右键单击状态，然后选择**设置为初始状态**。 此外，如果没有任何当前的初始状态，初始状态可以指定通过拖动中的一行**启动**的所需状态的工作流的顶部节点。 当<xref:System.Activities.Statements.StateMachine>活动拖放到工作流设计器，它具有名为初始状态预先配置**State1**。 一个状态机工作流必须有且只有一个初始状态。  
  
 表示状态机终止状态的状态称为最终状态。 最终状态是 <xref:System.Activities.Statements.State.IsFinal%2A> 属性设置为 `true`、没有 <xref:System.Activities.Statements.State.Exit%2A> 活动且没有源自它的转换的一种状态。 若要添加到工作流的最终状态，请拖动**FinalState**活动设计器从**状态机**一部分**工具箱**放到<xref:System.Activities.Statements.StateMachine>上的活动[!INCLUDE[wfd1](../../../includes/wfd1-md.md)]图面。 一个状态机工作流必须具有至少一个最终状态。  
  
### <a name="configuring-entry-and-exit-actions"></a>配置进入和退出操作  
 一个状态可以具有一个 <xref:System.Activities.Statements.State.Entry%2A> 和一个 <xref:System.Activities.Statements.State.Exit%2A> 操作。 （配置为最终状态的状态只能具有一个进入操作）。 当某个工作流实例进入某一状态时，进入操作中的所有活动都将执行。 在该进入操作完成后，将计划针对状态转换的触发器。 当确认转换到另一状态时，即使该状态转换回相同状态，也将执行退出操作中的活动。 退出操作完成后，转换操作中的活动将执行，然后转换到新状态，并将计划其进入操作。  
  
> [!NOTE]
>  当调试某一状态机工作流时，可以将断点放置在状态机根活动上以及状态机工作流内的状态上。 断点不能直接放置于转换上，但可以放置于状态和转换中包含的任何活动上。  
  
## <a name="creating-and-configuring-transitions"></a>创建和配置转换  
 所有状态必须均具有至少一个转换，只有最终状态除外，最终状态不能具有任何转换。 在某一状态添加到状态机工作流后可以添加转换，或者可以在删除状态时创建转换。  
  
 若要添加<xref:System.Activities.Statements.State>并在一个步骤中，将创建转换**状态**活动从**状态机**一部分**工具箱**并将其悬停在另一种状态工作流设计器。 在另一个 <xref:System.Activities.Statements.State> 上拖动 <xref:System.Activities.Statements.State> 时，在另一个 <xref:System.Activities.Statements.State> 周围将出现四个三角形。 如果将 <xref:System.Activities.Statements.State> 放置到其中一个三角形，则将其添加到状态机，而且创建从源 <xref:System.Activities.Statements.State> 到放置目标 <xref:System.Activities.Statements.State> 的转换。 有关详细信息，请参阅[Transition 活动设计器](/visualstudio/workflow-designer/transition-activity-designer)。  
  
 若要在添加状态后创建转换，有两个选项。 第一个选项就是从工作流设计器图面拖动状态，并悬停在现有状态上，然后放置在其中一个放置点上。 这个选项与上一节中介绍的方法非常相似。 您也可以将鼠标悬停在所需的源状态上，然后拖动线条到所需的目标状态上。  
  
> [!NOTE]
>  状态机中的单个状态使用工作流设计器可以创建多达 76 个转换。 对在设计器外创建的工作流状态的转换限制只受系统资源限制。  
  
 一个转换可以具有一个 <xref:System.Activities.Statements.Transition.Trigger%2A>、一个 <xref:System.Activities.Statements.Transition.Condition%2A> 和一个 <xref:System.Activities.Statements.Transition.Action%2A>。 在转换的源状态的 <xref:System.Activities.Statements.Transition.Trigger%2A> 操作完成时，将会计划转换的 <xref:System.Activities.Statements.State.Entry%2A>。 通常，<xref:System.Activities.Statements.Transition.Trigger%2A> 是一种等待某种类型的事件发生的活动，但它可以是任何活动，也可以是完全没有任何活动。 在 <xref:System.Activities.Statements.Transition.Trigger%2A> 活动完成后，将会对 <xref:System.Activities.Statements.Transition.Condition%2A>（如果有）进行计算。 如果没有 <xref:System.Activities.Statements.Transition.Trigger%2A> 活动，则立即对 <xref:System.Activities.Statements.Transition.Condition%2A> 进行计算。 如果条件的计算结果为 `false`，则取消转换，并且来自该状态的所有转换的 <xref:System.Activities.Statements.Transition.Trigger%2A> 活动都将重新计划。 如果存在与当前转换共享相同源状态的其他转换，也将取消并且重新计划这些 <xref:System.Activities.Statements.Transition.Trigger%2A> 操作。 如果 <xref:System.Activities.Statements.Transition.Condition%2A> 的计算结果为 `true` 或没有任何条件，则执行源状态的 <xref:System.Activities.Statements.State.Exit%2A> 操作，然后执行转换的 <xref:System.Activities.Statements.Transition.Action%2A>。 当<xref:System.Activities.Statements.Transition.Action%2A>完成后，控制权将传递给**目标**状态  
  
 共享公共触发器的转换称作共享触发器转换。 一组共享触发器转换中的每个转换都具有相同触发器，但具有唯一的 <xref:System.Activities.Statements.Transition.Condition%2A> 和 Action。 若要将其他操作添加到转换和创建共享转换，请单击指示所需转换的开始的圆并将它拖到所需的状态。 新转换将与初始转换共享相同的触发器，但它将具有一个唯一的条件和操作。 共享的转换还可以创建从在转换设计器通过单击**添加共享的触发器转换**底部的转换设计器，然后选择所需的目标状态从**若要连接的可用状态**下拉列表。  
  
> [!NOTE]
>  注意，如果转换的 <xref:System.Activities.Statements.Transition.Condition%2A> 计算结果为 `False`（或所有共享触发转换条件的计算结果均为 `False`），转换将不发生，并且此状态下的所有转换的所有触发将被重新计划。  
  
 有关创建状态机工作流的详细信息，请参阅[如何：创建状态机工作流](how-to-create-a-state-machine-workflow.md)， [StateMachine 活动设计器](/visualstudio/workflow-designer/statemachine-activity-designer)，[状态活动设计器](/visualstudio/workflow-designer/state-activity-designer)， [FinalState 活动设计器](/visualstudio/workflow-designer/finalstate-activity-designer)，并且[转换活动设计器](/visualstudio/workflow-designer/transition-activity-designer)。  
  
## <a name="state-machine-terminology"></a>状态机术语  
 本节定义本主题中使用的状态机词汇。  
  
 状态  
 构成状态机的基本单位。 状态机在任何特定时间都可处于某一状态。  
  
 进入操作  
 进入状态时执行的活动  
  
 退出操作  
 退出状态时执行的活动  
  
 切换  
 两个状态之间的定向关系，表示状态机对发生的特定类型事件的整个响应。  
  
 共享转换  
 与一个或多个转换共享源状态和触发器、但具有唯一条件和操作的一种转换。  
  
 触发器  
 导致转换发生的触发活动。  
  
 条件  
 一个约束条件，该约束的计算结果必须为 `true`，然后触发器才会发生以便完成转换。  
  
 转换操作  
 在执行某个转换时执行的活动。  
  
 条件转换  
 具有显式条件的转换。  
  
 自行转换  
 从某一状态转换到该状态本身的一种转换。  
  
 初始状态  
 表示状态机起始点的一种状态。  
  
 最终状态  
 表示状态机完成的一种状态。  
  
## <a name="see-also"></a>请参阅
- [如何：创建状态机工作流](how-to-create-a-state-machine-workflow.md)
- [StateMachine 活动设计器](/visualstudio/workflow-designer/statemachine-activity-designer)
- [State 活动设计器](/visualstudio/workflow-designer/state-activity-designer)
- [FinalState 活动设计器](/visualstudio/workflow-designer/finalstate-activity-designer)
- [Transition 活动设计器](/visualstudio/workflow-designer/transition-activity-designer)
