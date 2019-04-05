---
title: 演练：在运行时的更新状态栏信息
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- status bars [Windows Forms], updating at run time
- status bars [Windows Forms], refreshing panels
- StatusBar control [Windows Forms], refreshing panels
- panels [Windows Forms], refreshing status bar
ms.assetid: cc2abb06-c082-49f7-a5a3-2fd1bbcb58d1
ms.openlocfilehash: 3ad76899f86013e3395b5b7859538c4c59c9b1ee
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716460"
---
# <a name="walkthrough-updating-status-bar-information-at-run-time"></a>演练：在运行时的更新状态栏信息
> [!IMPORTANT]
>  <xref:System.Windows.Forms.StatusStrip>并<xref:System.Windows.Forms.ToolStripStatusLabel>控件替换，并将功能添加到<xref:System.Windows.Forms.StatusBar>并<xref:System.Windows.Forms.StatusBarPanel>控制; 但是，<xref:System.Windows.Forms.StatusBar>和<xref:System.Windows.Forms.StatusBarPanel>控件将保留用于向后兼容性并供将来使用，如果你选择。  
  
 通常情况下，程序会要求根据应用程序状态的更改或其他用户交互情况，在运行时动态更新状态栏面板的内容。 这是一种用于执行以下任务的常用方式：通知用户启用了 CAPS LOCK、NUM LOCK 或 SCROLL LOCK 之类的键，或者将日期或时钟作为方便的引用提供。  
  
 在以下示例中，您将使用的实例<xref:System.Windows.Forms.StatusBarPanel>类来承载时钟。  
  
### <a name="to-get-the-status-bar-ready-for-updating"></a>准备更新状态栏  
  
1.  创建新的 Windows 窗体。  
  
2.  向窗体添加一个 <xref:System.Windows.Forms.StatusBar> 控件。 有关详细信息，请参阅[如何：将控件添加到 Windows 窗体](how-to-add-controls-to-windows-forms.md)。  
  
3.  添加到状态栏面板在<xref:System.Windows.Forms.StatusBar>控件。 有关详细信息，请参阅[如何：向 StatusBar 控件添加面板](how-to-add-panels-to-a-statusbar-control.md)。  
  
4.  有关<xref:System.Windows.Forms.StatusBar>控件添加到窗体中，设置<xref:System.Windows.Forms.StatusBar.ShowPanels%2A>属性设置为`true`。  
  
5.  添加 Windows 窗体<xref:System.Windows.Forms.Timer>组件到窗体。  
  
    > [!NOTE]
    >  Windows 窗体<xref:System.Windows.Forms.Timer?displayProperty=nameWithType>组件专为 Windows 窗体环境。 如果需要适合服务器环境的计时器，请参阅[基于服务器的计时器介绍](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90))。  
  
6.  将 <xref:System.Windows.Forms.Timer.Enabled%2A> 属性设置为 `true`。  
  
7.  设置<xref:System.Windows.Forms.Timer.Interval%2A>属性的<xref:System.Windows.Forms.Timer>为 30000。  
  
    > [!NOTE]
    >  <xref:System.Windows.Forms.Timer.Interval%2A>属性的<xref:System.Windows.Forms.Timer>成分设置为 30 秒 （30000 毫秒） 以确保显示的时间反映准确的时间。  
  
### <a name="to-implement-the-timer-to-update-the-status-bar"></a>通过实现计时器更新状态栏  
  
1.  将以下代码插入到的事件处理程序<xref:System.Windows.Forms.Timer>组件来更新的面板<xref:System.Windows.Forms.StatusBar>控件。  
  
    ```vb  
    Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick  
       StatusBar1.Panels(0).Text = Now.ToShortTimeString  
    End Sub  
    ```  
  
    ```csharp  
    private void timer1_Tick(object sender, System.EventArgs e)  
    {  
       statusBar1.Panels[0].Text = DateTime.Now.ToShortTimeString();  
    }  
    ```  
  
    ```cpp  
    private:  
      System::Void timer1_Tick(System::Object ^ sender,  
        System::EventArgs ^ e)  
      {  
        statusBar1->Panels[0]->Text =  
          DateTime::Now.ToShortTimeString();  
      }  
    ```  
  
     此时，就可以运行该应用程序并观察在状态栏面板中运行的时钟。  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  调试该应用程序，然后按 F5 运行。 有关调试的详细信息，请参阅[在 Visual Studio 中进行调试](/visualstudio/debugger/debugging-in-visual-studio)。  
  
    > [!NOTE]
    >  大约 30 秒之后，时钟才会出现在状态栏上。 这样可以获得最精确的时间。 相反，若要使时钟早些出现，可以减少的值<xref:System.Windows.Forms.Timer.Interval%2A>在前一过程中的步骤 7 中设置的属性。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.StatusBar>
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- [如何：向 StatusBar 控件添加面板](how-to-add-panels-to-a-statusbar-control.md)
- [如何：确定已单击 Windows 窗体 StatusBar 控件中的面板](determine-which-panel-wf-statusbar-control-was-clicked.md)
- [StatusBar 控件概述](statusbar-control-overview-windows-forms.md)
