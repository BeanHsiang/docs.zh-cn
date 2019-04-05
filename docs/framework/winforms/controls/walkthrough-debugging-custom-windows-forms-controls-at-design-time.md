---
title: 演练：在设计时调试自定义 Windows 窗体控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- debugging [Visual Studio], walkthroughs
- custom controls [Windows Forms], walkthroughs
- visual editors
- debugging [Visual Studio], Windows Forms
- custom controls [Windows Forms], debugging
- designers
- controls [Windows Forms], debugging
- walkthroughs [Windows Forms], debugging
- design-time debugging
ms.assetid: 1fd83ccd-3798-42fc-85a3-6cba99467387
ms.openlocfilehash: 9bd3f822e5a1f8572ebb7f5991abccde904150b8
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57717825"
---
# <a name="walkthrough-debugging-custom-windows-forms-controls-at-design-time"></a>演练：在设计时调试自定义 Windows 窗体控件
时创建自定义控件，您通常会发现它需要调试其设计时行为。 这是如果自定义设计器创作自定义控件尤其如此。 有关详细信息，请参阅[演练：创建 Windows 窗体控件都使用了 Visual Studio 设计时功能](creating-a-wf-control-design-time-features.md)。  
  
 您可以调试使用 Visual Studio 中，您自定义控件，就像就像调试任何其他.NET Framework 类。 不同之处是待调试正在运行自定义控件的代码的 Visual Studio 的单独实例  
  
 本演练涉及以下任务：  
  
-   创建用于承载自定义控件的 Windows 窗体项目  
  
-   创建控件库项目  
  
-   将属性添加到自定义控件  
  
-   将自定义控件添加到主机窗体  
  
-   设置设计时调试项目  
  
-   在设计时调试自定义控件  
  
 完成后，必须了解调试自定义控件的设计时行为所需的任务。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="creating-the-project"></a>创建项目  
 第一步是创建应用程序项目。 将使用此项目以生成承载自定义控件的应用程序。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
-   创建一个名为"DebuggingExample"的 Windows 应用程序项目 (**文件** > **新建** > **项目** >  **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**)。  
  
## <a name="creating-a-control-library-project"></a>创建控件库项目  
 下一步是创建控件库项目并设置自定义控件。  
  
#### <a name="to-create-the-control-library-project"></a>若要创建的控件库项目  
  
1.  添加**Windows 控件库**到解决方案。  
  
2.  添加一个新**UserControl** DebugControlLibrary 项目项。 有关详细信息，请参阅[如何：添加新项目项](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w0572c5b(v=vs.100))。 新的源文件基名称指定为"DebugControl"。  
  
3.  使用**解决方案资源管理器**，通过删除代码文件的基名称中删除项目的默认控件"`UserControl1`"。 有关详细信息，请参阅[如何：移除、 删除和排除项](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0ebzhwsk(v=vs.100))。  
  
4.  生成解决方案。  
  
## <a name="checkpoint"></a>检查点  
 此时，你将能够查看自定义控件**工具箱**。  
  
#### <a name="to-check-your-progress"></a>若要检查您的进度  
  
-   查找名为新选项卡**DebugControlLibrary 组件**并单击以选择它。 在打开时将看到控件列为**DebugControl**使用其旁边的默认图标。  
  
## <a name="adding-a-property-to-your-custom-control"></a>将属性添加到自定义控件  
 若要演示自定义控件的代码运行在设计时，将添加一个属性，并实现属性的代码中设置断点。  
  
#### <a name="to-add-a-property-to-your-custom-control"></a>若要将属性添加到自定义控件  
  
1.  打开**DebugControl**中**代码编辑器**。 将以下代码添加到类定义：  
  
    ```vb  
    Private demoStringValue As String = Nothing  
    <BrowsableAttribute(true)>  
    Public Property DemoString() As String  
  
        Get  
            Return Me.demoStringValue  
        End Get  
  
        Set(ByVal value As String)  
            Me.demoStringValue = value  
        End Set  
  
    End Property  
    ```  
  
    ```csharp  
    private string demoStringValue = null;  
    [Browsable(true)]  
    public string DemoString  
    {  
        get  
        {  
            return this.demoStringValue;  
        }  
        set  
        {  
            demoStringValue = value;  
        }  
    }  
    ```  
  
2.  生成解决方案。  
  
## <a name="adding-your-custom-control-to-the-host-form"></a>将自定义控件添加到主机窗体  
 若要调试自定义控件的设计时行为，将主机窗体上将自定义控件类的一个实例。  
  
#### <a name="to-add-your-custom-control-to-the-host-form"></a>若要将自定义控件添加到主机窗体  
  
1.  在"DebuggingExample"项目中，打开在 Form1 **Windows 窗体设计器**。  
  
2.  在中**工具箱**，打开**DebugControlLibrary 组件**选项卡，将**DebugControl**拖到窗体的实例。  
  
3.  查找`DemoString`中的自定义属性**属性**窗口。 请注意，您可以更改其值，就像任何其他属性。 此外请注意，当`DemoString`属性处于选中状态，该属性的描述字符串会显示在底部**属性**窗口。  
  
## <a name="setting-up-the-project-for-design-time-debugging"></a>设置设计时调试项目  
 若要调试自定义控件的设计时行为，将调试正在运行自定义控件的代码的 Visual Studio 的单独实例。  
  
#### <a name="to-set-up-the-project-for-design-time-debugging"></a>若要设置项目以便进行设计时调试  
  
1.  右键单击**DebugControlLibrary**项目中**解决方案资源管理器**，然后选择**属性**。  
  
2.  在中**DebugControlLibrary**属性表中，选择**调试**选项卡。  
  
     在中**启动操作**部分中，选择**启动外部程序**。 你将调试的单独实例的 Visual Studio 中，因此请单击省略号 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 按钮以浏览 Visual Studio IDE。 可执行文件的名称是**devenv.exe**，如果已安装到默认位置，其路径为 %programfiles%\Microsoft Visual Studio 9.0\Common7\IDE\devenv.exe。  
  
3.  单击“确定”关闭对话框。  
  
4.  右键单击**DebugControlLibrary**项目，然后选择**设为启动项目**若要启用此调试配置。  
  
## <a name="debugging-your-custom-control-at-design-time"></a>在设计时调试自定义控件  
 现在已准备好调试自定义控件在设计模式下运行。 启动调试会话时，将创建 Visual Studio 的新实例，并且将以加载"DebuggingExample"解决方案。 当你打开中的 Form1**窗体设计器**，将创建并将开始运行自定义控件的实例。  
  
#### <a name="to-debug-your-custom-control-at-design-time"></a>若要在设计时调试自定义控件  
  
1.  打开**DebugControl**中的源文件**代码编辑器**，将断点放在`Set`访问器的`DemoString`属性。  
  
2.  按 F5 启动调试会话。 请注意，创建 Visual Studio 的新实例。 你可以区分两种方法中的实例：  
  
    -   调试实例包含单词**运行**标题栏中  
  
    -   调试实例都有**启动**按钮及其**调试**禁用工具栏  
  
     在调试实例中设置断点。  
  
3.  在 Visual Studio 的新实例中，打开"DebuggingExample"解决方案。 您可以轻松地找到解决方案，通过选择**最近使用的项目**从**文件**菜单。 将列出"DebuggingExample.sln"解决方案文件，如最近使用的文件。  
  
4.  打开在 Form1**窗体设计器**，然后选择**DebugControl**控件。  
  
5.  更改 `DemoString` 属性的值。 请注意，当提交更改时，Visual Studio 的调试实例获取焦点并且执行在断点处停止。 你可以单步执行属性访问器就像在任何其他代码一样。  
  
6.  在您完成与调试会话，请可以退出，请关闭 Visual Studio 的托管的实例，或单击**停止调试**调试实例中的按钮。  
  
## <a name="next-steps"></a>后续步骤  
 现在，可以在设计时调试自定义控件，有许多可能的扩展与 Visual Studio IDE 的控件的交互。  
  
-   可以使用<xref:System.ComponentModel.Component.DesignMode%2A>属性的<xref:System.ComponentModel.Component>类来编写代码，将仅在设计时执行。 有关详细信息，请参阅 <xref:System.ComponentModel.Component.DesignMode%2A>。  
  
-   有几个特性可应用于控件的属性，以处理与设计器的自定义控件的交互。 您可以找到这些属性在<xref:System.ComponentModel?displayProperty=nameWithType>命名空间。  
  
-   自定义控件，可以编写自定义设计器。 这样，您对使用由 Visual Studio 公开可扩展设计器基础结构的设计体验的完全控制。 有关详细信息，请参阅[演练：创建 Windows 窗体控件都使用了 Visual Studio 设计时功能](creating-a-wf-control-design-time-features.md)。  
  
## <a name="see-also"></a>请参阅
- [演练：创建利用 Visual Studio 设计时功能的 Windows 窗体控件](creating-a-wf-control-design-time-features.md)
- [如何：访问设计时服务](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171822(v=vs.120))
- [如何：在 Windows 窗体中访问设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ms171827(v=vs.120))
