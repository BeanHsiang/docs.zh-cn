---
title: XAML 语法详述
ms.date: 03/30/2017
helpviewer_keywords:
- XML [WPF], namespaces
- XAML [WPF], parsing of attributes
- parsing of attributes [WPF]
- XAML [WPF], markup extensions
- attached properties [WPF]
- tag syntax [XAML]
- markup extensions [WPF]
- XAML [WPF], object element syntax
- XAML [WPF], syntax terminology
- attached events [WPF]
- lookup semantics [WPF]
- XAML [WPF], attached events
- XAML [WPF], content syntax
- XAML [WPF], lookup semantics
- content syntax [WPF]
- object element syntax [WPF]
- syntax terminology [XAML]
- XAML [WPF], attached properties
- attributes [XAML], parsing
- XAML [WPF], tag syntax
- XAML [WPF], attribute syntax
- property element syntax [WPF]
- terminology [XAML]
- namespaces [WPF], XML
- attribute syntax [XAML]
- XAML [WPF], property element syntax
ms.assetid: 67cce290-ca26-4c41-a797-b68aabc45479
ms.openlocfilehash: ecea2575503ad8fe4ff8a190a417bae75a7b31f7
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57367955"
---
# <a name="xaml-syntax-in-detail"></a>XAML 语法详述
本主题定义的术语，用于描述的 XAML 语法的元素。 这些条款通常使用，本文档中，同时用于 WPF 文档的其余部分专门以及其他使用 XAML 或通过 XAML 语言支持在 System.Xaml 级别启用的基本 XAML 概念的框架。 本主题进一步在本主题中引入的基本术语[XAML 概述 (WPF)](xaml-overview-wpf.md)。  
  

  
<a name="the_xaml_language_specification"></a>   
## <a name="the-xaml-language-specification"></a>XAML 语言规范  
 在此处定义的 XAML 语法术语还定义或引用中 XAML 语言规范。 XAML 是一种基于 XML 语言并遵循或 XML 结构规则进行了扩展。 一些术语从共享或基于描述 XML 语言或 XML 文档对象模型时，通常使用的术语。  
  
 有关 XAML 语言规范的详细信息，请下载[ \[MS XAML\] ](https://go.microsoft.com/fwlink/?LinkId=114525)从 Microsoft 下载中心获得。  
  
<a name="xaml_and_clr"></a>   
## <a name="xaml-and-clr"></a>XAML 和 CLR  
 XAML 是一种标记语言。 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]、 为隐含按其名称，启用运行时执行。 XAML 不是本身直接由 CLR 运行时的常见语言之一。 相反，您可以将 XAML 为支持其自己的类型系统。 CLR 和 CLR 类型系统上构建 WPF 使用的特定 XAML 分析系统。 XAML 类型映射到 CLR 类型时用于 WPF XAML 分析实例化的运行的时表示形式。 出于此原因，讨论本文档中的语法的其余部分将包括对 CLR 类型系统，即使在 XAML 语言规范中的等效语法讨论不这样做也是如此。 （每个 XAML 语言规范级别，XAML 类型无法映射到任何其他类型的系统，这不一定要 CLR，但这需要创建和使用不同的 XAML 分析器。）  
  
#### <a name="members-of-types-and-class-inheritance"></a>类型和类继承的成员  
 属性和事件作为它们显示为的 XAML 成员[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]类型通常继承自基类型。 例如，请考虑以下示例： `<Button Background="Blue" .../>`。 <xref:System.Windows.Controls.Control.Background%2A>属性不是立即声明的属性上<xref:System.Windows.Controls.Button>类，如果要查看的类定义、 反射结果或文档。 相反，<xref:System.Windows.Controls.Control.Background%2A>继承自基类<xref:System.Windows.Controls.Control>类。  
  
 类继承行为的[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]XAML 元素是从 XML 标记的架构上强制实施解释大不同之处。 类继承可能非常复杂，特别是在中间基类为抽象类，或当涉及到接口时。 这是原因之一，很难进行表示准确完整地使用架构类型的 XAML 元素和其允许的属性集通常用于[!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]编程，如 DTD 或 XSD 格式。 另一个原因是可扩展性和类型映射功能的 XAML 语言本身不允许的类型和成员的任何固定表示形式的完整性。  
  
<a name="object_element_syntax"></a>   
## <a name="object-element-syntax"></a>对象元素语法  
 *对象元素语法*是实例的 CLR 类或结构化通过声明的 XML 元素的 XAML 标记语法。 此语法类似于其他标记语言，如 HTML 元素语法。 对象元素语法开头左尖括号 (\<)，然后立即由类或结构被实例化的类型名称。 类型名称，后面可以有零个或多个空格和零个或多个属性还可以声明的对象元素上使用一个或多个空格来分隔每个特性名称 ="值"对。 最后，必须是以下值之一，则返回 true:  
  
-   必须由正斜杠 （/） 后紧跟右尖括号 (>) 关闭的元素和标记。  
  
-   必须是右尖括号 (>) 完成的开始标记。 其他对象元素、 属性元素或内部文本，可以按照开始标记。 完全可能此处包含哪些内容通常受对象模型的元素。 关闭对象元素标记的等效项也必须位于正确的嵌套，并与其他开始和结束标记对之间实现平衡。  
  
 由.NET 实现的 XAML 具有一组规则可将对象元素映射到类型，为属性或事件和 XAML 命名空间到 CLR 命名空间和程序集的属性。 对于 WPF 和.NET Framework 中，XAML 对象元素将映射到[!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)]中定义的类型引用的程序集，它的属性映射到这些类型的成员。 在引用 XAML 中的 CLR 类型时，你有权访问该类型的继承成员。  
  
 例如，下面的示例是实例化的新实例的对象元素语法<xref:System.Windows.Controls.Button>类，并且还指定了<xref:System.Windows.FrameworkElement.Name%2A>属性和该属性值：  
  
 [!code-xaml[XAMLOvwSupport#SyntaxOE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxoe)]  
  
 下面的示例是对象元素语法，它还包括 XAML 内容属性语法。 中包含的内部文本将用于设置<xref:System.Windows.Controls.TextBox>XAML 内容属性<xref:System.Windows.Controls.TextBox.Text%2A>。  
  
 [!code-xaml[XAMLOvwSupport#ThisIsATextBox](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#thisisatextbox)]  
  
### <a name="content-models"></a>内容模型  
 类可能支持作为 XAML 对象元素语法中，根据使用情况，但该元素将仅在中正常工作的应用程序或页放在整体内容的模型或元素树的预期位置。 例如，<xref:System.Windows.Controls.MenuItem>通常只能放置的小孩<xref:System.Windows.Controls.Primitives.MenuBase>派生类，如<xref:System.Windows.Controls.Menu>。 内容模型的特定元素编写为的控件和其他类页上的备注部分一部分[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]可以用作 XAML 元素的类。  
  
<a name="properties_of_object_elements"></a>   
## <a name="properties-of-object-elements"></a>对象元素的属性  
 在 XAML 中的属性是设置各种可能的语法。 根据要设置的属性的基础类型系统特征，哪种语法可用于特定属性将有所不同。  
  
 通过设置属性的值，您向特性或功能对象存在于运行的时对象图中。 从对象元素创建的对象的初始状态基于默认构造函数行为。 通常情况下，应用程序将使用的任何给定的对象的完全默认实例以外的内容。  
  
<a name="attribute_syntax_properties"></a>   
## <a name="attribute-syntax-properties"></a>特性语法（属性）  
 特性语法是通过现有的对象元素上声明属性来设置属性的值的 XAML 标记语法。 属性名称必须与支持相关对象元素的类的属性的 CLR 成员名称相匹配。 属性名称后跟赋值运算符 （=）。 特性值必须括在引号内的字符串。  
  
> [!NOTE]
>  可以使用替代引号将文本引号在特性中。 例如可以作为一种方式使用单引号来声明包含在其中一个双引号字符的字符串。 无论使用单引号或双引号时，应使用匹配对用于打开和关闭属性值字符串。 也有转义序列或其他技术可用于解决施加任何特定的 XAML 语法的字符限制。 请参阅[XML 字符实体和 XAML](../../xaml-services/xml-character-entities-and-xaml.md)。  
  
 若要通过特性语法进行设置，属性必须是公共的并且必须是可写。 在后备类型系统中的属性的值必须是值类型，或必须一个引用类型，可以实例化或访问相关时引用由 XAML 处理器支持类型。  
  
 WPF XAML 事件的事件的属性名称作为引用必须是公共的和具有公共委托。  
  
 属性或事件必须是类或结构，它包含的对象元素由实例化的成员。  
  
### <a name="processing-of-attribute-values"></a>处理的属性值  
 由 XAML 处理器进行处理的开始和结束引号内包含的字符串值。 对于属性，由基础的 CLR 属性的类型确定的默认处理行为。  
  
 通过下列选项之一来填充属性值使用此处理顺序：  
  
1.  如果 XAML 处理器遇到大括号或从派生的对象元素<xref:System.Windows.Markup.MarkupExtension>、 然后引用的标记扩展而不是处理为字符串，值首先计算和标记扩展返回的对象用作值。 在许多情况下通过标记扩展返回的对象将对现有对象或一个表达式，用于将计算推迟到运行时，不是一个新实例化的对象的引用。  
  
2.  如果属性声明与特性化<xref:System.ComponentModel.TypeConverter>，或该属性的值类型声明与特性化<xref:System.ComponentModel.TypeConverter>属性的字符串值提交到作为转换输入的类型转换器，则转换器将返回新的对象实例。  
  
3.  如果没有任何<xref:System.ComponentModel.TypeConverter>，尝试直接转换为属性类型。 最后一个级别是在 XAML 语言基元类型或检查枚举 （分析器，然后访问匹配的值） 中的命名常量的名称之间的分析器本机值的直接转换。  
  
#### <a name="enumeration-attribute-values"></a>枚举属性值  
 XAML 中的枚举本质上处理的 XAML 分析程序，并应通过指定一个枚举的已命名常数的字符串名称来指定枚举的成员。  
  
 无标志枚举值，对于本机行为是处理的属性值的字符串，并将其解析为枚举值之一。 未指定枚举的格式*枚举*。*值*，如代码中执行操作。 相反，您指定仅*值*，并*枚举*由你设置的属性的类型推断。 如果指定中的属性*枚举*。*值*窗体，它将无法正确解析。  
  
 对于按标志枚举，该行为基于<xref:System.Enum.Parse%2A?displayProperty=nameWithType>方法。 可以用逗号分隔每个值来指定多个按标志枚举值。 但是，不能合并不按标志的枚举值。 例如，不能使用逗号语法以尝试创建<xref:System.Windows.Trigger>作用于无标志枚举的多个条件：  
  
```  
<!--This will not compile, because Visibility is not a flagwise enumeration.-->  
...  
<Trigger Property="Visibility" Value="Collapsed,Hidden">  
  <Setter ... />  
</Trigger>  
...  
```  
  
 支持可在 XAML 中设置的属性的按标志枚举是在 WPF 中不常见。 但是，一个此类枚举是<xref:System.Windows.Media.StyleSimulations>。 例如，可以使用以逗号分隔按标志特性语法来修改提供的备注中的示例<xref:System.Windows.Documents.Glyphs>类;`StyleSimulations = "BoldSimulation"`可能会变得`StyleSimulations = "BoldSimulation,ItalicSimulation"`。 <xref:System.Windows.Input.KeyBinding.Modifiers%2A?displayProperty=nameWithType> 是另一个属性可以指定多个枚举值的位置。 但是，此属性恰好是一种特殊情况，因为<xref:System.Windows.Input.ModifierKeys>枚举支持其自己的类型转换器。 修饰符的类型转换器使用加号 （+） 作为分隔符，而不是逗号 （，）。 此转换支持更传统的语法来表示在 Microsoft Windows 编程中，如"Ctrl + Alt"键组合。  
  
### <a name="properties-and-event-member-name-references"></a>属性和事件成员名称的引用  
 在指定特性时，可以引用任何属性或作为您实例化包含的对象元素的 CLR 类型的成员存在的事件。  
  
 或者，可以引用的附加的属性或附加事件，独立于包含的对象元素。 （下一节讨论是附加的属性）。  
  
 也可以命名通过使用可通过默认命名空间访问的任何对象中的任何事件*typeName*。*事件*部分限定的名称; 此语法支持附加路由事件的处理程序用于处理从子元素，但父元素路由事件处理程序未安装该事件在其成员表中。 此语法类似于附加的事件语法，但此处的事件不是真正的附加的事件。 相反，正在引用具有限定名称的事件。 有关详细信息，请参阅[路由事件概述](routed-events-overview.md)。  
  
 在某些情况下，作为一个属性，而不是属性名称的值有时提供属性名称。 该属性名称还可以包括限定符，例如窗体中指定的属性*ownerType*。*依赖项属性名称*。 在 XAML 中编写样式或模板时，此方案中很常见。 处理规则的属性名称用作属性值不同，并按所设置的属性的类型或特定 WPF 子系统的行为受控。 有关详细信息，请参阅[样式和模板化](../controls/styling-and-templating.md)。  
  
 当属性值描述的属性关系时，属性名称的另一个使用情况。 此功能用于数据绑定和情节提要目标和情况下启用<xref:System.Windows.PropertyPath>类，其类型转换器。 查找语义的更完整说明，请参阅[PropertyPath XAML 语法](propertypath-xaml-syntax.md)。  
  
<a name="property_element_syntax"></a>   
## <a name="property-element-syntax"></a>属性元素语法  
 *属性元素语法*是一种语法与元素的基本 XML 语法规则略有不同。 在 XML 中，属性值是一个实际的字符串，唯一可能的变化是正在使用哪种字符串编码格式。 在 XAML 中，可以将其他对象元素的属性的值。 此功能启用的属性元素语法。 而不是作为元素标记中的属性所指定的属性，属性使用指定的开始元素标记中的*元素类型名称*。*propertyName*窗体中，指定的属性的值，然后结束属性元素。  
  
 具体而言，该语法以左尖括号 (\<)，然后立即由类或结构中包含的属性元素语法的类型名称。 这被紧跟由单个点 （.），然后属性的名称，然后是右尖括号 (>)。 与特性语法中，该属性必须存在于指定类型的声明的公共成员。 要分配给属性的值包含在属性元素中。 通常情况下，给出的值作为一个或多个对象元素，因为对象指定为值是该方案的属性元素语法的意图是地址。 最后，指定相同的等效的结束标记*元素类型名称*。*propertyName*必须提供组合中正确嵌套和与其他元素标记的平衡。  
  
 例如，以下是属性元素语法<xref:System.Windows.FrameworkElement.ContextMenu%2A>属性的<xref:System.Windows.Controls.Button>。  
  
 [!code-xaml[XAMLOvwSupport#ContextMenu](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#contextmenu)]  
  
 属性元素中的值可以还提供内部文本，在所指定的属性类型的基元值类型，情况下如<xref:System.String>，或指定名称的枚举。 这两种用法是某种程度上不常见，因为每个这种情况下也可以使用更简单的属性语法。 用字符串填充的属性元素的一个方案是不是 XAML 内容属性，但仍用于 UI 文本表示形式的属性和特定的空白元素，如的换行所需的 UI 文本中显示。 特性语法不能保留的换行，但属性元素语法可以前提是重要的空白区域保留处于活动状态 (有关详细信息，请参阅[处理在 XAML 中的空白区域](../../xaml-services/whitespace-processing-in-xaml.md))。 另一种情况是，以便[X:uid 指令](../../xaml-services/x-uid-directive.md)可以应用于属性元素，并作为一个值，应在 WPF 中本地化输出 BAML 或通过其他技术，因此标记内的值。  
  
 WPF 逻辑树中不会显示的属性元素。 Property 元素是只是一种特定的语法，来设置属性，并且不具有的实例或对象支持它的元素。 (逻辑树概念的详细信息，请参阅[WPF 中的树](trees-in-wpf.md)。)  
  
 对于支持属性和属性元素语法的位置的属性，这两种语法通常具有相同的结果，尽管微妙之处，例如空白处理语法之间略有不同。  
  
<a name="collection_syntax"></a>   
## <a name="collection-syntax"></a>集合语法  
 XAML 规范要求 XAML 处理器实现来标识的属性的值类型的集合。 在.NET 中的常规 XAML 处理器实现取决于托管的代码和 CLR，并标识集合类型通过以下项之一：  
  
-   类型实现<xref:System.Collections.IList>。  
  
-   类型实现<xref:System.Collections.IDictionary>。  
  
-   派生自类型<xref:System.Array>(有关在 XAML 中数组的详细信息，请参阅[X:array 标记扩展](../../xaml-services/x-array-markup-extension.md)。)  
  
 如果属性的类型是一个集合，然后不需要为对象元素标记中指定推断的集合类型。 相反，旨在成为集合中的项的元素被指定为一个或多个属性元素的子元素。 每个此类项在加载期间计算为一个对象，然后通过调用添加到集合`Add`隐式集合的方法。 例如，<xref:System.Windows.Style.Triggers%2A>的属性<xref:System.Windows.Style>采用专用的集合类型<xref:System.Windows.TriggerCollection>，它可以实现<xref:System.Collections.IList>。 不需要实例化<xref:System.Windows.TriggerCollection>标记中的对象元素。 相反，您可以指定一个或多个<xref:System.Windows.Trigger>项中的元素作为`Style.Triggers`属性元素中，其中<xref:System.Windows.Trigger>（或派生的类） 是应作为项类型的强类型化和隐式类型<xref:System.Windows.TriggerCollection>。  
  
 [!code-xaml[XAMLOvwSupport#SyntaxPECollection](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxpecollection)]  
  
 属性可能是集合类型和该类型的 XAML 内容属性和派生类型，对其进行讨论此主题的下一节中。  
  
 尽管不会显示为元素的标记中，隐式集合元素中的逻辑树表示形式中，创建的成员。 父类型的构造函数通常是其属性之一的集合执行实例化并最初为空集合成为对象树的一部分。  
  
> [!NOTE]
>  泛型列表和字典接口 (<xref:System.Collections.Generic.IList%601>和<xref:System.Collections.Generic.IDictionary%602>) 不支持对于集合检测。 但是，可以使用<xref:System.Collections.Generic.List%601>类作为基类，因为它实现<xref:System.Collections.IList>直接，或<xref:System.Collections.Generic.Dictionary%602>作为基类，因为它实现了<xref:System.Collections.IDictionary>直接。  
  
 在集合类型的.NET 参考页，此语法与集合的对象元素有意省略偶尔需要注意的 XAML 语法部分中作为隐式集合语法。  
  
 除了根元素中，嵌套另一个元素的子元素作为 XAML 文件中的每个对象元素实际上是一个或两个在以下情况下的元素： 其父元素的隐式集合属性的成员或指定的父元素 (XAML 内容属性将在下一节中讨论) 的 XAML 内容属性的值的元素。 换而言之，父元素和标记页面中的子元素的关系实际上是单个对象根位置，并对根下的每个对象元素都是单个实例提供的父代、 属性值或列中的项之一也是父项的集合类型属性值的 lection。 此单根概念通常是使用 XML，并且还经常进一步巩固 Api，如加载 XAML 行为中<xref:System.Windows.Markup.XamlReader.Load%2A>。  
  
 下面的示例是使用集合的对象元素语法 (<xref:System.Windows.Media.GradientStopCollection>) 显式指定。  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <GradientStopCollection>  
      <GradientStop Offset="0.0" Color="Red" />  
      <GradientStop Offset="1.0" Color="Blue" />  
    </GradientStopCollection>  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
 请注意，它并不总是可以显式声明集合。 例如，尝试声明<xref:System.Windows.TriggerCollection>中前面所示显式<xref:System.Windows.Style.Triggers%2A>示例将失败。 显式声明集合需要集合类必须支持默认构造函数，和<xref:System.Windows.TriggerCollection>没有默认构造函数。  
  
<a name="xaml_content_properties"></a>   
## <a name="xaml-content-properties"></a>XAML 内容属性  
 XAML 内容语法是一种语法仅启用指定的类上的<xref:System.Windows.Markup.ContentPropertyAttribute>作为其类声明的一部分。 <xref:System.Windows.Markup.ContentPropertyAttribute>引用该类型的元素 （包括派生的类） 的 content 属性的属性名称。 当 XAML 处理器处理，将分配的任何子元素或找到开始标记和结束标记的对象元素之间的内部文本，该对象的 XAML 内容属性的值。 允许您指定显式属性元素的内容属性，但.NET 参考中的 XAML 语法部分中一般不介绍这种用法。 显式/详细的方法有偶尔值标记起见或作为一种标记样式，但通常内容属性的目的是简化标记，以便可以直接嵌套的直观相关的父-子元素。 作为"内容"每个严格的 XAML 语言定义; 未分配的上一个元素的其他属性的属性元素标记它们以前 XAML 分析器处理顺序进行处理，并且不会考虑为"内容"。  
  
### <a name="xaml-content-property-values-must-be-contiguous"></a>必须是连续的 XAML 内容属性值  
 XAML 内容属性的值必须在该对象元素完全之前或之后的任何其他属性元素指定。 XAML 内容属性的值指定为字符串，或作为一个或多个对象是否也是如此。 例如，以下标记不会分析：  
  
```  
<Button>I am a   
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 这是非法的实质上是因为此语法所做的内容属性使用属性元素语法显式，如果内容的属性将设置两次：  
  
```xml  
<Button>  
  <Button.Content>I am a </Button.Content>  
  <Button.Background>Blue</Button.Background>  
  <Button.Content> blue button</Button.Content>  
</Button>  
```  
  
 类似的非法示例是如果内容属性是一个集合，并且子元素混杂在一起属性元素：  
  
```xml  
<StackPanel>  
  <Button>This example</Button>  
  <StackPanel.Resources>  
    <SolidColorBrush x:Key="BlueBrush" Color="Blue"/>  
  </StackPanel.Resources>  
  <Button>... is illegal XAML</Button>  
</StackPanel>  
```  
  
<a name="content_properties_and_collection_syntax_combined"></a>   
## <a name="content-properties-and-collection-syntax-combined"></a>内容属性和集合语法组合  
 多个单个对象元素作为内容，以便接受内容属性的类型具体而言必须是集合类型。 为集合类型的属性元素语法类似，XAML 处理器必须确定属于集合类型的类型。 如果元素具有 XAML 内容属性，XAML 内容属性的类型是一个集合，然后隐含的集合类型不需要为对象元素标记中指定并不需要指定为属性 el XAML 内容属性ement。 因此在标记中明显的内容模型现在有多个分配作为内容的子元素。 以下是内容语法<xref:System.Windows.Controls.Panel>派生的类。 所有<xref:System.Windows.Controls.Panel>派生的类建立 XAML 内容属性为<xref:System.Windows.Controls.Panel.Children%2A>，这需要类型的值<xref:System.Windows.Controls.UIElementCollection>。  
  
 [!code-xaml[XAMLOvwSupport#SyntaxContent](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page5.xaml#syntaxcontent)]  
  
 请注意，对于既不在属性元素<xref:System.Windows.Controls.Panel.Children%2A>也不为元素<xref:System.Windows.Controls.UIElementCollection>所需的标记中。 这是 XAML 设计功能，使其以递归方式包含用于定义元素的[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]更直观地表示为具有直接父-子元素间的关系，而无需干预属性元素标记嵌套元素树或集合对象。 事实上，<xref:System.Windows.Controls.UIElementCollection>不能指定显式标记为对象元素，通过设计。 因为其唯一用途是作为隐式的集合，<xref:System.Windows.Controls.UIElementCollection>不公开公共默认构造函数，因此无法实例化作为对象元素。  
  
### <a name="mixing-property-elements-and-object-elements-in-an-object-with-a-content-property"></a>混合使用属性元素和具有内容的属性的对象中的对象元素  
 XAML 规范声明用于填充对象元素内的 XAML 内容属性的对象元素必须是连续的并且必须不混合型 XAML 处理器可以强制执行。 通过强制实施此限制针对混合使用属性元素和内容[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]XAML 处理器。  
  
 您可以将子对象元素作为对象元素中的第一个即时标记。 然后，可以引入属性元素。 或者，你可以指定一个或多个属性元素的内容，然后更多属性元素。 但是，一旦属性元素内容后面跟，不能引入任何进一步的内容，你可以仅添加属性元素。  
  
 此内容 / 属性元素顺序要求并不适用于作为内容的内部文本。 但是，它仍是要保留的内部文本连续的因为有意义的空白将很难直观地检测到的标记中如果混杂内部文本的属性元素的好的标记样式。  
  
<a name="xaml_namespaces"></a>   
## <a name="xaml-namespaces"></a>XAML 命名空间  
 上述语法示例未指定默认 XAML 命名空间之外的 XAML 命名空间。 在典型[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序，默认 XAML 命名空间指定为[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]命名空间。 您可以指定默认 XAML 命名空间之外的 XAML 命名空间，而且仍使用类似的语法。 但是，然后，任何位置其中一个类名为无法访问默认 XAML 命名空间内，则该类的名称必须在前面加上的 XAML 命名空间前缀映射到相应的 CLR 命名空间。 例如，`<custom:Example/>`是对象元素语法来实例化的实例`Example`类，其中包含此类 （和可能包含后备类型的外部程序集信息） 的 CLR 命名空间之前映射到`custom`前缀。  
  
 有关 XAML 命名空间的详细信息，请参阅[XAML 命名空间和 WPF XAML Namespace 映射](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
<a name="markup_extensions"></a>   
## <a name="markup-extensions"></a>标记扩展  
 XAML 定义编程实体，使从正常的 XAML 处理器处理的字符串属性值或对象元素，转义符并将推迟到支持类处理标记扩展。 标识 XAML 处理器的标记扩展时使用特性语法是左大括号 （{}） 后, 跟右大括号 （}） 以外的任何字符的字符。 后面的左大括号的第一个字符串必须引用此子字符串是否真正的类名称的一部分提供的特定扩展行为，该引用可能会省略子字符串"Extension"的类。 此后，可能会出现一个空格，而然后每个后续字符用作输入的扩展插件实现中，直至遇到的右大括号。  
  
 .NET XAML 实现使用<xref:System.Windows.Markup.MarkupExtension>抽象类为所有支持的标记扩展的基础[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]以及其他框架或技术。 标记扩展的[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]专门实现通常用于提供一种方法，以引用其他现有对象，或使延迟将在运行时计算的对象引用。 例如，通过简单的 WPF 数据绑定指定`{Binding}`标记扩展通常将采用特定属性值的位置。 许多 WPF 标记扩展启用特性语法的其中一种属性语法，否则是不可能的属性。 例如，<xref:System.Windows.Style>对象是相对较复杂类型包含一系列嵌套的对象和属性。 通常将在 WPF 中的样式定义中的资源作为<xref:System.Windows.ResourceDictionary>，然后通过一个请求资源的两个 WPF 标记扩展引用。 标记扩展将推迟到一种资源查找的属性值的计算，并使提供的价值<xref:System.Windows.FrameworkElement.Style%2A>属性，采用类型<xref:System.Windows.Style>，在特性语法，如以下示例所示：  
  
 `<Button Style="{StaticResource MyStyle}">My button</Button>`  
  
 在这里，`StaticResource`标识<xref:System.Windows.StaticResourceExtension>类，用于提供标记扩展实现。 下一个字符串`MyStyle`作为输入用于非默认<xref:System.Windows.StaticResourceExtension>构造函数中，从扩展的字符串中提取的参数声明请求<xref:System.Windows.ResourceKey>。 `MyStyle` 应为[X:key](../../xaml-services/x-key-directive.md)的值<xref:System.Windows.Style>定义为资源。 [StaticResource 标记扩展](staticresource-markup-extension.md)用法要求使用的资源，以提供<xref:System.Windows.Style>静态资源查找逻辑在加载时通过属性值。  
  
 有关标记扩展的详细信息，请参阅[标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)。 有关标记扩展和编程功能在常规的.NET XAML 实现中启用其他 XAML 的参考，请参阅[XAML Namespace （x:）语言功能](../../xaml-services/xaml-namespace-x-language-features.md)。 有关特定于 WPF 的标记扩展，请参阅[WPF XAML 扩展](wpf-xaml-extensions.md)。  
  
<a name="attached_properties"></a>   
## <a name="attached-properties"></a>附加属性  
 附加的属性是在 XAML 属性可以拥有和某个特定类型定义，由此引入了一个编程概念但设置为属性或属性元素上的任何元素。 主要方案用于附加的属性是能够向父元素报告信息的标记结构中的子元素而无需在所有元素之间的广泛共享的对象模型。 相反，报表信息传递到子元素的父元素可以使用附加的属性。 有关详细信息的附加的属性以及如何创建你自己的目的附加属性，请参阅[附加属性概述](attached-properties-overview.md)。  
  
 附加的属性使用语法看起来类似于属性元素语法中，您还指定*typeName*。*propertyName*组合。 有两个重要的差异：  
  
-   可以使用*typeName*。*propertyName*甚至设置附加的属性通过特性语法时的组合。 附加的属性是唯一的用例，其中，符合条件的属性名称是在特性语法要求。  
  
-   此外可以附加属性使用属性元素语法。 但是，对于典型的属性元素语法*typeName*指定为包含属性的元素的对象元素。 如果您引用的附加属性，则*typeName*是定义附加的属性不包含的对象元素的类。  
  
<a name="attached_events"></a>   
## <a name="attached-events"></a>附加事件  
 附加的事件也是的 XAML 特定的类型，可以定义事件，但可能在任何对象元素上附加处理程序中引入的另一个编程概念。 在 WOF 实现中，定义附加的事件的类型通常是静态类型，用于定义一种服务，并公开该服务的类型中的路由的事件别名有时公开这些附加的事件。 通过特性语法指定的附加事件处理程序。 使用附加事件附加事件，以允许展开特性语法时*typeName*。*eventName*使用情况，其中*typeName*是类，提供`Add`并`Remove`事件附加的事件基础结构，处理程序的访问器和*eventName*是事件名称。  
  
<a name="anatomy_of_a_xaml_page_root_element"></a>   
## <a name="anatomy-of-a-xaml-root-element"></a>XAML 根元素的剖析  
 下表显示了一个典型 XAML 根元素细分它们，显示根元素的特定属性：  
  
|||  
|-|-|  
|`<Page`|打开根元素的对象元素|  
|`xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`|默认值 ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]) XAML 命名空间|  
|`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`|XAML 语言 XAML 命名空间|  
|`x:Class="ExampleNamespace.ExampleCode"`|连接到任何代码隐藏的标记的分部类声明为分部类定义|  
|`>`|根对象元素的末尾。 因为该元素包含子元素，不是尚未关闭对象|  
  
<a name="optional_and_nonrecommended_xaml_usages"></a>   
## <a name="optional-and-nonrecommended-xaml-usages"></a>可选的查找 XAML 用法  
 以下各节介绍 XAML 用法，从技术上讲支持由 XAML 处理器，但的生成详细级别或开发包含 XAML 源的应用程序时剩余的可读的 XAML 文件会干扰其他美观问题。  
  
### <a name="optional-property-element-usages"></a>可选属性元素用法  
 可选属性元素用法包括显式写出元素内容属性的 XAML 处理器将视为隐式。 例如，当声明的内容<xref:System.Windows.Controls.Menu>，你可以选择显式声明<xref:System.Windows.Controls.ItemsControl.Items%2A>系列<xref:System.Windows.Controls.Menu>作为`<Menu.Items>`属性元素标记和位置<xref:System.Windows.Controls.MenuItem>内`<Menu.Items>`，而不是比使用隐式的 XAML 处理器行为的所有子元素<xref:System.Windows.Controls.Menu>必须是<xref:System.Windows.Controls.MenuItem>并放入<xref:System.Windows.Controls.ItemsControl.Items%2A>集合。 有时可选用法可以帮助直观地阐明对象结构，按标记中的表示形式。 或者，有时显式属性元素用法可以避免从技术上讲功能，但在视觉混乱，例如嵌套的标记扩展的特性值中的标记。  
  
### <a name="full-typenamemembername-qualified-attributes"></a>完全限定的类型属性  
 *TypeName*。*memberName*窗体的属性的实际工作比仅仅使用路由的事件的情况更为普遍。 但在其他情况下该窗体是多余的应避免它，如果只是为了实现标记样式和可读性。 在以下示例中，这三个对引用<xref:System.Windows.Controls.Control.Background%2A>属性是完全等效：  
  
 [!code-xaml[XAMLOvwSupport#TypeNameProp](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenameprop)]  
  
 `Button.Background` 有效，因为该属性的限定的查找<xref:System.Windows.Controls.Button>成功 (<xref:System.Windows.Controls.Control.Background%2A>从控件继承) 和<xref:System.Windows.Controls.Button>是对象元素的类或基类。 `Control.Background` 有效，因为<xref:System.Windows.Controls.Control>类实际上定义了<xref:System.Windows.Controls.Control.Background%2A>并<xref:System.Windows.Controls.Control>是<xref:System.Windows.Controls.Button>基类。  
  
 但是，以下*typeName*。*memberName*窗体示例不起作用，因此显示为注释：  
  
 [!code-xaml[XAMLOvwSupport#TypeNameBadProp](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenamebadprop)]  
  
 <xref:System.Windows.Controls.Label> 作为另一个派生的类的<xref:System.Windows.Controls.Control>，并且如果已指定`Label.Background`内<xref:System.Windows.Controls.Label>对象元素，这种用法会起作用。 但是，由于<xref:System.Windows.Controls.Label>不是类或类的基类<xref:System.Windows.Controls.Button>，然后处理指定的 XAML 处理器行为是`Label.Background`作为附加属性。 `Label.Background` 不是可附加的属性，并将故障这种用法。  
  
### <a name="basetypenamemembername-property-elements"></a>baseTypeName.memberName 属性元素  
 如何以类似方式*typeName*。*memberName*窗体适用于特性语法*b t y p*。*memberName*语法适用于属性元素语法。 例如，以下语法的工作原理：  
  
 [!code-xaml[XAMLOvwSupport#GoofyPE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofype)]  
  
 在这里，为提供的属性元素`Control.Background`即使属性元素已包含在`Button`。  
  
 但是，正如*typeName*。*memberName*属性，用于窗体*b t y p*。*memberName*是在标记中，良好的样式，应避免它。  
  
## <a name="see-also"></a>请参阅
- [XAML 概述 (WPF)](xaml-overview-wpf.md)
- [XAML Namespace （x:）语言功能](../../xaml-services/xaml-namespace-x-language-features.md)
- [WPF XAML 扩展](wpf-xaml-extensions.md)
- [依赖项属性概述](dependency-properties-overview.md)
- [TypeConverter 和 XAML](typeconverters-and-xaml.md)
- [XAML 及 WPF 的自定义类](xaml-and-custom-classes-for-wpf.md)
