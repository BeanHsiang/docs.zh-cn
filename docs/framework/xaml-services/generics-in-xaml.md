---
title: XAML 中的泛型
ms.date: 03/30/2017
helpviewer_keywords:
- generics [XAML Services]
ms.assetid: 835bfed7-585c-4216-ae67-b674edab8b92
ms.openlocfilehash: 219c710e8552ae3291c2b144c6048f4ff6710540
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58048916"
---
# <a name="generics-in-xaml"></a>XAML 中的泛型
.NET Framework XAML 服务实现在 System.Xaml 中为使用 CLR 的泛型类型提供支持。 此支持包括作为类型参数指定的泛型约束和通过调用适当强制该约束`Add`泛型集合用例的方法。 本主题介绍使用和引用 XAML 中的泛型类型的方面。  
  
## <a name="xtypearguments"></a>x:TypeArguments  
 `x:TypeArguments` 由 XAML 语言定义一条指令。 当用作泛型类型，由提供支持的 XAML 类型的成员时`x:TypeArguments`约束类型的后备构造函数的泛型参数传递。 适用于.NET Framework XAML 服务的引用语法使用的`x:TypeArguments`，其中包括语法示例，请参阅[X:typearguments 指令](x-typearguments-directive.md)。  
  
 因为`x:TypeArguments`采用一个字符串，并具有类型转换器支持，它通常在 XAML 特性用法中声明。  
  
 在 XAML 节点流中，通过声明`x:TypeArguments`可从此<xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=nameWithType>在`StartObject`节点流中的位置。 返回值<xref:System.Xaml.XamlType.TypeArguments%2A?displayProperty=nameWithType>是一系列<xref:System.Xaml.XamlType>值。 可以通过调用来发出的 XAML 类型是否表示泛型类型确定<xref:System.Xaml.XamlType.IsGeneric%2A?displayProperty=nameWithType>。  
  
## <a name="rules-and-syntax-conventions-for-generics-in-xaml"></a>规则和 XAML 中的泛型的语法约定  
 在 XAML 中，必须始终将泛型类型表示为受约束的泛型;不受约束的泛型根本不存在于 XAML 类型系统或 XAML 节点流中，且不能在 XAML 标记中表示。 中的嵌套的类型约束的泛型引用的情况下用于 XAML 特性语法只能引用一个泛型`x:TypeArguments`，或用例其中`x:Type`提供泛型类型的 CLR 类型引用。 这通过支持<xref:System.Xaml.Schema.XamlTypeTypeConverter>由.NET Framework XAML 服务定义的类。  
  
 XAML 特性语法形式情况下启用<xref:System.Xaml.Schema.XamlTypeTypeConverter>更改典型 MSIL / 用角度的 CLR 语法约定的类型和约束的泛型，方括号，而是将替换为约束容器的括号。 有关示例，请参阅[X:typearguments 指令](x-typearguments-directive.md)。  
  
## <a name="generics-and-xaml-2009-features"></a>泛型和 XAML 2009 功能  
 如果使用 XAML 2009 而不是将 CLR 映射基类型来获取常用语言基元的 XAML 类型转换，则可以使用[XAML 2009 内置类型](built-in-types-for-common-xaml-language-primitives.md)中的信息项作为`x:TypeArguments`。 例如，您可以声明以下 (前缀映射不显示，但`x`是 XAML 2009 的 XAML 语言 XAML 命名空间):  
  
```xaml  
<my:BusinessObject x:TypeArguments="x:String,x:Int32"/>  
```  
  
## <a name="generics-support-in-wpf-and-other-v35-frameworks"></a>WPF 与其他 v3.5 框架中的泛型支持  
 有关 XAML 2006 使用情况时专门针对 WPF 中， [X:class](x-class-directive.md)还必须为相同的元素上提供`x:TypeArguments`，并且该元素必须是一个 XAML 文档中的根元素。 根元素必须映射到具有至少一个类型参数的泛型类型。 例如， <xref:System.Windows.Navigation.PageFunction%601>。  
  
 可能的解决方法，以支持泛型用法包括定义自定义标记扩展可以返回的泛型类型，或提供一个包装类派生自泛型类型，但将在其自己的类定义中的泛型约束的定义。  
  
 在 WPF 和面向[!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]，可以使用 XAML 2009 功能一起使用`x:TypeArguments`，但仅限松散 XAML (未标记编译的 XAML)。 WPF 的已编译标记的 XAML 以及 XAML 的 BAML 形式当前不支持 XAML 2009 关键字和功能。  
  
 有关 Windows Workflow Foundation 中的自定义工作流[!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)]不支持泛型的 XAML 用法。  
  
## <a name="see-also"></a>请参阅
- [x:TypeArguments 指令](x-typearguments-directive.md)
- [x:Class 指令](x-class-directive.md)
- [常见 XAML 语言基元的内置类型](built-in-types-for-common-xaml-language-primitives.md)
