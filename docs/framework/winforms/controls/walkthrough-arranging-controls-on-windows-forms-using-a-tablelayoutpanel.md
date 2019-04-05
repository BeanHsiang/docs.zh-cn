---
title: 演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], arranging with TableLayoutPanel
- TableLayoutPanel control [Windows Forms], walkthroughs
- Windows Forms controls, arranging
ms.assetid: d474885e-12cc-4ab7-b997-2a23a643049b
ms.openlocfilehash: 8999dba110ee21b735c79ccc10c5af52dbfcdea9
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712989"
---
# <a name="walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel"></a>演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件
某些应用程序需要这样一个窗体，该窗体的布局可在窗体重新调整大小或在内容更改大小时对自身进行排列。 当你需要动态布局并且不希望在代码中显式处理 <xref:System.Windows.Forms.Control.Layout> 事件时，请考虑使用布局面板。  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> 控件和 <xref:System.Windows.Forms.TableLayoutPanel> 控件提供可用于排列窗体上的控件的直观方式。 两种控件均提供一种自动的可配置能力来控制包含在控件内的子控件的相对位置，并且两种控件均在运行时提供动态布局功能，以便它们可以在父窗体的尺寸更改时重新调整子控件的大小和对其进行重新定位。 布局面板可以嵌套在布局面板内，从而实现复杂的用户界面。  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> 以特定的流向排列其内容：水平或垂直。 可从一行到下一行，或从一列到下列进行内容换行。 还可以剪切内容，而不是进行换行。 有关详细信息，请参见[演练：使用 FlowLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)。  
  
 <xref:System.Windows.Forms.TableLayoutPanel>排列其内容在网格中，提供的功能类似的 html\<表 > 元素。 <xref:System.Windows.Forms.TableLayoutPanel>让您可以将控件放在网格布局，而无需精确指定每个控件的位置。 其单元格排列为行和列，并且这些行和列可具有不同的大小。 可在中的行和列合并单元格。 单元格可以包含一个窗体可以包含，并在作为容器的大多数其他方面的行为的任何内容。  
  
 <xref:System.Windows.Forms.TableLayoutPanel>控件还提供了按比例调整大小功能在运行时，这样窗体调整大小时，你的布局可以顺利地更改。 这使得<xref:System.Windows.Forms.TableLayoutPanel>控件非常适合用于数据输入窗体和本地化的应用程序等目的。 有关详细信息，请参见[演练：创建数据输入可调整大小的 Windows 窗体](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/991eahec(v=vs.100))和[演练：创建可本地化 Windows 窗体](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/7k9fa71y(v=vs.100))。  
  
 一般情况下，不应使用<xref:System.Windows.Forms.TableLayoutPanel>作为整个布局的容器的控件。 使用<xref:System.Windows.Forms.TableLayoutPanel>控件提供的布局部分按比例调整大小的功能。  
  
 本演练涉及以下任务：  
  
-   创建 Windows 窗体项目  
  
-   在行和列中排列控件  
  
-   设置行和列属性  
  
-   跨越行和列与控件  
  
-   自动处理溢出  
  
-   通过在工具箱中双击控件将其插入  
  
-   通过绘制控件轮廓将其插入  
  
-   将现有控件重新分配给另一个父控件  
  
 完成上述操作后，你将会了解这些重要布局功能所发挥的作用。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="creating-the-project"></a>创建项目  
 第一步是创建项目并设置窗体。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
1.  创建一个名为"TableLayoutPanelExample"的 Windows 应用程序项目。 有关详细信息，请参阅[如何：创建 Windows 窗体应用程序项目](/visualstudio/ide/step-1-create-a-windows-forms-application-project)。  
  
2.  选择中的窗体**Windows** **窗体设计器**。  
  
## <a name="arranging-controls-in-rows-and-columns"></a>在行和列中排列控件  
 <xref:System.Windows.Forms.TableLayoutPanel>让您可以轻松地为行和列排列控件。  
  
#### <a name="to-arrange-controls-in-rows-and-columns-using-a-tablelayoutpanel"></a>若要排列在行和列使用 TableLayoutPanel 控件  
  
1.  从 <xref:System.Windows.Forms.TableLayoutPanel> “工具箱” **将** 控件拖到你的窗体上。 请注意，默认情况下，<xref:System.Windows.Forms.TableLayoutPanel>控件具有四个单元格。  
  
2.  拖动<xref:System.Windows.Forms.Button>控件从**工具箱**到<xref:System.Windows.Forms.TableLayoutPanel>控件并将它放到一个单元格。 请注意，<xref:System.Windows.Forms.Button>内所选的单元格创建控件。  
  
3.  将三个详细<xref:System.Windows.Forms.Button>控件从**工具箱**到<xref:System.Windows.Forms.TableLayoutPanel>控制，以便每个单元格都包含一个按钮。  
  
4.  获取两个列之间的垂直大小调整句柄并将其移到左侧。 请注意，<xref:System.Windows.Forms.Button>第一列中的控件调整为一个较小的宽度时的大小<xref:System.Windows.Forms.Button>第二列中的控件保持不变。  
  
5.  获取两个列之间的垂直大小调整句柄并将其移到右侧。 请注意，<xref:System.Windows.Forms.Button>控件中的第一列返回到其原始大小，而<xref:System.Windows.Forms.Button>第二列中的控件移到右侧。  
  
6.  将移动的水平大小调整句柄，向上和向下，若要查看在面板控件上的效果。  
  
## <a name="positioning-controls-within-cells-using-docking-and-anchoring"></a>使用停靠和锚定的单元格内定位控件  
 中的子控件的锚定行为<xref:System.Windows.Forms.TableLayoutPanel>不同于其他容器控件中的行为。 子控件的悬停行为等同于其他容器控件。  
  
#### <a name="positioning-controls-within-cells"></a>在单元格内定位控件  
  
1.  选择第一个<xref:System.Windows.Forms.Button>控件。 将其 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值更改为 <xref:System.Windows.Forms.DockStyle.Fill>。 请注意，<xref:System.Windows.Forms.Button>控件将展开以填充其的单元格。  
  
2.  选择另一个<xref:System.Windows.Forms.Button>控件。 将其 <xref:System.Windows.Forms.Control.Anchor%2A> 属性的值更改为 <xref:System.Windows.Forms.AnchorStyles.Right>。 请注意，它移动，使其右边框附近的单元格右边框。 边框之间的距离是总和<xref:System.Windows.Forms.Button>控件的<xref:System.Windows.Forms.Control.Margin%2A>属性和面板的<xref:System.Windows.Forms.Control.Padding%2A>属性。  
  
3.  更改的值<xref:System.Windows.Forms.Button>控件的<xref:System.Windows.Forms.Control.Anchor%2A>属性设置为<xref:System.Windows.Forms.AnchorStyles.Right>和<xref:System.Windows.Forms.AnchorStyles.Left>。 请注意，使用的控件大小为该单元格的宽度<xref:System.Windows.Forms.Control.Margin%2A>和<xref:System.Windows.Forms.Control.Padding%2A>考虑在内的值。  
  
4.  重复步骤 2 和 3，但<xref:System.Windows.Forms.AnchorStyles.Top>和<xref:System.Windows.Forms.AnchorStyles.Bottom>样式。  
  
## <a name="setting-row-and-column-properties"></a>设置行和列属性  
 可以通过设置行和列的单个属性<xref:System.Windows.Forms.TableLayoutPanel.RowStyles%2A>和<xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A>集合。  
  
#### <a name="to-set-row-and-column-properties"></a>若要设置行和列属性  
  
1.  选择<xref:System.Windows.Forms.TableLayoutPanel>控制**Windows 窗体设计器**。  
  
2.  在中**属性**打开窗口<xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A>集合，通过单击省略号 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 按钮下一步**列**条目。  
  
3.  选择第一列和更改的值及其<xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A>属性设置为<xref:System.Windows.Forms.SizeType.AutoSize>。 单击**确定**以接受更改。 请注意，第一列的宽度缩小以适合<xref:System.Windows.Forms.Button>控件。 另请注意，列的宽度不是可调整大小。  
  
4.  在中**属性**窗口中，打开<xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A>集合，然后选择第一列。 将其 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 属性的值更改为 <xref:System.Windows.Forms.SizeType.Percent>。 单击**确定**以接受更改。 重设大小<xref:System.Windows.Forms.TableLayoutPanel>控制转移到更大宽度，并记下的第一列的宽度将展开。 重设大小<xref:System.Windows.Forms.TableLayoutPanel>控制对较小的宽度，并记下的第一列中的按钮可以调整大小以适应单元格。 此外请注意，列的宽度可调整大小。  
  
5.  在中**属性**窗口中，打开<xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A>集合，然后选择所列出的所有列。 值设置每个<xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A>属性设置为<xref:System.Windows.Forms.SizeType.Percent>。 单击**确定**以接受更改。 重复使用<xref:System.Windows.Forms.TableLayoutPanel.RowStyles%2A>集合。  
  
6.  获取其中一个尺寸调整控点的角并调整其大小的宽度和高度<xref:System.Windows.Forms.TableLayoutPanel>控件。 请注意，行和列调整为<xref:System.Windows.Forms.TableLayoutPanel>控件的大小发生更改。 此外请注意，行和列可调整大小与水平和垂直大小调整控点。  
  
## <a name="spanning-rows-and-columns-with-a-control"></a>跨越行和列与控件  
 <xref:System.Windows.Forms.TableLayoutPanel>控件在设计时将多个新属性添加到控件。 这些属性的两个是`RowSpan`和`ColumnSpan`。 这些属性可用于使控件跨多个行或列。  
  
#### <a name="to-span-rows-and-columns-with-a-control"></a>若要跨的行和列与控件  
  
1.  选择<xref:System.Windows.Forms.Button>控件中的第一行和第一列。  
  
2.  在中**属性**的值的 windows 中，更改`ColumnSpan`属性设置为**2**。 请注意，<xref:System.Windows.Forms.Button>控件将填充第一列和第二个列。 此外请注意，添加了额外的行以适应此更改。  
  
3.  重复步骤 2`RowSpan`属性。  
  
## <a name="inserting-controls-by-double-clicking-them-in-the-toolbox"></a>通过在工具箱中双击控件将其插入  
 可通过在 <xref:System.Windows.Forms.TableLayoutPanel> “工具箱” **中双击控件来填充**控件。  
  
#### <a name="to-insert-controls-by-double-clicking-in-the-toolbox"></a>若要通过在工具箱中双击控件将其插入  
  
1.  从 <xref:System.Windows.Forms.TableLayoutPanel> “工具箱” **将** 控件拖到你的窗体上。  
  
2.  在“工具箱” <xref:System.Windows.Forms.Button>**中，双击**控件图标。 请注意，新按钮控件会出现在<xref:System.Windows.Forms.TableLayoutPanel>控件的第一个单元格。  
  
3.  在 **“工具箱”** 中再双击几个控件。 请注意，新控件会相继出现在<xref:System.Windows.Forms.TableLayoutPanel>控件的未占用的单元格。 另请注意，<xref:System.Windows.Forms.TableLayoutPanel>控件扩展以容纳新控件，如果没有打开的单元格都可用。  
  
## <a name="automatic-handling-of-overflows"></a>自动处理溢出  
 当插入控件添加到<xref:System.Windows.Forms.TableLayoutPanel>控件，您可能会用完空单元格的新控件。 <xref:System.Windows.Forms.TableLayoutPanel>控件处理这种情况下自动通过增加单元格的数目。  
  
#### <a name="to-observe-automatic-handling-of-overflows"></a>若要观察溢出的自动处理  
  
1.  如果有中的仍然为空单元格<xref:System.Windows.Forms.TableLayoutPanel>控件，继续插入新<xref:System.Windows.Forms.Button>控件，直至<xref:System.Windows.Forms.TableLayoutPanel>控件已满。  
  
2.  一次<xref:System.Windows.Forms.TableLayoutPanel>控件已满时，双击<xref:System.Windows.Forms.Button>中的图标**工具箱**插入另一个<xref:System.Windows.Forms.Button>控件。 请注意，<xref:System.Windows.Forms.TableLayoutPanel>控件创建新的单元格以容纳新控件。 插入几个控件，并观察调整大小行为。  
  
3.  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的 <xref:System.Windows.Forms.TableLayoutPanel.GrowStyle%2A> 属性值更改为 <xref:System.Windows.Forms.TableLayoutPanelGrowStyle.FixedSize>。 双击<xref:System.Windows.Forms.Button>中的图标**工具箱**插入<xref:System.Windows.Forms.Button>控件，直至<xref:System.Windows.Forms.TableLayoutPanel>控件已满。 双击<xref:System.Windows.Forms.Button>中的图标**工具箱**试。 请注意，收到错误消息**Windows 窗体设计器**通知您不能创建其他行和列。  
  
## <a name="inserting-a-control-by-drawing-its-outline"></a>通过绘制控件轮廓将其插入  
 你可以通过在单元格中绘制控件轮廓将控件插入 <xref:System.Windows.Forms.TableLayoutPanel> 控件并指定其大小。  
  
#### <a name="to-insert-a-control-by-drawing-its-outline"></a>通过绘制控件轮廓插入控件  
  
1.  从 <xref:System.Windows.Forms.TableLayoutPanel> “工具箱” **将** 控件拖到你的窗体上。  
  
2.  在“工具箱” 中，单击 <xref:System.Windows.Forms.Button> 控件图标。 请勿将其拖到窗体上。  
  
3.  将鼠标指针移到 <xref:System.Windows.Forms.TableLayoutPanel> 控件上。 请注意，指针会更改为十字形，同时会附上 <xref:System.Windows.Forms.Button> 控件图标。  
  
4.  单击并按住鼠标按钮。  
  
5.  拖动鼠标指针以绘制 <xref:System.Windows.Forms.Button> 控件的轮廓。 当获得所需大小时，释放鼠标。 请注意，<xref:System.Windows.Forms.Button>在其中绘制控件的轮廓的单元格中创建控件。  
  
## <a name="multiple-controls-within-cells-are-not-permitted"></a>不允许有多个控件中单元格  
 <xref:System.Windows.Forms.TableLayoutPanel>控件可以包含每个单元格的只有一个子控件。  
  
#### <a name="to-demonstrate-that-multiple-controls-within-cells-are-not-permitted"></a>为了演示不允许多个控件中单元格  
  
-   拖动<xref:System.Windows.Forms.Button>控件从**工具箱**到<xref:System.Windows.Forms.TableLayoutPanel>控件并将它放到一个已占用的单元格。 请注意，<xref:System.Windows.Forms.TableLayoutPanel>控件不允许您就可以删除<xref:System.Windows.Forms.Button>到占用的单元格的控件。  
  
## <a name="swapping-controls"></a>交换控件  
 <xref:System.Windows.Forms.TableLayoutPanel>控件使您能够交换占用两个不同的单元格的控件。  
  
#### <a name="to-swap-controls"></a>交换控件  
  
-   拖动其中一个<xref:System.Windows.Forms.Button>中占用的单元格和拖放到另一个占用的单元格上的控件。 请注意，两个控件也会移动从一个单元格将其他。  
  
## <a name="next-steps"></a>后续步骤  
 可使用布局面板和控件的组合实现复杂布局。 有关进一步探索的建议包括：  
  
-   尝试调整大小的一个<xref:System.Windows.Forms.Button>为更大的大小并注意对布局产生效果的控件。  
  
-   粘贴选择内容的多个控件添加到<xref:System.Windows.Forms.TableLayoutPanel>控件并请注意如何插入控件。  
  
-   布局面板可以包含其他布局面板。 试验将 <xref:System.Windows.Forms.TableLayoutPanel> 控件放入现有控件。  
  
-   将 <xref:System.Windows.Forms.TableLayoutPanel> 控件停靠到父窗体。 调整窗体大小，并注意对布局产生的效果。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.FlowLayoutPanel>
- <xref:System.Windows.Forms.TableLayoutPanel>
- [演练：使用 FlowLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [演练：使用对齐线的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
- [Microsoft Windows 用户体验，用户界面开发人员和设计人员的官方指南。Redmond，WA:Microsoft Press，1999年。(USBN:0-7356-0566-1)](https://www.microsoft.com/mspress/southpacific/books/book11588.htm)
- [演练：创建数据输入可调整大小的 Windows 窗体](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/991eahec(v=vs.100))
- [演练：创建可本地化 Windows 窗体](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/7k9fa71y(v=vs.100))
- [有关 TableLayoutPanel 控件的最佳做法](best-practices-for-the-tablelayoutpanel-control.md)
- [AutoSize 属性概述](autosize-property-overview.md)
- [如何：在 Windows 窗体上停靠控件](how-to-dock-controls-on-windows-forms.md)
- [如何：在 Windows 窗体上定位控件](how-to-anchor-controls-on-windows-forms.md)
- [演练：布局 Windows 窗体控件与 Padding、 Margins 和 AutoSize 属性](windows-forms-controls-padding-autosize.md)
