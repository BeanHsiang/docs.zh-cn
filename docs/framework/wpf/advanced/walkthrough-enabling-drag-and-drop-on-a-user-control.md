---
title: 演练：启用拖放用户控件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthrough [WPF], drag-and-drop
- drag-and-drop [WPF], walkthrough
ms.assetid: cc844419-1a77-4906-95d9-060d79107fc7
ms.openlocfilehash: 7009f56c25ff63729f0b0170503c2f356dc91301
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352914"
---
# <a name="walkthrough-enabling-drag-and-drop-on-a-user-control"></a>演练：启用拖放用户控件

本演练演示如何创建可在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中参与拖放数据传输的自定义用户控件。

在本演练中，你将创建自定义 WPF<xref:System.Windows.Controls.UserControl>表示圆形形状。 你将在该控件上实现可通过拖放进行数据传输的功能。 例如，如果从一个圆形控件拖到另一个圆形控件，则会将填充颜色数据从源圆形复制到目标圆形。 如果从到一个圆形控件拖<xref:System.Windows.Controls.TextBox>，填充颜色的字符串表示形式复制到<xref:System.Windows.Controls.TextBox>。 您还将创建包含两个面板控件的小型应用程序和一个<xref:System.Windows.Controls.TextBox>测试拖放功能。 你将编写可使面板处理放置的圆形数据的代码，这样就可以将圆形从一个面板的 Children 集合移动或复制到其他面板。

本演练阐释了以下任务：

-   创建自定义用户控件。

-   使用户控件成为拖动源。

-   使用户控件成为拖放目标。

-   使面板能够接收用户控件中放置的数据。

## <a name="prerequisites"></a>系统必备

若要完成本演练，必须具有 Visual Studio。

## <a name="create-the-application-project"></a>创建应用程序项目
 在本部分中，您将创建应用程序基础结构，其中包括主页，其中两个面板和<xref:System.Windows.Controls.TextBox>。

1.  在 Visual Basic 或 Visual C# 中创建名为 `DragDropExample` 的新 WPF 应用程序项目。 有关详细信息，请参见[演练：我第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。

2.  打开 MainWindow.xaml。

3.  添加以下标记的开始和结束之间<xref:System.Windows.Controls.Grid>标记。

     此标记将创建用于测试应用程序的用户界面。

     [!code-xaml[DragDropWalkthrough#PanelsStep1XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep1xaml)]

## <a name="add-a-new-user-control-to-the-project"></a>向项目添加新的用户控件
 本节将介绍如何向项目添加新的用户控件。

1.  在“项目”菜单中，选择“添加用户控件”。

2.  在中**添加新项**对话框框中，将名称更改为`Circle.xaml`，然后单击**添加**。

     Circle.xaml 及其代码隐藏内容将添加到项目中。

3.  打开 Circle.xaml。

     此文件将包含用户控件的用户界面元素。

4.  将以下标记添加到根<xref:System.Windows.Controls.Grid>若要创建将蓝色圆形作为其 UI 的简单用户控件。

     [!code-xaml[DragDropWalkthrough#EllipseXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#ellipsexaml)]

5.  打开 Circle.xaml.cs 或 Circle.xaml.vb。

6.  在 C# 中，在默认构造函数后面添加以下代码以创建复制构造函数。 在 Visual Basic 中，添加以下代码以同时创建默认构造函数和复制构造函数。

     若要允许复制用户控件，需在代码隐藏文件中添加复制构造函数方法。 在简化的圆形用户控件中，将只复制该用户控件的填充和大小。

     [!code-csharp[DragDropWalkthrough#CopyCtor](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#copyctor)]
     [!code-vb[DragDropWalkthrough#CopyCtor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#copyctor)]

## <a name="add-the-user-control-to-the-main-window"></a>将用户控件添加到主窗口

1.  打开 MainWindow.xaml。

2.  将以下 XAML 添加到起始<xref:System.Windows.Window>标记以创建对当前应用程序的 XML 命名空间引用。

    ```
    xmlns:local="clr-namespace:DragDropExample"
    ```

3.  在第一个<xref:System.Windows.Controls.StackPanel>，添加以下 XAML 在第一个面板中创建圆形用户控件的两个实例。

     [!code-xaml[DragDropWalkthrough#CirclesXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#circlesxaml)]

     此面板的完整 XAML 如下所示。

     [!code-xaml[DragDropWalkthrough#PanelsStep2XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep2xaml)]

## <a name="implement-drag-source-events-in-the-user-control"></a>在用户控件中实现拖动源事件
 在本部分中，你将重写<xref:System.Windows.UIElement.OnMouseMove%2A>方法并启动拖放操作。

 如果已开始拖动 （按下鼠标按钮并移动鼠标），将打包到传输的数据<xref:System.Windows.DataObject>。 在这种情况下，圆形控件将打包三个数据项：其填充颜色的字符串表示形式、其高度的双精度表示形式以及其自身的副本。

### <a name="to-initiate-a-drag-and-drop-operation"></a>启动拖放操作

1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。

2.  添加以下<xref:System.Windows.UIElement.OnMouseMove%2A>替代，以便提供类处理<xref:System.Windows.UIElement.MouseMove>事件。

     [!code-csharp[DragDropWalkthrough#OnMouseMove](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#onmousemove)]
     [!code-vb[DragDropWalkthrough#OnMouseMove](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#onmousemove)]

     这<xref:System.Windows.UIElement.OnMouseMove%2A>替代执行以下任务：

    -   检查移动鼠标时是否按下了鼠标左键。

    -   将圆形数据打包到<xref:System.Windows.DataObject>。 在这种情况下，圆形控件将打包三个数据项：其填充颜色的字符串表示形式、其高度的双精度表示形式以及其自身的副本。

    -   调用静态<xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=nameWithType>方法启动拖放操作。 传递到以下三个参数<xref:System.Windows.DragDrop.DoDragDrop%2A>方法：

        -   `dragSource` – 对此控件的引用。

        -   `data` –<xref:System.Windows.DataObject>前面的代码中创建。

        -   `allowedEffects` – 允许的拖放操作，即<xref:System.Windows.DragDropEffects.Copy>或<xref:System.Windows.DragDropEffects.Move>。

3.  按 F5 生成并运行该应用程序。

4.  单击其中一个圆形控件并将其拖到面板、 另一个圆形和<xref:System.Windows.Controls.TextBox>。 当上拖动<xref:System.Windows.Controls.TextBox>，光标发生变化，以指示移动。

5.  同时通过拖动圆形<xref:System.Windows.Controls.TextBox>，按**Ctrl**密钥。 请注意光标是如何更改以指示复制的。

6.  拖放到上的一个圆圈<xref:System.Windows.Controls.TextBox>。 圆形填充颜色的字符串表示形式追加到<xref:System.Windows.Controls.TextBox>。

     ![圆形填充颜色的字符串表示形式](./media/dragdrop-colorstring.png "DragDrop_ColorString")

默认情况下，光标会在拖放操作过程中更改，以指示放置数据会产生的效果。 你可以自定义提供给用户，通过处理反馈<xref:System.Windows.UIElement.GiveFeedback>事件和设置不同光标。

## <a name="give-feedback-to-the-user"></a>向用户提供反馈

1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。

2.  添加以下<xref:System.Windows.UIElement.OnGiveFeedback%2A>替代，以便提供类处理<xref:System.Windows.UIElement.GiveFeedback>事件。

     [!code-csharp[DragDropWalkthrough#OnGiveFeedback](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ongivefeedback)]
     [!code-vb[DragDropWalkthrough#OnGiveFeedback](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ongivefeedback)]

     这<xref:System.Windows.UIElement.OnGiveFeedback%2A>替代执行以下任务：

    -   检查<xref:System.Windows.GiveFeedbackEventArgs.Effects%2A>拖放目标中设置的值<xref:System.Windows.UIElement.DragOver>事件处理程序。

    -   设置基于自定义光标<xref:System.Windows.GiveFeedbackEventArgs.Effects%2A>值。 该光标旨在向用户提供关于放置数据所产生的效果的可视反馈。

3.  按 F5 生成并运行该应用程序。

4.  拖动其中一个圆形的面板，另一个圆形，通过控制和<xref:System.Windows.Controls.TextBox>。 请注意，现在的光标是你在中指定的自定义光标<xref:System.Windows.UIElement.OnGiveFeedback%2A>重写。

     ![使用自定义光标拖放](./media/dragdrop-customcursor.png "DragDrop_CustomCursor")

5.  选择的文本`green`从<xref:System.Windows.Controls.TextBox>。

6.  将 `green` 文本拖到一个圆形控件上。 请注意，将显示默认光标以指示拖放操作效果。 反馈光标始终由拖动源设置。

## <a name="implement-drop-target-events-in-the-user-control"></a>在用户控件中实现拖放目标事件
 在本节中，你将指定用户控件为拖放目标，替代可使用户控件成为拖放目标的方法，并处理用户控件上放置的数据。

### <a name="to-enable-the-user-control-to-be-a-drop-target"></a>使用户控件成为拖放目标

1.  打开 Circle.xaml。

2.  在左括号<xref:System.Windows.Controls.UserControl>标记中，添加<xref:System.Windows.UIElement.AllowDrop%2A>属性并将其设置为`true`。

     [!code-xaml[DragDropWalkthrough#UCTagXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#uctagxaml)]

<xref:System.Windows.UIElement.OnDrop%2A>时调用方法<xref:System.Windows.UIElement.AllowDrop%2A>属性设置为`true`和拖动源中的数据放置在圆形用户控件上。 在这种方法中，将处理已放置的数据，并将这些数据应用于圆形。

### <a name="to-process-the-dropped-data"></a>处理已放置的数据

1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。

2.  添加以下<xref:System.Windows.UIElement.OnDrop%2A>替代，以便提供类处理<xref:System.Windows.UIElement.Drop>事件。

     [!code-csharp[DragDropWalkthrough#OnDrop](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondrop)]
     [!code-vb[DragDropWalkthrough#OnDrop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondrop)]

     这<xref:System.Windows.UIElement.OnDrop%2A>替代执行以下任务：

    -   使用<xref:System.Windows.DataObject.GetDataPresent%2A>方法用于检查拖动的数据是否包含字符串对象。

    -   使用<xref:System.Windows.DataObject.GetData%2A>方法提取字符串数据，如果存在。

    -   使用<xref:System.Windows.Media.BrushConverter>尝试将字符串转换为<xref:System.Windows.Media.Brush>。

    -   如果转换成功，将应用到画笔<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Ellipse>提供圆形控件的 UI。

    -   标记<xref:System.Windows.UIElement.Drop>为已处理的事件。 应将放置事件标记为已处理，这样接收此事件的其他元素才会知道圆形用户控件已处理了该事件。

3.  按 F5 生成并运行该应用程序。

4.  选择的文本`green`在<xref:System.Windows.Controls.TextBox>。

5.  将文本拖放到一个圆形控件上。 该圆形会从蓝色变为绿色。

     ![将字符串转换为画笔](./media/dragdrop-dropgreentext.png "DragDrop_DropGreenText")

6.  键入的文本`green`在<xref:System.Windows.Controls.TextBox>。

7.  选择的文本`gre`在<xref:System.Windows.Controls.TextBox>。

8.  将其拖放到一个圆形控件上。 请注意，光标会更改以指示允许放置，但圆形的颜色不会更改，因为 `gre` 不是有效颜色。

9. 从绿色圆形控件拖放到蓝色圆形控件。 该圆形会从蓝色变为绿色。 请注意，显示的光标取决于是否<xref:System.Windows.Controls.TextBox>还是圆形作为拖动源。

设置<xref:System.Windows.UIElement.AllowDrop%2A>属性设置为`true`和处理放置的数据是只需要启用要拖放目标的元素。 但是，若要提供更好的用户体验，您还应处理<xref:System.Windows.UIElement.DragEnter>， <xref:System.Windows.UIElement.DragLeave>，和<xref:System.Windows.UIElement.DragOver>事件。 在这些事件中，你可以在放置数据前执行检查并向用户提供其他反馈。

将数据拖动到圆形用户控件上时，该控件应通知拖动源它是否可以处理所拖动的数据。 如果该控件不知如何处理这些数据，则它应拒绝放置。 若要执行此操作，你将处理<xref:System.Windows.UIElement.DragOver>事件并设置<xref:System.Windows.DragEventArgs.Effects%2A>属性。

### <a name="to-verify-that-the-data-drop-is-allowed"></a>验证是否允许数据放置

1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。

2.  添加以下<xref:System.Windows.UIElement.OnDragOver%2A>替代，以便提供类处理<xref:System.Windows.UIElement.DragOver>事件。

     [!code-csharp[DragDropWalkthrough#OnDragOver](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragover)]
     [!code-vb[DragDropWalkthrough#OnDragOver](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragover)]

     这<xref:System.Windows.UIElement.OnDragOver%2A>替代执行以下任务：

    -   将 <xref:System.Windows.DragEventArgs.Effects%2A> 属性设置为 <xref:System.Windows.DragDropEffects.None>。

    -   执行在中执行的相同检查<xref:System.Windows.UIElement.OnDrop%2A>方法，以确定圆形用户控件是否可以处理拖动的数据。

    -   如果用户控件可以处理数据，设置<xref:System.Windows.DragEventArgs.Effects%2A>属性设置为<xref:System.Windows.DragDropEffects.Copy>或<xref:System.Windows.DragDropEffects.Move>。

3.  按 F5 生成并运行该应用程序。

4.  选择的文本`gre`在<xref:System.Windows.Controls.TextBox>。

5.  将文本拖到一个圆形控件上。 请注意，光标此时会更改以指示不允许放置，因为 `gre` 不是有效颜色。

 可通过应用拖放操作预览进一步增强用户体验。 对于圆形用户控件，您将重写<xref:System.Windows.UIElement.OnDragEnter%2A>和<xref:System.Windows.UIElement.OnDragLeave%2A>方法。 当将数据拖动控件当前的背景上<xref:System.Windows.Shapes.Shape.Fill%2A>保存在一个占位符变量中。 然后转换为画笔并应用于字符串<xref:System.Windows.Shapes.Ellipse>提供圆形 UI。 如果将数据拖动出该圆形而没有放置，原始<xref:System.Windows.Shapes.Shape.Fill%2A>值重新应用于该圆形。

### <a name="to-preview-the-effects-of-the-drag-and-drop-operation"></a>预览拖放操作的效果

1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。

2.  在圆形类中，声明一个私有<xref:System.Windows.Media.Brush>名为变量`_previousFill`并将其初始化`null`。

     [!code-csharp[DragDropWalkthrough#Brush](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#brush)]
     [!code-vb[DragDropWalkthrough#Brush](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#brush)]

3.  添加以下<xref:System.Windows.UIElement.OnDragEnter%2A>替代，以便提供类处理<xref:System.Windows.UIElement.DragEnter>事件。

     [!code-csharp[DragDropWalkthrough#OnDragEnter](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragenter)]
     [!code-vb[DragDropWalkthrough#OnDragEnter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragenter)]

     这<xref:System.Windows.UIElement.OnDragEnter%2A>替代执行以下任务：

    -   将保存<xref:System.Windows.Shapes.Shape.Fill%2A>的属性<xref:System.Windows.Shapes.Ellipse>中`_previousFill`变量。

    -   执行在中执行的相同检查<xref:System.Windows.UIElement.OnDrop%2A>方法，以确定数据是否可以转换为<xref:System.Windows.Media.Brush>。

    -   如果数据转换为有效<xref:System.Windows.Media.Brush>，将其应用于<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Ellipse>。

4.  添加以下<xref:System.Windows.UIElement.OnDragLeave%2A>替代，以便提供类处理<xref:System.Windows.UIElement.DragLeave>事件。

     [!code-csharp[DragDropWalkthrough#OnDragLeave](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragleave)]
     [!code-vb[DragDropWalkthrough#OnDragLeave](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragleave)]

     这<xref:System.Windows.UIElement.OnDragLeave%2A>替代执行以下任务：

    -   适用<xref:System.Windows.Media.Brush>以保存`_previousFill`变量<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Ellipse>提供圆形用户控件的 UI。

5.  按 F5 生成并运行该应用程序。

6.  选择的文本`green`在<xref:System.Windows.Controls.TextBox>。

7.  将该文本拖到一个圆形控件上而不放置。 该圆形会从蓝色变为绿色。

     ![预览拖放操作的效果](./media/dragdrop-previeweffects.png "DragDrop_PreviewEffects")

8.  将文本拖离该圆形控件。 该圆形会从绿色变回蓝色。

## <a name="enable-a-panel-to-receive-dropped-data"></a>使面板能够接收放置的数据

在本部分中，允许承载圆形用户控件，使其作为拖动圆形数据的放置目标的面板。 将实现的代码，使你可以将圆形从一个面板移动到另一个，或通过按下创建一个圆形控件的副本**Ctrl**拖放圆形时键。

1.  打开 MainWindow.xaml。

2.  以下 XAML 中的每个中所示<xref:System.Windows.Controls.StackPanel>控件，则添加的处理程序<xref:System.Windows.UIElement.DragOver>和<xref:System.Windows.UIElement.Drop>事件。 名称<xref:System.Windows.UIElement.DragOver>事件处理程序`panel_DragOver`，并将命名<xref:System.Windows.UIElement.Drop>事件处理程序`panel_Drop`。

     [!code-xaml[DragDropWalkthrough#PanelsXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml#panelsxaml)]

3.  打开 MainWindows.xaml.cs 或 MainWindow.xaml.vb。

4.  添加以下代码为<xref:System.Windows.UIElement.DragOver>事件处理程序。

     [!code-csharp[DragDropWalkthrough#PanelDragOver](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldragover)]
     [!code-vb[DragDropWalkthrough#PanelDragOver](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldragover)]

     这<xref:System.Windows.UIElement.DragOver>事件处理程序执行以下任务：

    -   检查拖动的数据包含已打包的中的"对象"数据<xref:System.Windows.DataObject>由圆形用户控件，并对的调用中传递<xref:System.Windows.DragDrop.DoDragDrop%2A>。

    -   如果"对象"数据存在，检查是否**Ctrl**按下键。

    -   如果**Ctrl**按下键，集<xref:System.Windows.DragEventArgs.Effects%2A>属性设置为<xref:System.Windows.DragDropEffects.Copy>。 否则，设置<xref:System.Windows.DragEventArgs.Effects%2A>属性设置为<xref:System.Windows.DragDropEffects.Move>。

5.  添加以下代码为<xref:System.Windows.UIElement.Drop>事件处理程序。

     [!code-csharp[DragDropWalkthrough#PanelDrop](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldrop)]
     [!code-vb[DragDropWalkthrough#PanelDrop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldrop)]

     这<xref:System.Windows.UIElement.Drop>事件处理程序执行以下任务：

    -   检查是否<xref:System.Windows.UIElement.Drop>已处理事件。 例如，如果一个圆形放置在另一圈的句柄<xref:System.Windows.UIElement.Drop>事件，您不希望包含还处理该圆形的面板。

    -   如果<xref:System.Windows.UIElement.Drop>不处理事件，检查是否**Ctrl**按下键。

    -   如果**Ctrl**按下键时<xref:System.Windows.UIElement.Drop>发生，会复制该圆形控件并将其添加到<xref:System.Windows.Controls.Panel.Children%2A>的集合<xref:System.Windows.Controls.StackPanel>。

    -   如果**Ctrl**未按下键，将移动从圆<xref:System.Windows.Controls.Panel.Children%2A>到其父面板的集合<xref:System.Windows.Controls.Panel.Children%2A>面板已被删除的集合。

    -   集<xref:System.Windows.DragEventArgs.Effects%2A>属性以通知<xref:System.Windows.DragDrop.DoDragDrop%2A>方法是否执行了移动或复制操作。

6.  按 F5 生成并运行该应用程序。

7.  选择的文本`green`从<xref:System.Windows.Controls.TextBox>。

8.  将文本拖放到一个圆形控件上。

9. 将一个圆形控件从左面板拖放到右面板。 该圆形会从<xref:System.Windows.Controls.Panel.Children%2A>左面板中的集合并添加到右侧面板的 Children 集合。

10. 从面板到另一个面板将一个圆形控件拖放时按**Ctrl**密钥。 将复制该圆形并将副本添加到<xref:System.Windows.Controls.Panel.Children%2A>接收面板的集合。

     ![按住 Ctrl 键的同时拖动圆形](./media/dragdrop-paneldrop.png "DragDrop_PanelDrop")

## <a name="see-also"></a>请参阅

- [拖放概述](drag-and-drop-overview.md)