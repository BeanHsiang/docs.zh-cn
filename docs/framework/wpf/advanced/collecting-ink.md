---
title: WPF 应用程序中收集墨迹
ms.date: 08/15/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ink [WPF], collecting
- InkCanvas element [WPF]
- properties [WPF], DrawingAttributes
- collecting digital ink [WPF]
- digital ink [WPF], collecting
- properties [WPF], DefaultDrawingAttributes
- DefaultDrawingAttributes property [WPF]
ms.assetid: 66a3129d-9577-43eb-acbd-56c147282016
ms.openlocfilehash: 0d0796eae469f8a40e01e3de02c00149eb3f00c7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374669"
---
# <a name="collect-ink"></a>收集墨迹

[Windows Presentation Foundation](../index.md) 平台会收集数字墨迹，这是其功能中的核心部分之一。 本主题讨论用于收集墨迹 Windows Presentation Foundation (WPF) 中的方法。

## <a name="prerequisites"></a>系统必备

若要使用下面的示例，必须首先安装 Visual Studio 和[!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)]。 您还应了解如何编写 WPF 应用程序。 有关如何开始使用 WPF 的详细信息，请参阅[演练：我第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。

## <a name="use-the-inkcanvas-element"></a>使用 InkCanvas 元素

<xref:System.Windows.Controls.InkCanvas?displayProperty=fullName>元素提供 WPF 中收集墨迹的最简单方法。 使用<xref:System.Windows.Controls.InkCanvas>元素可接收和显示墨迹输入。 通常使用触笔（与数字化仪交互产生墨迹笔画）输入墨迹。 此外，还可以使用鼠标代替触笔。 创建的笔画表示为<xref:System.Windows.Ink.Stroke>对象，并且它们可以操作以编程方式和用户输入。 <xref:System.Windows.Controls.InkCanvas>使用户能够选择、 修改或删除现有<xref:System.Windows.Ink.Stroke>。

通过使用 XAML，您可以设置墨迹收集与添加轻松**InkCanvas**到树的元素。 下面的示例添加<xref:System.Windows.Controls.InkCanvas>到 Visual Studio 中创建一个默认 WPF 项目：

[!code-xaml[DigitalInkTopics#6](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#6)]

**InkCanvas**元素还可以包含子元素，这样便可以将墨迹批注功能添加到几乎任何类型的 XAML 元素。 例如，若要将墨迹功能添加到文本元素，只需使其成为子的<xref:System.Windows.Controls.InkCanvas>:

[!code-xaml[DigitalInkTopics#5](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#5)]

添加图像墨迹标记支持操作同样非常简单：

[!code-xaml[DigitalInkTopics#7](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#7)]

### <a name="inkcollection-modes"></a>InkCollection 模式

<xref:System.Windows.Controls.InkCanvas>提供支持，对各种输入模式通过其<xref:System.Windows.Controls.InkCanvas.EditingMode%2A>属性。

### <a name="manipulate-ink"></a>操作墨迹

<xref:System.Windows.Controls.InkCanvas>对多种墨迹编辑操作提供支持。 例如，<xref:System.Windows.Controls.InkCanvas>支持笔后清除图像以及任何其他代码需要将该功能添加到元素。

#### <a name="selection"></a>选择

设置选择模式非常简单，只设置<xref:System.Windows.Controls.InkCanvasEditingMode>属性设置为**选择**。

下面的代码设置值的基础的编辑模式<xref:System.Windows.Forms.CheckBox>:

[!code-csharp[DigitalInkTopics#8](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#8)]
[!code-vb[DigitalInkTopics#8](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#8)]

#### <a name="drawingattributes"></a>DrawingAttributes

使用<xref:System.Windows.Ink.Stroke.DrawingAttributes%2A>要更改墨迹笔画的外观属性。 例如，<xref:System.Windows.Ink.DrawingAttributes.Color%2A>的成员<xref:System.Windows.Ink.DrawingAttributes>设置的颜色呈现的<xref:System.Windows.Ink.Stroke>。

下面的示例更改选定笔画的颜色为红色：

[!code-csharp[DigitalInkTopics#9](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#9)]
[!code-vb[DigitalInkTopics#9](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#9)]

### <a name="defaultdrawingattributes"></a>DefaultDrawingAttributes

<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>属性提供访问权限属性，例如高度、 宽度和要在其中创建的笔画的颜色<xref:System.Windows.Controls.InkCanvas>。 一旦更改<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>，所有将来的笔画输入到<xref:System.Windows.Controls.InkCanvas>呈现使用新的属性值。

还可以修改<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>在代码隐藏文件中，可用于 XAML 语法指定<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>属性。

下面的示例演示如何设置<xref:System.Windows.Ink.DrawingAttributes.Color%2A>属性。 若要使用此代码，创建新的 WPF 项目在 Visual Studio 中名为"HelloInkCanvas"。 中的代码替换*MainWindow.xaml*文件使用以下代码：

[!code-xaml[HelloInkCanvas#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml#1)]

接下来，将以下按钮事件处理程序添加到代码隐藏文件，在 MainWindow 类中：

[!code-csharp[HelloInkCanvas#2](~/samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml.cs#2)]

复制此代码后, 按**F5** Visual Studio 调试器中运行程序中。

请注意如何<xref:System.Windows.Controls.StackPanel>的顶部将按钮置于<xref:System.Windows.Controls.InkCanvas>。 如果您尝试对墨迹上方的按钮，<xref:System.Windows.Controls.InkCanvas>收集和按钮后面呈现墨迹。 这是因为这些按钮是同级的<xref:System.Windows.Controls.InkCanvas>而不是子级。 此外，这些按钮的 Z 顺序较高，所以墨迹呈现在其后面。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Ink.DrawingAttributes>
- <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>
- <xref:System.Windows.Ink>