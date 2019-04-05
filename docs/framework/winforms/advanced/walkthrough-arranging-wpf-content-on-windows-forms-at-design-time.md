---
title: 演练：在设计时排列 Windows 窗体上的 WPF 内容
ms.date: 03/30/2017
helpviewer_keywords:
- WPF user control [Windows Forms], hosting in a layout panel
- WPF content [Windows Forms], arranging at design time
- Windows Forms, arranging WPF content at design time
- WPF content [Windows Forms], hosting in Windows Forms
- Windows Forms, anchoring and docking WPF content
- interoperability [WPF]
ms.assetid: 5efb1c53-1484-43d6-aa8a-f4861b99bb8a
ms.openlocfilehash: 0738d1522c8ade8f026a3bf69fbff0bc2c2d6d85
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712456"
---
# <a name="walkthrough-arranging-wpf-content-on-windows-forms-at-design-time"></a>演练：在设计时排列 Windows 窗体上的 WPF 内容
本演练演示如何使用 Windows 窗体布局功能（例如锚定和对齐线）排列 Windows Presentation Foundation (WPF) 控件。

 在本演练中，你将要执行以下任务：

-   创建项目。

-   创建 WPF 控件。

-   在布局面板中承载 WPF 控件。

-   使用对齐线对齐 WPF 控件。

-   锚定和停靠 WPF 控件。

> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="prerequisites"></a>系统必备  
 你需要以下组件来完成本演练：  
  
-   Visual Studio 2012.  
  
## <a name="creating-the-project"></a>创建项目  
 第一步是创建 Windows 窗体项目。  
  
> [!NOTE]
>  承载 WPF 内容时，仅支持 C# 和 Visual Basic 项目。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
-   创建新的 Windows 窗体应用程序项目在 Visual Basic 或 Visual C# 名为`ArrangeElementHost`。  
  
## <a name="creating-the-wpf-control"></a>创建 WPF 控件  
 将 WPF 控件添加到项目后，就可以在窗体上对其进行排列。  
  
#### <a name="to-create-wpf-controls"></a>创建 WPF 控件  
  
1.  将新的 WPF <xref:System.Windows.Controls.UserControl> 添加到项目。 使用控件类型的默认名称，`UserControl1.xaml`。 有关详细信息，请参见[演练：在设计时在 Windows 窗体上创建新的 WPF 内容](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  在设计视图中，请确保已选中 `UserControl1`。 有关详细信息，请参阅[如何：选择并在设计图面上移动元素](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb514527(v=vs.100))。  
  
3.  在中**属性**窗口中，设置的值<xref:System.Windows.FrameworkElement.Width%2A>并<xref:System.Windows.FrameworkElement.Height%2A>属性设置为`200`。  
  
4.  将 <xref:System.Windows.Controls.Control.Background%2A> 属性的值设置为 `Blue`。  
  
5.  生成项目。  
  
## <a name="hosting-wpf-controls-in-a-layout-panel"></a>在布局面板中承载 WPF 控件  
 在布局面板中使用 WPF 控件与使用其他 Windows 窗体控件的方式可以相同。  
  
#### <a name="to-host-wpf-controls-in-a-layout-panel"></a>若要在布局面板中承载 WPF 控件  
  
1.  在 Windows 窗体设计器中打开 `Form1`。  
  
2.  在中**工具箱**，拖动<xref:System.Windows.Forms.TableLayoutPanel>拖到窗体控件。  
  
3.  上<xref:System.Windows.Forms.TableLayoutPanel>控件的智能标记面板中，选择**移除最后一行**。  
  
4.  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的大小调整为更大的宽度和高度。  
  
5.  在中**工具箱**，双击`UserControl1`若要创建的实例`UserControl1`中的第一个单元<xref:System.Windows.Forms.TableLayoutPanel>控件。  
  
     
  `UserControl1` 的实例承载在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
6.  在中**工具箱**，双击`UserControl1`的第二个单元格中创建另一个实例<xref:System.Windows.Forms.TableLayoutPanel>控件。  
  
7.  在中**文档大纲**窗口中，选择`tableLayoutPanel1`。 有关详细信息，请参阅[文档大纲窗口](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/46xf4h0w(v=vs.100)#using-the-document-outline-window-for-silverlight-and-wpf)。  
  
8.  在中**属性**窗口中，设置的值<xref:System.Windows.Forms.Control.Padding%2A>属性设置为`10, 10, 10, 10`。  
  
     调整两个 <xref:System.Windows.Forms.Integration.ElementHost> 控件的大小以适应新的布局。  
  
## <a name="using-snaplines-to-align-wpf-controls"></a>使用对齐线对齐 WPF 控件  
 使用对齐线能够轻松对齐窗体上的控件。 还可以使用对齐线对齐 WPF 控件。 有关详细信息，请参见[演练：在 Windows 上排列控件窗体使用对齐线](../controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)。  
  
#### <a name="to-use-snaplines-to-align-wpf-controls"></a>若要使用对齐线对齐 WPF 控件  
  
1.  从**工具箱**，一个实例的拖放`UserControl1`拖到窗体并将它放在下方的空间<xref:System.Windows.Forms.TableLayoutPanel>控件。  
  
     
  `UserControl1` 的实例承载在名为 `elementHost3` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
2.  使用对齐线，将 `elementHost3` 的左边缘与 <xref:System.Windows.Forms.TableLayoutPanel> 控件的左边缘对齐。  
  
3.  使用对齐线，将 `elementHost3` 按与 <xref:System.Windows.Forms.TableLayoutPanel> 控件相同的宽度排列。  
  
4.  朝着 <xref:System.Windows.Forms.TableLayoutPanel> 控件移动 `elementHost3`，直到控件间显示居中对齐线。  
  
5.  在中**属性**窗口中，设置到边距属性的值`20, 20, 20, 20`。  
  
6.  向远离 <xref:System.Windows.Forms.TableLayoutPanel> 控件的方向移动 `elementHost3`，直到再次显示居中对齐线。 现在，居中对齐线指示边距为 20。  
  
7.  向右移动 `elementHost3`，直到其左边缘与 `elementHost1` 的左边缘对齐。  
  
8.  更改 `elementHost3` 的宽度，直到其右边缘与 `elementHost2` 的右边缘对齐。  
  
## <a name="anchoring-and-docking-wpf-controls"></a>锚定和停靠 WPF 控件  
 窗体上承载的 WPF 控件具有与其他 Windows 窗体控件相同的锚定和停靠行为。  
  
#### <a name="to-anchor-and-dock-wpf-controls"></a>若要锚定和停靠 WPF 控件  
  
1.  选择 `elementHost1`。  
  
2.  在中**属性**窗口中，将<xref:System.Windows.Forms.Control.Anchor%2A>属性设置为**顶部、 底部、 Left、 Right**。  
  
3.  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的大小调整为更大。  
  
     调整 `elementHost1` 控件大小，以填充单元格。  
  
4.  选择 `elementHost2`。  
  
5.  在中**属性**窗口中，设置的值<xref:System.Windows.Forms.Control.Dock%2A>属性设置为<xref:System.Windows.Forms.DockStyle.Fill>。  
  
     调整 `elementHost2` 控件大小，以填充单元格。  
  
6.  选择 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  
  
7.  将其 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值设置为 <xref:System.Windows.Forms.DockStyle.Top>。  
  
8.  选择 `elementHost3`。  
  
9. 将其 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值设置为 <xref:System.Windows.Forms.DockStyle.Fill>。  
  
     调整 `elementHost3` 控件大小，以填充窗体上的剩余空间。  
  
10. 调整窗体大小。  
  
     所有三个 <xref:System.Windows.Forms.Integration.ElementHost> 控件将相应地调整大小。  
  
     有关详细信息，请参阅[如何：锚定和停靠在 TableLayoutPanel 控件中的子控件](../controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [如何：锚定和停靠在 TableLayoutPanel 控件中的子控件](../controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)
- [如何：将控件与窗体边缘对齐在设计时](../controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)
- [演练：使用对齐线的 Windows 窗体上排列控件](../controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
- [迁移和互操作性](../../wpf/advanced/migration-and-interoperability.md)
- [使用 WPF 控件](using-wpf-controls.md)
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
