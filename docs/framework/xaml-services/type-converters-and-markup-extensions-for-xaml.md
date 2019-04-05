---
title: XAML 的类型转换器和标记扩展
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converter services
- XAML [XAML Services], value converters
- XAML [XAML Services], markup extension services
- value converters for XAML [XAML Services]
- XAML [XAML Services], service context
ms.assetid: db07a952-05ce-4aa4-b6f9-aac7397d0326
ms.openlocfilehash: 1704a7a86e89685763da7bf49a67c1fe8373124a
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58050540"
---
# <a name="type-converters-and-markup-extensions-for-xaml"></a>XAML 的类型转换器和标记扩展
类型转换器和标记扩展是 XAML 类型系统和 XAML 编写器用来生成对象图组件的两种技术。 尽管类型转换器和标记扩展共享一些特征，但它们在 XAML 节点流中以不同的方式表示。 在本文档集中，类型转换器、标记扩展和类似的构造有时统称为值转换器。  
  
<a name="value_converters"></a>   
## <a name="value-converters"></a>值转换器  
 在 XAML 中，值转换器能用于各种方案。 以下列表显示了 XAML 中不同类型的值转换器：  
  
-   类型转换器  
  
-   标记扩展  
  
-   值序列化程序  
  
-   为 XAML 文本语法提供逻辑的相关类或支持类  
  
<a name="type_converters"></a>   
## <a name="type-converters"></a>类型转换器  
 在 .NET Framework XAML 服务定义中，类型转换器是从 CLR <xref:System.ComponentModel.TypeConverter> 类派生的类。 <xref:System.ComponentModel.TypeConverter> 是 XAML 出现之前是 Microsoft.NET Framework 中的类。 它的原始用途是向 [!INCLUDE[TLA2#tla_ide](../../../includes/tla2sharptla-ide-md.md)] 属性提供对属性窗口和类似的基于文本的编辑隐喻的支持。 对 .NET Framework 引入 XAML 则使用 <xref:System.ComponentModel.TypeConverter> 将文本语法（如某一特性值或 XAML 值节点中的）转换为对象。 <xref:System.ComponentModel.TypeConverter> 还可用于将对象值序列化为文本语法。 <xref:System.ComponentModel.TypeConverter> 在 Windows Presentation Foundation (WPF) 和 Windows Communication Foundation (WCF) 中的上一个特定于框架的 XAML 实现中还使用。 有关 XAML 中 <xref:System.ComponentModel.TypeConverter> 的更多信息，请参见 [Type Converters for XAML Overview](type-converters-for-xaml-overview.md)中特定于框架的 XAML 实现。  
  
<a name="markup_extensions"></a>   
## <a name="markup-extensions"></a>标记扩展  
 在 .NET Framework XAML 服务实现中，标记扩展是从 <xref:System.Windows.Markup.MarkupExtension> 类派生的类。 标记扩展是此窗体中一个源于 XAML 语言的概念。 你可以将标记扩展视为类似于可扩展转义序列的东西，它会调入服务类以提供其逻辑。 就标记而言，XAML 处理器普遍通过以文本字符串中一个左大括号 ({) 开头的文本序列来识别标记扩展。  
  
 标记扩展不同于类型转换器。 类型转换器通常与类型或成员相关联。 当创建对象图或进行序列化期间遇到与那些实体相关联的文本语法时会调用它们。  
  
 标记扩展与单一支持服务类相关联，但可以应用于任意成员值。 （但是，通过使用服务上下文，你可以实现你的标记扩展以有意将其应用限制为仅对某些成员或目标类型进行应用。）标记扩展可以替代类型转换器关联。 或者，可将其用于为本来不支持文本语法的成员指定特性值。  
  
 有关 XAML 的标记扩展实现模式的详细信息，请参阅 [Markup Extensions for XAML Overview](markup-extensions-for-xaml-overview.md)。  
  
> [!NOTE]
>  <xref:System.Windows.Markup.MarkupExtension> 和 <xref:System.Windows.Markup.ValueSerializer> 类型都在 <xref:System.Windows.Markup> 命名空间内而不是在 <xref:System.Xaml> 命名空间内。 这并不意味着这些类型是特定于本来会填充包含字符串的 CLR 命名空间的 WPF 或 Windows 窗体技术`Windows`。 <xref:System.Windows.Markup.MarkupExtension> 和 <xref:System.Windows.Markup.ValueSerializer> 都在 System.Xaml 程序集中，并且没有特定的框架依赖关系。 这些类型存在于 [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] 的CLR 命名空间中，并保留在 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 的 CLR 命名空间中，以避免破坏现有 WPF 项目中的引用。 有关详细信息，请参阅 [Types Migrated from WPF to System.Xaml](types-migrated-from-wpf-to-system-xaml.md)。  
  
<a name="value_serializers"></a>   
## <a name="value-serializers"></a>值序列化程序  
 <xref:System.Windows.Markup.ValueSerializer> 是针对将对象转换为字符串进行了优化的专用的类型转换器。 XAML 的 <xref:System.Windows.Markup.ValueSerializer> 可能完全不会实现 `ConvertFrom` 方法。 <xref:System.Windows.Markup.ValueSerializer> 实现以类似于 <xref:System.ComponentModel.TypeConverter> 实现的方式获取服务。 虚方法提供了一个输入 `context` 参数。 `context` 参数的类型为 <xref:System.Windows.Markup.IValueSerializerContext>，它继承自 <xref:System.IServiceProvider> 接口，并具有 <xref:System.IServiceProvider.GetService%2A> 方法。  
  
 在 XAML 类型系统中，对于使用 XAML 节点循环处理进行序列化的 XAML 编写器实现，由其自身的 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 属性报告与某一类型或成员相关联的值转换器。 执行序列化的 XAML 编写器的含义是，如果存在 <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> 和 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> ，则类型转换器应用于加载路径，值序列化应用于保存路径。 如果 <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> 存在但 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 为 `null`，则类型转换器也用于保存路径。  
  
<a name="other_value_converters"></a>   
## <a name="other-value-converters"></a>其他值转换器  
 值转换器具有超越类型转换器或标记扩展的特定模式的可扩展性。 但是，此自定义也需要由 .NET Framework XAML 服务提供的 XAML 类型系统的重新定义。 现有的 XAML 类型系统具有针对类型转换器、标记扩展和值序列化程序（而无针对值转换的自定义窗体的）的表示形式和报告系统。 如果你想要创建自定义值转换器，请使用 <xref:System.Xaml.Schema.XamlValueConverter%601> 类型。  
  
<a name="type_converters_and_markup_extensions_in_combination"></a>   
## <a name="type-converters-and-markup-extensions-in-combination"></a>组合使用类型转换器和标记扩展  
 标记扩展和类型转换器在 XAML 中用于不同情况。 尽管上下文可用于标记扩展用途，但通常不会在标记扩展实现中检查属性的类型转换行为（其中标记扩展提供了一个值）。 换言之，即使标记扩展返回一个文本字符串作为其 `ProvideValue` 输出，该字符串上应用于特定属性或属性值类型的类型转换行为也不会被调用。 通常，标记扩展的目的是处理字符串并返回不涉及任意类型转换器的对象。  
  
<a name="service_context_for_a_value_converter"></a>   
## <a name="service-context-for-a-value-converter"></a>值转换器的服务上下文  
 当实现值转换器时，你经常需要访问在其中应用了值转换器的上下文。 此上下文称为服务上下文。 服务上下文可能包括如下信息：活动的 XAML 架构上下文、对 XAML 架构上下文和 XAML 对象编写器提供的类型映射系统的访问权限等等。 有关可用与值转换器的服务上下文和如何访问服务上下文可能会提供的服务的详细信息，请参阅[可供类型转换器和标记扩展使用的服务上下文](service-contexts-available-to-type-converters-and-markup-extensions.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Markup.MarkupExtension>
- <xref:System.Xaml.XamlObjectWriter>
- [XAML 的标记扩展概述](markup-extensions-for-xaml-overview.md)
- [XAML 的类型转换器概述](type-converters-for-xaml-overview.md)
- [Service Contexts Available to Type Converters and Markup Extensions](service-contexts-available-to-type-converters-and-markup-extensions.md)
