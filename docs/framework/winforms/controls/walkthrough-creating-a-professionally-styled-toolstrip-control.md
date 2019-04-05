---
title: 演练：创建具有专业样式的 ToolStrip 控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolStripProfessionalRenderer class [Windows Forms]
- ToolStripRenderer class [Windows Forms]
- toolbars [Windows Forms], walkthroughs
- ToolStrip control [Windows Forms], creating professionally styled controls
ms.assetid: b52339ae-f1d3-494e-996e-eb455614098a
ms.openlocfilehash: 64624508a50eb6e28337baa1a3600298e2c83fd7
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710740"
---
# <a name="walkthrough-creating-a-professionally-styled-toolstrip-control"></a>演练：创建具有专业样式的 ToolStrip 控件
可以为应用程序的<xref:System.Windows.Forms.ToolStrip>控制专业的外观和行为，通过编写自己的类派生自<xref:System.Windows.Forms.ToolStripProfessionalRenderer>类型。  
  
 本演练演示如何使用<xref:System.Windows.Forms.ToolStrip>控件，创建复合控件类似于**导航窗格**Microsoft Outlook® 提供的。 在本演练阐释了以下任务：  
  
-   创建 Windows 控件库项目。  
  
-   设计 StackView 控件。  
  
-   实现自定义呈现器。  
  
 完成后，必须具有专业外观的 Microsoft Office® XP 控件的可重用的自定义客户端控件。  
  
 要将本主题中的代码作为单个列表进行复制，请参阅[如何：创建具有专业样式的 ToolStrip 控件](how-to-create-a-professionally-styled-toolstrip-control.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，你将需要：  
  
-   若要能够创建和安装 Visual Studio 的计算机上运行 Windows 窗体应用程序项目的足够权限。  
  
## <a name="creating-a-windows-control-library-project"></a>创建 Windows 控件库项目  
 第一步是创建控件库项目。  
  
#### <a name="to-create-the-control-library-project"></a>若要创建的控件库项目  
  
1.  创建一个名为的新 Windows 控件库项目`StackViewLibrary`。  
  
2.  在中**解决方案资源管理器**，通过删除源文件，具体取决于你选择的语言中名为"UserControl1.cs"或"UserControl1.vb"来删除项目的默认控件。  
  
     有关详细信息，请参阅[如何：移除、 删除和排除项](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0ebzhwsk(v=vs.100))。  
  
3.  添加一个新<xref:System.Windows.Forms.UserControl>项**StackViewLibrary**项目。 新的源文件基名称指定为`StackView`。  
  
## <a name="designing-the-stackview-control"></a>设计 StackView 控件  
 `StackView`控件是一个复合控件具有一个子<xref:System.Windows.Forms.ToolStrip>控件。 关于复合控件的详细信息，请参阅[类型的自定义控件](varieties-of-custom-controls.md)。  
  
#### <a name="to-design-the-stackview-control"></a>若要设计 StackView 控件  
  
1.  从**工具箱**，拖动<xref:System.Windows.Forms.ToolStrip>至设计图面上的控件。  
  
2.  在中**属性**窗口中，设置<xref:System.Windows.Forms.ToolStrip>根据下表控件的属性。  
  
    |属性|值|  
    |--------------|-----------|  
    |name|`stackStrip`|  
    |CanOverflow|`false`|  
    |停靠|<xref:System.Windows.Forms.DockStyle.Bottom>|  
    |字体|`Tahoma, 10pt, style=Bold`|  
    |GripStyle|<xref:System.Windows.Forms.ToolStripGripStyle.Hidden>|  
    |LayoutStyle|<xref:System.Windows.Forms.ToolStripLayoutStyle.VerticalStackWithOverflow>|  
    |填充|`0, 7, 0, 0`|  
    |RenderMode|<xref:System.Windows.Forms.ToolStripRenderMode.Professional>|  
  
3.  在 Windows 窗体设计器中，单击<xref:System.Windows.Forms.ToolStrip>控件的**添加**按钮，然后添加<xref:System.Windows.Forms.ToolStripButton>到`stackStrip`控件。  
  
4.  在中**属性**窗口中，设置<xref:System.Windows.Forms.ToolStripButton>根据下表控件的属性。  
  
    |属性|值|  
    |--------------|-----------|  
    |name|`mailStackButton`|  
    |CheckOnClick|true|  
    |CheckState|<xref:System.Windows.Forms.CheckState.Checked>|  
    |DisplayStyle|<xref:System.Windows.Forms.ToolStripItemDisplayStyle.ImageAndText>|  
    |ImageAlign|<xref:System.Drawing.ContentAlignment.MiddleLeft>|  
    |ImageScaling|<xref:System.Windows.Forms.ToolStripItemImageScaling.None>|  
    |ImageTransparentColor|`238, 238, 238`|  
    |边距|`0, 0, 0, 0`|  
    |填充|`3, 3, 3, 3`|  
    |Text|**邮件**|  
    |TextAlign|<xref:System.Drawing.ContentAlignment.MiddleLeft>|  
  
5.  重复步骤 7 的三个<xref:System.Windows.Forms.ToolStripButton>控件。  
  
     命名控件`calendarStackButton`， `contactsStackButton`，和`tasksStackButton`。 设置的值<xref:System.Windows.Forms.Control.Text%2A>属性设置为**日历**，**联系人**，并且**任务**分别。  
  
## <a name="handling-events"></a>处理事件  
 两个事件都必须在做出`StackView`控件正常运行。 处理<xref:System.Windows.Forms.UserControl.Load>事件以正确定位该控件。 处理<xref:System.Windows.Forms.ToolStripItem.Click>为每个事件<xref:System.Windows.Forms.ToolStripButton>以便`StackView`控制状态行为类似于<xref:System.Windows.Forms.RadioButton>控件。  
  
#### <a name="to-handle-events"></a>若要处理的事件  
  
1.  在 Windows 窗体设计器中，选择`StackView`控件。  
  
2.  在“属性”窗口中，单击“事件”。  
  
3.  双击要生成的负载事件`StackView_Load`事件处理程序。  
  
4.  在 `StackView_Load` 事件处理程序中，复制并粘贴以下代码。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#3)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#3)]  
  
5.  在 Windows 窗体设计器中，选择`mailStackButton`控件。  
  
6.  在“属性”窗口中，单击“事件”。  
  
7.  双击 Click 事件。  
  
     Windows 窗体设计器生成`mailStackButton_Click`事件处理程序。  
  
8.  重命名`mailStackButton_Click`事件处理程序`stackButton_Click`。  
  
     有关详细信息，请参阅[重命名代码符号重构](/visualstudio/ide/reference/rename)。  
  
9. 将以下代码插入`stackButton_Click`事件处理程序。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#4)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#4)]  
  
10. 在 Windows 窗体设计器中，选择`calendarStackButton`控件。  
  
11. 在中**属性**窗口中，单击事件设置为`stackButton_Click`事件处理程序。  
  
12. 重复步骤 10 和 11 for`contactsStackButton`和`tasksStackButton`控件。  
  
## <a name="defining-icons"></a>定义图标  
 每个`StackView`按钮都有一个关联的图标。 为方便起见，每个图标表示为 Base64 编码的字符串，其中进行反序列化之前<xref:System.Drawing.Bitmap>从它创建的。 在生产环境中，将位图数据存储为一种资源，并图标将显示在 Windows 窗体设计器。 有关详细信息，请参阅[如何：向 Windows 窗体添加背景图像](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/dff9f95f(v=vs.100))。  
  
#### <a name="to-define-icons"></a>若要定义的图标  
  
1.  在代码编辑器中，将以下代码插入`StackView`类定义。 此代码将初始化为位图<xref:System.Windows.Forms.ToolStripButton>图标。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#2)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#2)]  
  
2.  添加对的调用`InitializeImages`中的方法`StackView`类构造函数。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]  
  
## <a name="implementing-a-custom-renderer"></a>实现自定义呈现器  
 你可以自定义的大多数元素`StackView`控制我实现派生自的类<xref:System.Windows.Forms.ToolStripRenderer>类。 在此过程中，您将实现<xref:System.Windows.Forms.ToolStripProfessionalRenderer>类的自定义手柄，并绘制渐变背景的<xref:System.Windows.Forms.ToolStripButton>控件。  
  
#### <a name="to-implement-a-custom-renderer"></a>若要实现自定义呈现器  
  
1.  将以下代码插入`StackView`控制定义。  
  
     这是用于定义`StackRenderer`类，该类会重写<xref:System.Windows.Forms.ToolStripRenderer.RenderGrip>， <xref:System.Windows.Forms.ToolStripRenderer.RenderToolStripBorder>，和<xref:System.Windows.Forms.ToolStripRenderer.RenderButtonBackground>方法生成的自定义外观。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#10)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#10)]  
  
2.  在中`StackView`控件的构造函数创建的新实例`StackRenderer`类，将分配到此实例`stackStrip`控件的<xref:System.Windows.Forms.ToolStrip.Renderer%2A>属性。  
  
     [!code-csharp[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/CS/StackView.cs#5)]
     [!code-vb[System.Windows.Forms.ToolStrip.StackView#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ToolStrip.StackView/VB/StackView.vb#5)]  
  
## <a name="testing-the-stackview-control"></a>测试 StackView 控件  
 `StackView`控件派生自<xref:System.Windows.Forms.UserControl>类。 因此，可以测试与该控件**UserControl 测试容器**。 有关详细信息，请参阅[如何：测试 UserControl 的运行时行为](how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
#### <a name="to-test-the-stackview-control"></a>若要测试 StackView 控件  
  
1.  按 F5 以生成项目并启动**UserControl 测试容器**。  
  
2.  将指针移动的按钮`StackView`控件，，然后单击按钮以查看其所选状态的外观。  
  
## <a name="next-steps"></a>后续步骤  
 在本演练中，已使用 Office XP 控件的专业的外观来创建可重用的自定义客户端控件。 可以使用<xref:System.Windows.Forms.ToolStrip>实现多种其他用途的控件的系列：  
  
-   创建与控件的快捷菜单<xref:System.Windows.Forms.ContextMenuStrip>。 有关详细信息，请参阅[ContextMenu 组件概述](contextmenu-component-overview-windows-forms.md)。  
  
-   创建一个自动填充的标准菜单的窗体。 有关详细信息，请参见[演练：向窗体提供标准菜单项](walkthrough-providing-standard-menu-items-to-a-form.md)。  
  
-   创建多文档界面 (MDI) 窗体通过停靠<xref:System.Windows.Forms.ToolStrip>控件。 有关详细信息，请参阅[如何：创建具有菜单合并功能和 ToolStrip 控件的 MDI 窗体](how-to-create-an-mdi-form-with-menu-merging-and-toolstrip-controls.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.MenuStrip>
- <xref:System.Windows.Forms.ToolStrip>
- <xref:System.Windows.Forms.StatusStrip>
- [ToolStrip 控件](toolstrip-control-windows-forms.md)
- [如何：向窗体提供标准菜单项](how-to-provide-standard-menu-items-to-a-form.md)
