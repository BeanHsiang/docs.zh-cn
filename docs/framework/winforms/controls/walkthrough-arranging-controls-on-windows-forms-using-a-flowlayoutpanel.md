---
title: 演练：使用 FlowLayoutPanel 的 Windows 窗体上排列控件
ms.date: 03/30/2017
helpviewer_keywords:
- FlowLayoutPanel control [Windows Forms], walkthroughs
- Windows Forms controls, arranging
- controls [Windows Forms], arranging with FlowLayoutPanel
- layout [Windows Forms], walkthroughs
ms.assetid: a1744323-0316-49c2-992e-ebfc0a976b85
ms.openlocfilehash: fdb92a1ec9aa349c8768b5dc4ddf3d403297cf7f
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703534"
---
# <a name="walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel"></a>演练：使用 FlowLayoutPanel 的 Windows 窗体上排列控件
某些应用程序需要这样一个窗体，该窗体的布局可在窗体重新调整大小或在内容更改大小时对自身进行排列。 当你需要动态布局并且不希望在代码中显式处理 <xref:System.Windows.Forms.Control.Layout> 事件时，请考虑使用布局面板。  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> 控件和 <xref:System.Windows.Forms.TableLayoutPanel> 控件提供可用于排列窗体上的控件的直观方式。 两种控件均提供一种自动的可配置能力来控制包含在控件内的子控件的相对位置，并且两种控件均在运行时提供动态布局功能，以便它们可以在父窗体的尺寸更改时重新调整子控件的大小和对其进行重新定位。 布局面板可以嵌套在布局面板内，从而实现复杂的用户界面。  
  
 <xref:System.Windows.Forms.TableLayoutPanel>排列其内容在网格中，提供的功能类似的 html\<表 > 元素。 其单元格排列为行和列，并且这些行和列可具有不同的大小。 有关详细信息，请参见[演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)。  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> 以特定的流向排列其内容：水平或垂直。 可从一行到下一行，或从一列到下列进行内容换行。 还可以剪切内容，而不是进行换行。 本演练涉及以下任务：  
  
-   创建 Windows 窗体项目  
  
-   沿水平方向和垂直方向排列控件  
  
-   更改流方向  
  
-   插入分流符  
  
-   使用填充和边距排列控件  
  
-   通过在工具箱中双击控件将其插入  
  
-   通过绘制控件轮廓将其插入  
  
-   使用插入符号插入控件  
  
-   将现有控件重新分配给另一个父控件  
  
 完成上述操作后，你将会了解这些重要布局功能所发挥的作用。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="creating-the-project"></a>创建项目  
 第一步是创建项目并设置窗体。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
1.  创建一个名为"FlowLayoutPanelExample"的基于 Windows 的应用程序项目 (**文件** > **新建** > **项目** > **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**).  
  
2.  在 **“窗体设计器”** 中选择窗体。  
  
## <a name="arranging-controls-horizontally-and-vertically"></a>沿水平方向和垂直方向排列控件  
 <xref:System.Windows.Forms.FlowLayoutPanel> 控件允许你沿行或列放置控件，而无需精确指定每个控件的位置。  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> 控件可在父窗体的尺寸更改时重新调整其子控件的大小或对其进行重排。  
  
#### <a name="to-arrange-controls-horizontally-and-vertically-using-a-flowlayoutpanel"></a>使用 FlowLayoutPanel 沿水平和垂直方向排列控件  
  
1.  从 <xref:System.Windows.Forms.FlowLayoutPanel> “工具箱” **将** 控件拖到你的窗体上。  
  
2.  从 <xref:System.Windows.Forms.Button> “工具箱” **将** 控件拖入 <xref:System.Windows.Forms.FlowLayoutPanel>。 请注意，会自动将其移动到 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的左上角。  
  
3.  将另一个 <xref:System.Windows.Forms.Button> 控件从 **“工具箱”** 拖入 <xref:System.Windows.Forms.FlowLayoutPanel>。 请注意，会自动将 <xref:System.Windows.Forms.Button> 控件移动到第一个 <xref:System.Windows.Forms.Button> 控件旁边的位置。 如果你的 <xref:System.Windows.Forms.FlowLayoutPanel> 过窄而导致两个控件无法位于同一行，则新的 <xref:System.Windows.Forms.Button> 控件将被自动移动到下一行。  
  
4.  从 <xref:System.Windows.Forms.Button> “工具箱” **将另外几个** 控件也拖入 <xref:System.Windows.Forms.FlowLayoutPanel>。 继续放置 <xref:System.Windows.Forms.Button> 控件，直到有一个被换到下一行。  
  
5.  将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的 <xref:System.Windows.Forms.FlowLayoutPanel.WrapContents%2A> 属性值更改为 `false`。 请注意，子控件不再流到下一行。 相反，会将其移动到第一行并将其剪切。  
  
6.  将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的 <xref:System.Windows.Forms.FlowLayoutPanel.WrapContents%2A> 属性值更改为 `true`。 请注意，子控件会再次流到下一行。  
  
7.  减小 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的宽度直至将所有 <xref:System.Windows.Forms.Button> 控件移入第一列。  
  
8.  增加 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的宽度直至将所有 <xref:System.Windows.Forms.Button> 控件移入第一行。 你可能需要重新调整窗体大小以容纳更大宽度。  
  
## <a name="changing-flow-direction"></a>更改流方向  
 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 属性允许你更改控件排列的方向。 你可以从左到右、从右到左、从顶部到底部或从底部到顶部排列子控件。  
  
#### <a name="to-change-the-flow-direction-in-a-flowlayoutpanel"></a>若要在 FlowLayoutPanel 中更改流方向  
  
1.  将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 属性值更改为 <xref:System.Windows.Forms.FlowDirection.TopDown>。 请注意，子控件排列为一列或多列，具体取决于控件的高度。  
  
2.  重新调整 <xref:System.Windows.Forms.FlowLayoutPanel> 的大小，以使其高度小于 <xref:System.Windows.Forms.Button> 控件的列高。 请注意， <xref:System.Windows.Forms.FlowLayoutPanel> 会重新排列子控件以流入下一列。 继续减小高度，并注意，子控件会流入连续列。 将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 属性值更改为 <xref:System.Windows.Forms.FlowDirection.RightToLeft>。 请注意，子控件的位置会反转。 将 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 属性的值更改为 <xref:System.Windows.Forms.FlowDirection.BottomUp>时，请观察布局。  
  
## <a name="inserting-flow-breaks"></a>插入分流符  
 <xref:System.Windows.Forms.FlowLayoutPanel> 控件向其子控件提供 FlowBreak 属性。 将 FlowBreak 属性的值设置为 `true` 导致 <xref:System.Windows.Forms.FlowLayoutPanel> 控件停止按当前排列方向对控件进行布局，并换行到下一行或下一列。  
  
#### <a name="to-insert-flow-breaks"></a>插入分流符  
  
1.  将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 属性值更改为 <xref:System.Windows.Forms.FlowDirection.TopDown>。  
  
2.  在最左边那一列的中间选择一个 <xref:System.Windows.Forms.Button> 控件。  
  
3.  将 <xref:System.Windows.Forms.Button> 控件的 FlowBreak 属性的值设为 `true`。 请注意，此列将断开，并且所选定的 <xref:System.Windows.Forms.Button> 控件后面的控件将流入下一列。 将 <xref:System.Windows.Forms.Button> 控件的 FlowBreak 属性的值设置为 `false` 以返回到初始行为。  
  
## <a name="positioning-controls-using-docking-and-anchoring"></a>使用停靠和锚定来定位控件  
 子控件的停靠和锚定行为不同于其他容器控件中的行为。 停靠和锚定均相对于流方向上的最大控件。  
  
#### <a name="to-position-controls-using-docking-and-anchoring"></a>使用停靠和锚定定位控件  
  
1.  增加 <xref:System.Windows.Forms.FlowLayoutPanel> 的大小直到 <xref:System.Windows.Forms.Button> 控件全部排列在一列中。  
  
2.  选择顶部 <xref:System.Windows.Forms.Button> 控件。 增加其宽度，以使其宽度约为其他 <xref:System.Windows.Forms.Button> 控件的两倍。  
  
3.  选择第二个 <xref:System.Windows.Forms.Button> 控件。 将其 <xref:System.Windows.Forms.Control.Anchor%2A> 属性的值更改为 <xref:System.Windows.Forms.AnchorStyles.Right>。 请注意，此操作会将它移动，使其右边框对齐第一个 <xref:System.Windows.Forms.Button> 控件的右边框。  
  
4.  将其 <xref:System.Windows.Forms.Control.Anchor%2A> 属性的值更改为 <xref:System.Windows.Forms.AnchorStyles.Right> 和 <xref:System.Windows.Forms.AnchorStyles.Left>。 请注意，会将其大小调整为与第一个 <xref:System.Windows.Forms.Button> 控件的宽度相同。  
  
5.  选择第三个 <xref:System.Windows.Forms.Button> 控件。 将其 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值更改为 <xref:System.Windows.Forms.DockStyle.Fill>。 请注意，会将其大小调整为与第一个 <xref:System.Windows.Forms.Button> 控件的宽度相同。  
  
## <a name="arranging-controls-using-padding-and-margins"></a>使用填充和边距排列控件  
 还可以通过更改 <xref:System.Windows.Forms.FlowLayoutPanel> 和 <xref:System.Windows.Forms.Control.Padding%2A> 属性排列 <xref:System.Windows.Forms.Control.Margin%2A> 控件中的控件。  
  
 <xref:System.Windows.Forms.Control.Padding%2A> 属性允许你在 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的单元格内控制控件的放置。 它指定子控件和 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的边框之间的间距。  
  
 <xref:System.Windows.Forms.Control.Margin%2A> 属性允许你控制控件之间的间距。  
  
#### <a name="to-arrange-controls-using-the-padding-and-margin-properties"></a>使用“填充”和“边距”属性排列控件  
  
1.  将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性值更改为 <xref:System.Windows.Forms.DockStyle.Fill>。 如果你的窗体足够大，则 <xref:System.Windows.Forms.Button> 控件将被移动到 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的第一列中。  
  
2.  通过在 <xref:System.Windows.Forms.FlowLayoutPanel> “属性” <xref:System.Windows.Forms.Control.Padding%2A> 窗口中展开 <xref:System.Windows.Forms.Control.Padding%2A> 条目并将 **属性设置为** 20 <xref:System.Windows.Forms.Padding.All%2A> ，可更改 **控件的**属性的值。 有关详细信息，请参见[演练：对 Windows 窗体控件使用 Padding、 Margins 和 AutoSize 属性](windows-forms-controls-padding-autosize.md)。 请注意，会将子控件向 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的中心移动。 增加 <xref:System.Windows.Forms.Control.Padding%2A> 属性的值会使子控件远离 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的边框。  
  
3.  选择 <xref:System.Windows.Forms.Button> 中全部的 <xref:System.Windows.Forms.FlowLayoutPanel> 控件，并将 <xref:System.Windows.Forms.Control.Margin%2A> 属性的值设置为 **20**。 请注意， <xref:System.Windows.Forms.Button> 控制之间的间距会增加，因此它们会分得更开。 你可能需要重新调整 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的大小，以使其变的更大，从而可看到全部子控件。  
  
## <a name="inserting-controls-by-double-clicking-them-in-the-toolbox"></a>通过在工具箱中双击控件将其插入  
 可通过在 <xref:System.Windows.Forms.FlowLayoutPanel> “工具箱” **中双击控件来填充**控件。  
  
#### <a name="to-insert-controls-by-double-clicking-in-the-toolbox"></a>若要通过在工具箱中双击控件将其插入  
  
1.  在“工具箱” <xref:System.Windows.Forms.Button>**中，双击**控件图标。 请注意，新的 <xref:System.Windows.Forms.Button> 控件会出现在 <xref:System.Windows.Forms.FlowLayoutPanel> 控件中。  
  
2.  在 **“工具箱”** 中再双击几个控件。 请注意，新控件会相继出现在 <xref:System.Windows.Forms.FlowLayoutPanel> 控件中。  
  
## <a name="inserting-a-control-by-drawing-its-outline"></a>通过绘制控件轮廓将其插入  
 你可以通过在单元格中绘制控件轮廓将控件插入 <xref:System.Windows.Forms.FlowLayoutPanel> 控件并指定其大小。  
  
#### <a name="to-insert-a-control-by-drawing-its-outline"></a>通过绘制控件轮廓插入控件  
  
1.  在“工具箱” 中，单击 <xref:System.Windows.Forms.Button> 控件图标。 请勿将其拖到窗体上。  
  
2.  将鼠标指针移到 <xref:System.Windows.Forms.FlowLayoutPanel> 控件上。 请注意，指针会更改为十字形，同时会附上 <xref:System.Windows.Forms.Button> 控件图标。  
  
3.  单击并按住鼠标按钮。  
  
4.  拖动鼠标指针以绘制 <xref:System.Windows.Forms.Button> 控件的轮廓。 当获得所需大小时，释放鼠标。 请注意，将在 <xref:System.Windows.Forms.Button> 控件的下一个打开位置创建 <xref:System.Windows.Forms.FlowLayoutPanel> 控件。  
  
## <a name="inserting-controls-using-the-insertion-bar"></a>使用插入栏插入控件  
 可在 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的特定位置插入控件。 将控件拖入 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的客户端区域时，会显示一个插入栏，指示控件将插入的位置。  
  
#### <a name="to-insert-a-control-using-the-caret"></a>若要使用插入符号插入控件  
  
1.  从 <xref:System.Windows.Forms.Button> “工具箱” **将** 控件拖入 <xref:System.Windows.Forms.FlowLayoutPanel> 控件并指向两个 <xref:System.Windows.Forms.Button> 控件之间的空白区域。 请注意，绘制一个插入栏，指示在何处<xref:System.Windows.Forms.Button>拖放到将放置<xref:System.Windows.Forms.FlowLayoutPanel>控件。 将新的 <xref:System.Windows.Forms.Button> 控件放入 <xref:System.Windows.Forms.FlowLayoutPanel> 控件之前，移动鼠标指针以观察插入栏移动的方式。  
  
2.  将新的 <xref:System.Windows.Forms.Button> 控件放入 <xref:System.Windows.Forms.FlowLayoutPanel> 控件。 请注意，新的 <xref:System.Windows.Forms.Button> 控件与其他控件未对齐，因为其 <xref:System.Windows.Forms.Control.Margin%2A> 属性具有不同的值。  
  
## <a name="reassigning-existing-controls-to-a-different-parent"></a>将现有控件重新分配给另一个父控件  
 可以将窗体中的控件分配给新的 <xref:System.Windows.Forms.FlowLayoutPanel> 控件。  
  
#### <a name="to-reparent-existing-controls"></a>若要重新设置现有控件的父级  
  
1.  将三个 <xref:System.Windows.Forms.Button> 控件从“工具箱”  拖到窗体上。 将其相邻放置，但不用对齐它们。  
  
2.  在“工具箱” 中，单击 <xref:System.Windows.Forms.FlowLayoutPanel> 控件图标。 请勿将其拖到窗体上。  
  
3.  将鼠标指针移至靠近这 3 个 <xref:System.Windows.Forms.Button> 控件。 请注意，指针会更改为十字形，同时会附上 <xref:System.Windows.Forms.FlowLayoutPanel> 控件图标。  
  
4.  单击并按住鼠标按钮。  
  
5.  拖动鼠标指针以绘制 <xref:System.Windows.Forms.FlowLayoutPanel> 控件的轮廓。 在这三个 <xref:System.Windows.Forms.Button> 控件周围绘制轮廓。  
  
6.  释放鼠标按钮。 请注意，这三个 <xref:System.Windows.Forms.Button> 控件插入到 <xref:System.Windows.Forms.FlowLayoutPanel> 控件中。  
  
## <a name="next-steps"></a>后续步骤  
 可使用布局面板和控件的组合实现复杂布局。 有关进一步探索的建议包括：  
  
-   将其中一个 <xref:System.Windows.Forms.Button> 控件调整为更大的大小，并注意对布局产生的效果。  
  
-   布局面板可以包含其他布局面板。 试验将 <xref:System.Windows.Forms.TableLayoutPanel> 控件放入现有控件。  
  
-   将 <xref:System.Windows.Forms.FlowLayoutPanel> 控件停靠到父窗体。 调整窗体大小，并注意对布局产生的效果。  
  
-   将其中一个控件的 <xref:System.Windows.Forms.Control.Visible%2A> 属性设置为 `false` ，并注意 <xref:System.Windows.Forms.FlowLayoutPanel> 作为响应是如何进行重排的。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.FlowLayoutPanel>
- <xref:System.Windows.Forms.TableLayoutPanel>
- [演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [演练：使用对齐线的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
- [Microsoft Windows 用户体验，用户界面开发人员和设计人员的官方指南。Redmond，WA:Microsoft Press，1999年。(USBN:0-7356-0566-1)](https://www.microsoft.com/mspress/southpacific/books/book11588.htm)
- [AutoSize 属性概述](autosize-property-overview.md)
- [如何：在 Windows 窗体上停靠控件](how-to-dock-controls-on-windows-forms.md)
- [如何：在 Windows 窗体上定位控件](how-to-anchor-controls-on-windows-forms.md)
- [演练：布局 Windows 窗体控件与 Padding、 Margins 和 AutoSize 属性](windows-forms-controls-padding-autosize.md)
