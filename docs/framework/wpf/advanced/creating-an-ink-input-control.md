---
title: 创建墨迹输入控件
ms.date: 03/30/2017
helpviewer_keywords:
- ink strokes [WPF], managing
- managing ink strokes [WPF]
- ink input control [WPF]
- input from mouse [WPF], accepting
- mouse input [WPF], accepting
- ink [WPF], rendering
- ink strokes [WPF], collecting
- rendering ink [WPF]
- collecting ink strokes [WPF]
- DynamicRenderer objects [WPF]
- StylusPlugIn objects [WPF]
ms.assetid: c31f3a67-cb3f-4ded-af9e-ed21f6575b26
ms.openlocfilehash: 329bad9d5e0fa24f66fbd63def4936cb047e62e3
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378062"
---
# <a name="creating-an-ink-input-control"></a>创建墨迹输入控件
您可以创建自定义控件的动态和静态呈现墨迹。 这就是，根据用户绘制笔划，从而导致出现"流"从 tablet 笔，并在其后显示墨迹添加到该控件，通过触笔从剪贴板粘贴数据或从文件加载的手写内容呈现墨迹。 若要动态呈现墨迹，控件必须使用<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>。 若要以静态方式呈现墨迹，您必须重写触笔事件方法 (<xref:System.Windows.UIElement.OnStylusDown%2A>， <xref:System.Windows.UIElement.OnStylusMove%2A>，并<xref:System.Windows.UIElement.OnStylusUp%2A>) 来收集<xref:System.Windows.Input.StylusPoint>数据，创建的笔画，并将其添加到<xref:System.Windows.Controls.InkPresenter>（它将呈现在控件上的墨迹）。  
  
 本主题包含以下小节：  
  
-   [如何：收集触笔接触点数据并创建墨迹笔画](#CollectingStylusPointDataAndCreatingInkStrokes)  
  
-   [如何：使控件能够接受从鼠标输入](#EnablingYourControlToAcceptInputTromTheMouse)  
  
-   [将它放在一起](#PuttingItTogether)  
  
-   [使用其他插件和 DynamicRenderers](#UsingAdditionalPluginsAndDynamicRenderers)  
  
-   [结束语](#AdvancedInkHandling_Conclusion)  
  
<a name="CollectingStylusPointDataAndCreatingInkStrokes"></a>   
## <a name="how-to-collect-stylus-point-data-and-create-ink-strokes"></a>如何：收集触笔接触点数据并创建墨迹笔画  
 若要创建的控件，可收集和管理墨迹笔画执行以下步骤：  
  
1.  从派生类<xref:System.Windows.Controls.Control>或其中一个类派生自<xref:System.Windows.Controls.Control>，如<xref:System.Windows.Controls.Label>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#20](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
    [!code-csharp[AdvancedInkTopicsSamples#14](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#14)]  
    [!code-csharp[AdvancedInkTopicsSamples#15](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#15)]  
  
2.  添加<xref:System.Windows.Controls.InkPresenter>向类和组<xref:System.Windows.Controls.ContentControl.Content%2A>属性设置为新<xref:System.Windows.Controls.InkPresenter>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#16](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#16)]  
  
3.  附加<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A>的<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>到<xref:System.Windows.Controls.InkPresenter>通过调用<xref:System.Windows.Controls.InkPresenter.AttachVisuals%2A>方法，并添加<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>到<xref:System.Windows.UIElement.StylusPlugIns%2A>集合。 这允许<xref:System.Windows.Controls.InkPresenter>触笔接触点数据收集由控件显示墨迹。  
  
     [!code-csharp[AdvancedInkTopicsSamples#17](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#17)]  
    [!code-csharp[AdvancedInkTopicsSamples#18](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControlSnippets.cs#18)]  
  
4.  重写 <xref:System.Windows.UIElement.OnStylusDown%2A> 方法。  在此方法，来获取调用触笔<xref:System.Windows.Input.Stylus.Capture%2A>。 通过捕获触笔，控件将继续接收<xref:System.Windows.UIElement.StylusMove>和<xref:System.Windows.UIElement.StylusUp>事件，即使在触笔离开控件的边界。 这不是严格必需的但几乎总是需要进行很好的用户体验。 创建一个新<xref:System.Windows.Input.StylusPointCollection>收集<xref:System.Windows.Input.StylusPoint>数据。 最后，添加一组初始<xref:System.Windows.Input.StylusPoint>数据到<xref:System.Windows.Input.StylusPointCollection>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#7](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#7)]  
  
5.  重写<xref:System.Windows.UIElement.OnStylusMove%2A>方法并添加<xref:System.Windows.Input.StylusPoint>数据到<xref:System.Windows.Input.StylusPointCollection>前面创建的对象。  
  
     [!code-csharp[AdvancedInkTopicsSamples#8](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#8)]  
  
6.  重写<xref:System.Windows.UIElement.OnStylusUp%2A>方法创建一个新<xref:System.Windows.Ink.Stroke>与<xref:System.Windows.Input.StylusPointCollection>数据。 添加新<xref:System.Windows.Ink.Stroke>创建到<xref:System.Windows.Controls.InkPresenter.Strokes%2A>的集合<xref:System.Windows.Controls.InkPresenter>并释放触笔捕获。  
  
     [!code-csharp[AdvancedInkTopicsSamples#10](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#10)]  
  
<a name="EnablingYourControlToAcceptInputTromTheMouse"></a>   
## <a name="how-to-enable-your-control-to-accept-input-from-the-mouse"></a>如何：使控件能够接受从鼠标输入  
 如果将前面的控件添加到你的应用程序、 运行它，并使用鼠标输入设备，你会注意到笔画不会保留。 若要持久保存的笔画鼠标用作输入的设备时执行以下步骤：  
  
1.  重写<xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A>并创建一个新<xref:System.Windows.Input.StylusPointCollection>在事件发生时获取鼠标的位置，并创建<xref:System.Windows.Input.StylusPoint>使用点数据，并添加<xref:System.Windows.Input.StylusPoint>到<xref:System.Windows.Input.StylusPointCollection>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#11](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#11)]  
  
2.  重写 <xref:System.Windows.UIElement.OnMouseMove%2A> 方法。 在事件发生时获取鼠标的位置，并创建<xref:System.Windows.Input.StylusPoint>使用点数据。  添加<xref:System.Windows.Input.StylusPoint>到<xref:System.Windows.Input.StylusPointCollection>前面创建的对象。  
  
     [!code-csharp[AdvancedInkTopicsSamples#12](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#12)]  
  
3.  重写 <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A> 方法。  创建一个新<xref:System.Windows.Ink.Stroke>与<xref:System.Windows.Input.StylusPointCollection>数据，并添加新<xref:System.Windows.Ink.Stroke>您创建到<xref:System.Windows.Controls.InkPresenter.Strokes%2A>的集合<xref:System.Windows.Controls.InkPresenter>。  
  
     [!code-csharp[AdvancedInkTopicsSamples#13](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#13)]  
  
<a name="PuttingItTogether"></a>   
## <a name="putting-it-together"></a>将它放在一起  
 下面的示例是当用户使用鼠标或触笔收集墨迹的自定义控件。  
  
 [!code-csharp[AdvancedInkTopicsSamples#20](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#20)]  
[!code-csharp[AdvancedInkTopicsSamples#6](~/samples/snippets/csharp/VS_Snippets_Wpf/AdvancedInkTopicsSamples/CSharp/StylusControl.cs#6)]  
  
<a name="UsingAdditionalPluginsAndDynamicRenderers"></a>   
## <a name="using-additional-plug-ins-and-dynamicrenderers"></a>使用其他插件和 DynamicRenderers  
 在 InkCanvas，如自定义控件可以具有自定义<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>和其他<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>对象。 将它们添加到<xref:System.Windows.UIElement.StylusPlugIns%2A>集合。 顺序<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>中的对象<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>呈现时，会影响墨迹的外观。 假设您有<xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>称为`dynamicRenderer`和自定义<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>调用`translatePlugin`的偏移量从 tablet 笔墨迹。 如果`translatePlugin`是第一个<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>中<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>，和`dynamicRenderer`是第二，当用户移动笔将偏移"流"的墨迹。 如果`dynamicRenderer`第一次，和`translatePlugin`是第二个，墨迹将不会在用户提起笔之前偏移。  
  
<a name="AdvancedInkHandling_Conclusion"></a>   
## <a name="conclusion"></a>结束语  
 可以创建一个控件，可收集和通过重写的触笔事件方法呈现墨迹。 通过创建自己的控件，派生您自己<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>类，并将它们插入到<xref:System.Windows.Input.StylusPlugIns.StylusPlugInCollection>，可以实现与数字墨迹想象几乎任何行为。 你有权<xref:System.Windows.Input.StylusPoint>生成数据时，您可以自定义<xref:System.Windows.Input.Stylus>输入，并根据你的应用程序在屏幕上呈现它。 因为此类低级别访问<xref:System.Windows.Input.StylusPoint>数据，可以实现墨迹收集，并使其具有优化性能的应用程序。  
  
## <a name="see-also"></a>请参阅
- [高级墨迹处理](advanced-ink-handling.md)
- [访问和操作笔输入](https://go.microsoft.com/fwlink/?LinkId=50752&clcid=0x409)
