---
title: Freezable 对象概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Freezable objects [WPF], description
- unfreezing Freezable objects [WPF]
- classes [WPF], Freezable
ms.assetid: 89c71692-4f43-4057-b611-67c6a8a863a2
ms.openlocfilehash: 9331c892b0c0abccf2ea8700d46fa4180a7225ed
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57375839"
---
# <a name="freezable-objects-overview"></a>Freezable 对象概述
本主题介绍如何有效地使用和创建<xref:System.Windows.Freezable>对象，它们提供特殊功能，可帮助提高应用程序性能。 Freezable 对象的示例包括画笔、 笔、 转换、 几何和动画。  
  
<a name="whatisafreezable"></a>   
## <a name="what-is-a-freezable"></a>什么是 Freezable？  
 一个<xref:System.Windows.Freezable>是一种特殊的对象，它有两种状态： 解冻和冻结。 当未冻结，<xref:System.Windows.Freezable>看起来就像任何其他对象的行为。 当冻结，<xref:System.Windows.Freezable>无法再进行修改。  
  
 一个<xref:System.Windows.Freezable>提供了<xref:System.Windows.Freezable.Changed>事件，以通知观察者的对对象进行任何修改。 冻结<xref:System.Windows.Freezable>可以提高其性能，因为它不再需要更改通知而消耗资源。 冻结<xref:System.Windows.Freezable>还可以在时未冻结的线程之间共享<xref:System.Windows.Freezable>不能。  
  
 尽管<xref:System.Windows.Freezable>类具有许多应用程序，最<xref:System.Windows.Freezable>中的对象[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]与图形子系统相关。  
  
 <xref:System.Windows.Freezable>类可以容易地使用某些图形系统对象，并有助于提高应用程序性能。 继承的类型的示例<xref:System.Windows.Freezable>包括<xref:System.Windows.Media.Brush>， <xref:System.Windows.Media.Transform>，和<xref:System.Windows.Media.Geometry>类。 因为它们包含非托管的资源，系统必须监视这些对象的修改，并对原始对象的更改时，然后更新其相应的非托管的资源。 即使你实际上无需修改图形系统对象，系统必须仍需花一些资源来监视对象，以防对其进行更改。  
  
 例如，假设您创建<xref:System.Windows.Media.SolidColorBrush>画笔，并使用它来绘制按钮的背景。  
  
 [!code-csharp[freezablesample_procedural#FrozenExamplePart1](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart1)]
 [!code-vb[freezablesample_procedural#FrozenExamplePart1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart1)]  
  
 当呈现该按钮时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]图形子系统使用您提供要绘制的一组像素，若要创建一个按钮的外观的信息。 尽管使用纯色画笔来描述应如何绘制按钮，但纯色画笔实际上不会进行绘制。 图形系统将生成用于按钮和画笔，快速、 低级别对象并且在屏幕实际显示这些对象。  
  
 如果您打算修改画笔，这些低级别对象需要重新生成。 Freezable 类是什么使画笔能够以查找其相应的生成的低级别对象，并且它发生更改时更新它们。 画笔时启用此功能，则称其"未冻结。"  
  
 Freezable 的<xref:System.Windows.Freezable.Freeze%2A>方法使您能够禁用此自我更新功能。 此方法可用于使画笔变为"冻结"或变为不可修改。  
  
> [!NOTE]
>  不是每个 Freezable 对象可以被冻结。 若要避免引发<xref:System.InvalidOperationException>，检查 Freezable 对象的值<xref:System.Windows.Freezable.CanFreeze%2A>属性来确定是否它可以冻结然后再尝试冻结它。  
  
 [!code-csharp[freezablesample_procedural#FrozenExamplePart2](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#frozenexamplepart2)]
 [!code-vb[freezablesample_procedural#FrozenExamplePart2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#frozenexamplepart2)]  
  
 当不再需要进行修改的 freezable 时，冻结它提供性能优势。 如果要冻结的画笔在此示例中，图形系统将不再需要监视的更改。 图形系统还可以进行其他优化，因为它知道画笔不会更改。  
  
> [!NOTE]
>  为方便起见，freezable 对象保持未冻结，除非显式冻结。  
  
<a name="frozenfreezables"></a>   
## <a name="using-freezables"></a>使用的可冻结对象  
 使用解冻 freezable 就像使用任何其他类型的对象。 在下面的示例中，颜色<xref:System.Windows.Media.SolidColorBrush>从黄色更改为红色后它用于绘制按钮背景。 图形系统来自动更改按钮从黄色为红色的下次刷新屏幕时在后台工作。  
  
 [!code-csharp[freezablesample_procedural#UnFrozenExampleShort](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#unfrozenexampleshort)]
 [!code-vb[freezablesample_procedural#UnFrozenExampleShort](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#unfrozenexampleshort)]  
  
### <a name="freezing-a-freezable"></a>冻结 Freezable  
 若要使<xref:System.Windows.Freezable>变为不可修改，则调用其<xref:System.Windows.Freezable.Freeze%2A>方法。 冻结包含 freezable 对象的对象，这些对象也会冻结起来。 例如，如果冻结<xref:System.Windows.Media.PathGeometry>，数字和其包含的段会被冻结。  
  
 Freezable**不能**被冻结，如果以下任何条件成立：  
  
-   它具有经过动画处理或数据绑定属性。  
  
-   它具有由动态资源设置的属性。 (请参阅[XAML 资源](xaml-resources.md)动态资源有关的详细信息。)  
  
-   它包含<xref:System.Windows.Freezable>不能冻结的子对象。  
  
 如果这些条件都为 false，并且不打算修改<xref:System.Windows.Freezable>，则应冻结其获得前面所述的性能优势。  
  
 一旦调用 freezable 的<xref:System.Windows.Freezable.Freeze%2A>方法，它无法再进行修改。 尝试修改的冻结对象会导致<xref:System.InvalidOperationException>引发。 下面的代码引发异常，因为我们试图修改画笔后已被冻结。  
  
 [!code-csharp[freezablesample_procedural#ExceptionExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#exceptionexample)]
 [!code-vb[freezablesample_procedural#ExceptionExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#exceptionexample)]  
  
 若要避免此异常，可以使用<xref:System.Windows.Freezable.IsFrozen%2A>方法，以确定是否<xref:System.Windows.Freezable>处于冻结状态。  
  
 [!code-csharp[freezablesample_procedural#CheckIsFrozenExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#checkisfrozenexample)]
 [!code-vb[freezablesample_procedural#CheckIsFrozenExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#checkisfrozenexample)]  
  
 在前面的代码示例中，可修改副本已冻结的对象使用的<xref:System.Windows.Freezable.Clone%2A>方法。 下一节讨论了更详细地克隆。  
  
 **请注意**因为冻结 freezable 不能进行动画处理时，动画系统将自动创建的可修改克隆冻结<xref:System.Windows.Freezable>对象时尝试与它们进行动画处理<xref:System.Windows.Media.Animation.Storyboard>。 若要消除开销引起的克隆的性能，请将解冻如果你想要对其进行动画处理的对象。 有关使用演示图板进行动画处理的详细信息，请参阅[情节提要概述](../graphics-multimedia/storyboards-overview.md)。  
  
### <a name="freezing-from-markup"></a>从标记冻结  
 若要冻结<xref:System.Windows.Freezable>对象声明在标记中，您使用`PresentationOptions:Freeze`属性。 在以下示例中，<xref:System.Windows.Media.SolidColorBrush>声明为页面资源和冻结。 然后使用来设置按钮的背景。  
  
 [!code-xaml[FreezableSample#FreezeFromMarkupWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/FreezableSample/CS/FreezeFromMarkupExample.xaml#freezefrommarkupwholepage)]  
  
 若要使用`Freeze`属性，则必须映射到演示文稿选项命名空间： `http://schemas.microsoft.com/winfx/2006/xaml/presentation/options`。 `PresentationOptions` 是映射此命名空间的建议的前缀：  
  
```  
xmlns:PresentationOptions="http://schemas.microsoft.com/winfx/2006/xaml/presentation/options"   
```  
  
 因为并非所有 XAML 读取器都识别此特性，建议你使用[mc: Ignorable 特性](mc-ignorable-attribute.md)标记`Presentation:Freeze`为可忽略属性：  
  
```  
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
mc:Ignorable="PresentationOptions"  
```  
  
 有关详细信息，请参阅[mc: Ignorable 特性](mc-ignorable-attribute.md)页。  
  
### <a name="unfreezing-a-freezable"></a>"解冻"Freezable  
 一次冻结<xref:System.Windows.Freezable>永远不会修改或解冻; 但是，可以创建使用一个未冻结的克隆<xref:System.Windows.Freezable.Clone%2A>或<xref:System.Windows.Freezable.CloneCurrentValue%2A>方法。  
  
 在以下示例中，使用一个画笔设置按钮的背景，然后冻结该画笔。 冻结的副本组成画笔使用<xref:System.Windows.Freezable.Clone%2A>方法。 克隆是修改并用于将按钮的背景由黄色更改为红色。  
  
 [!code-csharp[freezablesample_procedural#CloneExample](~/samples/snippets/csharp/VS_Snippets_Wpf/freezablesample_procedural/CSharp/freezablesample.cs#cloneexample)]
 [!code-vb[freezablesample_procedural#CloneExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/freezablesample_procedural/visualbasic/freezablesample.vb#cloneexample)]  
  
> [!NOTE]
>  无论使用哪种克隆方法，动画不会被复制到新<xref:System.Windows.Freezable>。  
  
 <xref:System.Windows.Freezable.Clone%2A>和<xref:System.Windows.Freezable.CloneCurrentValue%2A>方法会生成可冻结的深层副本。 如果 freezable 包含其他冻结 freezable 对象，它们是克隆，并且进行可修改的。 例如，如果你克隆的冻结<xref:System.Windows.Media.PathGeometry>使可供修改，数字和其包含的段也复制并进行修改。  
  
<a name="createyourownfreezableclass"></a>   
## <a name="creating-your-own-freezable-class"></a>创建您自己的 Freezable 类  
 从派生的类<xref:System.Windows.Freezable>可以获得以下功能。  
  
-   特殊状态： 只读 （冻结） 和可写状态。  
  
-   线程安全： 的冻结<xref:System.Windows.Freezable>可以在线程之间共享。  
  
-   详细的更改通知：与其他不同<xref:System.Windows.DependencyObject>s，对子属性值更改时 Freezable 对象提供更改通知。  
  
-   简单克隆： Freezable 类已经实现生成深层克隆的几种方法。  
  
 一个<xref:System.Windows.Freezable>是一种<xref:System.Windows.DependencyObject>，因此使用依赖项属性系统。 类属性不一定要依赖项属性，但使用依赖项属性可以减少需要编写，因为代码量<xref:System.Windows.Freezable>类的设计中考虑的依赖属性了。 有关依赖属性系统的详细信息，请参阅[依赖属性概述](dependency-properties-overview.md)。  
  
 每个<xref:System.Windows.Freezable>子类必须重写<xref:System.Windows.Freezable.CreateInstanceCore%2A>方法。 如果您的类的所有数据使用依赖项属性时，您已完成。  
  
 如果您的类包含非依赖项属性数据成员，还必须重写以下方法：  
  
-   <xref:System.Windows.Freezable.CloneCore%2A>  
  
-   <xref:System.Windows.Freezable.CloneCurrentValueCore%2A>  
  
-   <xref:System.Windows.Freezable.GetAsFrozenCore%2A>  
  
-   <xref:System.Windows.Freezable.GetCurrentValueAsFrozenCore%2A>  
  
-   <xref:System.Windows.Freezable.FreezeCore%2A>  
  
 此外必须遵守以下规则用于访问和写入不属于依赖项属性的数据成员：  
  
-   在任何开头[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]读取非依赖项属性数据成员，请调用<xref:System.Windows.Freezable.ReadPreamble%2A>方法。  
  
-   在开始任何 API，它将写入非依赖项属性数据成员时，调用<xref:System.Windows.Freezable.WritePreamble%2A>方法。 (调用后<xref:System.Windows.Freezable.WritePreamble%2A>中[!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)]，不需要进行额外调用<xref:System.Windows.Freezable.ReadPreamble%2A>如果还读取非依赖项属性数据成员。)  
  
-   调用<xref:System.Windows.Freezable.WritePostscript%2A>方法，然后再退出写入非依赖项属性数据成员的方法。  
  
 如果您的类包含的非依赖项属性数据成员<xref:System.Windows.DependencyObject>对象，还必须调用<xref:System.Windows.Freezable.OnFreezablePropertyChanged%2A>方法每次你更改其中一个其值，即使将该成员设置为`null`。  
  
> [!NOTE]
>  务必在开始各个<xref:System.Windows.Freezable>方法通过调用基实现重写。  
  
 有关自定义的示例<xref:System.Windows.Freezable>类，请参阅[自定义动画示例](https://go.microsoft.com/fwlink/?LinkID=159981)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Freezable>
- [自定义动画示例](https://go.microsoft.com/fwlink/?LinkID=159981)
- [依赖项属性概述](dependency-properties-overview.md)
- [自定义依赖属性](custom-dependency-properties.md)
