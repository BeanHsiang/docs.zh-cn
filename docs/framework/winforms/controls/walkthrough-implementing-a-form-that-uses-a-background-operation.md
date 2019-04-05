---
title: 演练：实现使用后台操作的窗体
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [Windows Forms], forms
- BackgroundWorker component
- background tasks
- forms [Windows Forms], multithreading
- threading [Windows Forms], walkthroughs
- forms [Windows Forms], background operations
- threading [Windows Forms], background operations
- background operations
ms.assetid: 4691b796-9200-471a-89c3-ba4c7cc78c03
ms.openlocfilehash: cb19dfb59ba36eea94f65005c2711ad58d098144
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716993"
---
# <a name="walkthrough-implementing-a-form-that-uses-a-background-operation"></a>演练：实现使用后台操作的窗体
如果某项操作需要很长时间才能完成，并且您不希望用户界面 (UI) 停止响应或"挂起，可以使用<xref:System.ComponentModel.BackgroundWorker>类，以另一个线程上执行此操作。  
  
 本演练演示了如何使用<xref:System.ComponentModel.BackgroundWorker>类来执行耗时的计算，"在后台，"尽管用户界面保持响应。  演练时，将有一个异步计算 Fibonacci 数列的应用程序。 即使计算大型 Fibonacci 数列需要花费大量时间，但主 UI 线程不会被这种延时中断，并且在计算期间窗体仍会响应。  
  
 本演练涉及以下任务：  
  
-   创建基于 Windows 的应用程序  
  
-   创建<xref:System.ComponentModel.BackgroundWorker>窗体中  
  
-   添加异步事件处理程序  
  
-   添加进度报告和取消支持  
  
 在此示例中使用的代码的完整列表，请参阅[如何：实现使用后台操作的窗体](how-to-implement-a-form-that-uses-a-background-operation.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="creating-the-project"></a>创建项目  
 第一步是创建项目并设置窗体。  
  
#### <a name="to-create-a-form-that-uses-a-background-operation"></a>创建使用后台操作的窗体  
  
1.  创建一个名为基于 Windows 的应用程序项目`BackgroundWorkerExample`(**文件** > **新建** > **项目** >  **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**)。  
  
2.  在“解决方案资源管理器”中，右键单击“Form1”，然后从快捷菜单中选择“重命名”。 将文件名更改为 `FibonacciCalculator`。 询问是否希望重命名对代码元素“**”的所有引用时，单击“是”**`Form1`按钮。  
  
3.  拖动<xref:System.Windows.Forms.NumericUpDown>控件从**工具箱**拖到窗体。 设置<xref:System.Windows.Forms.NumericUpDown.Minimum%2A>属性设置为`1`并<xref:System.Windows.Forms.NumericUpDown.Maximum%2A>属性设置为`91`。  
  
4.  添加两个<xref:System.Windows.Forms.Button>到窗体控件。  
  
5.  重命名第一个<xref:System.Windows.Forms.Button>控制`startAsyncButton`并设置<xref:System.Windows.Forms.Control.Text%2A>属性设置为`Start Async`。 重命名第二个<xref:System.Windows.Forms.Button>控制`cancelAsyncButton`，并设置<xref:System.Windows.Forms.Control.Text%2A>属性设置为`Cancel Async`。 设置其<xref:System.Windows.Forms.Control.Enabled%2A>属性设置为`false`。  
  
6.  创建事件处理程序的两个<xref:System.Windows.Forms.Button>控件的<xref:System.Windows.Forms.Control.Click>事件。 有关详细信息，请参阅[如何：创建事件处理程序使用设计器](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/zwwsdtbk(v=vs.100))。  
  
7.  拖动<xref:System.Windows.Forms.Label>控件从**工具箱**拖到窗体并将其重命名`resultLabel`。  
  
8.  拖动<xref:System.Windows.Forms.ProgressBar>控件从**工具箱**拖到窗体。  
  
## <a name="creating-a-backgroundworker-in-your-form"></a>在窗体中创建 BackgroundWorker  
 您可以创建<xref:System.ComponentModel.BackgroundWorker>异步操作使用**Windows** **窗体设计器**。  
  
#### <a name="to-create-a-backgroundworker-with-the-designer"></a>使用设计器创建 BackgroundWorker  
  
-   从**组件**选项卡**工具箱**，拖动<xref:System.ComponentModel.BackgroundWorker>拖到窗体。  
  
## <a name="adding-asynchronous-event-handlers"></a>添加异步事件处理程序  
 你现已准备好添加事件处理程序<xref:System.ComponentModel.BackgroundWorker>组件的异步事件。 这些事件处理程序将调用在后台运行的计算 Fibonacci 数列的耗时操作。  
  
#### <a name="to-implement-asynchronous-event-handlers"></a>实现异步事件处理程序  
  
1.  在中**属性**窗口中，使用<xref:System.ComponentModel.BackgroundWorker>组件仍处于选中状态，单击**事件**按钮。 双击<xref:System.ComponentModel.BackgroundWorker.DoWork>和<xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>事件创建事件处理程序。 有关如何使用事件处理程序的详细信息，请参阅[如何：创建事件处理程序使用设计器](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/zwwsdtbk(v=vs.100))。  
  
2.  在窗体中新建一个名为 `ComputeFibonacci` 的新方法。 此方法完成实际的工作，并在后台运行。 这些代码演示了 Fibonacci 算法的递归实现，这种算法的效率非常低，对于较大的数值花费的时间按指数增长。 在这里使用是出于演示的目的，为了说明在应用程序中某项操作可能带来长时间的延迟。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#10](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#10)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#10)]
     [!code-vb[System.ComponentModel.BackgroundWorker#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#10)]  
  
3.  在中<xref:System.ComponentModel.BackgroundWorker.DoWork>事件处理程序添加对的调用`ComputeFibonacci`方法。 采取的第一个参数`ComputeFibonacci`从<xref:System.ComponentModel.DoWorkEventArgs.Argument%2A>属性的<xref:System.ComponentModel.DoWorkEventArgs>。 <xref:System.ComponentModel.BackgroundWorker>和<xref:System.ComponentModel.DoWorkEventArgs>参数在更高版本将用于进度报告和取消支持。 从返回的值分配`ComputeFibonacci`到<xref:System.ComponentModel.DoWorkEventArgs.Result%2A>属性的<xref:System.ComponentModel.DoWorkEventArgs>。 此结果将可供<xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>事件处理程序。  
  
    > [!NOTE]
    >  <xref:System.ComponentModel.BackgroundWorker.DoWork>事件处理程序不引用`backgroundWorker1`直接，实例变量，因为这会耦合到的特定实例的此事件处理程序<xref:System.ComponentModel.BackgroundWorker>。 相反，对引用<xref:System.ComponentModel.BackgroundWorker>，引发此事件恢复从`sender`参数。 这是重要的当窗体承载多个<xref:System.ComponentModel.BackgroundWorker>。 还有一点不需要操作中的任何用户界面对象在<xref:System.ComponentModel.BackgroundWorker.DoWork>事件处理程序。 相反，通信的用户界面通过<xref:System.ComponentModel.BackgroundWorker>事件。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#5](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#5)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#5)]  
  
4.  在中`startAsyncButton`控件的<xref:System.Windows.Forms.Control.Click>事件处理程序中，添加启动异步操作的代码。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#13](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#13)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#13](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#13)]
     [!code-vb[System.ComponentModel.BackgroundWorker#13](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#13)]  
  
5.  在中<xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>事件处理程序，将结果分配到计算`resultLabel`控件。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#6](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#6)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#6)]  
  
## <a name="adding-progress-reporting-and-support-for-cancellation"></a>添加进度报告和取消支持  
 由于异步操作将会花费很长的时间，因此通常希望向用户报告进度并允许用户取消操作。 <xref:System.ComponentModel.BackgroundWorker>类提供了允许您以在后台操作进行发布进度的事件。 它还提供了一个标志，允许辅助代码检测到调用<xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A>并中断自身。  
  
#### <a name="to-implement-progress-reporting"></a>实现进度报告  
  
1.  在“属性”窗口中，选择 `backgroundWorker1`。 设置<xref:System.ComponentModel.BackgroundWorker.WorkerReportsProgress%2A>并<xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A>属性设置为`true`。  
  
2.  在 `FibonacciCalculator` 窗体中声明两个变量。 这将用于跟踪进度。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#14](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#14)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#14](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#14)]
     [!code-vb[System.ComponentModel.BackgroundWorker#14](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#14)]  
  
3.  为 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件添加事件处理程序。 在中<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件处理程序中，更新<xref:System.Windows.Forms.ProgressBar>与<xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A>属性的<xref:System.ComponentModel.ProgressChangedEventArgs>参数。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#7](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#7)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#7)]  
  
#### <a name="to-implement-support-for-cancellation"></a>实现取消支持  
  
1.  在中`cancelAsyncButton`控件的<xref:System.Windows.Forms.Control.Click>事件处理程序中，添加取消异步操作的代码。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#4](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#4)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#4)]  
  
2.  下面的 `ComputeFibonacci` 方法中的代码片段可报告进程并支持取消。  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#11](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#11)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#11)]
     [!code-vb[System.ComponentModel.BackgroundWorker#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#11)]  
    [!code-cpp[System.ComponentModel.BackgroundWorker#12](~/samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#12)]
    [!code-csharp[System.ComponentModel.BackgroundWorker#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#12)]
    [!code-vb[System.ComponentModel.BackgroundWorker#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#12)]  
  
## <a name="checkpoint"></a>检查点  
 此时，可以编译并运行 Fibonacci 计算器应用程序。  
  
#### <a name="to-test-your-project"></a>测试项目  
  
-   按 F5 编译并运行应用程序。  
  
     在后台运行计算时，您将看到<xref:System.Windows.Forms.ProgressBar>显示一段时间后计算的进度。 也可以取消挂起的操作。  
  
     对于较小数值，计算应非常快，但对于较大数值，将看到明显的延时。 如果输入 30 或更大的值，应看到有几秒钟的延时，这取决于计算机的速度。 对于大于 40 的值，完成计算可能要花费数分钟或数小时。 在计算器计算较大的 Fibonacci 数列时，注意可以自由地移动窗体、最小化、最大化甚至关闭窗体。 这是因为主 UI 线程不会等待计算完成。  
  
## <a name="next-steps"></a>后续步骤  
 现在，已实现使用的窗体<xref:System.ComponentModel.BackgroundWorker>组件在后台执行计算可以探究异步操作的其他可能性：  
  
-   使用多个<xref:System.ComponentModel.BackgroundWorker>多个同时操作的对象。  
  
-   若要调试多线程应用程序，请参阅[如何：使用线程窗口](/visualstudio/debugger/how-to-use-the-threads-window)。  
  
-   实现自己的支持异步编程模式的组件。 有关详细信息，请参阅[基于事件的异步模式概述](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)。  
  
    > [!CAUTION]
    >  使用任何一种多线程都可能引起极为严重和复杂的 Bug。 在实现任何使用多线程处理的解决方案之前，请参阅[托管线程处理最佳做法](../../../standard/threading/managed-threading-best-practices.md)。  
  
## <a name="see-also"></a>请参阅

- <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>
- [托管线程](../../../standard/threading/index.md)
- [托管线程处理的最佳做法](../../../standard/threading/managed-threading-best-practices.md)
- [基于事件的异步模式概述](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)
- [如何：实现使用后台操作的窗体](how-to-implement-a-form-that-uses-a-background-operation.md)
- [演练：在后台运行操作](walkthrough-running-an-operation-in-the-background.md)
- [BackgroundWorker 组件](backgroundworker-component.md)
