---
title: 演练：承载 3-D WPF 复合控件在 Windows 窗体中
ms.date: 08/18/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting WPF content in Windows Forms [WPF]
- composite controls [WPF], hosting WPF in
ms.assetid: 486369a9-606a-4a3b-b086-a06f2119c7b0
ms.openlocfilehash: b1bd003c6a408e7455bb5c45e1f34a740fce67d1
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367435"
---
# <a name="walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms"></a>演练：承载 3-D WPF 复合控件在 Windows 窗体中

本演练演示如何创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]复合控件并将其在托管[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件和窗体使用<xref:System.Windows.Forms.Integration.ElementHost>控件。

在本演练中，您将实现[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> ，其中包含两个子控件。 <xref:System.Windows.Controls.UserControl>显示三维 (3-D) 锥形区域。 呈现三维对象是变得更为简单[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]比使用[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]。 因此，对主机有意义[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.UserControl>类，以创建 3d 图形[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]。

本演练涉及以下任务：

-   创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl>。

-   创建 Windows 窗体宿主项目。

-   承载[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl>。

## <a name="prerequisites"></a>系统必备

你需要以下组件来完成本演练：

-   Visual Studio 2017

<a name="To_Create_the_UserControl"></a>
## <a name="create-the-usercontrol"></a>创建用户控件

1.  创建**WPF 用户控件库**名为项目`HostingWpfUserControlInWf`。

2.  打开 UserControl1.xaml 在[!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]。

3.  生成的代码替换为以下代码：

     [!code-xaml[HostingWpfUserControlInWf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/HostingWpfUserControlInWf/ConeControl.xaml#1)]

     此代码定义<xref:System.Windows.Controls.UserControl?displayProperty=nameWithType>，其中包含两个子控件。 第一个子控件是<xref:System.Windows.Controls.Label?displayProperty=nameWithType>控制; 第二个是<xref:System.Windows.Controls.Viewport3D>显示三维锥体控件。

<a name="To_Create_the_Windows_Forms_Host_Project"></a>
## <a name="create-the-host-project"></a>创建宿主项目

1.  添加**WPF 应用 (.NET Framework)** 名为项目`WpfUserControlHost`到解决方案。 有关详细信息，请参见[演练：我第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。

2.  在中**解决方案资源管理器**，添加对 WindowsFormsIntegration 程序集，它名为 WindowsFormsIntegration.dll 的引用。

3.  将引用添加到以下[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]程序集：

    -   PresentationCore

    -   PresentationFramework

    -   WindowsBase

4.  添加对引用`HostingWpfUserControlInWf`项目。

5.  在解决方案资源管理器，设置`WpfUserControlHost`项目为启动项目。

<a name="To_Host_the_Windows_Presentation_Foundation"></a>
## <a name="host-the-usercontrol"></a>托管用户控件

1.  在 Windows 窗体设计器中打开 Form1。

2.  在属性窗口中，单击**事件**，然后双击<xref:System.Windows.Forms.Form.Load>事件创建事件处理程序。

     在代码编辑器将打开到新生成`Form1_Load`事件处理程序。

3.  Form1.cs 中的代码替换为以下代码。

     `Form1_Load`事件处理程序创建的实例`UserControl1`，并将添加为<xref:System.Windows.Forms.Integration.ElementHost>子控件的控件的集合。 <xref:System.Windows.Forms.Integration.ElementHost>控件添加到的子控件的窗体的集合。

     [!code-csharp[HostingWpfUserControlInWf#10](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/WpfUserControlHost/Form1.cs#10)]
     [!code-vb[HostingWpfUserControlInWf#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWpfUserControlInWf/VisualBasic/WpfUserControlHost/Form1.vb#10)]

4.  按 F5 生成并运行该应用程序。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
- [演练：承载 WPF 复合控件在 Windows 窗体中](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [演练：承载在 WPF 中的 Windows 窗体复合控件](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [承载 WPF 复合控件在 Windows 窗体示例](https://go.microsoft.com/fwlink/?LinkID=160001)