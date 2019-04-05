---
title: 演练：在设计时在 Windows 窗体上创建新的 WPF 内容
ms.date: 08/18/2018
helpviewer_keywords:
- interoperability [Windows Forms], WPF and Windows Forms
- WPF content [Windows Forms], hosting in Windows Forms
- hosting WPF content in Windows Forms
- ElementHost control
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: 2e92d8e8-f0e4-4df7-9f07-2acf35cd798c
ms.openlocfilehash: ed48db399ba47f0e6be96f7bca33d3892b19e433
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57707906"
---
# <a name="walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time"></a>演练：在设计时在 Windows 窗体上创建新的 WPF 内容

本主题显示如何创建 Windows Presentation Foundation (WPF) 控件，以便在基于 Windows 窗体的应用程序中使用。

在本演练中，你将要执行以下任务：

- 创建项目。

- 创建一个新的 WPF 控件。

- 将新的 WPF 控件添加到 Windows 窗体。 WPF 控件承载在 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。

## <a name="prerequisites"></a>系统必备

你需要以下组件来完成本演练：

- Visual Studio 2017

## <a name="creating-the-project"></a>创建项目

第一步是创建 Windows 窗体项目。 打开 Visual Studio 并创建一个新**Windows 窗体应用 (.NET Framework)** 项目在 Visual Basic 或 Visual C# 名为`HostingWpf`。

> [!NOTE]
> 承载 WPF 内容时，仅支持 C# 和 Visual Basic 项目。

## <a name="creating-a-new-wpf-control"></a>创建新的 WPF 控件

创建新的 WPF 控件并将其添加到你的项目中，这与将任何其他项添加到你的项目中一样容易。 Windows 窗体设计器适用于特定类型的名为控件*复合控件*，或*用户控件*。 有关 WPF 用户控件的详细信息，请参阅 <xref:System.Windows.Controls.UserControl>。

> [!NOTE]
> WPF 的 <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType> 类型不同于 Windows 窗体提供的用户控件类型（也称为 <xref:System.Windows.Forms.UserControl?displayProperty=nameWithType>）。

### <a name="to-create-a-new-wpf-control"></a>创建新的 WPF 控件

1. 在中**解决方案资源管理器**，添加一个新**WPF 用户控件库 (.NET Framework)** 到解决方案。 使用控件库默认名称 `WpfControlLibrary1`。 默认控件名称是 `UserControl1.xaml`。

     添加新控件将产生以下影响：

    - 添加文件 UserControl1.xaml。

    - 添加文件 UserControl1.xaml.cs 或 UserControl1.xaml.vb。 此文件包含事件处理程序和其他实现的代码隐藏。

    - 添加对 WPF 程序集的引用。

    - 文件 UserControl1.xaml 在 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] 中打开。

2. 在设计视图中，请确保已选中 `UserControl1`。 有关详细信息，请参阅[如何：选择并在设计图面上移动元素](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb514527(v=vs.100))。

3. 在中**属性**窗口中，设置的值<xref:System.Windows.FrameworkElement.Width%2A>并<xref:System.Windows.FrameworkElement.Height%2A>属性设置为**200**。

4. 从**工具箱**，拖动<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType>控件拖到设计图面上的。

5. 在中**属性**窗口中，设置的值<xref:System.Windows.Controls.TextBox.Text%2A>属性设置为**承载的内容**。

    > [!NOTE]
    > 一般情况下，你应承载更复杂的 WPF 内容。 此处，<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> 控件仅为了便于说明。

6. 生成项目。

## <a name="adding-a-wpf-control-to-a-windows-form"></a>将 WPF 控件添加到 Windows 窗体

新的 WPF 控件可供在窗体上使用。 Windows 窗体使用<xref:System.Windows.Forms.Integration.ElementHost>承载 WPF 内容的控件。

### <a name="to-add-a-wpf-control-to-a-windows-form"></a>将 WPF 控件添加到 Windows 窗体

1. 在 Windows 窗体设计器中打开 `Form1`。

2. 在中**工具箱**，找到标记为选项卡**WPFUserControlLibrary WPF 用户控件**。

3. 将 `UserControl1` 的实例拖到窗体上。

    - 在窗体上自动创建 <xref:System.Windows.Forms.Integration.ElementHost> 控件以承载 WPF 控件。

    - <xref:System.Windows.Forms.Integration.ElementHost>控件被命名为`elementHost1`并在**属性**窗口中，您可以看到其<xref:System.Windows.Forms.Integration.ElementHost.Child%2A>属性设置为**UserControl1**。

    - 将对 WPF 程序集的引用添加到项目。

    - 
  `elementHost1` 控件具有显示可用承载选项的智能标记面板。

4. 在中**ElementHost 任务**智能标记面板中，选择**在父容器中的停靠**。

5. 按 F5 生成并运行该应用程序。

## <a name="next-steps"></a>后续步骤

Windows 窗体和 WPF 是不同的技术，但它们设计为可以密切地互操作。 若要提供更丰富的外观和行为应用程序中的，请尝试以下方法：

- 在 WPF 页中承载 Windows 窗体控件。 有关详细信息，请参见[演练：在 WPF 中承载 Windows 窗体控件](../../wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)。

- 将 Windows 窗体的视觉样式应用于你的 WPF 内容。 有关详细信息，请参阅[如何：混合应用程序中启用视觉样式](../../wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md)。

- 更改 WPF 内容的样式。 有关详细信息，请参见[演练：WPF 内容的样式](walkthrough-styling-wpf-content.md)。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [迁移和互操作性](../../wpf/advanced/migration-and-interoperability.md)
- [使用 WPF 控件](using-wpf-controls.md)
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
