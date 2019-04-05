---
title: XAML 资源
ms.date: 03/30/2017
helpviewer_keywords:
- reusing resources [WPF]
- resources [WPF], reusing
- reusing commonly defined objects [WPF]
- XAML [WPF], reusing resources
ms.assetid: 91580b89-a0a8-4889-aecb-fddf8e63175f
ms.openlocfilehash: f5d6ae2d21058e7e6dd9fa9736800237082766d1
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57364744"
---
# <a name="xaml-resources"></a>XAML 资源
资源是可以在应用程序中的不同位置重复使用的对象。 资源的示例包括画笔和样式。 本概述介绍如何使用中的资源[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。 此外可以创建并使用代码，或者通过互换使用代码访问资源和[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。 有关详细信息，请参阅[资源和代码](resources-and-code.md)。  
  
> [!NOTE]
>  本主题中所述的资源文件是不同的资源文件中所述[WPF 应用程序资源、 内容和数据文件](../app-development/wpf-application-resource-content-and-data-files.md)和不同于嵌入或链接的资源中所述[管理应用程序资源 (.NET)](/visualstudio/ide/managing-application-resources-dotnet)。  
  
  
<a name="usingresources"></a>   
## <a name="using-resources-in-xaml"></a>在 XAML 中使用资源  
 下面的示例定义<xref:System.Windows.Media.SolidColorBrush>作为页面的根元素上的资源。 该示例然后引用的资源，并使用它来设置多个子元素，其中包括的属性<xref:System.Windows.Shapes.Ellipse>、 一个<xref:System.Windows.Controls.TextBlock>，和一个<xref:System.Windows.Controls.Button>。  
  
 [!code-xaml[FEResourceSH_snip#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xaml)]  
  
 每个框架级元素 (<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>) 具有<xref:System.Windows.FrameworkElement.Resources%2A>属性，它是包含资源的属性 (作为<xref:System.Windows.ResourceDictionary>) 某个资源定义。 您可以在任意元素上定义资源。 但是，资源最常定义在根元素，它是<xref:System.Windows.Controls.Page>在示例中。  
  
 资源字典中的每个资源都必须具有唯一键。 在标记中定义的资源，则指定通过唯一键[X:key 指令](../../xaml-services/x-key-directive.md)。 通常情况下，这个键是一个字符串；但是，也可使用相应的标记扩展将其设置为其他对象类型。 非字符串键用于资源使用的某些功能区中[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，尤其是样式、 组件资源和数据样式。  
  
 在定义好资源后，可以使用能够指定键名称的资源标记扩展语法来引用该资源以用于属性值，例如：  
  
 [!code-xaml[FEResourceSH_snip#KeyNameUsage](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#keynameusage)]  
  
 在前面的示例中，当[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载程序处理值`{StaticResource MyBrush}`的<xref:System.Windows.Controls.Control.Background%2A>属性<xref:System.Windows.Controls.Button>，资源查找逻辑首先检查的资源字典<xref:System.Windows.Controls.Button>元素。 如果<xref:System.Windows.Controls.Button>不具有定义的资源键`MyBrush`（不是; 其资源集合为空），查找接下来检查父元素的<xref:System.Windows.Controls.Button>，这是<xref:System.Windows.Controls.Page>。 因此，当您定义资源上<xref:System.Windows.Controls.Page>根元素，在逻辑树中的所有元素<xref:System.Windows.Controls.Page>可以访问它，并可以重复使用相同的资源，为设置任何属性的值时，接受<xref:System.Type>的资源表示。 在上一示例中，相同`MyBrush`资源设置两个不同的属性：<xref:System.Windows.Controls.Control.Background%2A>的<xref:System.Windows.Controls.Button>，和<xref:System.Windows.Shapes.Shape.Fill%2A>的<xref:System.Windows.Shapes.Rectangle>。  
  
<a name="staticdynamic"></a>   
## <a name="static-and-dynamic-resources"></a>静态和动态资源  
 资源可以作为静态资源或动态资源加以引用。 这是通过使用任一[StaticResource 标记扩展](staticresource-markup-extension.md)或[DynamicResource 标记扩展](dynamicresource-markup-extension.md)。 标记扩展是一项功能[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]使您可以通过使用标记扩展来处理属性字符串，并返回到该对象指定的对象引用由此[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载程序。 有关标记扩展行为的详细信息，请参阅[标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)。  
  
 当使用标记扩展时，通常会以字符串的形式提供一个或多个参数，这些参数由该特定标记扩展来处理，而不是在所设置属性的上下文中进行计算。 [StaticResource 标记扩展](staticresource-markup-extension.md)通过查找所有可用的资源字典中的键的值来处理键。 这个操作会在加载期间执行；执行时，加载进程需要分配采用静态资源引用的属性值。 [DynamicResource 标记扩展](dynamicresource-markup-extension.md)改为进程通过创建一个表达式，并且该表达式的键会一直保持未计算直到实际运行该应用程序，在这段时间表达式进行计算，并提供一个值。  
  
 在引用某个资源时，下列注意事项可能会对于使用静态资源引用还是使用动态资源引用产生影响：  
  
-   如何为应用程序创建资源的整体设计 (每页上，在应用程序中，在宽松[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，在资源的唯一程序集中)。  
  
-   应用程序的功能：实时更新资源是应用程序的要求之一吗?  
  
-   该资源引用类型的相应查找行为。  
  
-   特定的属性或资源类型，以及这些类型的本机行为。  
  
### <a name="static-resources"></a>静态资源  
 在以下情况下，最适合使用静态资源引用：  
  
-   所采用的应用程序设计将其所含的大多数资源都集中到了页面级或应用程序级资源字典中。 静态资源引用不会基于运行时行为（如重载页面）重新进行计算，因此可以通过以下方式在一定程度上提高性能：当资源和所采用的应用程序设计无需使用大量动态资源引用时，就避免使用。  
  
-   设置不在属性的值<xref:System.Windows.DependencyObject>或<xref:System.Windows.Freezable>。  
  
-   正在创建的资源字典将编译成 DLL，并将打包为应用程序的一部分或在应用程序间共享。  
  
-   正在为自定义控件创建主题，并定义要在主题中使用的资源。 在这种情况下，通常不希望执行动态资源引用查找行为，而是希望执行静态资源引用行为，以确保查找可预测且自包含到主题中。 使用动态资源引用时，即使主题中的引用会保持未计算状态直至运行时，且主题可能会得到应用，但某个本地元素仍会重新定义主题正尝试引用的键，并且该本地元素在查找期间会排在主题前面。 如果发生这种情况，主题的行为将偏离预期方式。  
  
-   正在使用资源设置大量依赖属性。 依赖属性会通过属性系统启用有效值缓存功能；因此，如果为可在加载时进行计算的依赖属性提供了值，则该依赖属性不必检查是否存在重新计算的表达式并可返回上一个有效值。 此项技术可以提高性能。  
  
-   你想要为所有使用者更改基础资源，或者你想要使用的每个使用者维护单独的可写实例[x： 共享属性](../../xaml-services/x-shared-attribute.md)。  
  
#### <a name="static-resource-lookup-behavior"></a>静态资源查找行为  
  
1.  查找进程在用于设置属性的元素所定义的资源字典中查找请求的键。  
  
2.  查找进程随后会向上遍历逻辑树，以查找父元素及其资源字典。 直至到达根元素，遍历操作才会停止。  
  
3.  接下来，将检查应用程序资源。 应用程序的资源是由定义的资源字典中的这些资源<xref:System.Windows.Application>对象在[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序。  
  
 从资源字典中进行的静态资源引用必须引用已在资源引用前进行过词法定义的资源。 静态资源引用无法解析前向引用。 因此，如果使用静态资源引用，则必须对资源字典的结构进行设计，以便在每个相应资源字典的开头或临近位置定义要按资源使用的资源。  
  
 静态资源查找可以扩展到主题，或系统资源，但支持此功能只是因为[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载程序延迟了请求。 为了让页面加载时的运行时主题正确地应用至该应用程序，这种延迟是必需的。 但是，如果某些键已知仅存在于主题中或属于系统资源，则建议不要使用针对这类键的静态资源引用。 这是因为如果用户实时更改主题，此类引用不会重新计算。 请求主题或系统资源时，动态资源引用更为可靠。 例外情况是当主题元素自身请求另一个资源。 出于上述原因，这些引用应该是静态资源引用。  
  
 因找不到静态资源引用而引发的异常行为各不相同。 如果资源被延迟，则异常会在运行时发生。 如果资源未延迟，则异常会在加载时发生。  
  
### <a name="dynamic-resources"></a>动态资源  
 在以下情况下，最适合使用动态资源：  
  
-   资源的值取决于直到运行时才能获悉的条件。 这包括系统资源或用户可设置的资源。 例如，可以创建引用系统属性的 setter 值，如公开<xref:System.Windows.SystemColors>， <xref:System.Windows.SystemFonts>，或<xref:System.Windows.SystemParameters>。 这些值是真正的动态值，因为它们最终来自用户和操作系统的运行时环境。 或许还拥有可能会发生变化的应用程序级主题，而页面级资源访问也必须捕获其中的变化。  
  
-   正在为自定义控件创建或引用主题样式。  
  
-   你想要调整的内容<xref:System.Windows.ResourceDictionary>应用程序生存期内。  
  
-   拥有存在相互依赖关系且可能需要进行前向引用的复杂资源结构。 静态资源引用不支持前向引用，但动态资源引用却支持，因为该资源不需要进行计算，直到运行时，并且前向引用是不相关的概念。  
  
-   从编译或工作集的角度来看，所引用的资源特别大，而且该资源在页面加载时可能不会立即使用。 静态资源引用总是从加载[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]加载页面时; 但是，动态资源引用不实际使用之前未加载。  
  
-   所创建样式中的 Setter 值可能来自受主题或其他用户设置影响的其他值。  
  
-   正在将资源应用于可能会在应用程序生存期内在逻辑树中重定父级的元素。 父级更改后，资源查找范围也可能会随之更改；因此，如果希望重定父级的元素的资源基于新范围重新进行计算，请始终使用动态资源引用。  
  
#### <a name="dynamic-resource-lookup-behavior"></a>动态资源查找行为  
 动态资源引用的资源查找行为与在代码中的查找行为，如果您调用<xref:System.Windows.FrameworkElement.FindResource%2A>或<xref:System.Windows.FrameworkElement.SetResourceReference%2A>。  
  
1.  查找进程在用于设置属性的元素所定义的资源字典中查找请求的键。  
  
    -   如果该元素定义<xref:System.Windows.FrameworkElement.Style%2A>属性，<xref:System.Windows.Style.Resources%2A>中的字典<xref:System.Windows.Style>检查。  
  
    -   如果该元素定义<xref:System.Windows.Controls.Control.Template%2A>属性，<xref:System.Windows.FrameworkTemplate.Resources%2A>中的字典<xref:System.Windows.FrameworkTemplate>检查。  
  
2.  查找进程随后会向上遍历逻辑树，以查找父元素及其资源字典。 直至到达根元素，遍历操作才会停止。  
  
3.  接下来，将检查应用程序资源。 应用程序的资源是由定义的资源字典中的这些资源<xref:System.Windows.Application>对象在[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序。  
  
4.  在主题资源字典中查找当前处于活动状态的主题。 如果主题在运行时发生更改，则会重新计算值。  
  
5.  检查系统资源。  
  
 异常行为（如果有）各不相同：  
  
-   如果请求的资源的<xref:System.Windows.FrameworkElement.FindResource%2A>调用，但未找到，则引发异常。  
  
-   如果请求的资源的<xref:System.Windows.FrameworkElement.TryFindResource%2A>调用，但未找到，会引发任何异常，但返回的值是`null`。 如果要设置的属性不接受`null`，则仍可能会引发更深的异常 （这取决于要设置的单个属性）。  
  
-   如果通过中的动态资源引用请求了资源[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，和未找到，则行为取决于常规属性系统中，但常规行为是像在资源所在的级别发生任何属性设置操作。 例如，如果尝试使用无法计算的资源来设置个别按钮元素上的背景，则值设置操作不会产生任何结果，但是有效的值可能仍来自属性系统和值优先级中的其他参与者。 例如，背景值可能仍来自在本地定义的某个按钮样式，或来自主题样式。 对于并非由主题样式定义的属性，资源计算失败后的有效值可能来自属性元数据中的默认值。  
  
#### <a name="restrictions"></a>限制  
 动态资源引用存在一些重要限制。 必须至少满足以下条件之一：  
  
-   要设置的属性必须是属性上<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>。 属性必须为后盾<xref:System.Windows.DependencyProperty>。  
  
-   中的值是引用<xref:System.Windows.Style> <xref:System.Windows.Setter>。  
  
-   要设置的属性必须是属性上<xref:System.Windows.Freezable>提供的值作为<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>属性，或<xref:System.Windows.Setter>值。  
  
 因为要设置的属性必须是<xref:System.Windows.DependencyProperty>或<xref:System.Windows.Freezable>属性，属性的大多数更改可以传播到 UI，因为属性更改 （更改的动态资源值） 会经由属性系统。 大多数控件都包含逻辑将强制执行控件的另一个布局，如果<xref:System.Windows.DependencyProperty>更改和属性可能会影响布局。 但是，并非所有属性都都会[DynamicResource 标记扩展](dynamicresource-markup-extension.md)作为它们的值保证提供的值中在 UI 中的实时更新的方式。 此功能可能仍会因属性、属性所属的类型，甚至因应用程序的逻辑结果而异。  
  
<a name="stylesimplicitkeys"></a>   
## <a name="styles-datatemplates-and-implicit-keys"></a>样式、数据模板和隐式键  
 前面曾提到中的所有项<xref:System.Windows.ResourceDictionary>必须有一个键。 但是，这并不并不意味着所有资源必须都具有显式`x:Key`。 多种对象类型在定义为资源时都支持隐式键，其键值会与另一属性的值绑定。 这称为隐式键，而`x:Key`属性则为显式键。 任何隐式键都可通过指定显式键来覆盖。  
  
 资源的一个非常重要的方案是在定义时<xref:System.Windows.Style>。 事实上，<xref:System.Windows.Style>由于样式本质上是可供重复使用几乎始终定义为使用的资源字典中的条目。 有关样式的详细信息，请参阅[样式和模板化](../controls/styling-and-templating.md)。  
  
 控件样式可通过隐式键来创建和引用。 用于定义控件默认外观的主题样式依赖于该隐式键。 从请求它的角度来看，隐式键是<xref:System.Type>控件本身。 从资源定义的角度来看，隐式键是<xref:System.Windows.Style.TargetType%2A>的样式。 因此，如果要创建自定义控件的主题，现有主题样式，即创建进行交互的样式不需要指定[X:key 指令](../../xaml-services/x-key-directive.md)为此， <xref:System.Windows.Style>。 另外，如果想要使用主题样式，则根本无需指定任何样式。 例如，以下样式定义的工作原理，即使<xref:System.Windows.Style>资源似乎不具有键：  
  
 [!code-xaml[FEResourceSH_snip#ImplicitStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#implicitstyle)]  
  
 该样式实际上有一个键： 隐式键`typeof(` <xref:System.Windows.Controls.Button> `)`。 在标记中，可以指定<xref:System.Windows.Style.TargetType%2A>直接作为类型名称 (或者可以根据需要使用[{x: Type...}](../../xaml-services/x-type-markup-extension.md) 若要返回<xref:System.Type>。  
  
 通过使用的默认主题样式机制[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，为运行时样式的应用样式<xref:System.Windows.Controls.Button>页上，即使<xref:System.Windows.Controls.Button>本身不会尝试指定其<xref:System.Windows.FrameworkElement.Style%2A>属性或特定资源引用的样式。 比主题字典样式，使用相同键的主题字典样式位于查找序列中先前找到的页中定义的样式。 您可能只需指定`<Button>Hello</Button>`页上，使用定义的样式中的任意位置<xref:System.Windows.Style.TargetType%2A>的`Button`会应用于该按钮。 如果需要，可以仍显式键使用类型值与相同的样式<xref:System.Windows.Style.TargetType%2A>、 清楚起见，在您的标记，但这是可选的。  
  
 如果不在控件上适用样式的隐式键<xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A>是`true`(另请注意，<xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A>可能设置为本机行为对于控件类中，而不是显式的控件实例的一部分)。 此外，为了支持派生的类应用场景的隐式键，控件必须重写<xref:System.Windows.FrameworkElement.DefaultStyleKey%2A>(作为的一部分提供的所有现有控件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]执行此操作)。 有关样式、 主题和控件设计的详细信息，请参阅[控件的设计准则的指导原则](../controls/guidelines-for-designing-stylable-controls.md)。  
  
 <xref:System.Windows.DataTemplate> 还有一个隐式键。 隐式键<xref:System.Windows.DataTemplate>是<xref:System.Windows.DataTemplate.DataType%2A>属性值。 <xref:System.Windows.DataTemplate.DataType%2A> 也可以指定为的类型名称而不是使用显式[{x: Type...}](../../xaml-services/x-type-markup-extension.md). 有关详细信息，请参阅[数据模板化概述](../data/data-templating-overview.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.ResourceDictionary>
- [应用程序资源](optimizing-performance-application-resources.md)
- [资源和代码](resources-and-code.md)
- [定义和引用资源](how-to-define-and-reference-a-resource.md)
- [应用程序管理概述](../app-development/application-management-overview.md)
- [x:Type 标记扩展](../../xaml-services/x-type-markup-extension.md)
- [StaticResource 标记扩展](staticresource-markup-extension.md)
- [DynamicResource 标记扩展](dynamicresource-markup-extension.md)
