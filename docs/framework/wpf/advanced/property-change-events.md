---
title: 属性更改事件
ms.date: 03/30/2017
helpviewer_keywords:
- dependency properties [WPF], change events
- property value changes [WPF]
- change events [WPF], property
- events [WPF], change in property values
- creating property triggers [WPF]
- property change events [WPF], types of
- property change events [WPF]
- property triggers [WPF]
- identifying changed property events [WPF]
- property triggers [WPF], definition of
ms.assetid: 0a7989df-9674-4cc1-bc50-5d8ef5d9c055
ms.openlocfilehash: 2997696a6617bb9c17bb98bba0b352cb27c07896
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57351989"
---
# <a name="property-change-events"></a>属性更改事件
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 定义几个为响应属性值的更改而引发的事件。 该属性通常是依赖项属性。 事件本身有时是路由事件，有时是标准 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 事件。 事件的定义因具体情况而异，因为有些属性更改更适于通过元素树路由，而其他属性更改则通常只与属性发生更改的对象有关。  
  
## <a name="identifying-a-property-change-event"></a>标识属性更改事件  
 并非所有报告属性更改的事件都通过签名模式或命名模式显式地标识为属性更改事件。 通常，[!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] 文档中的事件描述会指出事件是否直接与属性值更改相关，以及是否提供属性与事件之间的交叉引用。  
  
### <a name="routedpropertychanged-events"></a>RoutedPropertyChanged 事件  
 某些事件使用显式用于属性更改事件的事件数据类型和委托。 事件数据类型是<xref:System.Windows.RoutedPropertyChangedEventArgs%601>，委托是<xref:System.Windows.RoutedPropertyChangedEventHandler%601>。 事件数据和委托都具有用于在定义处理程序时指定更改属性实际类型的泛型类型参数。 事件数据包含两个属性，<xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A>和<xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>，它们均然后作为类型参数在事件传递数据。  
  
 名称中的“Routed”部分表示属性更改事件注册为路由事件。 路由属性更改事件的好处是，如果子元素（控件的复合部分）上的属性更改了值，控件的顶层可以接收到属性更改事件。 例如，可能会创建控件，其中包含<xref:System.Windows.Controls.Primitives.RangeBase>控件如<xref:System.Windows.Controls.Slider>。 如果的值<xref:System.Windows.Controls.Primitives.RangeBase.Value%2A>在滑块部分的属性更改，你可能想要处理父控件，而不是上一部分所做的更改。  
  
 因为有一个旧值和一个新值，所以很可能使用此事件处理程序作为属性值的验证程序。 但是，这不是大多数属性更改事件的设计意图。 通常，提供这些值是为了能够在代码的其他逻辑领域处理这些值，但实际上，在事件处理程序内更改值并不明智，并且可能导致意外的递归，具体取决于处理程序的实现方式。  
  
 如果您的属性是自定义依赖项属性，或如果您正在使用派生类定义了实例化代码，则多更好地跟踪的机制内置的属性更改[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]属性系统：属性系统回叫<xref:System.Windows.CoerceValueCallback>和<xref:System.Windows.PropertyChangedCallback>。 若要深入了解如何使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统进行验证和强制转换，请参阅[依赖属性回调和验证](dependency-property-callbacks-and-validation.md)和[自定义依赖属性](custom-dependency-properties.md)。  
  
### <a name="dependencypropertychanged-events"></a>DependencyPropertyChanged 事件  
 另一对是属性更改的事件方案的一部分的类型是<xref:System.Windows.DependencyPropertyChangedEventArgs>和<xref:System.Windows.DependencyPropertyChangedEventHandler>。 这些属性更改的事件不会路由；它们是标准 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件。 <xref:System.Windows.DependencyPropertyChangedEventArgs> 是通常的事件数据报告类型，因为它不是派生自<xref:System.EventArgs>;<xref:System.Windows.DependencyPropertyChangedEventArgs>是一种结构，不是类。  
  
 使用事件<xref:System.Windows.DependencyPropertyChangedEventArgs>并<xref:System.Windows.DependencyPropertyChangedEventHandler>比稍微更常见`RoutedPropertyChanged`事件。 使用这些类型的事件的一个示例是<xref:System.Windows.UIElement.IsMouseCapturedChanged>。  
  
 像<xref:System.Windows.RoutedPropertyChangedEventArgs%601>，<xref:System.Windows.DependencyPropertyChangedEventArgs>还报告的属性具有旧的和新值。 此外，关于如何处理这些值的注意事项也同样适用；通常不建议为响应事件而尝试在发送方再次更改值。  
  
## <a name="property-triggers"></a>属性触发器  
 与属性更改事件密切相关的一个概念是属性触发器。 属性触发器是在样式或模板内创建的，通过它可以创建基于分配了属性触发器的属性的值的条件行为。  
  
 属性触发器的属性必须是依赖项属性。 它可以是（且通常是）只读依赖项属性。 判断控件公开的依赖项属性是否至少部分设计为属性触发器的一个好方法是查看属性名称是否以“Is”开头。 采用此命名规则的属性通常是只读的布尔依赖项属性，其属性的主要作用是报告可能与实时 UI 具有因果关系的控件状态，因此它是一个属性触发器候选。  
  
 其中一些属性还具有专用属性更改事件。 例如，属性<xref:System.Windows.UIElement.IsMouseCaptured%2A>具有属性更改事件<xref:System.Windows.UIElement.IsMouseCapturedChanged>。 该属性本身是只读的其值由输入系统调整，并在输入的系统引发<xref:System.Windows.UIElement.IsMouseCapturedChanged>上每次实时更改。  
  
 与真正的属性更改事件相比，使用属性触发器来处理属性更改具有一些限制。  
  
 属性触发器通过完全匹配逻辑来工作。 指定一个属性和一个值，该值指示触发器将执行操作的特定值。例如：`<Setter Property="IsMouseCaptured" Value="true"> ... </Setter>`。 由于此限制，大多数属性触发器用法都将针对布尔属性或者采用专用枚举值的属性，其可能值范围是可管理的，足以为每种情况定义一个触发器。 或者属性触发器可能仅仅用于特殊值，例如，当项计数达到零，却没有触发器来处理当属性值再次从零变为其他值（此处可能需要代码事件处理程序，或者当值不为零时再次从触发器状态切换回来的默认行为，而非针对所有情况的触发器）。  
  
 属性触发器语法与编程中的“if”语句类似。 如果触发器条件为 true，将“执行”属性触发器的“主体”。 属性触发器的“主体”是标记，而不是代码。 该标记被限制为使用一个或多个<xref:System.Windows.Setter>元素来设置该对象的其他属性，其中应用样式或模板。  
  
 若要偏移的具有各种可能的值的属性触发器的"if"条件，通常，最好是使用相同的属性值设置为默认值<xref:System.Windows.Setter>。 这样一来，<xref:System.Windows.Trigger>包含的 setter 将具有优先权，如果触发器条件为 true，并<xref:System.Windows.Setter>这是在不<xref:System.Windows.Trigger>将具有优先权，只要触发器条件为 false。  
  
 属性触发器通常适合于一个或多个外观属性应基于同一元素的其他属性的状态而更改的情况。  
  
 若要深入了解属性触发器，请参阅[样式设置和模板化](../controls/styling-and-templating.md)。  
  
## <a name="see-also"></a>请参阅
- [路由事件概述](routed-events-overview.md)
- [依赖项属性概述](dependency-properties-overview.md)
