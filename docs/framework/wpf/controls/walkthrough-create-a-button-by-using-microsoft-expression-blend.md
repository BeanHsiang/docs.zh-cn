---
title: 演练：使用 Microsoft Expression Blend 创建按钮
ms.date: 03/30/2017
helpviewer_keywords:
- buttons [WPF]
- converting [WPF], shape to button
- Expression Blend [WPF Designer]
ms.assetid: ff5037c2-bba7-4cae-8abb-6475b686c48e
ms.openlocfilehash: cd143b55190ce398cc33e57a832ae85aabc36c41
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352693"
---
# <a name="walkthrough-create-a-button-by-using-microsoft-expression-blend"></a>演练：使用 Microsoft Expression Blend 创建按钮
本演练将引导你完成创建过程[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]使用 Microsoft Expression Blend 的自定义的按钮。  
  
> [!IMPORTANT]
>  Microsoft Expression Blend 的工作原理是生成[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]然后编译以使可执行程序。 如果使用中而不是所起的作用[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]直接，没有创建一个使用此条件的应用程序的另一个演练[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]与 Visual Studio 而不是 Blend。 请参阅[创建一个按钮通过使用 XAML](walkthrough-create-a-button-by-using-xaml.md)有关详细信息。  
  
 下图显示了您将创建的自定义的按钮。  
  
 ![您将创建的自定义的按钮](./media/custom-button-blend-intro.jpg "custom_button_blend_Intro")  
  
## <a name="convert-a-shape-to-a-button"></a>将形状转换为一个按钮  
 在本演练的第一部分创建的自定义按钮的自定义外观。 若要执行此操作，您首先将一个矩形成一个按钮。 您将添加其他形状到模板的按钮，创建更复杂的美观按钮。 为什么不使用常规按钮启动和自定义它？ 因为一个按钮具有内置功能，您不需要;对于自定义按钮，它是更轻松地开始一个矩形。  
  
#### <a name="to-create-a-new-project-in-expression-blend"></a>若要在 Expression Blend 中创建新项目  
  
1.  开始在 Expression Blend。 (单击**启动**，依次指向**所有程序**，指向**Microsoft Expression**，然后单击**Microsoft Expression Blend**。)  
  
2.  如果需要最大化应用程序。  
  
3.  在“文件”菜单上，单击“新建项目”。  
  
4.  选择**标准应用程序 (.exe)**。  
  
5.  将项目命名`CustomButton`并按**确定**。  
  
 此时您已具有一个空[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]项目。 可以按 F5 运行该应用程序。 正如您所料，此应用程序包含一个空白的窗口。 接下来，创建一个圆角的矩形，并将其转换为一个按钮。  
  
#### <a name="to-convert-a-rectangle-to-a-button"></a>若要将一个矩形转换为一个按钮  
  
1.  **窗口背景属性设置为黑色：** 选择该窗口中，单击**属性选项卡**，并设置<xref:System.Windows.Controls.Control.Background%2A>属性设置为`Black`。  
  
     ![如何将按钮的背景设置为黑色](./media/custom-button-blend-changebackground.png "custom_button_blend_ChangeBackground")  
  
2.  **窗口上绘制一个矩形大小与按钮：** 选择左侧的工具面板上的矩形工具并将该矩形拖到窗口。  
  
     ![如何绘制一个矩形](./media/custom-button-blend-drawrect.png "custom_button_blend_DrawRect")  
  
3.  **为圆角矩形：** 拖动矩形的控点，或者直接设置<xref:System.Windows.Shapes.Rectangle.RadiusX%2A>和<xref:System.Windows.Shapes.Rectangle.RadiusY%2A>属性。 设置的值<xref:System.Windows.Shapes.Rectangle.RadiusX%2A>和<xref:System.Windows.Shapes.Rectangle.RadiusY%2A>为 20。  
  
     ![如何使矩形的角倒圆角](./media/custom-button-blend-roundcorners.png "custom_button_blend_RoundCorners")  
  
4.  **将矩形更改为一个按钮：** 选择该矩形。 上**工具**菜单上，单击**使按钮**。  
  
     ![如何使形状变为按钮](./media/custom-button-blend-makebutton.png "custom_button_blend_MakeButton")  
  
5.  **指定样式模板的作用域：** 会显示如下所示的对话框。  
  
     !["创建样式资源"对话框](./media/custom-button-blend-makebutton2.gif "custom_button_blend_MakeButton2")  
  
     有关**资源名称 （键）**，选择**应用到所有**。  这将使生成的样式和应用于所有对象的按钮的按钮模板。 有关**中定义**，选择**应用程序**。 这将使生成的样式和按钮模板的范围涵盖整个应用程序。 当这两个框中设置的值，在按钮样式和模板应用于整个应用程序中的所有按钮，创建应用程序中任何按钮将默认情况下，使用此模板。  
  
## <a name="edit-the-button-template"></a>编辑按钮模板  
 你现在有一个已更改为一个按钮的矩形。 在本部分中，将修改的按钮模板并进一步自定义其外观。  
  
#### <a name="to-edit-the-button-template-to-change-the-button-appearance"></a>若要编辑要更改按钮外观的按钮模板  
  
1.  **请转到编辑模板视图：** 若要进一步自定义按钮的外观，我们需要编辑按钮模板。 此模板创建时我们转换成一个按钮的矩形。 若要编辑的按钮模板，右键单击该按钮，然后选择**编辑控件部件 （模板）** ，然后**编辑模板**。  
  
     ![如何编辑模板](./media/custom-button-blend-edittemplate.jpg "custom_button_blend_EditTemplate")  
  
     在模板编辑器中，请注意，现在分为按钮<xref:System.Windows.Shapes.Rectangle>和<xref:System.Windows.Controls.ContentPresenter>。 <xref:System.Windows.Controls.ContentPresenter>用于呈现按钮 （例如，字符串"Button"） 中的内容。 这两个矩形并<xref:System.Windows.Controls.ContentPresenter>内的布局<xref:System.Windows.Controls.Grid>。  
  
     ![组件中的矩形的演示文稿](./media/custom-button-blend-templatepanel.png "custom_button_blend_TemplatePanel")  
  
2.  **更改模板组件的名称：** 右键单击在模板清单，更改矩形<xref:System.Windows.Shapes.Rectangle>名称从"[Rectangle]"到"outerRectangle"，并将"[ContentPresenter]"更改为"myContentPresenter"。  
  
     ![如何重命名模板的组件](./media/custom-button-blend-renamecomponents.png "custom_button_blend_RenameComponents")  
  
3.  **Alter 矩形，使其为空内 （如一个圆环图）：** 选择**outerRectangle**并设置<xref:System.Windows.Shapes.Shape.Fill%2A>为"透明"和<xref:System.Windows.Shapes.Shape.StrokeThickness%2A>为 5。  
  
     ![如何使矩形为空](./media/custom-button-blend-changerectproperties.png "custom_button_blend_ChangeRectProperties")  
  
     然后设置<xref:System.Windows.Shapes.Shape.Stroke%2A>该模板将在任何内容的颜色。 若要执行此操作，请单击小白色框旁边**笔划**，选择**CustomExpression**，并在对话框中键入"{TemplateBinding 后台}"。  
  
     ![如何设置使用的模板的颜色](./media/custom-button-blend-templatestroke.png "custom_button_blend_TemplateStroke")  
  
4.  **创建一个内部矩形：** 现在，创建另一个矩形 （名称"innerRectangle"） 并将其定位对称的内部**outerRectangle** 。 对于此类型的工作，可能需要放大以使该按钮编辑区域在更大。  
  
    > [!NOTE]
    >  在矩形可能看起来比图中的一个不同 （例如，它可能会有了圆形角）。  
  
     ![如何创建一个矩形内另一个矩形](./media/custom-button-blend-innerrectangleproperties.png "custom_button_blend_innerRectangleProperties")  
  
5.  **将 ContentPresenter 移到顶部：** 此时，就可以文本"Button"才能不再可见。 如果该条件，否则这是因为**innerRectangle**之上**myContentPresenter**。 若要解决此问题，拖动**myContentPresenter**如下**innerRectangle**。 重新定位矩形并**myContentPresenter** ，看起来像下面。  
  
    > [!NOTE]
    >  或者，您可以定位**myContentPresenter**通过右键单击它并按顶部**转发发送**。  
  
     ![如何移动一个按钮在另一个按钮之上](./media/custom-button-blend-innerrectangle2.png "custom_button_blend_innerRectangle2")  
  
6.  **更改 innerRectangle 的外观：** 设置<xref:System.Windows.Shapes.Rectangle.RadiusX%2A>， <xref:System.Windows.Shapes.Rectangle.RadiusY%2A>，和<xref:System.Windows.Shapes.Shape.StrokeThickness%2A>值为 20。 此外，设置<xref:System.Windows.Shapes.Shape.Fill%2A>到后台，使用自定义表达式"{TemplateBinding 后台}"的模板) 并设置<xref:System.Windows.Shapes.Shape.Stroke%2A>"透明"。 请注意，设置<xref:System.Windows.Shapes.Shape.Fill%2A>并<xref:System.Windows.Shapes.Shape.Stroke%2A>的**innerRectangle**那些与相对**outerRectangle**。  
  
     ![如何更改矩形的外观](./media/custom-button-blend-glassrectangleproperties1.png "custom_button_blend_glassRectangleProperties1")  
  
7.  **在最前面添加玻璃层：** 自定义按钮的外观的最后一部分是在最前面添加玻璃层。 此平台层由第三个矩形构成。 玻璃矩形玻璃将涵盖整个按钮，因为是在维度与类似**outerRectangle**。 因此，创建矩形，从而只需一份**outerRectangle**。 突出显示**outerRectangle** ，并使用 CTRL + C 和 CTRL + V 制作副本。 命名此新矩形"glassCube"。  
  
8.  **如有必要，重新定位 glassCube:** 如果**glassCube**是尚不存在定位，以便它涵盖了整个按钮，将其拖至相应位置。  
  
9. **为 glassCube 提供比 outerRectangle 略有不同的形状：** 更改的属性**glassCube**。 首先，更改<xref:System.Windows.Shapes.Rectangle.RadiusX%2A>并<xref:System.Windows.Shapes.Rectangle.RadiusY%2A>属性设置为 10 和<xref:System.Windows.Shapes.Shape.StrokeThickness%2A>为 2。  
  
     ![GlassCube 的外观设置](./media/custom-button-blend-glasscubeappearance.gif "custom_button_blend_GlassCubeAppearance")  
  
10. **请看起来像玻璃 glassCube:** 设置<xref:System.Windows.Shapes.Shape.Fill%2A>到玻璃介绍通过使用线性渐变的 75%不透明和之间交替颜色白色和透明超过 6 大约均匀分布的时间间隔。 这是要设置为梯度停止点：  
  
    -   梯度停止点 1:Alpha 值为 75%的白色  
  
    -   梯度停止点 2:透明  
  
    -   梯度停止点 3:Alpha 值为 75%的白色  
  
    -   梯度停止点 4:透明  
  
    -   梯度停止点 5:Alpha 值为 75%的白色  
  
    -   梯度停止点 6:透明  
  
     这将创建"波浪"玻璃外观。  
  
     ![看起来像玻璃的矩形](./media/custom-button-blend-glassrectangleproperties2.png "custom_button_blend_glassRectangleProperties2")  
  
11. **隐藏玻璃层：** 现在，您看到玻璃层如下所示，请转到**外观窗格**的**属性面板**和不透明度设置为 0%，以将其隐藏。 在以下各部分，我们将使用属性触发器和事件来显示和操作玻璃层。  
  
     ![如何隐藏玻璃矩形](./media/custom-button-glassrectangleproperties3.gif "custom_button_glassRectangleProperties3")  
  
## <a name="customize-the-button-behavior"></a>自定义按钮行为  
 此时，已通过编辑其模板自定义按钮的演示文稿，但该按钮不响应用户操作作为典型的按钮执行操作 （例如，更改在鼠标悬停时的外观，接收焦点，然后单击。）接下来两个过程演示如何构建类似这样到自定义按钮的行为。 我们将使用简单的属性触发器启动，然后添加事件触发器和动画。  
  
#### <a name="to-set-property-triggers"></a>若要设置属性触发器  
  
1.  **创建新的属性触发器：** 与**glassCube**处于选中状态，单击 **+ 属性**中**触发器**面板 （见图后面的下一步）。 这将创建具有默认属性触发器的属性触发器。  
  
2.  **请 IsMouseOver 由触发器使用的属性：** 将属性更改为<xref:System.Windows.UIElement.IsMouseOver%2A>。 这使属性触发器激活时<xref:System.Windows.UIElement.IsMouseOver%2A>属性是`true`（当用户指向使用鼠标按钮）。  
  
     ![如何在属性上设置触发器](./media/custom-button-blend-ismousedoverpropertytrigger.png "custom_button_blend_IsMousedOverPropertyTrigger")  
  
3.  **IsMouseOver 触发 glasscube 的 100%的不透明度：** 请注意，**触发器录制已打开**（请参阅上图中）。 这意味着，对的属性值进行任何更改**glassCube**录制已打开时将会发生时的操作<xref:System.Windows.UIElement.IsMouseOver%2A>是`true`。 录制时，更改<xref:System.Windows.UIElement.Opacity%2A>的**glassCube**为 100%。  
  
     ![如何设置按钮的不透明度](./media/custom-button-blend-ismousedoverpropertytrigger2.gif "custom_button_blend_IsMousedOverPropertyTrigger2")  
  
     现在已创建你的第一个属性触发器。 请注意，**触发器面板**编辑器的已记录<xref:System.Windows.UIElement.Opacity%2A>更改为 100%。  
  
     ![“触发器”面板](./media/custom-button-blend-propertytriggerinfo.png "custom_button_blend_PropertyTriggerInfo")  
  
     按 F5 以运行应用程序，并将鼠标指针移动和关闭按钮。 应会看到玻璃层时显示鼠标悬停按钮并在指针离开时消失。  
  
4.  **IsMouseOver 触发器进行描边值更改：** 让我们将一些其他操作相关联<xref:System.Windows.UIElement.IsMouseOver%2A>触发器。 尽管仍录制，切换您的选择从**glassCube**到**outerRectangle**。 然后设置<xref:System.Windows.Shapes.Shape.Stroke%2A>的**outerRectangle**到"{DynamicResource {x： 静态 SystemColors.HighlightBrushKey}}"的自定义表达式。 这将设置<xref:System.Windows.Shapes.Shape.Stroke%2A>到典型突出显示使用按钮的颜色。 按 f5 键来查看当你将鼠标置于按钮上的效果。  
  
     ![如何将笔画设置为突出显示颜色](./media/custom-button-blend-ismousedoverpropertytrigger3.png "custom_button_blend_IsMousedOverPropertyTrigger3")  
  
5.  **IsMouseOver 触发模糊的文本：** 让我们将关联到一个更多操作<xref:System.Windows.UIElement.IsMouseOver%2A>属性触发器。 使玻璃出现其上方时显示有点模糊按钮的内容。 若要执行此操作，我们可以应用模糊<xref:System.Windows.Media.Effects.BitmapEffect>到<xref:System.Windows.Controls.ContentPresenter>(**myContentPresenter**)。  
  
     ![如何使按钮内容变得模糊](./media/custom-button-blend-propertytriggerwithbitmapeffect.png "custom_button_blend_PropertyTriggerWithBitMapEffect")  
  
    > [!NOTE]
    >  若要返回**属性面板**回其是你之前的搜索<xref:System.Windows.Media.Effects.BitmapEffect>，清除从文本**搜索框**。  
  
     此时，我们使用了属性触发器与多个关联的操作时将鼠标指针进入和离开按钮区域创建突出显示行为。 另一个按钮的典型行为是突出显示具有焦点时 （如后单击它）。 我们可以通过添加另一个属性触发器中添加此类行为<xref:System.Windows.UIElement.IsFocused%2A>属性。  
  
6.  **创建 IsFocused 属性触发器：** 使用相同的过程<xref:System.Windows.UIElement.IsMouseOver%2A>（请参阅本部分中的第一步），创建另一个属性触发器<xref:System.Windows.UIElement.IsFocused%2A>属性。 虽然**触发器录制已打开**，到触发器中添加下列操作：  
  
    -   **glassCube**获取<xref:System.Windows.UIElement.Opacity%2A>的 100%。  
  
    -   **outerRectangle**获取<xref:System.Windows.Shapes.Shape.Stroke%2A>"{DynamicResource {x： 静态 SystemColors.HighlightBrushKey}}"的自定义表达式值。  
  
 作为本演练的最后一步，我们将向按钮添加动画。 将由事件触发这些动画 — 具体而言，<xref:System.Windows.UIElement.MouseEnter>和<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件。  
  
#### <a name="to-use-event-triggers-and-animations-to-add-interactivity"></a>若要使用事件触发器和动画添加交互性  
  
1.  **创建 MouseEnter 事件触发器：** 添加新的事件触发器，然后选择<xref:System.Windows.UIElement.MouseEnter>作为要在触发器中使用的事件。  
  
     ![如何创建 MouseEnter 事件触发器](./media/custom-button-blend-mouseovereventtrigger.png "custom_button_blend_MouseOverEventTrigger")  
  
2.  **创建动画时间线：** 接下来，将关联到动画时间线<xref:System.Windows.UIElement.MouseEnter>事件。  
  
     ![如何向事件添加动画时间线](./media/custom-button-blend-mouseovereventtrigger2.png "custom_button_blend_MouseOverEventTrigger2")  
  
     按后**确定**若要创建新的时间线**时间线面板**显示，"时间线录制已打开"设计面板中。 这意味着我们可以开始 （进行动画处理属性更改） 在时间线中记录属性更改。  
  
    > [!NOTE]
    >  您可能需要调整大小窗口和/或面板，以查看它们的显示。  
  
     ![时间线面板](./media/custom-button-blend-mouseovereventtrigger3.png "custom_button_blend_MouseOverEventTrigger3")  
  
3.  **创建关键帧：** 若要创建动画，请选择你想要进行动画处理，创建两个或多个关键帧在时间线，并在这些关键帧，设置您希望该动画之间进行内插的属性值的对象。 下图将引导您完成创建关键帧。  
  
     ![如何创建关键帧](./media/custom-button-blend-mouseovereventtrigger4.png "custom_button_blend_MouseOverEventTrigger4")  
  
4.  **此关键帧处收缩 glassCube:** 所选的第二个关键帧的大小收缩**glassCube**为使用其完整大小的 90%**大小转换**。  
  
     ![如何缩小按钮的大小](./media/custom-button-blend-sizetransform.png "custom_button_blend_SizeTransform")  
  
     按 F5 运行该应用程序。 将鼠标指针移到按钮上方。 请注意，玻璃层会缩小按钮的顶部。  
  
5.  **创建另一个事件触发器，并将不同的动画与它相关联：** 让我们添加一个更多的动画。 使用你用于创建上一个事件触发器动画到类似的步骤：  
  
    1.  创建新的事件触发器使用<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件。  
  
    2.  将相关联的新时间线<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件。  
  
     ![如何创建新的时间线](./media/custom-button-blend-clickeventtrigger1.png "custom_button_blend_ClickEventTrigger1")  
  
    1.  对于此时间线，创建两个关键帧，0.0 秒时的一个，另一个位于 0.3 秒之间。  
  
    2.  在突出显示的 0.3 秒之间的关键帧，设置**旋转变换角度**到 360 度。  
  
     ![如何创建旋转转换](./media/custom-button-blend-rotatetransform.gif "custom_button_blend_RotateTransform")  
  
    1.  按 F5 运行该应用程序。 单击按钮。 请注意，在玻璃层会旋转一周。  
  
## <a name="conclusion"></a>结束语  
 您已经完成了自定义的按钮。 执行此过程通过已应用到应用程序中的所有按钮的按钮模板。 如果将模板编辑模式 （请参阅下图） 并创建多个按钮，会看到它们的外观和行为类似自定义按钮而不是像默认按钮。  
  
 ![自定义按钮模板](./media/custom-button-blend-scopeup.gif "custom_button_blend_ScopeUp")  
  
 ![使用相同的模板的多个按钮](./media/custom-button-blend-createmultiplebuttons.png "custom_button_blend_CreateMultipleButtons")  
  
 按 F5 运行该应用程序。 单击的按钮，并请注意，所有的行为方式相同。  
  
 请记住，虽然您已自定义模板，您设置<xref:System.Windows.Shapes.Shape.Fill%2A>的属性**innerRectangle**并且<xref:System.Windows.Shapes.Shape.Stroke%2A>属性**outerRectangle**到模板背景 （{TemplateBinding 后台}）。 正因为如此，当你设置的各个按钮的背景色时您设置的背景将用于这些相应的属性。 请尝试现在更改背景。 在下图中，使用不同的渐变效果。 因此，尽管模板非常有用的控件类似按钮的整体自定义项，使用模板的控件可以仍可修改看起来彼此不同。  
  
 ![查找其他具有相同模板按钮](./media/custom-button-blend-blendconclusion.jpg "custom_button_blend_BlendConclusion")  
  
 总之，自定义按钮模板的过程中已了解如何执行以下操作在 Microsoft Expression Blend 中：  
  
-   自定义控件的外观。  
  
-   设置属性触发器。 属性触发器是非常有用，因为它们可以用于大多数对象，而不仅仅是控件。  
  
-   设置事件触发器。 事件触发器是非常有用，因为它们可以用于大多数对象，而不仅仅是控件。  
  
-   创建动画。  
  
-   杂项： 创建渐变添加 BitmapEffects，使用转换，并设置对象的基本属性。  
  
## <a name="see-also"></a>请参阅
- [使用 XAML 创建按钮](walkthrough-create-a-button-by-using-xaml.md)
- [样式设置和模板化](styling-and-templating.md)
- [动画概述](../graphics-multimedia/animation-overview.md)
- [使用纯色和渐变进行绘制概述](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [位图效果概述](../graphics-multimedia/bitmap-effects-overview.md)
