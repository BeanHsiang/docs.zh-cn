---
title: 如何：运行工作流
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: f814ff82-fe2b-4614-aebb-b768c3e61179
ms.openlocfilehash: a5866bae5217b8c8ea22ba66a344b464694583ac
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720966"
---
# <a name="how-to-run-a-workflow"></a>如何：运行工作流
本主题是 Windows Workflow Foundation 入门教程的延续，讨论如何创建工作流宿主并运行在以前定义的工作流[如何：创建工作流](how-to-create-a-workflow.md)主题。

> [!NOTE]
>  入门教程中的每个主题都依赖于前面的主题。 若要完成本主题，必须首先完成[如何：创建活动](how-to-create-an-activity.md)和[如何：创建工作流](how-to-create-a-workflow.md)。

> [!NOTE]
>  若要下载完整版教程，请参阅 [Windows Workflow Foundation (WF45) — 入门教程](https://go.microsoft.com/fwlink/?LinkID=248976)。  
  
### <a name="to-create-the-workflow-host-project"></a>创建工作流宿主项目  
  
1.  从以前打开的解决方案[如何：创建活动](how-to-create-an-activity.md)通过使用 Visual Studio 2012 的主题。  
  
2.  在 **解决方案资源管理器** 中右键单击 **WF45GettingStartedTutorial** 解决方案，选择 **“添加”** 和 **“新建项目”**。  
  
    > [!TIP]
    >  如果未显示 **解决方案资源管理器** 窗口，请从 **“视图”** 菜单选择 **“解决方案资源管理器** 。

3.  在 **“已安装”** 节点中，选择 **“Visual C#”**、 **“工作流”** （或 **“Visual Basic”**、 **“工作流”**）。

    > [!NOTE]
    >  根据在 Visual Studio 中配置为主要语言的编程语言的不同， **“Visual C#”** 或 **“Visual Basic”** 节点可能位于 **“已安装”** 节点下的 **“其他语言”** 节点中。

     请确保在 .NET Framework 版本下拉列表中选择 **“.NET Framework 4.5”** 。 从 **“工作流”** 列表中选择 **“工作流控制台应用程序”** 。 类型`NumberGuessWorkflowHost`成**名称**框，然后单击**确定**。 这将创建适合初学者的工作流应用程序，它具备基本的工作流承载支持。 基本承载代码将修改用于运行工作流应用程序。

4.  在 **解决方案资源管理器** 中右键单击新添加的 **NumberGuessWorkflowHost** ，然后选择 **“添加引用”**。 在 **“添加引用”** 列表中选择 **“解决方案”** ，选中 **NumberGuessWorkflowActivities**旁边的复选框，然后单击 **“确定”**。

5.  在 **解决方案资源管理器** 中右键单击 **Workflow1.xaml** ，然后选择 **“删除”**。 单击 **“确定”** 以确认。

### <a name="to-modify-the-workflow-hosting-code"></a>修改工作流承载代码

1.  在 **解决方案资源管理器** 中双击 **“Program.cs”** 或 **“Module1.vb”** ，以显示其代码。

    > [!TIP]
    >  如果未显示 **解决方案资源管理器** 窗口，请从 **“视图”** 菜单选择 **“解决方案资源管理器** 。

     因为此项目是用 **“工作流控制台应用程序”** 模板创建的，所以 **“Program.cs”** 或 **“Module1.vb”** 包含以下基本工作流承载代码。

    ```vb
    ' Create and cache the workflow definition
    Activity workflow1 = new Workflow1()
    WorkflowInvoker.Invoke(workflow1)
    ```

    ```csharp
    // Create and cache the workflow definition
    Activity workflow1 = new Workflow1();
    WorkflowInvoker.Invoke(workflow1);
    ```

     生成的承载代码使用 <xref:System.Activities.WorkflowInvoker>。 <xref:System.Activities.WorkflowInvoker> 提供一种简单工作流调用方法，就像方法调用一样，仅可用于不使用持久性的工作流。 <xref:System.Activities.WorkflowApplication> 为执行工作流（包括生命周期事件通知、执行控制、书签恢复和持久性）提供更丰富的模型。 此示例使用书签并且将 <xref:System.Activities.WorkflowApplication> 用于承载工作流。 在 `using` Program.cs **或** Module1.vb **顶部的现有** using **或** Imports **语句下面，添加以下** 或 **Imports** 语句。

    ```vb
    Imports NumberGuessWorkflowActivities
    Imports System.Threading
    ```

    ```csharp
    using NumberGuessWorkflowActivities;
    using System.Threading;
    ```

     用以下基本 <xref:System.Activities.WorkflowInvoker> 承载代码替换使用 <xref:System.Activities.WorkflowApplication> 的代码行。 此示例承载代码演示承载和调用工作流的基本步骤，但尚不包含用于成功运行本主题中的工作流的功能。 在以下步骤中，将修改此基本代码并添加其他功能，直到完成应用程序。

    > [!NOTE]
    >  请替换`Workflow1`在这些示例中使用`FlowchartNumberGuessWorkflow`， `SequentialNumberGuessWorkflow`，或`StateMachineNumberGuessWorkflow`，具体在以前完成的工作流取决于[如何：创建工作流](how-to-create-a-workflow.md)步骤。 如果不替换 `Workflow1` ，在尝试生成或运行工作流时会出现生成错误。

     [!code-csharp[CFX_WF_GettingStarted#4](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/extrasnippets.cs#4)]
     [!code-vb[CFX_WF_GettingStarted#4](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/extrasnippets.vb#4)]

     此代码将创建一个 <xref:System.Activities.WorkflowApplication>，订阅三个工作流生命周期事件，通过调用 <xref:System.Activities.WorkflowApplication.Run%2A>来启动工作流，然后等待工作流完成。 工作流完成时，将设置 <xref:System.Threading.AutoResetEvent> ，并且宿主应用程序也完成。

### <a name="to-set-input-arguments-of-a-workflow"></a>设置工作流的输入参数

1.  在 **“Program.cs”** 或 **“Module1.vb”** 顶部的现有 `using` 或 `Imports` 语句下面，添加以下语句。

     [!code-csharp[CFX_WF_GettingStarted#5](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#5)]
     [!code-vb[CFX_WF_GettingStarted#5](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#5)]

2.  将创建新 <xref:System.Activities.WorkflowApplication> 的代码行替换为以下代码，该代码创建一个参数字典并在创建后将其传递给工作流。

    > [!NOTE]
    >  请替换`Workflow1`在这些示例中使用`FlowchartNumberGuessWorkflow`， `SequentialNumberGuessWorkflow`，或`StateMachineNumberGuessWorkflow`，具体在以前完成的工作流取决于[如何：创建工作流](how-to-create-a-workflow.md)步骤。 如果不替换 `Workflow1` ，在尝试生成或运行工作流时会出现生成错误。

     [!code-csharp[CFX_WF_GettingStarted#6](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#6)]
     [!code-vb[CFX_WF_GettingStarted#6](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#6)]

     此字典包含一个键为 `MaxNumber`的元素。 输入字典中的键对应工作流根活动的输入参数。 工作流使用`MaxNumber` 来确定随机生成数的上边界。

### <a name="to-retrieve-output-arguments-of-a-workflow"></a>检索工作流的输出参数

1.  修改 <xref:System.Activities.WorkflowApplication.Completed%2A> 处理程序以检索并显示工作流使用的轮数。

     [!code-csharp[CFX_WF_GettingStarted#7](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#7)]
     [!code-vb[CFX_WF_GettingStarted#7](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#7)]

### <a name="to-resume-a-bookmark"></a>继续执行书签

1.  将以下代码添加到 `Main` 方法顶部，紧接在现有 <xref:System.Threading.AutoResetEvent> 声明之后。

     [!code-csharp[CFX_WF_GettingStarted#8](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#8)]
     [!code-vb[CFX_WF_GettingStarted#8](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#8)]

2.  将以下 <xref:System.Activities.WorkflowApplication.Idle%2A> 处理程序添加到 `Main`中，紧接在现有的三个工作流生命周期处理程序的下面。

     [!code-csharp[CFX_WF_GettingStarted#9](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#9)]
     [!code-vb[CFX_WF_GettingStarted#9](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#9)]

     每次工作流变为空闲状态等待下一个猜测时，都会调用此处理程序并设置 `idleAction` <xref:System.Threading.AutoResetEvent> 。 下面步骤中的代码使用 `idleEvent` 和 `syncEvent` 来确定工作流是在等待下一个猜测还是已完成。

    > [!NOTE]
    >  在本示例中，宿主应用程序在 <xref:System.Activities.WorkflowApplication.Completed%2A> 和 <xref:System.Activities.WorkflowApplication.Idle%2A> 处理程序中使用自动重置事件将宿主应用程序与工作流的进度同步。 在继续执行书签之前，不需要阻止并等待工作流变为空闲状态，但在此示例中需要同步事件，以使宿主知道工作流是否已完成，或是否在等待使用 <xref:System.Activities.Bookmark>的更多用户输入。 有关详细信息，请参阅[书签](bookmarks.md)。

3.  移除对 `WaitOne`的调用，并替换为收集用户输入并恢复 <xref:System.Activities.Bookmark>的代码。

     移除下面的代码行。

     [!code-csharp[CFX_WF_GettingStarted#10](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/extrasnippets.cs#10)]
     [!code-vb[CFX_WF_GettingStarted#10](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/extrasnippets.vb#10)]

     使用下面的示例替换它。

     [!code-csharp[CFX_WF_GettingStarted#11](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#11)]
     [!code-vb[CFX_WF_GettingStarted#11](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#11)]

## <a name="BKMK_ToRunTheApplication"></a> 生成并运行应用程序

1.  在 **解决方案资源管理器** 中，右键单击 **NumberGuessWorkflowHost** 项目，然后选择 **“设为启动项目”**。

2.  按 Ctrl+F5 生成并运行应用程序。 尝试以尽可能少的次数猜出该数。

     要尝试其他工作流样式的应用程序，请用 `Workflow1` 、 <xref:System.Activities.WorkflowApplication> 或 `FlowchartNumberGuessWorkflow`（取决于所需工作流样式）替换代码中用于创建 `SequentialNumberGuessWorkflow`的 `StateMachineNumberGuessWorkflow`。

     [!code-csharp[CFX_WF_GettingStarted#6](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#6)]
     [!code-vb[CFX_WF_GettingStarted#6](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#6)]

     有关如何向工作流应用程序添加持久性的说明，请参阅下一主题[如何：创建和运行长时间运行工作流](how-to-create-and-run-a-long-running-workflow.md)。

## <a name="example"></a>示例
 下面的示例是 `Main` 方法的完整代码清单。

> [!NOTE]
>  请替换`Workflow1`在这些示例中使用`FlowchartNumberGuessWorkflow`， `SequentialNumberGuessWorkflow`，或`StateMachineNumberGuessWorkflow`，具体在以前完成的工作流取决于[如何：创建工作流](how-to-create-a-workflow.md)步骤。 如果不替换 `Workflow1` ，在尝试生成或运行工作流时会出现生成错误。

 [!code-csharp[CFX_WF_GettingStarted#12](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_wf_gettingstarted/cs/program.cs#12)]
 [!code-vb[CFX_WF_GettingStarted#12](~/samples/snippets/visualbasic/VS_Snippets_CFX/cfx_wf_gettingstarted/vb/module1.vb#12)]

## <a name="see-also"></a>请参阅

- <xref:System.Activities.WorkflowApplication>
- <xref:System.Activities.Bookmark>
- [Windows Workflow Foundation 编程](programming.md)
- [入门教程](getting-started-tutorial.md)
- [如何：创建工作流](how-to-create-a-workflow.md)
- [如何：创建和运行长时间运行工作流](how-to-create-and-run-a-long-running-workflow.md)
- [在工作流中等待输入](waiting-for-input-in-a-workflow.md)
- [托管工作流](hosting-workflows.md)