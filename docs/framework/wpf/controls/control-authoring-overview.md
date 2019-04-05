---
title: 控件创作概述
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], authoring overview
- authoring overview for controls [WPF]
ms.assetid: 3d864748-cff0-4e63-9b23-d8e5a635b28f
ms.openlocfilehash: 2007ee7680707cd1cc9628cc3900ca1068db8678
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57368722"
---
# <a name="control-authoring-overview"></a>控件创作概述
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 控件模型的扩展性极大地减少了创建新控件的需要。 但在某些情况下，仍可能需要创建自定义控件。 本主题讨论可最大限度减少在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中创建自定义控件以及其他控件创作模型的需要的功能。 本主题还演示如何创建新控件。  
  
 
  
<a name="when_to_write_a_new_control"></a>   
## <a name="alternatives-to-writing-a-new-control"></a>编写新控件的替代方法  
 以前，如果要通过现有控件获取自定义体验，只能更改控件的标准属性，例如背景色、边框宽度和字号。 如果希望在这些预定义参数的基础之上扩展控件的外观或行为，则需要创建新控件，常用的方法是继承现有控件并重写负责绘制该控件的方法。  虽然这仍是一种可选方法，但也可以利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的丰富内容模型、样式、模板和触发器来自定义现有的控件。 下表提供了一些示例，演示如何在不创建新控件的情况下使用这些功能来实现一致的自定义体验。  
  
-   **丰富内容。** 很多标准 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件都支持丰富内容。 例如，内容属性的<xref:System.Windows.Controls.Button>属于类型<xref:System.Object>，因此理论上的任何内容都可以显示在<xref:System.Windows.Controls.Button>。  若要使按钮显示图像和文本，可以添加的图像和一个<xref:System.Windows.Controls.TextBlock>到<xref:System.Windows.Controls.StackPanel>，并将分配<xref:System.Windows.Controls.StackPanel>到<xref:System.Windows.Controls.ContentControl.Content%2A>属性。 由于这些控件可以显示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 视觉元素和任意数据，因此，降低了创建新控件或修改现有控件来支持复杂可视化效果的需求。 详细了解的内容模型<xref:System.Windows.Controls.Button>和其他内容中的模型[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，请参阅[WPF 内容模型](wpf-content-model.md)。  
  
-   **样式。** 一个<xref:System.Windows.Style>是表示控件的属性的值的集合。 使用样式可创建所需控件外观和行为的可重用表示形式，而无需编写新控件。 例如，假设您希望的所有你<xref:System.Windows.Controls.TextBlock>控件具有红色 Arial 字体，并且字号为 14。 可以创建一个样式作为资源，并相应设置适当属性。 然后每个<xref:System.Windows.Controls.TextBlock>，您将添加到你的应用程序将具有相同的外观。  
  
-   **数据模板。** 一个<xref:System.Windows.DataTemplate>，可以自定义控件上显示数据的方式。 例如，<xref:System.Windows.DataTemplate>可用于指定数据中的显示方式<xref:System.Windows.Controls.ListBox>。  有关这种情况的示例，请参阅[数据模块化概述](../data/data-templating-overview.md)。  除了自定义的数据，外观<xref:System.Windows.DataTemplate>可以包含 UI 元素，后者可提供很大的灵活性在自定义 Ui。  例如，通过使用<xref:System.Windows.DataTemplate>，可以创建<xref:System.Windows.Controls.ComboBox>中的每个项包含一个复选框。  
  
-   **控件模板。** 中的许多控件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]使用<xref:System.Windows.Controls.ControlTemplate>来定义控件的结构和外观，将控件的外观与控件的功能分隔开来。 您可以极大地更改控件的外观，通过重新定义其<xref:System.Windows.Controls.ControlTemplate>。  例如，假设需要一个看起来像交通信号灯的控件。 此控件具有简单的用户界面和功能。  该控件有三个圆圈，一次只有一个圆圈亮起。 经过考虑之后，您可能会发现<xref:System.Windows.Controls.RadioButton>提供的功能只选择一个时间，但的默认外观<xref:System.Windows.Controls.RadioButton>完全不像交通信号灯上的灯。  因为<xref:System.Windows.Controls.RadioButton>使用的控件模板来定义其外观，很容易重新定义<xref:System.Windows.Controls.ControlTemplate>，使其适合的控件，要求使用单选按钮来制作交通信号灯。  
  
    > [!NOTE]
    >  尽管<xref:System.Windows.Controls.RadioButton>可以使用<xref:System.Windows.DataTemplate>、<xref:System.Windows.DataTemplate>不足在此示例中。  <xref:System.Windows.DataTemplate>定义控件的内容的外观。 情况下<xref:System.Windows.Controls.RadioButton>，内容是圆圈，以指示右侧出现的任何内容是否<xref:System.Windows.Controls.RadioButton>处于选中状态。  在交通信号灯的示例中，单选按钮只需要是可“点亮”的圆圈。 由于交通信号灯的外观要求很大差异的默认外观<xref:System.Windows.Controls.RadioButton>，有必要重新定义<xref:System.Windows.Controls.ControlTemplate>。  一般情况下<xref:System.Windows.DataTemplate>用于定义的内容 （或数据），一个控件，以及一个<xref:System.Windows.Controls.ControlTemplate>用于定义控件的方式。  
  
-   **触发器。** 一个<xref:System.Windows.Trigger>，可动态更改的外观和行为的控件，而无需创建一个新的控件。 例如，假设您有多个<xref:System.Windows.Controls.ListBox>应用程序中的控件，并且希望在每个项<xref:System.Windows.Controls.ListBox>在选中时为粗体和红色。 在第一个想到的可能是创建继承自类<xref:System.Windows.Controls.ListBox>并重写<xref:System.Windows.Controls.Primitives.Selector.OnSelectionChanged%2A>方法来更改外观，所选的项，但更好的方法是将触发器添加到样式的<xref:System.Windows.Controls.ListBoxItem>更改的外观所选的项。 触发器可以更改属性值或根据属性值执行操作。 <xref:System.Windows.EventTrigger>使您能够在事件发生时执行操作。  
  
 有关样式、模板和触发器的详细信息，请参阅[样式设置和模板化](styling-and-templating.md)。  
  
 一般情况下，如果控件可以镜像现有控件的功能，但希望该控件具有不同的外观，则应先考虑是否可以使用本节中讨论的某些方法来更改现有控件的外观。  
  
<a name="models_for_control_authoring"></a>   
## <a name="models-for-control-authoring"></a>控件创作模型  
 通过丰富内容模型、样式、模板和触发器，最大程度地减少创建新控件的需要。 但是，如果确实需要创建新控件，则理解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的不同控件创作模型就显得非常重要。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供三个用于创建控件的常规模型，每个模型都提供不同的功能集和灵活度。 基类的三个模型都<xref:System.Windows.Controls.UserControl>， <xref:System.Windows.Controls.Control>，和<xref:System.Windows.FrameworkElement>。  
  
### <a name="deriving-from-usercontrol"></a>从 UserControl 派生  
 若要创建的控件中的最简单方法[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]是从派生<xref:System.Windows.Controls.UserControl>。 当你生成控件的继承<xref:System.Windows.Controls.UserControl>，将添加到现有的组件<xref:System.Windows.Controls.UserControl>，命名组件，并引用中的事件处理程序[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]。 随后可以在代码中引用命名的元素和定义事件处理程序。 此开发模型与用于在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中开发应用程序的模型非常相似。  
  
 如果生成无误，<xref:System.Windows.Controls.UserControl>可以充分利用丰富的内容、 样式和触发器的优势。 但是，如果控件继承自<xref:System.Windows.Controls.UserControl>，使用您的控件的用户将无法再使用<xref:System.Windows.DataTemplate>或<xref:System.Windows.Controls.ControlTemplate>来自定义其外观。  必须派生自<xref:System.Windows.Controls.Control>类或其派生类之一 (而不<xref:System.Windows.Controls.UserControl>) 创建支持模板的自定义控件。  
  
#### <a name="benefits-of-deriving-from-usercontrol"></a>从 UserControl 派生的优点  
 请考虑从派生<xref:System.Windows.Controls.UserControl>如果所有以下应用：  
  
-   希望采用与生成应用程序相似的方法生成控件。  
  
-   控件仅包含现有组件。  
  
-   无需支持复杂的自定义项。  
  
### <a name="deriving-from-control"></a>从 Control 派生  
 派生自<xref:System.Windows.Controls.Control>类是使用大多数现有的模型[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]控件。 当你创建的控件的继承<xref:System.Windows.Controls.Control>类，您通过使用模板定义其外观。 通过这种方式，可以将运算逻辑从视觉表示形式中分离出来。 您还可以确保 UI 和逻辑分离而不是事件和避免引用元素中的使用命令和绑定<xref:System.Windows.Controls.ControlTemplate>只要有可能。  如果 UI 和控件的逻辑正确分离，您的控件的用户可以重新定义控件的<xref:System.Windows.Controls.ControlTemplate>来自定义其外观。 尽管生成自定义<xref:System.Windows.Controls.Control>不是作为构造简单<xref:System.Windows.Controls.UserControl>，自定义<xref:System.Windows.Controls.Control>提供最大的灵活性。  
  
#### <a name="benefits-of-deriving-from-control"></a>从 Control 派生的优点  
 请考虑从派生<xref:System.Windows.Controls.Control>而不是使用<xref:System.Windows.Controls.UserControl>类如果以下任一情况:  
  
-   你想要通过可自定义控件的外观<xref:System.Windows.Controls.ControlTemplate>。  
  
-   希望控件支持不同的主题。  
  
### <a name="deriving-from-frameworkelement"></a>从 FrameworkElement 派生  
 从派生的控件<xref:System.Windows.Controls.UserControl>或<xref:System.Windows.Controls.Control>依赖于组合现有元素。 对于许多方案，这是一个可接受的解决方案，因为任何对象，它继承自<xref:System.Windows.FrameworkElement>可以是<xref:System.Windows.Controls.ControlTemplate>。 但是，某些时候，简单的元素组合不能满足控件的外观需要。 对于这些方案，使组件基于<xref:System.Windows.FrameworkElement>是正确的选择。  
  
 有两种标准方法，用于生成<xref:System.Windows.FrameworkElement>-基于组件： 直接呈现和自定义元素组合。 直接呈现涉及重写<xref:System.Windows.UIElement.OnRender%2A>方法<xref:System.Windows.FrameworkElement>，并提供<xref:System.Windows.Media.DrawingContext>显式定义组件视觉对象的操作。 这是使用的方法<xref:System.Windows.Controls.Image>和<xref:System.Windows.Controls.Border>。 自定义元素组合涉及到使用类型的对象<xref:System.Windows.Media.Visual>组件的外观。 有关示例，请参阅[使用 DrawingVisual 对象](../graphics-multimedia/using-drawingvisual-objects.md)。 <xref:System.Windows.Controls.Primitives.Track> 是一个示例中的控件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，它使用自定义元素组合。 在同一控件中，也可以混合使用直接呈现和自定义元素组合。  
  
#### <a name="benefits-of-deriving-from-frameworkelement"></a>从 FrameworkElement 派生的优点  
 请考虑从派生<xref:System.Windows.FrameworkElement>如果以下任一情况:  
  
-   希望对控件的外观进行精确控制，而不仅仅是简单的元素组合提供的效果。  
  
-   希望通过定义自己的呈现逻辑来定义控件的外观。  
  
-   你想要在超过可能采用的新颖方式组合现有元素<xref:System.Windows.Controls.UserControl>和<xref:System.Windows.Controls.Control>。  
  
<a name="control_authoring_basics"></a>   
## <a name="control-authoring-basics"></a>控件创作基础知识  
 如前所述，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的最强大功能之一在于，它能够在不需要创建自定义控件的情况下，不只是通过设置控件的基本属性来更改其外观和行为。 样式设置、数据绑定和触发器功能通过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件系统实现。 以下各部分介绍应遵循的一些做法（与创建自定义控件时所用的模型无关），以便自定义控件的用户可以像使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附带的控件一样使用这些功能。  
  
### <a name="use-dependency-properties"></a>使用依赖属性  
 当属性为依赖属性时，可以执行以下操作：  
  
-   在样式中设置该属性。  
  
-   将该属性绑定到数据源。  
  
-   使用动态资源作为该属性的值。  
  
-   对该属性进行动画处理。  
  
 如果希望控件的属性支持以上任一功能，应将该属性实现为依赖属性。 下面的示例通过执行以下操作定义一个名为 `Value` 的依赖属性：  
  
-   定义<xref:System.Windows.DependencyProperty>名为标识符`ValueProperty`作为`public` `static` `readonly`字段。  
  
-   通过调用属性系统注册的属性名称<xref:System.Windows.DependencyProperty.Register%2A?displayProperty=nameWithType>，以指定以下内容：  
  
    -   属性的名称。  
  
    -   属性的类型。  
  
    -   拥有属性的类型。  
  
    -   属性的元数据。 元数据包含该属性的默认值<xref:System.Windows.CoerceValueCallback>和一个<xref:System.Windows.PropertyChangedCallback>。  
  
-   通过实现该属性的 `get` 和 `set` 访问器，定义一个名为 `Value`（与用来注册该依赖属性的名称相同）的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 包装器属性。 请注意，`get`并`set`访问器仅调用<xref:System.Windows.DependencyObject.GetValue%2A>和<xref:System.Windows.DependencyObject.SetValue%2A>分别。 建议依赖项属性的访问器不包含其他逻辑，因为客户端和[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]取值函数和调用可以绕过<xref:System.Windows.DependencyObject.GetValue%2A>和<xref:System.Windows.DependencyObject.SetValue%2A>直接。 例如，如果属性绑定到数据源，则不会调用该属性的 `set` 访问器。  而不是将额外的逻辑添加到 get 和 set 访问器，请使用<xref:System.Windows.ValidateValueCallback>， <xref:System.Windows.CoerceValueCallback>，和<xref:System.Windows.PropertyChangedCallback>委托进行响应或发生更改时检查的值。  有关这些回叫的详细信息，请参阅[依赖属性回叫和验证](../advanced/dependency-property-callbacks-and-validation.md)。  
  
-   定义一种方法<xref:System.Windows.CoerceValueCallback>名为`CoerceValue`。 `CoerceValue` 确保 `Value` 大于或等于 `MinValue` 且小于或等于 `MaxValue`。  
  
-   定义一种方法<xref:System.Windows.PropertyChangedCallback>名为`OnValueChanged`。 `OnValueChanged` 创建<xref:System.Windows.RoutedPropertyChangedEventArgs%601>对象，并准备引发`ValueChanged`路由的事件。 路由事件在下一节中讨论。  
  
 [!code-csharp[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#dependencyproperty)]
 [!code-vb[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#dependencyproperty)]  
  
 有关详细信息，请参阅[自定义依赖属性](../advanced/custom-dependency-properties.md)。  
  
### <a name="use-routed-events"></a>使用路由事件  
 就像依赖属性以附加功能扩展 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性的概念一样，路由事件扩展标准 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件的概念。 在创建新的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件时，将事件实现为路由事件也是一种好方法，因为路由事件支持以下行为：  
  
-   事件可以在多个控件的父级上进行处理。 如果事件是浮升事件，元素树中的单个父级可订阅该事件。 然后，应用程序作者可以使用一个处理程序来响应多个控件的该事件。 例如，如果您的控件是在每个项的一部分<xref:System.Windows.Controls.ListBox>(因为它包含在<xref:System.Windows.DataTemplate>)，应用程序开发人员可以在定义控件的事件的事件处理程序<xref:System.Windows.Controls.ListBox>。 每当其中任何控件发生该事件时，都会调用该事件处理程序。  
  
-   路由的事件可在<xref:System.Windows.EventSetter>，这使应用程序开发人员能够指定的样式中的事件处理程序。  
  
-   路由的事件可在<xref:System.Windows.EventTrigger>，可用于通过对属性进行动画处理[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。 有关详细信息，请参阅 [动画概述](../graphics-multimedia/animation-overview.md)。  
  
 下面的示例通过执行以下操作定义了一个路由事件：  
  
-   定义<xref:System.Windows.RoutedEvent>名为标识符`ValueChangedEvent`作为`public` `static` `readonly`字段。  
  
-   通过调用注册路由的事件<xref:System.Windows.EventManager.RegisterRoutedEvent%2A?displayProperty=nameWithType>方法。 该示例在调用时指定以下信息<xref:System.Windows.EventManager.RegisterRoutedEvent%2A>:  
  
    -   事件名称是 `ValueChanged`。  
  
    -   路由策略是<xref:System.Windows.RoutingStrategy.Bubble>，这意味着首先，调用源 （引发事件的对象） 上的事件处理程序，然后使用上的最近的事件处理程序开始，相继调用源的父元素上的事件处理程序父元素。  
  
    -   事件处理程序的类型是<xref:System.Windows.RoutedPropertyChangedEventHandler%601>、 构造与<xref:System.Decimal>类型。  
  
    -   该事件的所属类型为 `NumericUpDown`。  
  
-   声明一个名为 `ValueChanged` 的公共事件，并包含事件访问器声明。 此示例调用<xref:System.Windows.UIElement.AddHandler%2A>中`add`访问器声明并<xref:System.Windows.UIElement.RemoveHandler%2A>中`remove`访问器声明，以使用[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]事件服务。  
  
-   创建一个名为 `OnValueChanged` 的受保护的虚拟方法，该方法会引发 `ValueChanged` 事件。  
  
 [!code-csharp[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#routedevent)]
 [!code-vb[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#routedevent)]  
  
 有关详细信息，请参阅[路由事件概述](../advanced/routed-events-overview.md)和[创建自定义路由事件](../advanced/how-to-create-a-custom-routed-event.md)。  
  
### <a name="use-binding"></a>使用绑定  
 若要将控件的 UI 与其逻辑分离，请考虑使用数据绑定。 这一点特别重要，如果您通过使用定义控件外观<xref:System.Windows.Controls.ControlTemplate>。 使用数据绑定时，或许可以避免在代码中引用 UI 的特定部分。 它是一个好办法避免引用中的元素<xref:System.Windows.Controls.ControlTemplate>因为当代码引用中的元素<xref:System.Windows.Controls.ControlTemplate>并<xref:System.Windows.Controls.ControlTemplate>已更改，引用的元素需要包含在新<xref:System.Windows.Controls.ControlTemplate>。  
  
 以下示例更新<xref:System.Windows.Controls.TextBlock>的`NumericUpDown`向它分配一个名称，并且在代码中按名称引用该文本框控件。  
  
 [!code-xaml[UserControlNumericUpDownSimple#UIRefMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml#uirefmarkup)]  
  
 [!code-csharp[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml.cs#uirefcode)]
 [!code-vb[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDownSimple/VisualBasic/NumericUpDown.xaml.vb#uirefcode)]  
  
 下面的示例使用绑定来达到相同的目的。  
  
 [!code-xaml[UserControlNumericUpDown#Binding](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml#binding)]  
  
 有关数据绑定的详细信息，请参阅[数据绑定概述](../data/data-binding-overview.md)。  
  
### <a name="design-for-designers"></a>设计器的设计  
 若要在 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] 中获得对自定义 WPF 控件的支持（例如，使用“属性”窗口编辑属性），请遵循以下准则。  有关开发的详细信息[!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]，请参阅[Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)。  
  
#### <a name="dependency-properties"></a>依赖项属性  
 确保实现 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] `get` 和 `set` 访问器，如前面的“使用依赖属性”中所述。 设计器可以使用包装器来检测某个依赖属性是否存在，但与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和控件客户端一样，在获取或设置属性时不需要使用设计器来调用访问器。  
  
#### <a name="attached-properties"></a>附加属性  
 应使用以下准则在自定义控件上实现附加属性：  
  
-   具有`public` `static` `readonly` <xref:System.Windows.DependencyProperty>窗体*PropertyName* `Property`创建使用<xref:System.Windows.DependencyProperty.RegisterAttached%2A>方法。 属性名称传递给<xref:System.Windows.DependencyProperty.RegisterAttached%2A>必须匹配*PropertyName*。  
  
-   实现一对名为`Set`*属性名称*和`Get`*属性名称*的 `public` `static` CLR 方法。 这两种方法应接受派生自的类<xref:System.Windows.DependencyProperty>作为其第一个参数。 `Set`*属性名称*方法还接受其类型与属性的注册数据类型匹配的参数。 `Get`*属性名称* 方法应返回相同类型的值。 如果缺少 `Set`*属性名称*方法，则该属性标记为只读。  
  
-   `Set` *PropertyName*并`Get` *PropertyName*必须直接路由到<xref:System.Windows.DependencyObject.GetValue%2A>和<xref:System.Windows.DependencyObject.SetValue%2A>方法目标依赖对象，分别。 通过调用方法包装器或直接调用目标依赖对象，设计器可以访问附加属性。  
  
 有关附加属性的详细信息，请参阅[附加属性概述](../advanced/attached-properties-overview.md)。  
  
### <a name="define-and-use-shared-resources"></a>定义和使用共享资源  
 可以将控件包含在应用程序所在的程序集中，也可以将控件打包到可在多个应用程序中使用的单独程序集中。 大多数情况下，不管使用什么方法，本主题中讨论的信息都适用。  但有一处差异值得注意。  将控件放入应用程序所在的程序集中时，可以随意向 App.xaml 文件添加全局资源。 但只包含控件的程序集不具有<xref:System.Windows.Application>与其相关的对象，因此 App.xaml 文件不可用。  
  
 当应用程序查找资源时，它会按以下顺序在三个级别进行查找：  
  
1.  元素级别。  
  
     系统从引用该资源的元素开始搜索，接着搜索逻辑父级的资源，依此类推，直至到达根元素。  
  
2.  应用程序级别。  
  
     定义的资源，<xref:System.Windows.Application>对象。  
  
3.  主题级别。  
  
     主题级别的字典存储在名为“Themes”的子文件夹中。  Themes 文件夹中的文件与主题对应。  例如，可能有 Aero.NormalColor.xaml、Luna.NormalColor.xaml、Royale.NormalColor.xaml 等。  可能还有一个名为 generic.xaml 的文件。  当系统在主题级别查找资源时，它会先在特定于主题的文件中查找相应资源，然后在 generic.xaml 中进行查找。  
  
 当控件位于独立于应用程序的程序集中时，必须将全局资源放在元素级别或主题级别。 这两种方法都各有优点。  
  
#### <a name="defining-resources-at-the-element-level"></a>在元素级别定义资源  
 可以通过创建自定义资源字典并将其与控件的资源字典合并，在元素级别定义共享资源。  采用此方法时，可以为资源文件指定任意名称，并且资源文件可以与控件位于同一文件夹中。 元素级别的资源还可以使用简单字符串作为键。 下面的示例创建<xref:System.Windows.Media.LinearGradientBrush>名为 Dictionary1.xaml 的资源文件。  
  
 [!code-xaml[SharedResources#1](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/Dictionary1.xaml#1)]  
  
 定义字典后，需要将其与控件的资源字典合并。  可以使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 或代码执行此操作。  
  
 下面的示例通过使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 合并资源字典。  
  
 [!code-xaml[SharedResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml#2)]  
  
 这种方法的缺点是<xref:System.Windows.ResourceDictionary>引用它每次创建对象。  例如，如果您库中有 10 个自定义控件，并通过使用 XAML 来合并每个控件的共享的资源字典，则创建 10 相同<xref:System.Windows.ResourceDictionary>对象。  您可以避免这种情况创建合并在代码中的资源，并返回结果的静态类<xref:System.Windows.ResourceDictionary>。  
  
 下面的示例创建一个返回共享的类<xref:System.Windows.ResourceDictionary>。  
  
 [!code-csharp[SharedResources#3](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/SharedDictionaryManager.cs#3)]  
  
 下面的示例先在一个自定义控件的构造函数中将共享资源与该控件的资源合并，然后再调用 `InitializeComponent`。  因为`SharedDictionaryManager.SharedDictionary`是一个静态属性，<xref:System.Windows.ResourceDictionary>创建仅一次。 因为资源字典在调用 `InitializeComponent` 前已合并，所以控件可以在它的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件中使用资源。  
  
 [!code-csharp[SharedResources#4](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml.cs#4)]  
  
#### <a name="defining-resources-at-the-theme-level"></a>在主题级别定义资源  
 通过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可以为不同的 Windows 主题创建资源。  作为控件作者，可以为特定主题定义资源，以根据所使用的主题更改控件的外观。 例如的外观<xref:System.Windows.Controls.Button>在 Windows 经典主题 （Windows 2000 的默认主题） 不同于<xref:System.Windows.Controls.Button>Windows Luna 主题 （Windows XP 的默认主题） 中由于<xref:System.Windows.Controls.Button>使用不同<xref:System.Windows.Controls.ControlTemplate>为每个主题。  
  
 特定于主题的资源以特定文件名保留在资源字典中。 这些文件必须位于一个名为 `Themes` 的文件夹中，此文件夹是包含该控件的文件夹的子文件夹。 下表列出了资源字典文件以及与每个文件关联的主题：  
  
|资源字典文件名|Windows 主题|  
|-----------------------------------|-------------------|  
|`Classic.xaml`|Windows XP 中的经典 Windows 9x/2000 外观|  
|`Luna.NormalColor.xaml`|Windows XP 上的默认蓝色主题|  
|`Luna.Homestead.xaml`|Windows XP 上的橄榄色主题|  
|`Luna.Metallic.xaml`|Windows XP 上的银色主题|  
|`Royale.NormalColor.xaml`|Windows XP Media Center Edition 上的默认主题|  
|`Aero.NormalColor.xaml`|Windows Vista 上的默认主题|  
  
 无需为每一种主题都定义资源。 如果没有为特定主题定义资源，控件将在 `Classic.xaml` 中检查资源。 如果在与当前主题对应的文件或 `Classic.xaml` 中没有定义资源，控件将使用常规资源，该资源位于名为 `generic.xaml` 的资源字典文件中。  `generic.xaml` 文件与特定于主题的资源词典文件位于同一文件夹中。 尽管 `generic.xaml` 不与特定的 Windows 主题对应，但它仍是一个主题级别字典。  
  
 [带有主题和 UI 自动化支持的 NumericUpDown 自定义控件示例](https://go.microsoft.com/fwlink/?LinkID=160025)包含两个用于 `NumericUpDown` 控件的资源字典：一个在 generic.xaml 中，另一个在 Luna.NormalColor.xaml 中。  可以运行应用程序并在 Windows XP 中的银色主题和另一主题之间切换，以查看这两个控件模板之间的差别。 （如果运行的是 Windows Vista，可以将 Luna.NormalColor.xaml 重命名为 Aero.NormalColor.xaml，然后在两个主题之间切换，例如在 Windows 经典主题和 Windows Vista 的默认主题之间切换。）  
  
 当将<xref:System.Windows.Controls.ControlTemplate>必须在任何特定于主题资源字典文件，创建控件和调用静态构造函数<xref:System.Windows.DependencyProperty.OverrideMetadata%28System.Type%2CSystem.Windows.PropertyMetadata%29>方法<xref:System.Windows.FrameworkElement.DefaultStyleKey%2A>，如以下示例所示。  
  
 [!code-csharp[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/CSharp/NumericUpDown.cs#staticconstructor)]
 [!code-vb[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/visualbasic/numericupdown.vb#staticconstructor)]  
  
##### <a name="defining-and-referencing-keys-for-theme-resources"></a>定义和引用主题资源的键  
 在元素级别定义资源时，可以指定一个字符串作为它的键，然后通过该字符串访问该资源。 在定义在主题级别的资源时，必须使用<xref:System.Windows.ComponentResourceKey>作为键。  以下示例定义 generic.xaml 中的资源。  
  
 [!code-xaml[ThemeResourcesControlLibrary#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/Themes/generic.xaml#5)]  
  
 下面的示例通过指定引用的资源<xref:System.Windows.ComponentResourceKey>作为键。  
  
 [!code-xaml[ThemeResourcesControlLibrary#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/NumericUpDown.xaml#6)]  
  
##### <a name="specifying-the-location-of-theme-resources"></a>指定主题资源的位置  
 若要找到控件的资源，承载应用程序需要知道相应程序集包含特定于控件的资源。 您可以实现此目的通过添加<xref:System.Windows.ThemeInfoAttribute>到包含该控件的程序集。 <xref:System.Windows.ThemeInfoAttribute>已<xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A>属性，它指定泛型资源的位置和一个<xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A>属性，它指定特定于主题的资源的位置。  
  
 下面的示例设置<xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A>并<xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A>属性设置为<xref:System.Windows.ResourceDictionaryLocation.SourceAssembly>，以指定的通用和特定于主题资源位于控件所在的程序集。  
  
 [!code-csharp[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/Properties/AssemblyInfo.cs#themessection)]
 [!code-vb[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/my project/assemblyinfo.vb#themessection)]  
  
## <a name="see-also"></a>请参阅
- [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)
- [WPF 中的 Pack URI](../app-development/pack-uris-in-wpf.md)
- [控件自定义](control-customization.md)
