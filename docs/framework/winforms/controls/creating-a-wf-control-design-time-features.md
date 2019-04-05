---
title: 演练：创建利用 Visual Studio 设计时功能的 Windows 窗体控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms controls, creating
- design-time functionality [Windows Forms], Windows Forms
- DocumentDesigner class [Windows Forms]
- walkthroughs [Windows Forms], controls
ms.assetid: 6f487c59-cb38-4afa-ad2e-95edacb1d626
ms.openlocfilehash: 70cd08a9d7d03cec4e946d2acb806dbecfe774f7
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724613"
---
# <a name="walkthrough-creating-a-windows-forms-control-that-takes-advantage-of-visual-studio-design-time-features"></a>演练：创建利用 Visual Studio 设计时功能的 Windows 窗体控件

可以通过创作的关联的自定义设计器增强自定义控件的设计时体验。

本演练演示如何创建自定义控件的自定义设计器。 将实现`MarqueeControl`类型和关联的设计器类，名为`MarqueeControlRootDesigner`。

`MarqueeControl`类型实现类似于影院字幕，与经过动画处理的灯光和闪烁文本显示。

此控件的设计器与要提供自定义设计时体验的设计环境进行交互。 使用自定义设计器，来组合自定义`MarqueeControl`实现动画的灯光和闪烁文本以多种组合。 可以使用类似于任何其他 Windows 窗体控件在窗体上组合的控件。

本演练涉及以下任务：

- 创建项目

- 创建控件库项目

- 引用自定义控件项目

- 定义自定义控件和其自定义设计器

- 创建自定义控件的实例

- 设置设计时调试项目

- 实现自定义控件

- 创建子控件的自定义控件

- 创建放子控件

- 创建自定义设计器以隐藏和筛选器属性

- 处理组件更改

- 将设计器谓词添加到自定义设计器

- 创建自定义 UITypeEditor

- 在设计器中测试自定义控件

完成后，自定义控件看起来类似于以下内容：

![可能的 MarqueeControl 排列](./media/demomarqueecontrol.gif "器")

有关完整代码列表，请参阅[如何：创建利用设计时功能的 Windows 窗体控件](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。

## <a name="prerequisites"></a>系统必备

若要完成本演练，你将需要：

- 若要能够创建和安装 Visual Studio 的计算机上运行 Windows 窗体应用程序项目的足够权限。

## <a name="creating-the-project"></a>创建项目

第一步是创建应用程序项目。 将使用此项目以生成承载自定义控件的应用程序。

### <a name="to-create-the-project"></a>要创建项目

- 创建一个名为"MarqueeControlTest"的 Windows 窗体应用程序项目 (**文件** > **新建** > **项目** >  **Visual C#** 或**Visual Basic** > **经典桌面** > **Windows 窗体应用程序**)。

## <a name="creating-a-control-library-project"></a>创建控件库项目

下一步是创建控件库项目。 您将创建一个新的自定义控件和其相应的自定义设计器。

### <a name="to-create-the-control-library-project"></a>若要创建的控件库项目

1. 向解决方案添加 Windows 窗体控件库项目。 命名项目"MarqueeControlLibrary。"

2. 使用**解决方案资源管理器**，通过删除源文件，具体取决于你选择的语言中名为"UserControl1.cs"或"UserControl1.vb"来删除项目的默认控件。 有关详细信息，请参阅[如何：移除、 删除和排除项](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/0ebzhwsk(v=vs.100))。

3. 添加一个新<xref:System.Windows.Forms.UserControl>项`MarqueeControlLibrary`项目。 新的源文件基名称指定为"MarqueeControl。"

4. 使用**解决方案资源管理器**，创建一个新文件夹中的`MarqueeControlLibrary`项目。 有关详细信息，请参阅[如何：添加新项目项](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/w0572c5b(v=vs.100))。 将新文件夹命名为"设计"。

5. 右键单击**设计**文件夹并添加新类。 源文件基名称指定为"MarqueeControlRootDesigner。"

6. 将需要使用来自 System.Design 程序集类型，因此添加到此引用`MarqueeControlLibrary`项目。

    > [!NOTE]
    > 若要使用 System.Design 程序集，你的项目必须面向.NET Framework 中，而非.NET Framework 客户端配置文件的完整版本。 若要更改目标框架，请参阅[如何：面向 .NET Framework 的某个版本](/visualstudio/ide/how-to-target-a-version-of-the-dotnet-framework)。

## <a name="referencing-the-custom-control-project"></a>引用自定义控件项目

将使用`MarqueeControlTest`项目，以测试自定义控件。 测试项目就会变得注意的自定义控件添加到项目引用`MarqueeControlLibrary`程序集。

### <a name="to-reference-the-custom-control-project"></a>若要引用自定义控件项目

- 在中`MarqueeControlTest`项目中，添加到项目引用`MarqueeControlLibrary`程序集。 请务必使用**项目**选项卡**添加引用**而不是引用对话框的`MarqueeControlLibrary`直接的程序集。

## <a name="defining-a-custom-control-and-its-custom-designer"></a>定义自定义控件和其自定义设计器
 自定义控件都派生自<xref:System.Windows.Forms.UserControl>类。 这允许你控制用于包含其他控件，并为您的控件提供了大量的默认功能。

 自定义控件将具有关联的自定义设计器。 这允许您创建专门用于自定义控件量身定制的独特的设计体验。

 将控件与设计器关联使用<xref:System.ComponentModel.DesignerAttribute>类。 由于正在开发的自定义控件的整个设计时行为，自定义设计器将实现<xref:System.ComponentModel.Design.IRootDesigner>接口。

### <a name="to-define-a-custom-control-and-its-custom-designer"></a>若要定义自定义控件和其自定义设计器

1. 打开`MarqueeControl`中的源文件**代码编辑器**。 在该文件的顶部，导入以下命名空间：

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#220](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#220)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#220](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#220)]

2. 添加<xref:System.ComponentModel.DesignerAttribute>到`MarqueeControl`类声明。 这将与设计器关联的自定义控件。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#240](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#240)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#240](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#240)]

3. 打开`MarqueeControlRootDesigner`中的源文件**代码编辑器**。 在该文件的顶部，导入以下命名空间：

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#520](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#520)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#520](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#520)]

4. 更改的声明`MarqueeControlRootDesigner`从中继承<xref:System.Windows.Forms.Design.DocumentDesigner>类。 将应用<xref:System.ComponentModel.ToolboxItemFilterAttribute>以指定与设计器交互**工具箱**。

     **请注意**的定义`MarqueeControlRootDesigner`类将其括在命名空间名为"MarqueeControlLibrary.Design。" 此声明会放在设计器中的特殊命名空间保留为与设计相关的类型。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#530](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#530)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#530](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#530)]

5. 定义的构造函数`MarqueeControlRootDesigner`类。 插入<xref:System.Diagnostics.Trace.WriteLine%2A>构造函数主体中的语句。 这将是用于调试目的。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#540](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#540)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#540](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#540)]

## <a name="creating-an-instance-of-your-custom-control"></a>创建自定义控件的实例
 若要观察您的控件的自定义设计时行为，将放置在窗体上控件的实例`MarqueeControlTest`项目。

### <a name="to-create-an-instance-of-your-custom-control"></a>若要创建自定义控件的实例

1. 添加一个新<xref:System.Windows.Forms.UserControl>项`MarqueeControlTest`项目。 新的源文件基名称指定为"器。"

2. 打开`DemoMarqueeControl`文件中**代码编辑器**。 该文件顶部，导入`MarqueeControlLibrary`命名空间：

```vb
Imports MarqueeControlLibrary
```

```csharp
using MarqueeControlLibrary;
```

1. 更改的声明`DemoMarqueeControl`从中继承`MarqueeControl`类。

2. 生成项目。

3. 在 Windows 窗体设计器中打开 `Form1`。

4. 查找**MarqueeControlTest 组件**选项卡**工具箱**并将其打开。 拖动`DemoMarqueeControl`从**工具箱**拖动到窗体。

5. 生成项目。

## <a name="setting-up-the-project-for-design-time-debugging"></a>设置设计时调试项目

当你正在开发的自定义设计时体验时，将需要调试控件和组件。 没有将项目设置以允许在设计时调试的简单方法。 有关详细信息，请参见[演练：在设计时调试自定义 Windows 窗体的控件](walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)。

### <a name="to-set-up-the-project-for-design-time-debugging"></a>若要设置项目以便进行设计时调试

1. 右键单击`MarqueeControlLibrary`项目，然后选择**属性**。

2. 在"MarqueeControlLibrary 属性页"对话框中，选择**调试**页。

3. 在中**启动操作**部分中，选择**启动外部程序**。 你将调试的单独实例的 Visual Studio 中，因此请单击省略号 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 按钮以浏览 Visual Studio IDE。 可执行文件名称为 devenv.exe，并且如果已安装到默认位置，其路径为 %programfiles%\Microsoft Visual Studio 9.0\Common7\IDE\devenv.exe。

4. 单击确定以关闭对话框。

5. 右键单击`MarqueeControlLibrary`项目，然后选择"设为启动项目"来启用此调试配置。

## <a name="checkpoint"></a>检查点

现在您就可以调试自定义控件的设计时行为。 一旦您已确定正确设置调试环境，您将测试自定义控件和自定义设计器之间的关联。

### <a name="to-test-the-debugging-environment-and-the-designer-association"></a>若要测试的调试环境和设计器关联

1. 打开`MarqueeControlRootDesigner`中的源文件**代码编辑器**并将断点放置在<xref:System.Diagnostics.Trace.WriteLine%2A>语句。

2. 按 F5 启动调试会话。 请注意，创建 Visual Studio 的新实例。

3. 在 Visual Studio 的新实例中，打开"MarqueeControlTest"解决方案。 您可以轻松地找到解决方案，通过选择**最近使用的项目**从**文件**菜单。 将列出"MarqueeControlTest.sln"解决方案文件，如最近使用的文件。

4. 打开`DemoMarqueeControl`在设计器中。 请注意，Visual Studio 的调试实例获取焦点执行在断点处停止。 按 f5 键继续调试会话。

此时，所有内容已准备就绪，以便开发和调试自定义控件和其关联的自定义设计器。 本演练的其余部分将精力集中于实现的控件和设计器功能的详细信息。

## <a name="implementing-your-custom-control"></a>实现自定义控件

`MarqueeControl`是<xref:System.Windows.Forms.UserControl>极少量的自定义。 它公开两个方法： `Start`，从而启动字幕动画和`Stop`，后者会停止动画。 因为`MarqueeControl`包含实现的子控件`IMarqueeWidget`接口，`Start`并`Stop`枚举每个子控件和调用`StartMarquee`和`StopMarquee`方法，分别在每个子控件它实现`IMarqueeWidget`。

外观`MarqueeBorder`并`MarqueeText`控件是依赖于布局，因此`MarqueeControl`重写<xref:System.Windows.Forms.Control.OnLayout%2A>方法并调用<xref:System.Windows.Forms.Control.PerformLayout%2A>上此类型的子控件。

这是程度`MarqueeControl`自定义项。 运行时功能由实现`MarqueeBorder`并`MarqueeText`控件和设计时功能由实现`MarqueeBorderDesigner`和`MarqueeControlRootDesigner`类。

### <a name="to-implement-your-custom-control"></a>若要实现自定义控件

1. 打开`MarqueeControl`中的源文件**代码编辑器**。 实现`Start`和`Stop`方法。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#260](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#260)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#260](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#260)]

2. 重写 <xref:System.Windows.Forms.Control.OnLayout%2A> 方法。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#270](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#270)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#270](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#270)]

## <a name="creating-a-child-control-for-your-custom-control"></a>创建子控件的自定义控件

`MarqueeControl`将承载的子控件的两种类型：`MarqueeBorder`控件和`MarqueeText`控件。

- `MarqueeBorder`：此控件绘制"lights"其边缘周围的边框。 灯光闪烁在序列中，使其显示以围绕着边框移动。 由一个名为属性控制在其灯闪烁的速度`UpdatePeriod`。 多个其他自定义属性确定控件的外观的其他方面。 两种方法，称为`StartMarquee`和`StopMarquee`，控制动画启动和停止时。

- `MarqueeText`：此控件将绘制一个闪烁的字符串。 像`MarqueeBorder`控件中，文本会闪烁的速度由控制`UpdatePeriod`属性。 `MarqueeText`控件还具有`StartMarquee`并`StopMarquee`方法与`MarqueeBorder`控件。

在设计时`MarqueeControlRootDesigner`允许这些两个控件的类型添加到`MarqueeControl`的任意组合。

两个控件的常见功能包含在一个名为`IMarqueeWidget`。 这允许`MarqueeControl`发现任何字幕相关子控件，并为它们提供特殊处理。

若要实现定期动画功能，您将使用<xref:System.ComponentModel.BackgroundWorker>中的对象<xref:System.ComponentModel?displayProperty=nameWithType>命名空间。 可以使用<xref:System.Windows.Forms.Timer>对象，但是当许多`IMarqueeWidget`对象是否存在后，在单个 UI 线程可能无法及时了解动画。

### <a name="to-create-a-child-control-for-your-custom-control"></a>若要创建自定义控件的子控件

1. 添加到一个新类项`MarqueeControlLibrary`项目。 新的源文件基名称指定为"IMarqueeWidget。"

2. 打开`IMarqueeWidget`中的源文件**代码编辑器**并将更改从声明`class`到`interface`:

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#2)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#2)]

3. 将以下代码添加到`IMarqueeWidget`接口，以公开两个方法和操作字幕动画的属性：

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#3)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#3)]

4. 添加一个新**自定义控件**项`MarqueeControlLibrary`项目。 新的源文件基名称指定为"显示"。

5. 拖动<xref:System.ComponentModel.BackgroundWorker>组件从**工具箱**拖动到你`MarqueeText`控件。 此组件将允许`MarqueeText`控件以异步方式将自行更新。

6. 在属性窗口中设置<xref:System.ComponentModel.BackgroundWorker>组件的`WorkerReportsProgress`并<xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A>属性设置为`true`。 这些设置允许<xref:System.ComponentModel.BackgroundWorker>组件来定期引发<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件并取消异步更新。 有关详细信息，请参阅[BackgroundWorker 组件](backgroundworker-component.md)。

7. 打开`MarqueeText`中的源文件**代码编辑器**。 在该文件的顶部，导入以下命名空间：

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#120](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#120)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#120](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#120)]

8. 更改的声明`MarqueeText`继承自<xref:System.Windows.Forms.Label>以及实现`IMarqueeWidget`接口：

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#130](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#130)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#130](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#130)]

9. 声明与公开的属性相对应的实例变量，并在构造函数中对其进行初始化。 `isLit`字段确定是否要在指定的颜色绘制文本`LightColor`属性。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#140](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#140)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#140](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#140)]

10. 实现 `IMarqueeWidget` 接口。

    `StartMarquee`并`StopMarquee`方法调用<xref:System.ComponentModel.BackgroundWorker>组件的<xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A>和<xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A>方法来启动和停止动画。

    <xref:System.ComponentModel.CategoryAttribute.Category%2A>并<xref:System.ComponentModel.BrowsableAttribute.Browsable%2A>特性应用于`UpdatePeriod`属性使它出现在名为"Marquee。"属性窗口的自定义部分

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#150](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#150)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#150](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#150)]

11. 实现属性访问器。 您将会向客户端的两个属性：`LightColor`和`DarkColor`。 <xref:System.ComponentModel.CategoryAttribute.Category%2A>和<xref:System.ComponentModel.BrowsableAttribute.Browsable%2A>属性应用于这些属性，因此属性将出现在名为"Marquee。"属性窗口的自定义部分

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#160](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#160)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#160](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#160)]

12. 实现的处理程序<xref:System.ComponentModel.BackgroundWorker>组件的<xref:System.ComponentModel.BackgroundWorker.DoWork>和<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件。

    <xref:System.ComponentModel.BackgroundWorker.DoWork>事件处理程序指定的毫秒数将休眠`UpdatePeriod`然后引发<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件，直到你的代码通过调用停止动画<xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A>。

    <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件处理程序切换其浅色和深色状态，以提供闪烁外观之间的文本。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#180](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#180)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#180](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#180)]

13. 重写<xref:System.Windows.Forms.Control.OnPaint%2A>方法，以使动画。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#170](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#170)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#170](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#170)]

14. 按 F6 生成解决方案。

## <a name="create-the-marqueeborder-child-control"></a>创建放子控件

`MarqueeBorder`控件是比要稍微复杂`MarqueeText`控件。 它具有更多属性和在动画<xref:System.Windows.Forms.Control.OnPaint%2A>方法是更为复杂。 从原理上讲，它是非常类似于`MarqueeText`控件。

因为`MarqueeBorder`控件可以有子控件，它必须要注意<xref:System.Windows.Forms.Control.Layout>事件。

### <a name="to-create-the-marqueeborder-control"></a>若要创建放控件

1. 添加一个新**自定义控件**项`MarqueeControlLibrary`项目。 新的源文件基名称指定为"放"。

2. 拖动<xref:System.ComponentModel.BackgroundWorker>组件从**工具箱**拖动到你`MarqueeBorder`控件。 此组件将允许`MarqueeBorder`控件以异步方式将自行更新。

3. 在属性窗口中设置<xref:System.ComponentModel.BackgroundWorker>组件的`WorkerReportsProgress`并<xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A>属性设置为`true`。 这些设置允许<xref:System.ComponentModel.BackgroundWorker>组件来定期引发<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件并取消异步更新。 有关详细信息，请参阅[BackgroundWorker 组件](backgroundworker-component.md)。

4. 在属性窗口中，单击事件按钮。 附加处理程序<xref:System.ComponentModel.BackgroundWorker.DoWork>和<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件。

5. 打开`MarqueeBorder`中的源文件**代码编辑器**。 在该文件的顶部，导入以下命名空间：

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#20)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#20)]

6. 更改的声明`MarqueeBorder`继承自<xref:System.Windows.Forms.Panel>以及实现`IMarqueeWidget`接口。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#30)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#30)]

7. 声明用于管理的两个枚举`MarqueeBorder`控件的状态： `MarqueeSpinDirection`，用于确定在其中指示灯"旋转"周围边框的方向和`MarqueeLightShape`，用于确定形状的灯 （方形或循环）。 将这些声明`MarqueeBorder`类声明。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#97](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#97)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#97](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#97)]

8. 声明与公开的属性相对应的实例变量，并在构造函数中对其进行初始化。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#40](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#40)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#40](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#40)]

9. 实现 `IMarqueeWidget` 接口。

    `StartMarquee`并`StopMarquee`方法调用<xref:System.ComponentModel.BackgroundWorker>组件的<xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A>和<xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A>方法来启动和停止动画。

    因为`MarqueeBorder`控件可以包含子控件`StartMarquee`方法枚举所有子控件并调用`StartMarquee`上即可实现`IMarqueeWidget`。 `StopMarquee`方法具有一个类似的实现。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#50](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#50)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#50](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#50)]

10. 实现属性访问器。 `MarqueeBorder`控件具有多个属性用于控制其外观。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#60](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#60)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#60](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#60)]

11. 实现的处理程序<xref:System.ComponentModel.BackgroundWorker>组件的<xref:System.ComponentModel.BackgroundWorker.DoWork>和<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件。

    <xref:System.ComponentModel.BackgroundWorker.DoWork>事件处理程序指定的毫秒数将休眠`UpdatePeriod`然后引发<xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件，直到你的代码通过调用停止动画<xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A>。

    <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>事件处理程序递增的位置的"基"浅，从其确定其他系统正常运行的浅/深状态，并调用<xref:System.Windows.Forms.Control.Refresh%2A>方法可使控件重绘其自身。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#90](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#90)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#90](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#90)]

12. 实现帮助器方法`IsLit`和`DrawLight`。

    `IsLit`方法确定给定位置处的光的颜色。 中指定的颜色绘制"点亮"的灯`LightColor`中指定的颜色绘制属性，以及那些"深色"`DarkColor`属性。

    `DrawLight`方法绘制使用适当的颜色、 形状和位置的灯。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#80](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#80)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#80](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#80)]

13. 重写<xref:System.Windows.Forms.Control.OnLayout%2A>和<xref:System.Windows.Forms.Control.OnPaint%2A>方法。

    <xref:System.Windows.Forms.Control.OnPaint%2A>方法绘制的边缘沿灯`MarqueeBorder`控件。

    因为<xref:System.Windows.Forms.Control.OnPaint%2A>方法取决于的维度`MarqueeBorder`控件，您需要布局发生更改时调用它。 若要实现此目的，重写<xref:System.Windows.Forms.Control.OnLayout%2A>，并调用<xref:System.Windows.Forms.Control.Refresh%2A>。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#70](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#70)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#70](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#70)]

## <a name="creating-a-custom-designer-to-shadow-and-filter-properties"></a>创建自定义设计器以隐藏和筛选器属性

`MarqueeControlRootDesigner`类提供的根设计器的实现。 除了此设计器中，这对`MarqueeControl`，你将需要专门与相关联的自定义设计`MarqueeBorder`控件。 此设计器提供了相应的自定义根设计器的上下文中的自定义行为。

具体而言，`MarqueeBorderDesigner`将"隐藏"，并筛选某些属性`MarqueeBorder`控件，更改设计环境与它们交互。

截获对组件的属性访问器的调用被称为"隐藏。 它允许设计器来跟踪用户设置的值，并根据需要将该值传递到正在设计的组件。

对于本例，请<xref:System.Windows.Forms.Control.Visible%2A>和<xref:System.Windows.Forms.Control.Enabled%2A>属性将通过隐藏`MarqueeBorderDesigner`，这样用户将无法进行`MarqueeBorder`控件不可见或设计过程中已禁用。

设计器还可以添加和删除属性。 对于本例，请<xref:System.Windows.Forms.Control.Padding%2A>属性将在设计时，删除，因为`MarqueeBorder`控件以编程方式设置基于指定的灯大小的填充`LightSize`属性。

类的基类`MarqueeBorderDesigner`是<xref:System.ComponentModel.Design.ComponentDesigner>，其中包含可以更改属性、 属性和控件在设计时公开的事件的方法：

- <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterProperties%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterAttributes%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterAttributes%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterEvents%2A>

- <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterEvents%2A>

在更改时使用这些方法的组件的公共接口，必须遵循以下规则：

- 添加或删除中的项`PreFilter`仅方法

- 修改中的现有项`PostFilter`仅方法

- 始终首次调用基实现`PreFilter`方法

- 始终上一次调用基实现`PostFilter`方法

遵守这些规则可确保在设计时环境中的所有设计器正在设计的所有组件的一致视图。

<xref:System.ComponentModel.Design.ComponentDesigner>类提供用于管理属性的值被隐藏，从而免除了您需要创建特定的实例变量的字典。

### <a name="to-create-a-custom-designer-to-shadow-and-filter-properties"></a>若要创建自定义设计器为卷影和筛选器属性

1. 右键单击**设计**文件夹并添加新类。 源文件基名称指定为"MarqueeBorderDesigner。"

2. 打开`MarqueeBorderDesigner`中的源文件**代码编辑器**。 在该文件的顶部，导入以下命名空间：

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#420](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#420)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#420](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#420)]

3. 更改的声明`MarqueeBorderDesigner`从中继承<xref:System.Windows.Forms.Design.ParentControlDesigner>。

    因为`MarqueeBorder`控件可以包含子控件`MarqueeBorderDesigner`继承<xref:System.Windows.Forms.Design.ParentControlDesigner>，用于处理父-子交互。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#430](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#430)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#430](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#430)]

4. 重写的基实现<xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A>。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#450](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#450)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#450](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#450)]

5. 实现 <xref:System.Windows.Forms.Control.Enabled%2A> 和 <xref:System.Windows.Forms.Control.Visible%2A> 属性。 这些实现隐藏控件的属性。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#440](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#440)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#440](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#440)]

## <a name="handling-component-changes"></a>处理组件更改
 `MarqueeControlRootDesigner`类提供的自定义设计时体验您`MarqueeControl`实例。 大多数设计时功能继承自<xref:System.Windows.Forms.Design.DocumentDesigner>类; 您的代码将实现两个特定自定义： 处理组件更改和添加设计器谓词。

 为用户设计其`MarqueeControl`情况下，根设计器将跟踪更改`MarqueeControl`及其子控件。 在设计时环境提供了一项便利服务<xref:System.ComponentModel.Design.IComponentChangeService>、 跟踪更改到组件的状态。

 通过查询与环境获取对此服务的引用<xref:System.ComponentModel.Design.ComponentDesigner.GetService%2A>方法。 如果查询成功，您的设计器可以处理程序附加到<xref:System.ComponentModel.Design.IComponentChangeService.ComponentChanged>事件并执行任何任务所需在设计时保持一致的状态。

 情况下`MarqueeControlRootDesigner`类，将调用<xref:System.Windows.Forms.Control.Refresh%2A>方法在每个`IMarqueeWidget`包含对象`MarqueeControl`。 这将导致`IMarqueeWidget`对象重绘其自身适当时属性，例如其父级的<xref:System.Windows.Forms.Control.Size%2A>发生更改。

### <a name="to-handle-component-changes"></a>若要处理组件更改

1. 打开`MarqueeControlRootDesigner`中的源文件**代码编辑器**并重写<xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A>方法。 调用基实现的<xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A>并进行查询， <xref:System.ComponentModel.Design.IComponentChangeService>。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#580](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#580)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#580](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#580)]

2. 实现<xref:System.ComponentModel.Design.IComponentChangeService.OnComponentChanged%2A>事件处理程序。 测试发送组件的类型，如果它是`IMarqueeWidget`，调用其<xref:System.Windows.Forms.Control.Refresh%2A>方法。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#560](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#560)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#560](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#560)]

## <a name="adding-designer-verbs-to-your-custom-designer"></a>将设计器谓词添加到自定义设计器

设计器谓词是链接到一个事件处理程序的菜单命令。 设计器谓词在设计时添加到组件的快捷菜单。 有关详细信息，请参阅 <xref:System.ComponentModel.Design.DesignerVerb>。

会将两个设计器谓词添加到您的设计人员：**运行测试**并**停止测试**。 这些谓词将允许您查看的运行时行为`MarqueeControl`在设计时。 这些谓词将添加到`MarqueeControlRootDesigner`。

当**运行测试**是调用，则谓词事件处理程序将调用`StartMarquee`方法`MarqueeControl`。 当**停止测试**是调用，则谓词事件处理程序将调用`StopMarquee`方法`MarqueeControl`。 实现`StartMarquee`并`StopMarquee`方法的实现包含控件上调用这些方法`IMarqueeWidget`，因此任何包含`IMarqueeWidget`控件还将参与测试。

### <a name="to-add-designer-verbs-to-your-custom-designers"></a>若要将设计器谓词添加到自定义设计器

1. 在中`MarqueeControlRootDesigner`类中，添加事件处理程序名为`OnVerbRunTest`和`OnVerbStopTest`。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#570](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#570)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#570](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#570)]

2. 将这些事件处理程序连接到其相应设计器谓词。 `MarqueeControlRootDesigner` 继承<xref:System.ComponentModel.Design.DesignerVerbCollection>从其基类。 您将创建两个新<xref:System.ComponentModel.Design.DesignerVerb>对象，并将其添加到此集合中<xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A>方法。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#590](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#590)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#590](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#590)]

## <a name="creating-a-custom-uitypeeditor"></a>创建自定义 UITypeEditor

时创建用户提供自定义设计时体验，它通常是需要创建与属性窗口的自定义式交互。 您可以完成此操作通过创建<xref:System.Drawing.Design.UITypeEditor>。 有关详细信息，请参阅[如何：创建 UI 类型编辑器](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/fd3kt7d5(v=vs.120))。

`MarqueeBorder`控件公开多个属性在属性窗口中的。 这些属性的两个`MarqueeSpinDirection`和`MarqueeLightShape`枚举表示。 举例说明的 UI 类型编辑器，使用`MarqueeLightShape`属性将具有一个关联<xref:System.Drawing.Design.UITypeEditor>类。

### <a name="to-create-a-custom-ui-type-editor"></a>若要创建自定义 UI 类型编辑器

1. 打开`MarqueeBorder`中的源文件**代码编辑器**。

2. 中的定义`MarqueeBorder`类中，声明一个名为类`LightShapeEditor`派生<xref:System.Drawing.Design.UITypeEditor>。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#96](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#96)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#96](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#96)]

3. 声明<xref:System.Windows.Forms.Design.IWindowsFormsEditorService>调用的实例变量`editorService`。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#92](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#92)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#92](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#92)]

4. 重写 <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A> 方法。 此实现返回<xref:System.Drawing.Design.UITypeEditorEditStyle.DropDown>，它将告诉如何显示在设计环境`LightShapeEditor`。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#93](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#93)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#93](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#93)]

5. 重写 <xref:System.Drawing.Design.UITypeEditor.EditValue%2A> 方法。 此实现查询的设计环境<xref:System.Windows.Forms.Design.IWindowsFormsEditorService>对象。 如果成功，它将创建`LightShapeSelectionControl`。 <xref:System.Windows.Forms.Design.IWindowsFormsEditorService.DropDownControl%2A>方法调用以启动`LightShapeEditor`。 此调用的返回值返回到设计环境。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#94](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#94)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#94](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#94)]

## <a name="creating-a-view-control-for-your-custom-uitypeeditor"></a>为自定义 UITypeEditor 创建视图控件

1. `MarqueeLightShape`属性支持两种类型的光线的形状：`Square`和`Circle`。 您将创建专用于在属性窗口中以图形方式显示这些值的自定义控件。 此自定义控件将由你<xref:System.Drawing.Design.UITypeEditor>与属性窗口进行交互。

### <a name="to-create-a-view-control-for-your-custom-ui-type-editor"></a>若要创建自定义 UI 类型编辑器视图控件

1. 添加一个新<xref:System.Windows.Forms.UserControl>项`MarqueeControlLibrary`项目。 新的源文件基名称指定为"LightShapeSelectionControl。"

2. 将两个<xref:System.Windows.Forms.Panel>控件从**工具箱**拖动到`LightShapeSelectionControl`。 命名它们`squarePanel`和`circlePanel`。 排列它们并排显示。 设置<xref:System.Windows.Forms.Control.Size%2A>属性均<xref:System.Windows.Forms.Panel>控件添加到 （60，60）。 设置<xref:System.Windows.Forms.Control.Location%2A>属性的`squarePanel`控制对 （8，10）。 设置<xref:System.Windows.Forms.Control.Location%2A>属性的`circlePanel`控制对 （80，10）。 最后，设置<xref:System.Windows.Forms.Control.Size%2A>属性的`LightShapeSelectionControl`到 150 (80）。

3. 打开`LightShapeSelectionControl`中的源文件**代码编辑器**。 该文件顶部，导入<xref:System.Windows.Forms.Design?displayProperty=nameWithType>命名空间：

```vb
Imports System.Windows.Forms.Design
```

```csharp
using System.Windows.Forms.Design;
```

1. 实现<xref:System.Windows.Forms.Control.Click>事件处理程序`squarePanel`和`circlePanel`控件。 这些方法调用<xref:System.Windows.Forms.Design.IWindowsFormsEditorService.CloseDropDown%2A>若要结束自定义<xref:System.Drawing.Design.UITypeEditor>编辑会话。

    [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#390](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#390)]
    [!code-vb[System.Windows.Forms.Design.DocumentDesigner#390](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#390)]

2. 声明<xref:System.Windows.Forms.Design.IWindowsFormsEditorService>调用的实例变量`editorService`。

```vb
Private editorService As IWindowsFormsEditorService
```

```csharp
private IWindowsFormsEditorService editorService;
```

1. 声明`MarqueeLightShape`调用的实例变量`lightShapeValue`。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#330](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#330)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#330](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#330)]

2. 在中`LightShapeSelectionControl`构造函数中，附加<xref:System.Windows.Forms.Control.Click>的事件处理程序`squarePanel`并`circlePanel`控件的<xref:System.Windows.Forms.Control.Click>事件。 另外，定义将分配一个构造函数重载`MarqueeLightShape`到设计环境中的值`lightShapeValue`字段。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#340](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#340)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#340](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#340)]

3. 在中<xref:System.ComponentModel.Component.Dispose%2A>方法中，分离<xref:System.Windows.Forms.Control.Click>事件处理程序。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#350](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#350)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#350](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#350)]

4. 在“解决方案资源管理器”中，单击“显示所有文件”按钮。 打开 LightShapeSelectionControl.Designer.cs 或 LightShapeSelectionControl.Designer.vb 文件，并删除的默认定义<xref:System.ComponentModel.Component.Dispose%2A>方法。

5. 实现 `LightShape` 属性。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#360](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#360)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#360](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#360)]

6. 重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。 此实现将绘制一个实心的方形和圆。 它还将通过绘制一个形状或其他周围的边框来突出显示所选的值。

     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#380](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#380)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#380](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#380)]

## <a name="testing-your-custom-control-in-the-designer"></a>在设计器中测试自定义控件

此时，您可以构建`MarqueeControlLibrary`项目。 通过创建继承的控件来测试您的实现`MarqueeControl`类并在窗体上使用它。

### <a name="to-create-a-custom-marqueecontrol-implementation"></a>若要创建自定义的 MarqueeControl 实现

1. 在 Windows 窗体设计器中打开 `DemoMarqueeControl`。 这将创建的实例`DemoMarqueeControl`类型并将其显示实例中`MarqueeControlRootDesigner`类型。

2. 在中**工具箱**，打开**MarqueeControlLibrary 组件**选项卡。你将看到`MarqueeBorder`和`MarqueeText`控件可供选择。

3. 实例拖`MarqueeBorder`控件拖动到`DemoMarqueeControl`设计图面。 停靠此`MarqueeBorder`到父控件的控件。

4. 实例拖`MarqueeText`控件拖动到`DemoMarqueeControl`设计图面。

5. 生成解决方案。

6. 右键单击`DemoMarqueeControl`并从快捷菜单选择**运行测试**选项来启动动画。 单击**停止测试**停止动画。

7. 在设计视图中打开“Form1”。

8. 放置两个<xref:System.Windows.Forms.Button>窗体控件。 命名它们`startButton`和`stopButton`，并将更改<xref:System.Windows.Forms.Control.Text%2A>属性值复制到**启动**并**停止**分别。

9. 实现<xref:System.Windows.Forms.Control.Click>两个事件处理程序<xref:System.Windows.Forms.Button>控件。

10. 在中**工具箱**，打开**MarqueeControlTest 组件**选项卡。你将看到`DemoMarqueeControl`可供选择。

11. 实例拖`DemoMarqueeControl`拖到**Form1**设计图面。

12. 在中<xref:System.Windows.Forms.Control.Click>事件处理程序调用`Start`并`Stop`上的方法`DemoMarqueeControl`。

```vb
Private Sub startButton_Click(sender As Object, e As System.EventArgs)
    Me.demoMarqueeControl1.Start()
End Sub 'startButton_Click

Private Sub stopButton_Click(sender As Object, e As System.EventArgs)
Me.demoMarqueeControl1.Stop()
End Sub 'stopButton_Click
```

```csharp
private void startButton_Click(object sender, System.EventArgs e)
{
    this.demoMarqueeControl1.Start();
}

private void stopButton_Click(object sender, System.EventArgs e)
{
    this.demoMarqueeControl1.Stop();
}
```

1. 设置`MarqueeControlTest`项目为启动项目，然后运行它。 你将看到显示的窗体在`DemoMarqueeControl`。 单击**启动**按钮以启动动画。 您应该看到灯光移动边框和闪烁的文本。

## <a name="next-steps"></a>后续步骤

`MarqueeControlLibrary`演示了一个简单的自定义控件和关联的设计器实现。 你可以多种方式来进行此示例更复杂：

- 更改的属性值`DemoMarqueeControl`在设计器中。 添加更多`MarqueBorder`控制并将其停靠在其父实例中以创建嵌套的效果。 使用不同的设置`UpdatePeriod`和 light 相关的属性。

- 编写您自己的实现的`IMarqueeWidget`。 例如，可以包含多个映像创建闪烁的"neon 登录"或经过动画处理的登录。

- 进一步自定义设计时体验。 您可以尝试隐藏更多属性比<xref:System.Windows.Forms.Control.Enabled%2A>和<xref:System.Windows.Forms.Control.Visible%2A>，可以添加新属性。 添加新的设计器谓词来简化常见任务，例如停靠子控件。

- 许可证`MarqueeControl`。 有关详细信息，请参阅[如何：授予组件和控件许可](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/fe8b1eh9(v=vs.120))。

- 控制如何序列化您的控件以及如何为其生成代码。 有关详细信息，请参阅[动态源代码生成和编译](../../reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Forms.UserControl>
- <xref:System.Windows.Forms.Design.ParentControlDesigner>
- <xref:System.Windows.Forms.Design.DocumentDesigner>
- <xref:System.ComponentModel.Design.IRootDesigner>
- <xref:System.ComponentModel.Design.DesignerVerb>
- <xref:System.Drawing.Design.UITypeEditor>
- <xref:System.ComponentModel.BackgroundWorker>
- [如何：创建利用设计时功能的 Windows 窗体控件](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/307hck25(v=vs.120))
- [扩展设计时支持](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/37899azc(v=vs.120))
- [自定义设计器](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/h51z5c0x(v=vs.120))
