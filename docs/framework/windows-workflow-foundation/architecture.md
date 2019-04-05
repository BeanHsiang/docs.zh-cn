---
title: Windows 工作流体系结构
ms.date: 03/30/2017
ms.assetid: 1d4c6495-d64a-46d0-896a-3a01fac90aa9
ms.openlocfilehash: 5d6e1ead9184bfb61eb466389671ca2e74264ae3
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57723733"
---
# <a name="windows-workflow-architecture"></a>Windows 工作流体系结构
Windows Workflow Foundation (WF) 引发了开发长时间运行的交互式应用程序的抽象级别。 工作单元封装为活动。 活动运行环境提供用于流控制、异常处理、错误传播、状态数据保存、从内存加载和卸载正在进行的工作流、跟踪以及事务流的功能。  
  
## <a name="activity-architecture"></a>活动体系结构  
 活动作为 CLR 类型开发，这些类型或者派生自 <xref:System.Activities.Activity>、<xref:System.Activities.CodeActivity>、<xref:System.Activities.AsyncCodeActivity> 或 <xref:System.Activities.NativeActivity>，或者派生自返回某个值的对应 <xref:System.Activities.Activity%601>、<xref:System.Activities.CodeActivity%601>、<xref:System.Activities.AsyncCodeActivity%601> 或 <xref:System.Activities.NativeActivity%601> 变体。 通过开发派生自 <xref:System.Activities.Activity> 的活动，用户可以组合预先存在的活动，以便快速创建在工作流环境中执行的工作单元。 另一方面，<xref:System.Activities.CodeActivity> 支持通过将 <xref:System.Activities.CodeActivityContext> 主要用于访问活动参数，在托管代码中创作执行逻辑。 <xref:System.Activities.AsyncCodeActivity> 类似于 <xref:System.Activities.CodeActivity>，只不过它可以用于实现异步任务。 通过开发派生自 <xref:System.Activities.NativeActivity> 的活动，用户可以通过 <xref:System.Activities.NativeActivityContext> 访问运行时，以实现安排子级、创建书签、调用异步工作、注册事务等功能。  
  
 创作派生自 <xref:System.Activities.Activity> 的活动是声明性的，可以在 XAML 中创作这些活动。 下面的示例使用其他活动作为执行体来创建一个名为 `Prompt` 的活动。  
  
```xml  
<Activity x:Class='Prompt'  
  xmlns:x='http://schemas.microsoft.com/winfx/2006/xaml'  
    xmlns:z='http://schemas.microsoft.com/netfx/2008/xaml/schema'  
xmlns:my='clr-namespace:XAMLActivityDefinition;assembly=XAMLActivityDefinition'  
xmlns:s="clr-namespace:System;assembly=mscorlib"  
xmlns="http://schemas.microsoft.com/2009/workflow">  
<z:SchemaType.Members>  
    <z:SchemaType.SchemaProperty Name='Text' Type=' InArgument(s:String)' />  
  <z:SchemaType.SchemaProperty Name='Response' Type='OutArgument(s:String)' />  
</z:SchemaType.Members>  
  <Sequence>  
    <my:WriteLine Text='[Text]' />  
    <my:ReadLine BookmarkName='r1' Result='[Response]' />  
  </Sequence>  
</Activity>  
```  
  
## <a name="activity-context"></a>活动上下文  
 <xref:System.Activities.ActivityContext> 是活动作者的工作流运行时接口，提供对诸多运行时功能的访问。 下面的示例定义一个使用执行上下文创建书签（一种机制，允许活动在其执行中注册一个延续点，该延续点可由将数据传入活动的主机恢复）的活动。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
## <a name="activity-life-cycle"></a>活动生命周期  
 活动实例启动时处于 <xref:System.Activities.ActivityInstanceState.Executing> 状态。 除非发生异常，否则活动将保持此状态，直到已完成执行所有子活动和所有其他挂起的工作（如 <xref:System.Activities.Bookmark> 对象），此时，该活动将转换为 <xref:System.Activities.ActivityInstanceState.Closed> 状态。 活动实例的父级可以请求取消子级；如果可以取消子级，该子级则在完成时处于 <xref:System.Activities.ActivityInstanceState.Canceled> 状态。 如果在执行期间引发异常，运行时会使活动进入 <xref:System.Activities.ActivityInstanceState.Faulted> 状态，并将此异常向上传播到活动父链。 下面列出了活动的三个完成状态：  
  
-   **关闭：** 该活动已完成其工作并退出。  
  
-   **已取消：** 该活动已正常放弃其工作并退出。 当进入此状态时，不会显式回滚工作。  
  
-   **出现故障：** 活动遇到了错误，并且具有未完成其工作的情况下退出。  
  
 当保存或卸载活动时，活动会保持 <xref:System.Activities.ActivityInstanceState.Executing> 状态。
