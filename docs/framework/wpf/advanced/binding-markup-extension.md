---
title: 绑定标记扩展
ms.date: 03/30/2017
f1_keywords:
- Binding
helpviewer_keywords:
- Binding markup extensions [WPF]
- XAML [WPF], Binding markup extension
ms.assetid: 83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63
ms.openlocfilehash: 960bc953345e3f6ed632b7a136b626978c8a9bce
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379180"
---
# <a name="binding-markup-extension"></a>绑定标记扩展
延迟输入属性值，将数据绑定值，创建一个中间表达式对象，并解释适用于的元素，并在运行时与其绑定的数据上下文。  
  
## <a name="binding-expression-usage"></a>绑定表达式的使用  
  
```  
<object property="{Binding}" .../>  
-or-  
<object property="{Binding  bindProp1=value1[, bindPropN=valueN]*}" ...  
/>  
-or-  
<object property="{Binding path}" .../>  
-or  
<object property="{Binding path[, bindPropN=valueN]*}" .../>  
```  
  
## <a name="syntax-notes"></a>语法说明  
 在这些语法`[]`和`*`不是文本。 它们是一部分表示法表示的零个或多个*绑定属性*`=`*值*可以使用对，使用`,`它们与上述之间的分隔符*绑定属性* `=`*值*对。  
  
 在"绑定属性，可以使用绑定扩展设置"一节中列出的任何的属性可以改为设置使用特性的<xref:System.Windows.Data.Binding>对象元素。 但是，这并非真正意义的标记扩展用法<xref:System.Windows.Data.Binding>，它是一种 XAML 处理的设置的 CLR 属性的属性只是常规<xref:System.Windows.Data.Binding>类。 换而言之， `<Binding` *绑定属性 1*`="`*value1* `"[` *绑定属性 n*`="`*valueN*`"]*/>`是属性的等效语法<xref:System.Windows.Data.Binding>对象而不是元素用法`Binding`表达式的使用。 若要了解有关的特定属性的 XAML 属性用法<xref:System.Windows.Data.Binding>，请参阅相关的属性的"XAML 属性用法"部分<xref:System.Windows.Data.Binding>.NET Framework 类库中。  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`bindProp1, bindPropN`|名称<xref:System.Windows.Data.Binding>或<xref:System.Windows.Data.BindingBase>属性来设置。 不是所有<xref:System.Windows.Data.Binding>属性可以用来设置`Binding`扩展和某些属性是可在设置`Binding`表达式只能通过进一步使用嵌套标记扩展。 请参阅"绑定属性，可以将设置与绑定扩展"部分。|  
|`value1, valueN`|要将属性设置为的值。 属性值处理方法是最终特定于类型和特定的逻辑<xref:System.Windows.Data.Binding>要设置属性。|  
|`path`|设置的隐式的路径字符串<xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>属性。 另请参阅[PropertyPath XAML 语法](propertypath-xaml-syntax.md)。|  
  
## <a name="unqualified-binding"></a>非限定 {Binding}  
 `{Binding}` "绑定表达式使用情况"中所示的使用情况创建<xref:System.Windows.Data.Binding>对象的默认值，其中包括一个初始<xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>的`null`。 这仍可在许多情况下，因为创建<xref:System.Windows.Data.Binding>可能依赖于重要的数据绑定属性如<xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>和<xref:System.Windows.Data.Binding.Source%2A?displayProperty=nameWithType>设置在运行时数据上下文中。 数据上下文的概念的详细信息，请参阅[数据绑定](../data/data-binding-wpf.md)。  
  
## <a name="implicit-path"></a>隐式的路径  
 `Binding`标记扩展用法<xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>作为概念"默认属性"，其中`Path=`不需要该表达式中出现。 如果指定`Binding`具有隐式路径表达式，隐式的路径必须首先出现在表达式中，在任何其他之前`bindProp` = `value`对，其中<xref:System.Windows.Data.Binding>按名称指定属性。 例如： `{Binding PathString}`，其中`PathString`是一个字符串的计算结果为的值，<xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>中<xref:System.Windows.Data.Binding>创建的标记扩展用法。 您可以与其他命名属性的隐式路径后追加逗号分隔符，例如， `{Binding LastName, Mode=TwoWay}`。  
  
## <a name="binding-properties-that-can-be-set-with-the-binding-extension"></a>可以使用绑定扩展设置的绑定属性  
 本主题中所示的语法使用泛型`bindProp` = `value`近似值，因为提供了许多的读/写属性<xref:System.Windows.Data.BindingBase>或<xref:System.Windows.Data.Binding>，可以通过设置`Binding`标记扩展 /表达式语法。 它们可以按任何顺序，除了隐式设置<xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>。 (您可以选择显式指定`Path=`，在这种情况下可以按任何顺序设置它)。 基本上，您可以设置零个或多个属性，下面的列表中使用`bindProp` = `value`对以逗号分隔。  
  
 这些属性值的几个需要的对象类型，不支持 XAML 中的文本语法中的本机类型转换，因此需标记扩展设置作为属性值。 检查每个属性以获取详细信息;.NET Framework 类库中的 XAML 属性用法部分有关使用 XAML 特性语法使用字符串或而无需进一步的标记扩展用法基本上是在中指定的值相同`Binding`表达式，与您未放置引号将每个异常`bindProp` =`value`在`Binding`表达式。  
  
-   <xref:System.Windows.Data.BindingBase.BindingGroupName%2A>： 一个字符串，标识可能的绑定组。 这是一个相对高级的绑定的概念;请参阅参考页面的<xref:System.Windows.Data.BindingBase.BindingGroupName%2A>。  
  
-   <xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A>：布尔值，可以是`true`或`false`。 默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.Converter%2A>： 可设置为`bindProp` = `value`在表达式中，但若要执行此操作的字符串值，需要对象引用，如[StaticResource 标记扩展](staticresource-markup-extension.md)。 在这种情况下，值是自定义转换器类的实例。  
  
-   <xref:System.Windows.Data.Binding.ConverterCulture%2A>： 可设置为基于标准的标识符; 表达式中请参阅参考主题<xref:System.Windows.Data.Binding.ConverterCulture%2A>。  
  
-   <xref:System.Windows.Data.Binding.ConverterParameter%2A>： 可设置为`bindProp` = `value`字符串表达式，但这是依赖于所传递的参数的类型。 如果传递引用类型的值，这种用法需要对象引用，如嵌套[StaticResource 标记扩展](staticresource-markup-extension.md)。  
  
-   <xref:System.Windows.Data.Binding.ElementName%2A>： 与互斥<xref:System.Windows.Data.Binding.RelativeSource%2A>和<xref:System.Windows.Data.Binding.Source%2A>; 每个绑定属性表示的这些特定的绑定方法。 请参阅[数据绑定概述](../data/data-binding-overview.md)。  
  
-   <xref:System.Windows.Data.BindingBase.FallbackValue%2A>： 可设置为`bindProp` = `value`字符串表达式，但这是依赖于所传递的值的类型。 如果传递引用类型，需要对象引用，如嵌套[StaticResource 标记扩展](staticresource-markup-extension.md)。  
  
-   <xref:System.Windows.Data.Binding.IsAsync%2A>：布尔值，可以是`true`或`false`。 默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.Mode%2A>:*值*是中的常量名<xref:System.Windows.Data.BindingMode>枚举。 例如 `{Binding Mode=OneWay}`。  
  
-   <xref:System.Windows.Data.Binding.NotifyOnSourceUpdated%2A>：布尔值，可以是`true`或`false`。 默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.NotifyOnTargetUpdated%2A>：布尔值，可以是`true`或`false`。 默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.NotifyOnValidationError%2A>：布尔值，可以是`true`或`false`。 默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.Path%2A>： 为数据对象或常规对象模型中描述的路径的字符串。 格式为遍历不能进行详细介绍本主题中的对象模型提供多个不同的约定。 请参阅[PropertyPath XAML 语法](propertypath-xaml-syntax.md)。  
  
-   <xref:System.Windows.Data.Binding.RelativeSource%2A>： 与互斥<xref:System.Windows.Data.Binding.ElementName%2A>和<xref:System.Windows.Data.Binding.Source%2A>; 每个绑定属性表示的这些特定的绑定方法。 请参阅[数据绑定概述](../data/data-binding-overview.md)。 需要一个嵌套[RelativeSource 标记扩展](relativesource-markupextension.md)使用情况，以指定的值。  
  
-   <xref:System.Windows.Data.Binding.Source%2A>： 与互斥<xref:System.Windows.Data.Binding.RelativeSource%2A>和<xref:System.Windows.Data.Binding.ElementName%2A>; 每个绑定属性表示的这些特定的绑定方法。 请参阅[数据绑定概述](../data/data-binding-overview.md)。 需要嵌套的扩展用法，通常[StaticResource 标记扩展](staticresource-markup-extension.md)到对象数据源引用键控的资源字典中。  
  
-   <xref:System.Windows.Data.BindingBase.StringFormat%2A>： 一个字符串，描述绑定的数据的字符串格式约定。 这是一个相对高级的绑定的概念;请参阅参考页面的<xref:System.Windows.Data.BindingBase.StringFormat%2A>。  
  
-   <xref:System.Windows.Data.BindingBase.TargetNullValue%2A>： 可设置为`bindProp` = `value`字符串表达式，但这是依赖于所传递的参数的类型。 如果传递引用类型的值需要对象引用，如嵌套[StaticResource 标记扩展](staticresource-markup-extension.md)。  
  
-   <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>:*值*是中的常量名<xref:System.Windows.Data.UpdateSourceTrigger>枚举。 例如 `{Binding UpdateSourceTrigger=LostFocus}`。 特定控件可能具有不同的默认值为此绑定属性。 请参阅 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>。  
  
-   <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A>：布尔值，可以是`true`或`false`。 默认值为 `false`。 请参阅“备注”。  
  
-   <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A>：布尔值，可以是`true`或`false`。 默认值为 `false`。 请参阅“备注”。  
  
-   <xref:System.Windows.Data.Binding.XPath%2A>： 描述到 XML 数据源的 XMLDOM 的路径的字符串。 请参阅[绑定到 XML 数据使用 XMLDataProvider 和 XPath 查询](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)。  
  
 以下是属性的<xref:System.Windows.Data.Binding>不能使用设置的`Binding`标记扩展 /`{Binding}`表达式形式。  
  
-   <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A>： 此属性需要对回调实现的引用。 不能在 XAML 语法引用回调/事件处理程序之外的方法。  
  
-   <xref:System.Windows.Data.Binding.ValidationRules%2A>： 该属性会采用的泛型集合<xref:System.Windows.Controls.ValidationRule>对象。 这可能表示为属性元素中<xref:System.Windows.Data.Binding>对象元素，但具有中的使用情况没有现成的特性分析技术`Binding`表达式。 请参阅参考主题<xref:System.Windows.Data.Binding.ValidationRules%2A>。  
  
-   <xref:System.Windows.Data.Binding.XmlNamespaceManager%2A>  
  
## <a name="remarks"></a>备注  
  
> [!IMPORTANT]
>  依赖关系属性在优先级方面，`Binding`表达式等效于本地设置值。 如果将以前的属性的本地值`Binding`表达式，`Binding`完全删除。 有关详细信息，请参阅[依赖属性值优先级](dependency-property-value-precedence.md)。  
  
 本主题未介绍基本级别的数据绑定。 请参阅[数据绑定概述](../data/data-binding-overview.md)。  
  
> [!NOTE]
>  <xref:System.Windows.Data.MultiBinding> 并<xref:System.Windows.Data.PriorityBinding>不支持[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]扩展语法。 应改用属性元素。 请参阅参考主题<xref:System.Windows.Data.MultiBinding>和<xref:System.Windows.Data.PriorityBinding>。  
  
 有关 XAML 的布尔值为不区分大小写。 例如，您可以指定`{Binding NotifyOnValidationError=true}`或`{Binding NotifyOnValidationError=True}`。  
  
 涉及数据验证的绑定通常由显式指定`Binding`元素而不是`{Binding ...}`表达式，并设置<xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A>或<xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A>在表达式中不常见。 这是因为配套属性<xref:System.Windows.Data.Binding.ValidationRules%2A>不能以表达式形式轻松设置。 有关详细信息，请参阅[实现绑定验证](../data/how-to-implement-binding-validation.md)。  
  
 `Binding` 是标记扩展。 当要求转义特性值应为非文本值或处理程序名称，并且要求是更具有全局性比基于特定的类型或属性特性化类型转换器，通常会实现标记扩展。 在 XAML 使用的所有标记扩展`{`和`}`是依据 XAML 处理器认定标记扩展必须处理字符串的内容的约定其特性语法中的字符。 有关详细信息，请参阅[标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)。  
  
 `Binding` 是中的异常标记扩展<xref:System.Windows.Data.Binding>实现 WPF 的 XAML 实现的扩展功能的类还实现多种其他方法和与 XAML 无关的属性。 其他成员旨在使<xref:System.Windows.Data.Binding>可以解决许多数据绑定方案，除了作为 XAML 标记扩展的更多情形且自包含类。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Data.Binding>
- [数据绑定概述](../data/data-binding-overview.md)
- [XAML 概述 (WPF)](xaml-overview-wpf.md)
- [标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)
