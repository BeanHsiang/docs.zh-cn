---
title: 演练：在 WPF 中排列 Windows 窗体控件
ms.date: 04/03/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- arranging controls [WPF]
ms.assetid: a1db8049-15c7-45d6-ae3d-36a6735cb848
ms.openlocfilehash: bfb0aba2798179c31674377104bbff633b6f48fc
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367184"
---
# <a name="walkthrough-arranging-windows-forms-controls-in-wpf"></a>演练：在 WPF 中排列 Windows 窗体控件
本演练演示如何使用[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局功能来排列[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]混合应用程序中的控件。  
  
 本演练涉及以下任务：  
  
-   创建项目。  
  
-   使用默认布局设置。  
  
-   根据内容调整大小。  
  
-   使用绝对定位。  
  
-   显式指定大小。  
  
-   设置布局属性。  
  
-   了解 Z 顺序限制。  
  
-   停靠。  
  
-   设置可见性。  
  
-   承载不拉伸的控件。  
  
-   缩放。  
  
-   旋转。  
  
-   设置填充和边距。  
  
-   使用动态布局容器。  
  
 在本演练中所涉及任务的完整代码列表，请参阅[在 WPF 示例中排列 Windows 窗体控件](https://go.microsoft.com/fwlink/?LinkID=159971)。  
  
 完成后，必须了解[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]布局中的功能[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-基于应用程序。  
  
## <a name="prerequisites"></a>系统必备  

若要完成本演练，必须具有 Visual Studio。
  
## <a name="creating-the-project"></a>创建项目  
  
#### <a name="to-create-and-set-up-the-project"></a>创建并设置项目  
  
1.  创建一个名为的 WPF 应用程序项目`WpfLayoutHostingWf`。  
  
2.  在解决方案资源管理器中，添加对下列程序集的引用。  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
    -   System.Drawing  
  
3.  双击 MainWindow.xaml，在 XAML 视图中将其打开。  
  
4.  在中<xref:System.Windows.Window>元素中，添加以下[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]命名空间映射。  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5.  在中<xref:System.Windows.Controls.Grid>元素集<xref:System.Windows.Controls.Grid.ShowGridLines%2A>属性设置为`true`并定义五行三列。  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#2)]  
  
## <a name="using-default-layout-settings"></a>使用默认布局设置  
 默认情况下<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素处理承载的布局[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
#### <a name="to-use-default-layout-settings"></a>使用默认布局设置  
  
1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#3)]  
  
2.  按 F5 生成并运行该应用程序。 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.Button?displayProperty=nameWithType>控件会出现在<xref:System.Windows.Controls.Canvas>。 所承载的控件根据其内容调整大小和<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素大小以适应所承载的控件。  
  
## <a name="sizing-to-content"></a>按内容调整大小  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素可确保所承载的控件调整大小以正确显示其内容。  
  
#### <a name="to-size-to-content"></a>按内容调整大小  
  
1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#4)]  
  
2.  按 F5 生成并运行该应用程序。 两个新按钮控件会调整大小以正确，显示较长文本字符串和较大字号和<xref:System.Windows.Forms.Integration.WindowsFormsHost>调整元素大小以容纳所承载的控件。  
  
## <a name="using-absolute-positioning"></a>使用绝对定位  
 可以使用绝对定位将<xref:System.Windows.Forms.Integration.WindowsFormsHost>用户界面 (UI) 中的任意位置的元素。  
  
#### <a name="to-use-absolute-positioning"></a>使用绝对定位  
  
1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#5](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#5)]  
  
2.  按 F5 生成并运行该应用程序。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素放在距顶部的网格单元格的 20 像素，距左侧 20 像素。  
  
## <a name="specifying-size-explicitly"></a>显式指定大小  
 可以指定的大小<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素使用<xref:System.Windows.FrameworkElement.Width%2A>和<xref:System.Windows.FrameworkElement.Height%2A>属性。  
  
#### <a name="to-specify-size-explicitly"></a>显式指定大小  
  
1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#6](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#6)]  
  
2.  按 F5 生成并运行该应用程序。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素设置为的大小为宽 50 像素高 70 像素，这是比默认布局设置小。 内容[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]相应重新排列控件。  
  
## <a name="setting-layout-properties"></a>设置布局属性  
 始终使用的属性对承载控件设置布局相关属性<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素。 直接对承载控件设置布局属性会产生意外结果。  
  
 在承载控件设置布局相关属性[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]不起作用。  
  
#### <a name="to-see-the-effects-of-setting-properties-on-the-hosted-control"></a>查看对承载控件设置属性的效果  
  
1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。  
  
     [!code-xaml[WpfLayoutHostingWfWithXaml#7](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#7)]  
  
2.  在“解决方案资源管理器”中，双击 MainWindow.xaml. vb 或 MainWindow.xaml.cs 在代码编辑器中将其打开。  
  
3.  以下代码复制到`MainWindow`类定义。  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#101](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#101)]
     [!code-vb[WpfLayoutHostingWfWithXaml#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#101)]

4.  按 F5 生成并运行该应用程序。

5.  单击**Click me**按钮。 `button1_Click`事件处理程序集<xref:System.Windows.Forms.Control.Top%2A>和<xref:System.Windows.Forms.Control.Left%2A>上所承载的控件的属性。 这将导致中重新定位承载的控件<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素。 宿主保持相同的屏幕区域，但承载控件被剪裁。 相反，所承载的控件应始终填充<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素。

## <a name="understanding-z-order-limitations"></a>了解 Z 顺序限制
 可见<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素始终绘制在其他 WPF 元素，之上，因而它们不受 z 顺序。 若要查看此 z 顺序行为，请执行以下操作：

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#8](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#8)]

2.  按 F5 生成并运行该应用程序。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素绘于标签元素上方。


## <a name="docking"></a>停靠
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素支持[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]停靠。 设置<xref:System.Windows.Controls.DockPanel.Dock%2A>附加属性以停靠中承载的控件<xref:System.Windows.Controls.DockPanel>元素。

#### <a name="to-dock-a-hosted-control"></a>停靠承载控件

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#9](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#9)]

2.  按 F5 生成并运行该应用程序。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素的右侧停靠<xref:System.Windows.Controls.DockPanel>元素。

## <a name="setting-visibility"></a>设置可见性
 可以让你[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不可见或通过设置折叠<xref:System.Windows.UIElement.Visibility%2A>属性上的<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素。 当控件不可见时，控件不会显示，但会占据布局空间。 当控件处于折叠状态时，控件不会显示，也不会占据布局空间。

#### <a name="to-set-the-visibility-of-a-hosted-control"></a>设置承载控件的可见性

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#10](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#10)]

2.  在 MainWindow.xaml.vb 或 MainWindow.xaml.cs 中，将以下代码复制到类定义。

     [!code-csharp[WpfLayoutHostingWfWithXaml#102](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#102)]
     [!code-vb[WpfLayoutHostingWfWithXaml#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#102)]

3.  按 F5 生成并运行该应用程序。

4.  单击**单击此项可使不可见**按钮，使<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素不可见。

5.  单击**单击此项可折叠**按钮以隐藏<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素在布局完全。 当[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件处于折叠状态，周围的元素会重新排列以占据其空间。

## <a name="hosting-a-control-that-does-not-stretch"></a>承载不拉伸的控件
 某些[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件具有固定的大小，不会拉伸以填充布局中的可用空间。 例如，<xref:System.Windows.Forms.MonthCalendar>控件在固定的空间中显示一个月。

#### <a name="to-host-a-control-that-does-not-stretch"></a>承载不拉伸的控件

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#11)]

2.  按 F5 生成并运行该应用程序。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素居中在网格行中，但它不会拉伸以填充可用空间。 如果窗口足够大，可能会看到显示所承载的两个或多个月<xref:System.Windows.Forms.MonthCalendar>控件，但这些行中居中。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局引擎中心无法调整大小以填充可用空间的元素。

## <a name="scaling"></a>缩放
 与 WPF 元素不同大多数 Windows 窗体控件不是连续方式缩放。 若要提供自定义缩放，重写<xref:System.Windows.Forms.Integration.WindowsFormsHost.ScaleChild%2A?displayProperty=nameWithType>方法。

#### <a name="to-scale-a-hosted-control-by-using-the-default-behavior"></a>使用默认行为缩放承载控件

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#12)]

2.  按 F5 生成并运行该应用程序。 承载控件及其周围元素按 0.5 的比例进行缩放。 但是，承载控件的字体不缩放。

<!-- This could use an example of custom scaling. -->

## <a name="rotating"></a>旋转
 与 WPF 元素不同 Windows 窗体控件不支持旋转。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素不会不会旋转与其他 WPF 元素时应用旋转转换。 180 度引发以外的任何旋转值<xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError>事件。

#### <a name="to-see-the-effect-of-rotation-in-a-hybrid-application"></a>查看混合应用程序中的旋转效果

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#13)]

2.  按 F5 生成并运行该应用程序。 承载控件不旋转，但是它周围的元素旋转 180 度。 可能必须调整窗口大小才能看到这些元素。


## <a name="setting-padding-and-margins"></a>设置填充和边距
 填充和边距中的[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局是类似于填充和边距中的[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]。 只需将设置<xref:System.Windows.Controls.Control.Padding%2A>并<xref:System.Windows.FrameworkElement.Margin%2A>上的属性<xref:System.Windows.Forms.Integration.WindowsFormsHost>元素。

#### <a name="to-set-padding-and-margins-for-a-hosted-control"></a>为承载控件设置填充和边距

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#14](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#14)]
    [!code-xaml[WpfLayoutHostingWfWithXaml#15](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#15)]

2.  按 F5 生成并运行该应用程序。 填充和边距设置应用于承载[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件中的应用方式相同[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]。

## <a name="using-dynamic-layout-containers"></a>使用动态布局容器
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 提供了两个动态布局容器，<xref:System.Windows.Forms.FlowLayoutPanel>和<xref:System.Windows.Forms.TableLayoutPanel>。 此外可以使用这些容器[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]布局。

#### <a name="to-use-a-dynamic-layout-container"></a>使用动态布局容器

1.  将复制到以下 XAML<xref:System.Windows.Controls.Grid>元素。

     [!code-xaml[WpfLayoutHostingWfWithXaml#16](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#16)]

2.  在 MainWindow.xaml.vb 或 MainWindow.xaml.cs 中，将以下代码复制到类定义。

     [!code-csharp[WpfLayoutHostingWfWithXaml#103](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#103)]
     [!code-vb[WpfLayoutHostingWfWithXaml#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#103)]

3.  将调用添加到构造函数中的 `InitializeFlowLayoutPanel` 方法。

     [!code-csharp[WpfLayoutHostingWfWithXaml#104](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#104)]
     [!code-vb[WpfLayoutHostingWfWithXaml#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#104)]  
  
4.  按 F5 生成并运行该应用程序。 <xref:System.Windows.Forms.Integration.WindowsFormsHost>元素填充<xref:System.Windows.Controls.DockPanel>，并<xref:System.Windows.Forms.FlowLayoutPanel>排列其子控件在默认<xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
- [WindowsFormsHost 元素的布局注意事项](layout-considerations-for-the-windowsformshost-element.md)
- [在 WPF 示例中排列 Windows 窗体控件](https://go.microsoft.com/fwlink/?LinkID=159971)
- [演练：承载在 WPF 中的 Windows 窗体复合控件](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [演练：承载 WPF 复合控件在 Windows 窗体中](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
