---
title: ComponentResourceKey 标记扩展
ms.date: 03/30/2017
f1_keywords:
- ComponentResourceKey
- ComponentResourceKeyExtension
helpviewer_keywords:
- ComponentResourceKey markup extension [WPF]
- XAML [WPF], ComponentResourceKey markup extension
ms.assetid: d6bcdbe6-61b3-40a7-b381-4e02185b5a85
ms.openlocfilehash: 89459223108c0190a485b25193e44d379a1e1c19
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379024"
---
# <a name="componentresourcekey-markup-extension"></a>ComponentResourceKey 标记扩展
定义和引用从外部程序集加载的资源键。 这样一种资源查找程序集，而不是显式的资源字典在程序集或对类中指定目标类型。  
  
## <a name="xaml-attribute-usage-setting-key-compact"></a>XAML 特性用法 （设置键，compact）  
  
```xml  
<object x:Key="{ComponentResourceKey {x:Type targetTypeName}, targetID}" .../>  
```  
  
## <a name="xaml-attribute-usage-setting-key-verbose"></a>XAML 特性用法 （设置键、 verbose）  
  
```xml  
<object x:Key="{ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}" .../>  
```  
  
## <a name="xaml-attribute-usage-requesting-resource-compact"></a>XAML 特性用法 （请求资源，compact）  
  
```xml  
<object property="{DynamicResource {ComponentResourceKey {x:Type targetTypeName}, targetID}}" .../>  
```  
  
## <a name="xaml-attribute-usage-requesting-resource-verbose"></a>XAML 特性用法 （请求资源，详细）  
  
```xml  
<object property="{DynamicResource {ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}}" .../>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`targetTypeName`|公共名称[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]资源程序集中定义的类型。|  
|`targetID`|资源键。 当资源查找`targetID`将类似于[X:key 指令](../../xaml-services/x-key-directive.md)的资源。|  
  
## <a name="remarks"></a>备注  
 如上面的用法中所示 {`ComponentResourceKey`} 标记扩展用法在两个位置找到：  
  
-   内的主题资源字典，由控件作者提供的键的定义。  
  
-   从程序集访问主题资源，当你重新模板化控件但想要使用来自控件的主题提供资源的属性值。  
  
 用于引用来自主题的组件资源，通常建议您使用`{DynamicResource}`而非`{StaticResource}`。 这是与用法中所示。 `{DynamicResource}` 建议，因为用户可以更改主题本身。 如果你想与支持该主题的控件作者的意图最匹配的组件资源，应启用组件资源参考，用于也是动态的。  
  
 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A>标识存在于实际定义资源所在的目标集中的类型。 一个`ComponentResourceKey`可以定义和使用独立于完全了解其中<xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A>已定义，但最终必须解决通过引用的程序集的类型。  
  
 常见用法<xref:System.Windows.ComponentResourceKey>是定义键，然后公开为类的成员。 对于此用法中，你使用<xref:System.Windows.ComponentResourceKey>类构造函数，不是标记扩展。 有关详细信息，请参阅<xref:System.Windows.ComponentResourceKey>，或主题的"定义和引用主题资源的键"部分[控件创作概述](../controls/control-authoring-overview.md)。  
  
 有关建立键和引用键控资源，特性语法通常用于`ComponentResourceKey`标记扩展。  
  
 依赖于简洁的语法所示<xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=nameWithType>构造函数签名和标记扩展的位置参数用法。 依据的顺序`targetTypeName`和`targetID`提供非常重要。 详细语法依赖<xref:System.Windows.ComponentResourceKey.%23ctor%2A?displayProperty=nameWithType>默认构造函数，然后设置<xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A>和<xref:System.Windows.ComponentResourceKey.ResourceId%2A>类似于在对象元素上的实际特性语法的方式。 在详细的语法中，将设置属性的顺序并不重要。 主题中的更多详细信息中所述的以下两个替代方法 （compact 和 verbose） 机制以及关系[标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)。  
  
 从技术上讲，值`targetID`可以是任何对象，它不需要为的字符串。 但是，在 WPF 中最常见的用法是对齐`targetID`值，该值具有窗体的字符串，并且其中此类字符串中可[XamlName 语法](../../xaml-services/xamlname-grammar.md)。  
  
 `ComponentResourceKey` 可以在对象元素语法中使用。 在这种情况下，指定的值都<xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A>和<xref:System.Windows.ComponentResourceKey.ResourceId%2A>正确初始化该扩展所需的属性。  
  
 在中[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)][!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]读取器实现，对此标记扩展的处理由定义<xref:System.Windows.ComponentResourceKey>类。  
  
 `ComponentResourceKey` 是标记扩展。 当要求转义特性值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性上放置类型转换器而言，此需求更具有全局性。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的所有标记扩展在其特性语法中都使用 { 和 } 字符，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器通过这一约定确认标记扩展必须处理该特性。 有关详细信息，请参阅[标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.ComponentResourceKey>
- <xref:System.Windows.Controls.ControlTemplate>
- [控件创作概述](../controls/control-authoring-overview.md)
- [XAML 概述 (WPF)](xaml-overview-wpf.md)
- [标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)
