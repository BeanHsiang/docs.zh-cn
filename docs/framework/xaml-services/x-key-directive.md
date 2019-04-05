---
title: x:Key 指令
ms.date: 03/30/2017
f1_keywords:
- xKey
- Key
- x:Key
helpviewer_keywords:
- x:Key attribute [XAML Services]
- Key attribute in XAML [XAML Services]
- XAML [XAML Services], x:Key attribute
ms.assetid: 1985cd45-f197-42d5-b75e-886add64b248
ms.openlocfilehash: 8474fd5ee6f9f6e6dccda5fb57fbed9ddd787c26
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58046207"
---
# <a name="xkey-directive"></a>x:Key 指令
唯一标识创建和引用 XAML 定义的字典中的元素。 添加`x:Key`XAML 对象元素的值是标识资源字典，例如在 WPF 中的资源的最常见方法<xref:System.Windows.ResourceDictionary>。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```  
<object x:Key="stringKeyValue".../>  
-or-  
<object x:Key="{markupExtensionUsage}".../>  
```  
  
## <a name="xaml-attribute-usage-wpf-specific"></a>XAML 特性用法 （特定于 WPF 的）  
  
```  
<object.Resources>  
  <object x:Key="stringKeyValue".../>  
</object.Resources>  
-or-  
<object.Resources>  
  <object x:Key="{markupExtensionUsage}".../>  
</object.Resources>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`stringKeyValue`|要用作键的文本字符串。 文本字符串必须符合[XamlName 语法](xamlname-grammar.md)。|  
|`markupExtensionUsage`|在标记扩展分隔符内{}，提供一个对象，用作键的标记扩展用法。 请参阅“备注”。|  
  
## <a name="remarks"></a>备注  
 `x:Key` 支持 XAML 资源字典概念。 作为一种语言的 XAML 不定义资源字典实现，而由特定 UI 框架。 若要了解有关如何在 WPF 中实现 XAML 资源字典的详细信息，请参阅[XAML 资源](../wpf/advanced/xaml-resources.md)。  
  
 在 XAML 2006 和 WPF，`x:Key`必须为属性提供。 您仍可以使用非字符串键，但这需要标记扩展用法来提供特性窗体中的非字符串值。 如果使用 XAML 2009`x:Key`可以指定为元素，以显式支持以外的对象类型进行键控的字典字符串而不需要标记扩展中间语言。 请参阅本主题中的"XAML 2009"一节。 备注部分的其余部分特别适用于 XAML 2006 实现。  
  
 属性值`x:Key`可以中定义的任何字符串[XamlName 语法](xamlname-grammar.md)也可以是计算通过标记扩展的对象。 从 WPF 示例，请参阅"WPF 用法说明"。  
  
 父元素的子元素<xref:System.Collections.IDictionary>实现通常必须包括`x:Key`指定该字典中的唯一键值的属性。 Frameworks 可以实现具有别名的键属性将替换为`x:Key`对特定类型; 定义此类属性的类型应归因与<xref:System.Windows.Markup.DictionaryKeyPropertyAttribute>。  
  
 指定的代码等效项`x:Key`是用于基础的关键<xref:System.Collections.IDictionary>。 例如， `x:Key` WPF 中的资源是等效的值应用于标记`key`的参数<xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType>时将资源添加到 WPF<xref:System.Windows.ResourceDictionary>在代码中。  
  
## <a name="wpf-usage-notes"></a>WPF 用法说明  
 子对象的父对象，它是<xref:System.Collections.IDictionary>实现，如 WPF <xref:System.Windows.ResourceDictionary>，通常必须包括`x:Key`特性和密钥值必须是唯一的字典中。 有两个值得注意的例外情况：  
  
-   某些 WPF 类型声明一个隐式字典用法键。 例如，<xref:System.Windows.Style>与<xref:System.Windows.Style.TargetType%2A>，或<xref:System.Windows.DataTemplate>与<xref:System.Windows.DataTemplate.DataType%2A>，可以采用<xref:System.Windows.ResourceDictionary>，并使用隐式键。  
  
-   WPF 支持合并的资源字典概念。 可之间合并的字典中，共享密钥和共享的键行为可以使用访问<xref:System.Windows.FrameworkContentElement.FindResource%2A>。 有关详细信息，请参阅[合并资源字典](../wpf/advanced/merged-resource-dictionaries.md)。  
  
 在整个 WPF XAML 实现和应用程序模型中，不会 XAML 标记编译器检查键唯一性。 相反，丢失或非唯一`x:Key`值会导致加载时 XAML 分析器错误。 但是，WPF 的字典的 Visual Studio 处理可以通常在设计阶段注意此类错误。  
  
 请注意，在所示的语法<xref:System.Windows.ResourceDictionary>对象是隐式的 WPF XAML 处理器如何生成一个集合来填充<xref:System.Windows.FrameworkElement.Resources%2A>集合。 一个<xref:System.Windows.ResourceDictionary>未通常提供显式为元素在标记中，但也可以是在某些情况下，如果为了清楚起见希望 (它将是一个集合对象元素之间<xref:System.Windows.FrameworkElement.Resources%2A>属性元素，并在其中的项填充字典）。 有关为什么集合对象几乎始终是在标记中的隐式元素的信息，请参阅[XAML 语法详述](../wpf/advanced/xaml-syntax-in-detail.md)。  
  
 在 WPF XAML 实现中，通过定义资源字典键处理<xref:System.Windows.ResourceKey>抽象类。 但是，WPF XAML 处理器会生成有关基于其用法的密钥不同的基础扩展类型。 例如，键<xref:System.Windows.DataTemplate>或任何派生的类单独处理的并生成一个不同<xref:System.Windows.DataTemplateKey>对象。  
  
 键和名称使用不同的指令和语言元素 (`x:Key`与`x:Name`) 中的基本 XAML 定义。 键和名称也使用不同的情况下的 WPF 定义和应用程序的这些概念。 有关详细信息，请参阅[WPF XAML 名称范围](../wpf/advanced/wpf-xaml-namescopes.md)。  
  
 如前面所述，密钥的值可以通过标记扩展提供，并可以是字符串值以外的值。 示例 WPF 方案是，值`x:Key`可能[ComponentResourceKey](../wpf/advanced/componentresourcekey-markup-extension.md)。 某些控件公开该类型的自定义样式资源的影响而不替换样式的外观和行为，该控件的样式键。 此类密钥的一个示例是<xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A>。  
  
 WPF 合并的词典功能引入了关于键唯一性和键查找行为的其他注意事项。 有关详细信息，请参阅[合并资源字典](../wpf/advanced/merged-resource-dictionaries.md)。  
  
## <a name="xaml-2009"></a>XAML 2009  
 XAML 2009 解除此限制的`x:Key`始终以特性形式提供。  
  
 在 WPF 中，您可以使用 XAML 2009 功能，但仅针对未标记编译的 XAML。 WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  
  
 您可以指定在 XAML 2009 下`x:Key`元素通过下面的用法：  
  
### <a name="xaml-element-usage-xaml-2009-only"></a>XAML 元素使用情况 (仅 XAML 2009)  
  
```  
<object>  
  <x:Key>  
keyObject  
  </x:Key>  
...  
</object>  
```  
  
### <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`keyObject`|用作键的对象的对象元素给定`object`专用字典中。|  
  
-   使用此类容器/父级不在此处显示。 `object` 应为表示专用的词典实现的对象元素的子级。 `keyObject` 应为对象实例 （或值类型的值），适合用作该特定专用的词典实现的密钥。  
  
-   WPF 不实现需要这种用法的字典。 对象键是更常规 XAML 语言，其中在 XAML 中创建字典是需要某些自定义词典方案可能是有用的功能。 有关使用非字符串键用于资源的隐式样式等 WPF 功能，用于建立或指定键的其他方法存在，因此不需要使用对象键。  
  
-   *keyObject*也可能是在对象元素窗体，而不是直接对象实例中的标记扩展用法。  
  
## <a name="silverlight-usage-notes"></a>Silverlight Usage 备注。  
 `x:Key` 适用于 Silverlight 单独说明了。 有关详细信息，请参阅[XAML Namespace （x:）语言功能 (Silverlight)](https://go.microsoft.com/fwlink/?LinkId=199081)。  
  
## <a name="see-also"></a>请参阅
- [XAML 资源](../wpf/advanced/xaml-resources.md)
- [资源和代码](../wpf/advanced/resources-and-code.md)
- [StaticResource 标记扩展](../wpf/advanced/staticresource-markup-extension.md)
