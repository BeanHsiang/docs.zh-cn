---
title: x:Type 标记扩展
ms.date: 03/30/2017
f1_keywords:
- x:TypeExtension
- Type
- x:Type
- xType
- TypeExtension
helpviewer_keywords:
- x:Type markup extension [XAML Services]
- XAML [XAML Services], x:Type markup extension
- XAML [XAML Services], TargetType attribute
- TargetType attribute [XAML Services]
- Type markup extension in XAML [XAML Services]
ms.assetid: e0e0ce6f-e873-49c7-8ad7-8b840eb353ec
ms.openlocfilehash: 86e5619774cc1512e39fa2fb50f4c0ba5f1d074c
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58042094"
---
# <a name="xtype-markup-extension"></a>x:Type 标记扩展
提供 CLR<xref:System.Type>是指定的 XAML 类型的基础类型的对象。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```xaml  
<object property="{x:Type prefix:typeNameValue}" .../>  
```  
  
## <a name="xaml-object-element-usage"></a>XAML 对象元素用法  
  
```xaml  
<x:Type TypeName="prefix:typeNameValue"/>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`prefix`|可选。 将非默认 XAML 命名空间映射前缀。 指定前缀经常是不必要。 请参阅“备注”。|  
|`typeNameValue`|必需。 类型名称解析为当前的默认 XAML 命名空间;或指定的映射前缀如果`prefix`提供。|  
  
## <a name="remarks"></a>备注  
 `x:Type`标记扩展有函数相似`typeof()`C# 中的运算符或`GetType`运算符在 Microsoft Visual Basic。  
  
 `x:Type`标记扩展提供接受类型的属性从字符串转换行为<xref:System.Type>。 输入是 XAML 类型。 输入的 XAML 类型和 CLR 的输出之间的关系<xref:System.Type>是输出<xref:System.Type>是<xref:System.Xaml.XamlType.UnderlyingType%2A>输入的<xref:System.Xaml.XamlType>，查找所需的后<xref:System.Xaml.XamlType>基于 XAML 架构上下文和<xref:System.Windows.Markup.IXamlTypeResolver>上下文提供的服务。  
  
 在.NET Framework XAML 服务中，对此标记扩展的处理由定义<xref:System.Windows.Markup.TypeExtension>类。  
  
 在特定的框架实现中，某些属性，采用<xref:System.Type>值可直接接受类型的名称 (该类型的字符串值`Name`)。 但是，实现此行为是复杂的方案。 有关示例，请参阅后面的"WPF 用法说明"部分。  
  
 特性语法是最常用于该标记扩展的语法。 在 `x:Type` 标识符字符串之后提供的字符串标记被指定为基础 <xref:System.Windows.Markup.TypeExtension.TypeName%2A> 扩展类的 <xref:System.Windows.Markup.TypeExtension> 值。 在.NET Framework XAML 服务，基于 CLR 类型的默认 XAML 架构上下文下，此属性的值是<xref:System.Reflection.MemberInfo.Name%2A>所需的类型，或包含的<xref:System.Reflection.MemberInfo.Name%2A>跟在非默认 XAML 命名空间的前缀映射。  
  
 `x:Type`可以在对象元素语法中使用标记扩展。 在这种情况下，指定的值<xref:System.Windows.Markup.TypeExtension.TypeName%2A>正确初始化该扩展所需的属性。  
  
 `x:Type`标记扩展还可以用作详细属性; 但是此，请使用不是典型： `<object property="{x:Type TypeName=typeNameValue}" .../>`  
  
## <a name="wpf-usage-notes"></a>WPF 用法说明  
  
### <a name="default-xaml-namespace-and-type-mapping"></a>默认 XAML Namespace 和类型映射  
 WPF 编程的默认 XAML 命名空间包含大部分所需的典型 XAML 方案; XAML 类型因此，引用 XAML 类型的值时，通常可以避免前缀。 您可能需要，如果所引用的类型，从自定义程序集或类型存在于 WPF 程序集中，但来自未映射到默认 XAML 命名空间的 CLR 命名空间映射前缀。 有关前缀、 XAML 命名空间和映射 CLR 命名空间的详细信息，请参阅[XAML 命名空间和 WPF XAML 的 Namespace 映射](../wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
### <a name="type-properties-that-support-typename-as-string"></a>类型属性的支持类型名称作为-字符串  
 WPF 支持技术，使指定类型的某些属性的值<xref:System.Type>而无需`x:Type`标记扩展用法。 相反，您可以指定为的类型命名的字符串的值。 示例包括<xref:System.Windows.Controls.ControlTemplate.TargetType%2A?displayProperty=nameWithType>和<xref:System.Windows.Style.TargetType%2A?displayProperty=nameWithType>。 通过类型转换器或标记扩展不提供此行为的支持。 相反，这是通过实现延迟行为<xref:System.Windows.FrameworkElementFactory>。  
  
 Silverlight 支持类似的约定。 事实上，Silverlight 目前不支持`{x:Type}`XAML 语言支持，并且不接受`{x:Type}`之外，旨在支持 WPF Silverlight XAML 迁移在某些环境下的用法。 因此，类型名称作为字符串行为是内置于所有 Silverlight 本机属性评估其中<xref:System.Type>的值。  
  
## <a name="xaml-2009"></a>XAML 2009  
 XAML 2009 提供额外支持泛型类型，并修改的功能行为`x:TypeArguments`和`x:Type`能够提供此支持。  
  
-   `x:TypeArguments` 并且，泛型对象实例化的关联的对象元素可在根以外的其他元素。 有关详细信息，请参阅"XAML 2009"一节[X:typearguments 指令](x-typearguments-directive.md)。  
  
-   XAML 2009 支持用于在标记中指定的泛型类型约束的语法。 这可由`x:TypeArguments`，也可由`x:Type`，或结合使用的两个功能。  
  
-   WPF XAML 实现的负载也将此功能添加到使用类型的某些 framework 属性的隐式类型转换行为处理 XAML 2009 时<xref:System.Type>。  
  
 在 WPF 中，可以使用 XAML 2009 功能但仅针对松散 XAML (未标记编译的 XAML) 中。 WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Style>
- [样式设置和模板化](../wpf/controls/styling-and-templating.md)
- [XAML 概述 (WPF)](../wpf/advanced/xaml-overview-wpf.md)
- [标记扩展和 WPF XAML](../wpf/advanced/markup-extensions-and-wpf-xaml.md)
