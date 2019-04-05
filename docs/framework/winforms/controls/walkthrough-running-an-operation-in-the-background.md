---
title: 演练：在后台运行操作
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- background tasks
- forms [Windows Forms], multithreading
- forms [Windows Forms], background operations
- background threads
- BackgroundWorker class [Windows Forms], examples
- threading [Windows Forms], background operations
- background operations
ms.assetid: 1b9a4e0a-f134-48ff-a1be-c461446a31ba
ms.openlocfilehash: 0ba4ca2589a61a9331308a816da6ddb5276adbc9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703655"
---
# <a name="walkthrough-running-an-operation-in-the-background"></a>演练：在后台运行操作
如果某项操作需要很长时间才能完成，而你不希望造成用户界面的延迟，则可以使用 <xref:System.ComponentModel.BackgroundWorker> 类在另一个线程上运行此操作。  
  
 在此示例中使用的代码的完整列表，请参阅[如何：在后台运行操作](how-to-run-an-operation-in-the-background.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-run-an-operation-in-the-background"></a>若要在后台运行操作  
  
1.  使用窗体中 Windows 窗体设计器处于活动状态中，将两个<xref:System.Windows.Forms.Button>控件从**工具箱**窗体，且然后将设置为`Name`和<xref:System.Windows.Forms.Control.Text%2A>根据下表的按钮的属性。  
  
    |Button|name|Text|  
    |------------|----------|----------|  
    |`button1`|`startBtn`|**Start**|  
    |`button2`|`cancelBtn`|**取消**|  
  
2.  打开**工具箱**，单击**组件**选项卡，，然后将<xref:System.ComponentModel.BackgroundWorker>组件拖动到窗体上。  
  
     `backgroundWorker1`部分显示在**组件栏**。  
  
3.  在“属性”  窗口中，将 <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> 属性设置为 `true`。  
  
4.  在中**属性**窗口中，单击**事件**按钮，然后再双击<xref:System.ComponentModel.BackgroundWorker.DoWork>和<xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>事件创建事件处理程序。  
  
5.  你需花时间将代码插入到<xref:System.ComponentModel.BackgroundWorker.DoWork>事件处理程序。  
  
6.  从操作所需的任何参数中提取<xref:System.ComponentModel.DoWorkEventArgs.Argument%2A>属性的<xref:System.ComponentModel.DoWorkEventArgs>参数。  
  
7.  将结果分配到计算<xref:System.ComponentModel.DoWorkEventArgs.Result%2A>属性的<xref:System.ComponentModel.DoWorkEventArgs>。  
  
     这是将可供<xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>事件处理程序。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#2)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#2)]  
  
8.  插入代码来检索操作结果<xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted>事件处理程序。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#3)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#3)]  
  
9. 实现 `TimeConsumingOperation` 方法。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#4)]  
  
10. 在 Windows 窗体设计器中，双击`startButton`若要创建<xref:System.Windows.Forms.Control.Click>事件处理程序。  
  
11. 调用<xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A>中的方法<xref:System.Windows.Forms.Control.Click>事件处理程序`startButton`。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#5)]  
  
12. 在 Windows 窗体设计器中，双击`cancelButton`若要创建<xref:System.Windows.Forms.Control.Click>事件处理程序。  
  
13. 调用<xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A>中的方法<xref:System.Windows.Forms.Control.Click>事件处理程序`cancelButton`。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#6)]  
  
14. 在文件顶部，导入在 System.ComponentModel 和 System.Threading 命名空间。  
  
     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#7)]  
  
15. 按 F6 生成解决方案，然后按 CTRL-F5 运行该应用程序在调试器外部。  
  
> [!NOTE]
>  在中按 F5 运行应用程序在调试器下的，如果引发异常`TimeConsumingOperation`方法是捕获并显示由调试器。 在调试器外部应用程序运行时<xref:System.ComponentModel.BackgroundWorker>处理异常并将其在缓存<xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A>属性的<xref:System.ComponentModel.RunWorkerCompletedEventArgs>。  
  
1.  单击**启动**按钮运行异步操作，并单击**取消**按钮可停止正在运行的异步操作。  
  
     每个操作的结果显示在 <xref:System.Windows.Forms.MessageBox> 中。  
  
## <a name="next-steps"></a>后续步骤  
  
-   实现异步操作将继续报告进度的窗体。 有关详细信息，请参阅[如何：实现使用后台操作的窗体](how-to-implement-a-form-that-uses-a-background-operation.md)。  
  
-   实现支持异步模式的组件的类。 有关详细信息，请参阅[实现基于事件的异步模式](../../../standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.DoWorkEventArgs>
- [如何：实现使用后台操作的窗体](how-to-implement-a-form-that-uses-a-background-operation.md)
- [如何：在后台运行操作](how-to-run-an-operation-in-the-background.md)
- [BackgroundWorker 组件](backgroundworker-component.md)
