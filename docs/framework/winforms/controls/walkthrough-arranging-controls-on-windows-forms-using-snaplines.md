---
title: 演练：使用对齐线的 Windows 窗体上排列控件
ms.date: 03/30/2017
helpviewer_keywords:
- controls [Windows Forms], arranging with snaplines
- snaplines [Windows Forms], arranging Windows Forms controls
- SnapLine class [Windows Forms], walkthroughs
- Windows Forms controls, arranging
ms.assetid: d5c9edc7-cf30-4a97-8ebe-201d569340f8
ms.openlocfilehash: f898a15fd2157c625767d53d8b53c5469fb9a957
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703590"
---
# <a name="walkthrough-arranging-controls-on-windows-forms-using-snaplines"></a>演练：使用对齐线的 Windows 窗体上排列控件
在窗体上精确地放置控件对于许多应用程序而言是高优先级。 Windows 窗体设计器提供许多布局工具来实现此目的。 一个最重要的是<xref:System.Windows.Forms.Design.Behavior.SnapLine>功能。  
  
 对齐线显示精确位置与其他控件的控件对齐。 它们还显示控件，指定的 Windows 用户界面指南之间的边距的建议的距离。 有关详细信息，请参阅[用户界面设计和开发](https://go.microsoft.com/FWLink/?LinkId=83878)。  
  
 对齐线轻松地对齐您控件，获得简洁、 专业的外观和行为 （外观和感受）。  
  
 本演练涉及以下任务：  
  
-   创建 Windows 窗体项目  
  
-   间距和对齐控件使用对齐线  
  
-   向窗体和容器的边缘对齐  
  
-   对齐到分组后的控件  
  
-   使用对齐线将控件的大纲显示其大小  
  
-   从工具箱拖动控件时使用对齐线  
  
-   调整控件使用对齐线的大小  
  
-   对齐到控件的文本标签  
  
-   使用对齐线和键盘导航  
  
-   对齐线和布局面板  
  
-   禁用对齐线  
  
 完成后，必须了解所发挥的对齐线功能布局作用。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="creating-the-project"></a>创建项目  
 第一步是创建项目并设置窗体。  
  
#### <a name="to-create-the-project"></a>要创建项目  
  
1.  创建一个名为"SnaplineExample"的基于 Windows 的应用程序项目 (**文件** > **新建** > **项目** >  **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**)。  
  
2.  在窗体设计器中选择窗体。  
  
## <a name="spacing-and-aligning-controls-using-snaplines"></a>间距和对齐控件使用对齐线  
 对齐线使您可以在你的窗体上对齐控件准确而直观的方式。 它们就符合与另一个控件或一组控件的位置附近移动选定的控件时。 你的选择将"对齐"到建议的位置为越过其他控件。  
  
#### <a name="to-arrange-controls-using-snaplines"></a>使用对齐线排列控件  
  
1.  从 <xref:System.Windows.Forms.Button> “工具箱” **将** 控件拖到你的窗体上。  
  
2.  移动<xref:System.Windows.Forms.Button>的窗体右下角的控件。 请注意对齐线显示为<xref:System.Windows.Forms.Button>控件接近下边框和右边框的窗体。 这些对齐线显示在窗体控件的边框之间的建议的距离。  
  
3.  移动<xref:System.Windows.Forms.Button>控件周围的边框窗体和注意对齐线的显示位置。 在完成后，请移动<xref:System.Windows.Forms.Button>窗体的中心附近的控件。  
  
4.  将另一个<xref:System.Windows.Forms.Button>控件从**工具箱**拖动到窗体。  
  
5.  移动第二个<xref:System.Windows.Forms.Button>控制直到几乎与第一个级别。 请注意出现在这两个按钮的文本基线对齐线，并记下要移动的控件对齐到的位置，则完全与另一个控件的级别。  
  
6.  移动第二个<xref:System.Windows.Forms.Button>控件，直到它位于正上方第一个。 请注意对齐线沿两个按钮的左侧和右侧边缘显示，请注意，该控件要移动到完全对应与另一个控件的位置的快照。  
  
7.  选择其中一个<xref:System.Windows.Forms.Button>控制并将其移近另一个，直到它们几乎触摸。 请注意它们之间出现对齐线。 此距离是控件的边框之间的建议的距离。 另请注意要移动的控件对齐到此位置。  
  
8.  将两个<xref:System.Windows.Forms.Panel>控件从**工具箱**拖动到窗体。  
  
9. 将其中一个移动<xref:System.Windows.Forms.Panel>控件，直到它是几乎与第一个级别。 请注意这两个控件边缘和下边缘沿显示并记下要移动的控件对齐到的位置，则完全级别与另一个控件的对齐线。  
  
## <a name="aligning-to-form-and-container-margins"></a>向窗体和容器的边缘对齐  
 对齐线帮助您将控件与窗体和容器边缘对齐以一致的方式。  
  
#### <a name="to-align-controls-to-form-and-container-margins"></a>若要将控件添加到窗体和容器边缘对齐  
  
1.  选择其中一个<xref:System.Windows.Forms.Button>控制并将其移近右边框的窗体中，直到显示对齐线。 从右边框对齐线的距离是控件的总和<xref:System.Windows.Forms.Control.Margin%2A>属性和窗体的<xref:System.Windows.Forms.Control.Padding%2A>属性值。  
  
> [!NOTE]
>  如果窗体的<xref:System.Windows.Forms.Control.Padding%2A>属性设置为 0,0,0,0、 Windows 窗体设计器将为窗体指定隐藏<xref:System.Windows.Forms.Control.Padding%2A>9,9,9,9 的值。 若要重写此行为，分配 0,0,0,0 以外的值。  
  
1.  更改的值<xref:System.Windows.Forms.Button>控件的<xref:System.Windows.Forms.Control.Margin%2A>展开属性<xref:System.Windows.Forms.Control.Margin%2A>中的条目**属性**窗口和设置<xref:System.Windows.Forms.Padding.All%2A>属性设为 0。 有关详细信息，请参阅[演练：对 Windows 窗体控件使用 Padding、 Margins 和 AutoSize 属性](windows-forms-controls-padding-autosize.md)。  
  
2.  移动<xref:System.Windows.Forms.Button>接近直到对齐线显示在窗体的右边框的控件。 窗体的值现在提供此距离<xref:System.Windows.Forms.Control.Padding%2A>属性。  
  
3.  从 <xref:System.Windows.Forms.GroupBox> “工具箱” **将** 控件拖到你的窗体上。  
  
4.  更改的值<xref:System.Windows.Forms.GroupBox>控件的<xref:System.Windows.Forms.Control.Padding%2A>展开属性<xref:System.Windows.Forms.Control.Padding%2A>中的条目**属性**窗口和设置<xref:System.Windows.Forms.Padding.All%2A>属性设置为 10。  
  
5.  拖动<xref:System.Windows.Forms.Button>控件从**工具箱**到<xref:System.Windows.Forms.GroupBox>控件。  
  
6.  移动<xref:System.Windows.Forms.Button>控件的右边框的接近<xref:System.Windows.Forms.GroupBox>控件，直到出现对齐线。 移动<xref:System.Windows.Forms.Button>控件中<xref:System.Windows.Forms.GroupBox>控件并记下对齐线的显示位置。  
  
## <a name="aligning-to-grouped-controls"></a>对齐到分组后的控件  
 您可以使用对齐线对齐分组后的控件一样，很好地控制内<xref:System.Windows.Forms.GroupBox>控件。  
  
#### <a name="to-align-to-grouped-controls"></a>对齐到一组控件  
  
1.  选择两个窗体上的控件。 移动所选内容并记下你的选择和其他控件之间显示的对齐线。  
  
2.  从 <xref:System.Windows.Forms.GroupBox> “工具箱” **将** 控件拖到你的窗体上。  
  
3.  拖动<xref:System.Windows.Forms.Button>控件从**工具箱**到<xref:System.Windows.Forms.GroupBox>控件。  
  
4.  选择其中一个<xref:System.Windows.Forms.Button>控制并将其四处移动<xref:System.Windows.Forms.GroupBox>控件。 请注意显示的边缘的对齐线<xref:System.Windows.Forms.GroupBox>控件。 另请注意显示的边缘的对齐线<xref:System.Windows.Forms.Button>包含由控件<xref:System.Windows.Forms.GroupBox>控件。 容器控件的子级的控件还支持对齐线。  
  
## <a name="using-snaplines-to-place-a-control-by-outlining-its-size"></a>使用对齐线将控件的大纲显示其大小  
 对齐线帮助您对齐控件时，首先将它们放在窗体上。  
  
#### <a name="to-use-snaplines-to-place-a-control-by-outlining-its-size"></a>若要使用对齐线将控件置于大纲显示其大小  
  
1.  在“工具箱” 中，单击 <xref:System.Windows.Forms.Button> 控件图标。 请勿将其拖到窗体上。  
  
2.  将鼠标指针移动窗体的设计图面。 请注意，指针会更改为十字形，同时会附上 <xref:System.Windows.Forms.Button> 控件图标。 另请注意显示建议的对齐的位置的对齐线<xref:System.Windows.Forms.Button>控件。  
  
3.  单击并按住鼠标按钮。  
  
4.  拖动鼠标指针在窗体。 请注意，绘制轮廓，指示的位置和控件的大小。  
  
5.  拖动指针，直到它与另一个控件在窗体上对齐。 请注意，对齐线将出现以指示对齐方式。  
  
6.  释放鼠标按钮。 在的位置和大小由概要中创建控件。  
  
## <a name="using-snaplines-when-dragging-a-control-from-the-toolbox"></a>从工具箱拖动控件时使用对齐线  
 对齐线帮助您对齐控件时将它们从**工具箱**拖动到窗体。  
  
#### <a name="to-use-snaplines-when-dragging-a-control-from-the-toolbox"></a>若要从工具箱拖动控件时使用对齐线  
  
1.  拖动<xref:System.Windows.Forms.Button>控件从**工具箱**拖动到窗体，但不会释放鼠标按钮。  
  
2.  将鼠标指针移动窗体的设计图面。 请注意，指针更改以指示在其位置的新<xref:System.Windows.Forms.Button>将创建控件。  
  
3.  拖动鼠标指针在窗体。 请注意显示建议的对齐的位置的对齐线<xref:System.Windows.Forms.Button>控件。 查找与其他控件对齐位置。  
  
4.  释放鼠标按钮。 在指示对齐线的位置创建控件。  
  
## <a name="resizing-controls-using-snaplines"></a>调整控件使用对齐线的大小  
 对齐线帮助您对齐控件调整其大小。  
  
#### <a name="to-resize-a-control-using-snaplines"></a>调整控件使用对齐线的大小  
  
1.  从 <xref:System.Windows.Forms.Button> “工具箱” **将** 控件拖到你的窗体上。  
  
2.  重设大小<xref:System.Windows.Forms.Button>抓住角大小调整控点和拖动某个控件。 有关详细信息，请参阅[如何：调整 Windows 窗体上的控件的大小](how-to-resize-controls-on-windows-forms.md)。  
  
3.  拖动调整大小控点，直到一位<xref:System.Windows.Forms.Button>与其他控件对齐控件的边框。 请注意，显示对齐线。 另请注意，调整大小控点会对齐到对齐线指示的位置。  
  
4.  重设大小<xref:System.Windows.Forms.Button>控制在不同的方向和对齐到不同的控件的大小调整句柄。 请注意如何对齐线显示在不同的方向，以指示对齐方式。  
  
## <a name="aligning-a-label-to-a-controls-text"></a>对齐到控件的文本标签  
 某些控件提供了用于对齐到显示的文本的其他控件的对齐线。  
  
#### <a name="to-align-a-label-to-a-controls-text"></a>若要对齐到控件的文本标签  
  
1.  从 <xref:System.Windows.Forms.TextBox> “工具箱” **将** 控件拖到你的窗体上。 当 drop<xref:System.Windows.Forms.TextBox>拖到窗体控件，单击智能标记标志符号，选择**将文本设置为 textBox1**选项。 有关详细信息，请参阅[演练：在 Windows 上使用智能标记执行常见任务窗体控件](performing-common-tasks-using-smart-tags-on-wf-controls.md)。  
  
2.  从 <xref:System.Windows.Forms.Label> “工具箱” **将** 控件拖到你的窗体上。  
  
3.  将 <xref:System.Windows.Forms.Label> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性值更改为 `true`。 请注意该控件的边框调整为适合的显示文本。  
  
4.  移动<xref:System.Windows.Forms.Label>控件的左侧<xref:System.Windows.Forms.TextBox>控件，以便使用的下边缘对齐<xref:System.Windows.Forms.TextBox>控件。 请注意两个控件的底部边缘的对齐线。  
  
5.  移动<xref:System.Windows.Forms.Label>控制略微向上，直到<xref:System.Windows.Forms.Label>文本和<xref:System.Windows.Forms.TextBox>对齐文本。 请注意以不同的方式应用了样式显示，该值指示当对齐这两个控件的文本字段的对齐线。  
  
## <a name="using-snaplines-with-keyboard-navigation"></a>使用对齐线和键盘导航  
 对齐线帮助您对齐控件时排列它们使用键盘上的箭头键。  
  
#### <a name="to-use-snaplines-with-keyboard-navigation"></a>若要使用的键盘导航使用对齐线  
  
1.  从 <xref:System.Windows.Forms.Button> “工具箱” **将** 控件拖到你的窗体上。 将其放置在窗体的左上角。  
  
2.  按 CTRL + 向下箭头。 请注意，控件将向下移动窗体的第一个可用的水平对齐位置。  
  
3.  按 CTRL + 向下箭头，直到该控件达到窗体的底部。 注意，它占用的是因为它将下移窗体的位置。  
  
4.  按 CTRL + 向右键。 请注意，该控件在窗体移动到第一个可用的垂直对齐位置。  
  
5.  该控件在窗体左侧直到按 CTRL + 向右键。 注意，它占用的是在窗体中移动的位置。  
  
6.  使用箭头键的组合中移动窗体控件。 请注意控件所占据的位置并附带有它们的对齐线。  
  
7.  按 SHIFT + 任意箭头键来调整大小<xref:System.Windows.Forms.Button>控件按 1 个像素的增量。  
  
8.  按 CTRL + SHIFT + 任意箭头键来调整大小<xref:System.Windows.Forms.Button>控件中对齐线的增量。  
  
## <a name="snaplines-and-layout-panels"></a>对齐线和布局面板  
 在布局面板内禁用对齐线。  
  
#### <a name="to-selectively-disable-snaplines"></a>若要有选择性地禁用对齐线  
  
1.  从 <xref:System.Windows.Forms.TableLayoutPanel> “工具箱” **将** 控件拖到你的窗体上。  
  
2.  在“工具箱” <xref:System.Windows.Forms.Button>**中，双击**控件图标。 请注意，新按钮控件会出现在<xref:System.Windows.Forms.TableLayoutPanel>控件的第一个单元格。  
  
3.  双击<xref:System.Windows.Forms.Button>中的控件图标**工具箱**两次。 这将使中的一个空单元格<xref:System.Windows.Forms.TableLayoutPanel>控件。  
  
4.  拖动<xref:System.Windows.Forms.Button>控件从**工具箱**到的空单元格中<xref:System.Windows.Forms.TableLayoutPanel>控件。 请注意，会出现不对齐线。  
  
5.  拖动<xref:System.Windows.Forms.Button>控制共<xref:System.Windows.Forms.TableLayoutPanel>控件并将其四处移动<xref:System.Windows.Forms.TableLayoutPanel>控件。 请注意，对齐线会再次出现。  
  
## <a name="disabling-snaplines"></a>禁用对齐线  
 默认情况下启用对齐线。 您可以有选择地，禁用对齐线或您可以在设计环境中禁用它们。  
  
#### <a name="to-selectively-disable-snaplines"></a>若要有选择性地禁用对齐线  
  
-   按 ALT 键和而移动一个窗体控件。  
  
     请注意，没有对齐线显示该控件不会按任何可能的对齐位置。  
  
#### <a name="to-disable-snaplines-in-the-design-environment"></a>若要禁用设计环境中的对齐线  
  
1.  从**工具**菜单中，打开**选项**对话框。 打开 Windows 窗体设计器对话框。 有关详细信息，请参阅[选项对话框常规 Windows 窗体设计器](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/5aazxs78(v=vs.100))。  
  
2.  选择**常规**节点。 在中**布局模式下**部分中，更改从所选**对齐线**到**网格线对齐**。  
  
3.  单击确定以应用设置。  
  
4.  选择你的窗体上的控件，并移动其他控件。 请注意，不会显示对齐线。  
  
## <a name="next-steps"></a>后续步骤  
 对齐线提供了直观的窗体上的控件对齐方式。 有关进一步探索的建议包括：  
  
-   请尝试嵌套<xref:System.Windows.Forms.GroupBox>在另一个控件<xref:System.Windows.Forms.GroupBox>控件。 位置<xref:System.Windows.Forms.Button>内的子控件<xref:System.Windows.Forms.GroupBox>控件，并在父级内的另一个<xref:System.Windows.Forms.GroupBox>控件。 移动<xref:System.Windows.Forms.Button>控件即可看到如何对齐线跨容器边界。  
  
-   创建的列<xref:System.Windows.Forms.TextBox>控件与相应的列的<xref:System.Windows.Forms.Label>控件。 设置的值<xref:System.Windows.Forms.Label>控件的<xref:System.Windows.Forms.Control.AutoSize%2A>属性设置为`true`。 使用对齐线将移动<xref:System.Windows.Forms.Label>控制使其显示的文本与中的文本对齐<xref:System.Windows.Forms.TextBox>控件。  
  
 有关 Windows 用户界面设计的信息，请参阅此书*Microsoft Windows 用户体验、 用户界面开发人员和设计人员的官方指南*Redmond，WA:Microsoft Press，1999年。 (USBN:0-7356-0566-1).  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Design.Behavior.SnapLine>
- [演练：使用 FlowLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [演练：使用 TableLayoutPanel 的 Windows 窗体上排列控件](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [演练：布局 Windows 窗体控件与 Padding、 Margins 和 AutoSize 属性](windows-forms-controls-padding-autosize.md)
- [在 Windows 窗体上排列控件](arranging-controls-on-windows-forms.md)
