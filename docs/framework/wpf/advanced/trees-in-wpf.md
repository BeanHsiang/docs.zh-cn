---
title: WPF 中的树
ms.date: 03/30/2017
helpviewer_keywords:
- logical tree [WPF]
- element tree [WPF]
- visual tree [WPF]
ms.assetid: e83f25e5-d66b-4fc7-92d2-50130c9a6649
ms.openlocfilehash: 581bd29de07697794e1e752c02068d31db9e0de8
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354643"
---
# <a name="trees-in-wpf"></a>WPF 中的树
在许多技术中，元素和组件都按树结构的形式组织。在这种结构中，开发人员可以直接操作树中的对象节点来影响应用程序的绘制或行为。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 也使用了若干树结构形式来定义程序元素之间的关系。 多数情况下，在概念层面考虑对象树形式时，WPF 开发人员会用代码创建应用程序，或用 XAML 定义应用程序的组成部分，但他们会调用具体的 API 或使用特定的标记来执行此操作，而不是像在 XML DOM 中那样，使用某些常规对象树操作 API。 WPF 公开提供树形式视图的两个帮助器类<xref:System.Windows.LogicalTreeHelper>和<xref:System.Windows.Media.VisualTreeHelper>。 WPF 文档中还使用了“可视化树”和“逻辑树”两个术语，它们有助于理解某些关键 WPF 功能的行为。 本主题定义的可视化树和逻辑树的表示，讨论这些树与总体对象树概念，并引入了<xref:System.Windows.LogicalTreeHelper>和<xref:System.Windows.Media.VisualTreeHelper>s。  
  

  
<a name="element_tree"></a>   
## <a name="trees-in-wpf"></a>WPF 中的树  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，最完整的树结构是对象树。 如果在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中定义一个应用程序页，然后加载 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，将根据标记中元素之间的嵌套关系来创建树结构。 如果使用代码定义应用程序或应用程序的一部分，则将根据为属性（属性实现给定对象的内容模型）分配属性值的方式来创建树结构。 在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中，完整的对象树可通过两种方式进行概念化并报告给其公共 API：作为逻辑树和作为可视化树。 逻辑树与可视化树之间的区别不一定重要，但在某些 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 子系统中它们偶尔可能会导致问题，并影响你对标记或代码的选择。  
  
 尽管你并不会总是直接操作逻辑树或可视化树，但理解它们之间的关系有助于你从技术角度了解 WPF。 若要理解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中属性继承和事件路由的工作原理，将 WPF 视为某种树形式也相当重要。  
  
> [!NOTE]
>  因为对象树更像是概念，而不像是实际 API，所以还可以将此概念视为对象图。 实际上，在运行时，对象之间的某些关系不能由树形式表示。 尽管如此，树形式的相关性还是很强，尤其是对于 XAML 定义的 UI。因此，大多数 WPF 文档在引用这个常见概念时，仍使用术语“对象树”。  
  
<a name="logical_tree"></a>   
## <a name="the-logical-tree"></a>逻辑树  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，通过为支持 UI 元素的对象设置属性，可以向这些 UI 元素添加内容。 例如，你将项添加到<xref:System.Windows.Controls.ListBox>通过操作控制其<xref:System.Windows.Controls.ItemsControl.Items%2A>属性。 通过执行此操作，你将项放入<xref:System.Windows.Controls.ItemCollection>，它是<xref:System.Windows.Controls.ItemsControl.Items%2A>属性值。 同样，可以将对象添加到<xref:System.Windows.Controls.DockPanel>，则操作其<xref:System.Windows.Controls.Panel.Children%2A>属性值。 在这里，你会将对象添加到<xref:System.Windows.Controls.UIElementCollection>。 有关代码示例，请参阅[如何：动态添加元素](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms752374(v=vs.100))。  
  
 中[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，当你将在列表项放入<xref:System.Windows.Controls.ListBox>控件或中的其他 UI 元素<xref:System.Windows.Controls.DockPanel>，还使用<xref:System.Windows.Controls.ItemsControl.Items%2A>和<xref:System.Windows.Controls.Panel.Children%2A>属性，显式或隐式，如以下示例所示。  
  
 [!code-xaml[TreeOvwsSupport#AllCode](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeOvwsSupport/CS/page1.xaml#allcode)]  
  
 如果此 XAML 是作为文档对象模型下的 XML 进行处理，且已包含作为隐式项禁止注释的标记（可能是合法的），生成的 XML DOM 树已包含 `<ListBox.Items>` 的元素以及其他隐式项。 但是，读取标记和写入对象时，XAML 不会这样处理，生成的对象图不包含 `ListBox.Items`。 但是，它也有<xref:System.Windows.Controls.ListBox>名为属性`Items`，其中包含<xref:System.Windows.Controls.ItemCollection>，并且<xref:System.Windows.Controls.ItemCollection>已初始化，但为空时<xref:System.Windows.Controls.ListBox>处理 XAML。 然后，作为内容存在于每个子对象元素<xref:System.Windows.Controls.ListBox>添加到<xref:System.Windows.Controls.ItemCollection>的分析器调用`ItemCollection.Add`。 此示例将 XAML 处理成对象树，目前这似乎表明所创建的对象树基本上是逻辑树。  
  
 不过，即使不考虑 XAML 隐式语法项，该逻辑树也不是应用程序 UI 在运行时存在的整个对象图。这主要是因为视觉对象和模板。 例如，考虑<xref:System.Windows.Controls.Button>。 逻辑树报告<xref:System.Windows.Controls.Button>对象以及其字符串`Content`。 但在运行时对象树中，此按钮还有更多内容。 具体而言，该按钮才会显示在屏幕上是因为它的方法特定<xref:System.Windows.Controls.Button>应用控件模板。 来自应用的模板的视觉对象 (例如模板定义<xref:System.Windows.Controls.Border>可视化按钮周围的深灰色的) 不会报告逻辑树中，即使您正在查看逻辑树在运行时 (例如处理来自的输入的事件可见的 UI，然后读取逻辑树）。 若要查找模板视觉对象，需要改为检查可视化树。  
  
 有关 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法如何映射到所创建的对象图，以及 XAML 中隐式语法的详细信息，请参阅 [XAML 语法详述](xaml-syntax-in-detail.md)或 [XAML 概述 (WPF)](xaml-overview-wpf.md)。  
  
<a name="tree_property_inheritance_event_routing"></a>   
### <a name="the-purpose-of-the-logical-tree"></a>逻辑树用途  
 借助逻辑树，内容模型可以方便地循环访问其可能的子对象，从而实现扩展。 此外，逻辑树还为某些通知提供框架，例如在加载逻辑树中的所有对象时。 基本上，逻辑树是框架级别的近似运行时对象图（排除了视觉对象），但其足以用于对你自己的运行时应用程序组合执行多种查询操作。  
  
 此外，通过沿逻辑树向上查找来解析这两个静态和动态资源引用<xref:System.Windows.FrameworkElement.Resources%2A>上请求的初始对象，然后继续向上逻辑树并检查每个集合<xref:System.Windows.FrameworkElement>（或<xref:System.Windows.FrameworkContentElement>)为另一个`Resources`值，该值包含<xref:System.Windows.ResourceDictionary>，可能包含该键。 当同时存在逻辑树和可视化树时，将使用逻辑树进行资源查找。 有关资源字典和查找的详细信息，请参见 [XAML 资源](xaml-resources.md)。  
  
<a name="composition"></a>   
### <a name="composition-of-the-logical-tree"></a>逻辑树的构成  
 逻辑树在 WPF 框架级别，这意味着是逻辑树操作关系最为密切的 WPF 基元素是定义<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>。 但是，可以看出，是否实际使用<xref:System.Windows.LogicalTreeHelper>API，逻辑树有时会包含节点不是选择题<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>。 例如，逻辑树报告<xref:System.Windows.Controls.TextBlock.Text%2A>的值<xref:System.Windows.Controls.TextBlock>，它是一个字符串。  
  
<a name="override_logical_tree"></a>   
### <a name="overriding-the-logical-tree"></a>替代逻辑树  
 经验丰富的控件作者会通过替代若干 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]（用于定义常规对象或内容模型如何在逻辑树中添加或删除对象）来替代逻辑树。 有关如何替代逻辑树的示例，请参阅[替代逻辑树](how-to-override-the-logical-tree.md)。  
  
<a name="pvi"></a>   
### <a name="property-value-inheritance"></a>属性值继承  
 属性值继承通过混合树操作。 包含的实际元数据<xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>启用属性继承的属性是 WPF 框架级<xref:System.Windows.FrameworkPropertyMetadata>类。 因此，保留原始值的父和子对象继承该值都必须<xref:System.Windows.FrameworkElement>或<xref:System.Windows.FrameworkContentElement>，并且它们必须都是一些逻辑树的一部分。 但是，对于支持属性继承的现有 WPF 属性，属性值的继承可通过逻辑树中没有的中介对象永久存在。 这主要适用于以下情况：让模板元素使用在应用了模板的实例上设置的任何继承属性值，或者使用在更高级别的页级构成（因此在逻辑树中也位于更高位置）中设置的任何继承属性值。 为了使属性值的继承在这两种情况下保持一致，继承属性必须注册为附加属性。如果要定义具有属性继承行为的自定义依赖属性，则应采用这种模式。 无法通过帮助器类实用工具方法完全预测属性继承确切使用的树，即使在运行时也是如此。 有关详细信息，请参阅[属性值继承](property-value-inheritance.md)。  
  
<a name="two_trees"></a>   
## <a name="the-visual-tree"></a>可视化树  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中除了逻辑树的概念，还存在可视化树的概念。 可视化树描述的视觉对象的结构，由表示<xref:System.Windows.Media.Visual>基类。 为控件编写模板时，将定义或重新定义适用于该控件的可视化树。 对于出于性能和优化考虑需要对绘图进行较低级别控制的开发人员来说，他们也会对可视化树感兴趣。 在传统 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序编程中，可视化树的一个应用是：路由事件的事件路由大多遍历可视化树而非逻辑树。 路由事件行为的这种微妙之处可能不会很明显，除非你是控件作者。 通过可视化树对事件进行路由可使控件在可视化级别实现组合以处理事件或创建事件资源库。  
  
<a name="trees_content"></a>   
## <a name="trees-content-elements-and-content-hosts"></a>树、内容元素和内容宿主  
 内容元素 (派生的类<xref:System.Windows.ContentElement>) 不属于可视化树的一部分; 它们不是继承<xref:System.Windows.Media.Visual>和不具有可视表示形式。 若要显示在 UI 中，<xref:System.Windows.ContentElement>必须承载在既是内容宿主<xref:System.Windows.Media.Visual>和逻辑树参与者。 此类对象通常是<xref:System.Windows.FrameworkElement>。 从概念上讲，内容宿主有些类似于内容的“浏览器”，它选择在该宿主控制的屏幕区域中显示内容的方式。 承载内容时，可以使内容成为通常与可视化树关联的某些树进程的参与者。 通常情况下，<xref:System.Windows.FrameworkElement>宿主类包括添加所有托管的实现代码<xref:System.Windows.ContentElement>到通过内容逻辑树的子节点的事件路由，即使所承载的内容不属于实际可视化树。 这是必需的以便<xref:System.Windows.ContentElement>可以获得将路由到非自身的任何元素的路由的事件。  
  
<a name="tree_traversal"></a>   
## <a name="tree-traversal"></a>树遍历  
 <xref:System.Windows.LogicalTreeHelper>类提供了<xref:System.Windows.LogicalTreeHelper.GetChildren%2A>， <xref:System.Windows.LogicalTreeHelper.GetParent%2A>，和<xref:System.Windows.LogicalTreeHelper.FindLogicalNode%2A>逻辑树遍历的方法。 在大多数情况下，不需要遍历现有控件的逻辑树，因为这些控件几乎总是将其逻辑子元素公开为一个专用集合属性，这种属性支持集合访问，如 `Add`、索引器等等。 树遍历是一种主要方案由控件作者选择不从预期的控件模式派生，如<xref:System.Windows.Controls.ItemsControl>或<xref:System.Windows.Controls.Panel>其中已定义集合属性，并且希望提供自己的集合属性的支持。  
  
 可视化树还支持用于可视化树遍历的帮助器类<xref:System.Windows.Media.VisualTreeHelper>。 不通过特定于控件的属性，方便地公开可视化树，因此<xref:System.Windows.Media.VisualTreeHelper>类是遍历可视化树，如果这是你的编程方案所需的建议的方法。 有关详细信息，请参阅 [WPF 图形呈现概述](../graphics-multimedia/wpf-graphics-rendering-overview.md)。  
  
> [!NOTE]
>  有时有必要检查所应用模板的可视化树。 执行此操作时应谨慎。 即使遍历可视化树的控件在其中定义该模板，您的控件的使用者始终可以通过设置更改模板<xref:System.Windows.Controls.Control.Template%2A>属性情况下，甚至最终用户可以通过以下方式影响应用的模板更改系统主题。  
  
<a name="routes"></a>   
## <a name="routes-for-routed-events-as-a-tree"></a>“树”形式路由事件的路由  
 如前所述，对于任何给定的路由事件，其路由都沿着一条预定的树路径进行，这棵树是可视化树和逻辑树表示形式的混合体。 事件路由可在树中向上或向下进行，具体取决于该事件是隧道路由事件还是浮升路由事件。 事件路由概念没有直接支持的帮助器类（此类可用于独立于引发实际路由的事件，遍历事件）。 没有一个类，表示路由， <xref:System.Windows.EventRoute>，但该类的方法通常仅供内部使用。  
  
<a name="resourcesandtrees"></a>   
## <a name="resource-dictionaries-and-trees"></a>资源字典和树  
 对页中定义的所有 `Resources` 进行资源字典查找时，基本上遍历逻辑树。 逻辑树之外的对象可以引用键控资源，但资源查找顺序将从该对象与逻辑树的连接点开始。 在 WPF 中，只有逻辑树节点可以具有`Resources`属性，其中包含<xref:System.Windows.ResourceDictionary>，因此没有任何益处在遍历可视化树中查找键控资源从<xref:System.Windows.ResourceDictionary>。  
  
 但是，资源查找也可以超出直接逻辑树。 对于应用程序标记，资源查找可向前继续进行到应用程序级资源字典，然后再到作为静态属性或键进行引用的主题支持和系统值。 如果资源引用是动态的，则主题本身也可以引用主题逻辑树之外的系统值。 有关资源字典和查找逻辑的详细信息，请参阅 [XAML 资源](xaml-resources.md)。  
  
## <a name="see-also"></a>请参阅
- [输入概述](input-overview.md)
- [WPF 图形呈现概述](../graphics-multimedia/wpf-graphics-rendering-overview.md)
- [路由事件概述](routed-events-overview.md)
- [不在对象树中的对象元素的初始化](initialization-for-object-elements-not-in-an-object-tree.md)
- [WPF 体系结构](wpf-architecture.md)
