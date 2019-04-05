---
title: 将路由事件标记为“已处理”和“类处理”
ms.date: 03/30/2017
helpviewer_keywords:
- tunneling events [WPF]
- class listeners [WPF]
- listeners [WPF]
- Preview routed events [WPF]
- instance listeners [WPF]
- events [WPF], bubbling
- suppressing events [WPF]
- routed events [WPF], Preview
- composited controls [WPF]
- events [WPF], tunneling
- routed events [WPF], marking as handled
- controls [WPF], compositing
- events [WPF], suppressing
- bubbling events [WPF]
ms.assetid: 5e745508-4861-4b48-b5f6-5fc7ce5289d2
ms.openlocfilehash: 34bb8c1cde71f6280ae2924a82ddb2efb0efbdf2
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378822"
---
# <a name="marking-routed-events-as-handled-and-class-handling"></a>将路由事件标记为“已处理”和“类处理”
路由事件的处理程序可以在事件数据内将事件标记为已处理。 处理事件将有效地缩短路由。 类处理是一个编程概念，受路由事件支持。 类处理程序有机会在类级别使用处理程序处理特定路由事件，在类的任何实例上存在任何实例处理程序之前调用该处理程序。  
  

  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>系统必备  
 本主题将详细介绍[路由事件概述](routed-events-overview.md)中引入的概念。  
  
<a name="When_to_Mark_Events_as_Handled"></a>   
## <a name="when-to-mark-events-as-handled"></a>何时将事件标记为“已处理”  
 如果设置的值<xref:System.Windows.RoutedEventArgs.Handled%2A>属性设置为`true`在事件路由事件的数据，这被称为"标记处理的事件"。 对于应用程序创作者或者响应现有路由事件或实现新路由事件的控件创建者而言，何时应将路由事件标记为已处理，没有绝对规则。 大多数情形下，路由事件的事件数据中携带的“已处理”概念应当用作一种限定协议，用于自己的应用程序响应 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 中公开的各种路由事件时以及用于任意自定义路由事件。 考虑“已处理”问题的另一种方式为：如果代码以重要且相对完整的方式响应路由事件，则通常应将路由事件标记为已处理。 通常，重要响应不应该超过一个。所谓重要响应，是指对于单个任意路由事件，都需要单独的处理程序实现。 如果需要多个响应，则应通过在单个处理程序内链接的应用程序逻辑实现必要的代码，而不是使用路由事件系统进行转发。 是否“重要”这一概念比较主观，视应用程序或代码而定。 作为一般性指导原则，一些“重要响应”示例包括：设置焦点、修改公共状态、设置影响视觉表示形式的属性以及引发其他新事件。 非重要响应的示例包括：修改私有状态（无视觉影响，或编程表示形式）、记录事件或查看事件参数并选择不响应该事件。  
  
 路由的事件系统行为强调了此"重要响应"模型，用于使用路由事件的处理的状态，因为处理程序中添加[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]或公用签名来<xref:System.Windows.UIElement.AddHandler%2A>不调用以响应路由事件的事件数据已标记为已处理。 您必须经过额外添加处理程序替换`handledEventsToo`参数版本 (<xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>) 若要处理的标记为已由早期参与者处理路由的事件在事件路由。  
  
 在某些情况下，控件本身会将某些路由事件标记为已处理。 已处理的路由事件表示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件作者做出的以下决定：响应路由事件的控件操作是重要的，或者作为控件实现的一部分已完成，并且事件无需进一步处理。 通常，通过为事件添加一个类处理程序，或重写存在于基类上的其中一个类处理程序虚方法，可以完成此操作。 必要时仍然可以应对此事件处理；请参阅本主题后面部分的[通过控件解决事件禁止问题](#WorkingAroundEventSuppressionByControls)。  
  
<a name="Preview_Events_vs__Bubbling_Events_and_Handling"></a>   
## <a name="preview-tunneling-events-vs-bubbling-events-and-event-handling"></a>“预览”（隧道）事件与冒泡事件的对比以及事件处理  
 预览路由事件是指遵循元素树的隧道路由的事件。 命名约定中的“Preview”是指输入事件的一般原则，即预览（隧道）路由事件是在对等的冒泡路由事件之前引发的。 另外，具有隧道和冒泡对的输入路由事件具有截然不同的处理逻辑。 如果隧道/预览路由事件标记为已由事件侦听器处理，则冒泡路由事件将标记为已处理，然而此时冒泡路由事件的任何侦听器尚未接收到该事件。 隧道路由事件和冒泡路由事件在技术层面上是单独的事件，但是它们有意共享相同的事件数据实例以实现此行为。  
  
 任意给定的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类引发其声明的路由事件的方式的内部实现可在隧道路由事件与冒泡路由事件之间建立连接，对于成对的输入路由事件也是如此。 但是除非该类级实现存在，否则共享命名方案的隧道路由事件与冒泡路由事件之间将没有连接：没有上述实现，它们将是两个完全独立的路由事件，不会顺次引发，也不会共享事件数据。  
  
 有关如何在自定义类中实现隧道/冒泡输入路由事件对的详细信息，请参阅[创建自定义路由事件](how-to-create-a-custom-routed-event.md)。  
  
<a name="Class_Handlers_and_Instance_Handlers"></a>   
## <a name="class-handlers-and-instance-handlers"></a>类处理程序和实例处理程序  
 路由事件会考虑事件的两种不同类型的侦听器：类侦听器和实例侦听器。 类侦听器已存在，因为类型具有名为特定<xref:System.Windows.EventManager> [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] ，<xref:System.Windows.EventManager.RegisterClassHandler%2A>，在其静态构造函数，或已重写中的元素的基类的类处理程序虚方法。 实例侦听器是特定类实例/元素，其中一个或多个处理程序已附加为该路由事件调用<xref:System.Windows.UIElement.AddHandler%2A>。 现有[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]路由的事件调用<xref:System.Windows.UIElement.AddHandler%2A>作为的一部分[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]事件包装器添加{}并删除{}的事件，这也是如何实现简单[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]附加的机制启用通过特性语法的事件处理程序。 因此，即使简单[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]用法最终也等同于<xref:System.Windows.UIElement.AddHandler%2A>调用。  
  
 将检查可视化树内的元素是否有注册的处理程序实现。 可能会在整个路由中以该路由事件的路由策略类型所固有的顺序调用处理程序。 例如，冒泡路由事件将首先调用那些附加到引发该路由事件的同一元素的处理程序。 然后，路由事件“冒泡”到下一父元素，以此类推，直到到达应用程序根元素。  
  
 从冒泡路由中的根元素的角度看，如果类处理或者更靠近路由事件源的任意元素调用那些将事件参数标记为正在处理的处理程序，那么就不会调用根元素上的处理程序，这样在到达该根元素之前的事件路由会大大缩短。 不过，路由并未完全停止，因为可以使用仍应调用处理程序的特殊条件来添加处理程序，即使类处理程序或实例处理程序已将路由事件标记为已处理也是如此。 本主题后面部分的[即使在事件标记为已处理时也要添加引发的实例处理程序](#AddingInstanceHandlersthatAreRaisedEvenWhenEventsareMarkedHandled)对此进行了说明。  
  
 在比事件路由更深的级别上，还可能有多个类处理程序处理任意给定的类实例。 这是因为，路由事件的类处理模型使得类层次结构中的所有可能的类都可以针对每个路由事件注册自己的类处理程序。 每个类处理程序都会添加到一个内部存储，当构造应用程序的事件路由时，所有类处理程序都会添加到该事件路由中。 类处理程序按以下顺序添加到路由：最先调用派生程度最高的类处理程序，然后调用每个后续基类中的类处理程序。 通常，不会注册类处理程序以便它们也响应标记为已处理的路由事件。 因此，此类处理机制可提供以下两个选项之一：  
  
-   派生类可以通过添加一个不将路由事件标记为已处理的处理程序，来补充从基类继承的类处理，因为有时会在派生类处理程序之后调用基类处理程序。  
  
-   派生类可以通过添加一个将路由事件标记为已处理的类处理程序，来替换基类中的类处理。 应慎用此方法，因为它可能会更改视觉外观、状态逻辑、输入处理和命令处理等方面原本的基控件设计。  
  
<a name="Class_Handling_of_Routed_Events"></a>   
## <a name="class-handling-of-routed-events-by-control-base-classes"></a>按控件基类进行的路由事件类处理  
 在事件路由中的每个给定元素节点上，类侦听器都有机会在元素的任意实例侦听器之前响应路由事件。 为此，类处理程序有时用于禁止某个特定控件类实现不希望继续传播的路由事件，或者用于提供类的一项功能，即对该路由事件进行特殊处理。 例如，类可能引发特定于其自身的事件，其中包含有关某个用户输入条件在该特定类的上下文中所代表的意义的更多具体信息。 然后，此类实现可能会将较为常规的路由事件标记为已处理。 类处理程序通常添加，以便它们不会调用的路由的事件在其中共享的事件数据已标记为已处理，但对于非典型情况还有<xref:System.Windows.EventManager.RegisterClassHandler%28System.Type%2CSystem.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>注册类处理程序来调用即使路由的事件在签名标记为已处理。  
  
### <a name="class-handler-virtuals"></a>类处理程序虚方法  
 某些元素，尤其是元素，如基<xref:System.Windows.UIElement>，公开空"上 * 事件"和"OnPreview\*事件"其公共路由事件的列表与对应的虚拟方法。 可以重写这些虚方法以便为该路由事件实现类处理程序。 基元素类注册这些虚拟方法，因为对于每个这样的类处理程序路由事件使用<xref:System.Windows.EventManager.RegisterClassHandler%28System.Type%2CSystem.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>如前面所述。 因为无需在静态构造函数中针对每个类型进行特殊初始化，所以 On\*Event 虚方法使得为相关路由事件实现类处理变得简单得多。 例如，可以添加类处理<xref:System.Windows.UIElement.DragEnter>中任何事件<xref:System.Windows.UIElement>通过重写派生类<xref:System.Windows.UIElement.OnDragEnter%2A>虚方法。 在重写内，可以处理路由事件、引发其他事件、启动可能更改实例的元素属性的特定于类的逻辑或上述操作的任意组合。 通常情况下，在此类重写中，即使将事件标记为已处理，也应调用基实现。 强烈建议调用基实现，因为虚方法是在基类上。 从每个虚方法调用基实现的标准受保护虚拟模式实质上会替换和比较路由事件类处理所固有的类似机制，因此可以在任意给定实例上调用类层次结构中所有类的类处理程序，并从派生程度最高的类的处理程序开始，一直继续到基类处理程序。 如果类明确要求更改基类处理逻辑，则应仅忽略基实现调用。 在重写代码之前还是之后调用基实现取决于实现的性质。  
  
#### <a name="input-event-class-handling"></a>输入事件类处理  
 类处理程序虚方法均已注册，只有当存在任何共享事件数据尚未标记为已处理的情况时才调用这些方法。 另外，仅仅对于输入事件而言，隧道和冒泡版本通常是顺次引发的，并且共享事件数据。 对于一对给定的输入事件的类处理程序（其中一个是隧道版本，另一个是冒泡版本），当你可能不希望立即将事件标记为已处理时也需要此项。 如果实现隧道类处理虚方法以便将事件标记为已处理，这将会阻止调用冒泡类处理程序（并阻止调用隧道或冒泡事件的任意正常注册的实例处理程序）。  
  
 节点上的类处理一经完成，就会考虑实例侦听器。  
  
<a name="AddingInstanceHandlersthatAreRaisedEvenWhenEventsareMarkedHandled"></a>   
## <a name="adding-instance-handlers-that-are-raised-even-when-events-are-marked-handled"></a>即使在事件标记为已处理时也要添加引发的实例处理程序  
 <xref:System.Windows.UIElement.AddHandler%2A>方法提供的特定重载，可用于添加处理程序将调用事件系统只要事件到达的处理元素在路由中，即使其他处理程序已调整的事件数据标记，为已处理的事件。 但一般不这样操作。 通常情况下，不论事件是在元素树中的什么位置处理，即使需要多个最终结果，都可以通过编写处理程序来调整可能受事件影响的应用程序代码的各个方面。 另外，通常情况下，需要响应该事件的实际只有一个元素，并且已发生了适当的应用程序逻辑。 但是 `handledEventsToo` 重载适用于某些例外情况，例如元素数或控件复合中的某些其他元素已将事件标记为已处理，但是元素数中较高或较低的其他元素（视路由而定）仍希望调用自己的处理程序。  
  
#### <a name="when-to-mark-handled-events-as-unhandled"></a>何时将已处理事件标记为未处理  
 通常情况下，标记为已处理的路由的事件不应标记未处理 (<xref:System.Windows.RoutedEventArgs.Handled%2A>重新设置为`false`) 甚至由处理程序，对`handledEventsToo`。 不过，某些输入事件具有高级别和低级别两种事件表示形式，当在树中的一个位置看到高级别事件，在另一个位置看到低级别事件时，这两种表示形式可以重叠。 例如，假设其中的子元素侦听高级别键事件如<xref:System.Windows.UIElement.TextInput>父元素侦听低级别事件如时<xref:System.Windows.UIElement.KeyDown>。 如果父元素处理低级别事件，则高级别事件甚至可能在子元素中被禁止，尽管直观看来子元素应该具有处理事件的先机。  
  
 在上述情形下，可能需要针对低级别事件向父元素和子元素中添加处理程序。 子元素处理程序实现可以将低级别事件标记为已处理，但父元素处理程序实现会再次将其设置为未处理，这样树上方的更多元素（以及高级别事件）就可以有机会响应。 这种情形应该非常少见。  
  
<a name="Deliberately_Suppressing_Input_Events_for_Control"></a>   
## <a name="deliberately-suppressing-input-events-for-control-compositing"></a>有意对控件复合禁止输入事件  
 路由事件的类处理主要是用于输入事件和复合控件。 按照定义，复合控件是由多个实际控件或控件基类组成的。 控件作者通常希望合并每个子组件可能引发的所有可能的输入事件，以便将整个控件报告为单事件源。 某些情况下，控件作者可能希望完全禁止来自组件的事件，或者替换上携带更多信息或者指示更具体行为的组件定义的事件。 是一个规范示例立即看到任何组件作者如何[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]<xref:System.Windows.Controls.Button>处理最终会解析为直观的事件，所有按钮都有任何鼠标事件：<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件。  
  
 <xref:System.Windows.Controls.Button>基类 (<xref:System.Windows.Controls.Primitives.ButtonBase>) 派生自<xref:System.Windows.Controls.Control>又又派生自<xref:System.Windows.FrameworkElement>和<xref:System.Windows.UIElement>，并且大部分事件基础结构所需的控件输入的处理，请参阅<xref:System.Windows.UIElement>级别。 具体而言，<xref:System.Windows.UIElement>处理常规<xref:System.Windows.Input.Mouse>处理鼠标光标在其边界内的命中测试和最常见的提供不同的事件的事件按钮的操作，如<xref:System.Windows.UIElement.MouseLeftButtonDown>。 <xref:System.Windows.UIElement> 此外提供了一个空的虚拟<xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A>为注册的类处理程序<xref:System.Windows.UIElement.MouseLeftButtonDown>，和<xref:System.Windows.Controls.Primitives.ButtonBase>将重写它。 同样，<xref:System.Windows.Controls.Primitives.ButtonBase>使用类的处理程序<xref:System.Windows.UIElement.MouseLeftButtonUp>。 中的替代，传递的事件数据，实现标记<xref:System.Windows.RoutedEventArgs>实例为已处理通过设置<xref:System.Windows.RoutedEventArgs.Handled%2A>到`true`，和相同的事件数据，会继续沿路由到其他类处理程序的其余部分和指向实例处理程序或事件资源库。 此外，<xref:System.Windows.Controls.Primitives.ButtonBase.OnMouseLeftButtonUp%2A>重写接下来会引发<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件。 大多数侦听器的最终结果将是<xref:System.Windows.UIElement.MouseLeftButtonDown>并<xref:System.Windows.UIElement.MouseLeftButtonUp>事件"消失"，而是替换为<xref:System.Windows.Controls.Primitives.ButtonBase.Click>，保存更多意义，因为它从真正的按钮和一些不知道此事件源自的事件复合完全拼凑的按钮或其他某个元素。  
  
<a name="WorkingAroundEventSuppressionByControls"></a>   
### <a name="working-around-event-suppression-by-controls"></a>通过控件解决事件禁止问题  
 有时，各个控件内的此事件禁止行为可能会干扰应用程序的事件处理逻辑的某些较为常规的意图。 例如，如果出于某种原因，应用程序有一个处理程序<xref:System.Windows.UIElement.MouseLeftButtonDown>位于应用程序根元素，您会注意到，将不会调用一个按钮上的任意单击鼠标<xref:System.Windows.UIElement.MouseLeftButtonDown>或<xref:System.Windows.UIElement.MouseLeftButtonUp>根级别的处理程序。 事件本身实际上会向上冒泡（同样，事件路由未真正结束，但路由事件系统会在事件标记为已处理后更改其处理程序调用行为）。 当路由的事件到达按钮时，<xref:System.Windows.Controls.Primitives.ButtonBase>类处理标记<xref:System.Windows.UIElement.MouseLeftButtonDown>进行处理，因为它希望替换<xref:System.Windows.Controls.Primitives.ButtonBase.Click>具有更多意义的事件。 因此，任何标准<xref:System.Windows.UIElement.MouseLeftButtonDown>进一步路由将不会调用处理程序。 可以使用两种方法来确保在此情形下会调用处理程序。  
  
 第一项技术是有意添加处理程序使用`handledEventsToo`的签名<xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>。 这种方法的局限性在于用于附加事件处理程序的这种技术只可能来自代码，而不能来自标记。 通过 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 将事件处理程序名称指定为事件特性值的简单语法不能实现此行为。  
  
 第二种技术仅适用于输入事件，其中路由事件的隧道版本和冒泡版本是配对的。 对于这些路由事件，可以改为将处理程序添加到预览/隧道对等路由事件。 假如在应用程序的元素树中的某个上级元素级别附加了 Preview 处理程序，该路由事件将从根开始在路由中传递，所以按钮类处理代码不会截获到该事件。 如果使用此方法，则将任意 Preview 事件标记为已处理时一定要谨慎。 对于与给定的示例<xref:System.Windows.UIElement.PreviewMouseLeftButtonDown>如果标记该事件作为根元素，在处理<xref:System.Windows.RoutedEventArgs.Handled%2A>在处理程序实现中，实际上会禁止<xref:System.Windows.Controls.Primitives.ButtonBase.Click>事件。 这通常不是希望的行为。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.EventManager>
- [预览事件](preview-events.md)
- [创建自定义路由事件](how-to-create-a-custom-routed-event.md)
- [路由事件概述](routed-events-overview.md)
