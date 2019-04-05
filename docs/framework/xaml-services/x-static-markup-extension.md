---
title: x:Static 标记扩展
ms.date: 03/30/2017
f1_keywords:
- StaticExtension
- xStatic
- x:Static
helpviewer_keywords:
- x:Static markup extension [XAML Services]
- Static markup extension in XAML [XAML Services]
- XAML [XAML Services], x:Static markup extension
ms.assetid: 056aee79-7cdd-434f-8174-dfc856cad343
ms.openlocfilehash: 0956bb6daa60f947c1cd410ce4728da7d1bb707d
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58037691"
---
# <a name="xstatic-markup-extension"></a>x:Static 标记扩展
引用中定义的任何静态的值的代码实体[!INCLUDE[TLA#tla_cls](../../../includes/tlasharptla-cls-md.md)]– 合规的方式。 引用的静态属性可以用于提供在 XAML 中属性的值。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```xaml  
<object property="{x:Static prefix:typeName.staticMemberName}" .../>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
| | |  
|-|-|  
|`prefix`|可选。 指的是一个映射的非默认的 XAML 命名空间前缀。 `prefix` 所示显式使用因为很少引用来自默认 XAML 命名空间的静态属性。 请参阅“备注”。|  
|`typeName`|必需。 定义的所需的静态成员的类型的名称。|  
|`staticMemberName`|必需。 所需的静态值成员 （一个常量、 静态属性、 字段或枚举值） 的名称。|  
  
## <a name="remarks"></a>备注  

引用的代码实体必须是以下值之一：  
  
-   一个常量  
-   静态属性  
-   一个字段  
-   一个枚举值

指定任何其他代码实体，例如非静态属性，会导致编译时错误，如果 XAML 标记编译或 XAML 加载时间分析异常。  

可以进行`x:Static`对静态字段或属性不在当前的 XAML 文档; 的默认 XAML 命名空间中的引用但是，这需要的前缀映射。 几乎总是 XAML 文档的根元素上定义的 XAML 命名空间。  

与默认 XAML 架构上下文中运行时，可以通过.NET Framework XAML 服务及其 XAML 读取器和 XAML 编写器执行查找操作对于静态属性。 此 XAML 架构上下文中可以使用 CLR 反射对象关系图构造为提供所需的静态值。 `typeName`你指定为实际的 XAML 类型名称，不是 CLR 类型名称，尽管这些是实质上是相同的名称，或使用所有现有的基于 CLR 的 XAML 实现框架时使用的默认 XAML 架构上下文。  

进行时要格外小心`x:Static`不直接类型的属性的值的引用。 在 XAML 处理序列中，从标记扩展提供的值不调用其他值的转换。 这是 true 即使你`x:Static`引用创建文本字符串，并通常基于文本的字符串的属性值的值转换发生的特定成员或返回类型的任何成员值。  

特性语法是最常用于该标记扩展的语法。 在 `x:Static` 标识符字符串之后提供的字符串标记被指定为基础 <xref:System.Windows.Markup.StaticExtension.Member%2A> 扩展类的 <xref:System.Windows.Markup.StaticExtension> 值。  

有两个从技术上讲可能其他 XAML 用法。 但是，这些用法并不常见，因为它们是不必要地详细：  

1.  对象元素语法。

    ```xaml
    <x:Static Member="prefix:typeName.staticMemberName" ... />
    ```

2.  特性具有显式成员属性的初始化字符串的语法。

    ```xaml
    <object property="{x:Static Member=prefix:typeName.staticMemberName}" ... />
    ```

在.NET Framework XAML 服务实现中，对此标记扩展的处理由定义<xref:System.Windows.Markup.StaticExtension>类。  

`x:Static` 是标记扩展。 在 XAML 使用的所有标记扩展`{`和`}`约定所依据的 XAML 处理器识别标记扩展，必须提供一个值，其特性语法中的字符。 有关标记扩展的详细信息，请参阅 [Markup Extensions for XAML Overview](markup-extensions-for-xaml-overview.md)。  
  
## <a name="wpf-usage-notes"></a>WPF 用法说明  
 用于 WPF 编程的默认 XAML 命名空间不包含许多有用的静态属性和有用的静态属性大多具有支持类型转换器，可协助而无需使用如`{x:Static}`。 对于静态属性，必须映射 XAML 命名空间的前缀，如果以下项之一为 true:  
  
-   所引用的类型存在于 WPF 中但不是 WPF 默认 XAML 命名空间的一部分 ([!INCLUDE[TLA#tla_wpfxmlnsv1](../../../includes/tlasharptla-wpfxmlnsv1-md.md)])。 这是相当普遍使用`x:Static`。 例如，可以使用`x:Static`XAML 命名空间映射到引用<xref:System>CLR 命名空间和 mscorlib 程序集引用的静态属性以<xref:System.Environment>类。  
  
-   从自定义程序集引用类型。  
  
-   正在引用存在于 WPF 程序集中的类型，但该类型是未映射到 WPF 默认 XAML 命名空间的一部分的 CLR 命名空间中。 WPF 默认 XAML 命名空间到 CLR 命名空间的映射由中各种 WPF 程序集的定义 (有关这一概念的详细信息，请参阅[XAML 命名空间和 WPF XAML 的 Namespace 映射](../wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md))。 如果该 CLR 命名空间主要是组成通常不适用于 XAML，如类定义非映射 CLR 命名空间可存在<xref:System.Windows.Threading>。  
  
 有关如何为 WPF 使用前缀和 XAML 命名空间的详细信息，请参阅[XAML 命名空间和 WPF XAML Namespace 映射](../wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
## <a name="see-also"></a>请参阅
- [x:Type 标记扩展](x-type-markup-extension.md)
- [从 WPF 迁移到 System.Xaml 的类型](types-migrated-from-wpf-to-system-xaml.md)
