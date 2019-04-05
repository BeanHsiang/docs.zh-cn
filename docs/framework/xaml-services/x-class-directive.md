---
title: x:Class 指令
ms.date: 03/30/2017
f1_keywords:
- x:Class
- xClass
- Class
helpviewer_keywords:
- Class attribute in XAML [XAML Services]
- XAML [XAML Services], x:Class attribute
- x:Class attribute [XAML Services]
ms.assetid: bc4a3d8e-76e2-423e-a5d1-159a023e82ec
ms.openlocfilehash: 8acc1ac099a71fbf624049b119ebe908f27cbb55
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58031232"
---
# <a name="xclass-directive"></a>x:Class 指令
配置 XAML 标记编译加入之间标记和代码隐藏的分部类。 代码的分部类定义在单独的代码文件中[!INCLUDE[TLA#tla_cls](../../../includes/tlasharptla-cls-md.md)]语言中，而在 XAML 编译的代码生成通常创建标记分部类。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```  
<object x:Class="namespace.classname"...>  
  ...  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`namespace`|可选。 指定[!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)]命名空间包含由标识的分部类`classname`。 如果`namespace`指定一个点 （.） 分隔`namespace`和`classname`。 请参阅“备注”。|  
|`classname`|必需。 指定[!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)]连接加载的 XAML 和代码隐藏中为该 XAML 的分部类的名称。|  
  
## <a name="dependencies"></a>依赖项  
 `x:Class` 只能指定 XAML 生产的根元素上。 `x:Class` 无效的任何对象，在 XAML 生产环境中具有一个父级。 有关详细信息，请参阅[ \[MS XAML\]部分 4.3.1.6](https://go.microsoft.com/fwlink/?LinkId=114525)。  
  
## <a name="remarks"></a>备注  
 `namespace`值可能包含相关命名空间组织到层次结构名称，这是一种常用技术在.NET Framework 编程中的其他点。 仅字符串中的最后一个句点`x:Class`值解释为隔开`namespace`和`classname.`用作类`x:Class`不能为嵌套的类。 不允许嵌套的类，因为确定的点的含义`x:Class`字符串是不明确，如果允许使用嵌套的类。  
  
 在现有编程模型，可使用`x:Class`，`x:Class`意义上说，它是完全有效，在 XAML 页面中都没有代码隐藏中是可选的。 但是，该功能与生成操作交互，如通过使用 XAML 的框架实现。 `x:Class` 角色的 XAML 指定的内容的各种类型的应用程序模型中以及在相应的生成操作也会影响功能。 如果你的 XAML 声明事件处理特性值，或者实例化自定义元素定义的类在代码隐藏类中的位置，则必须提供`x:Class`指令引用 (或[x： 子类](x-subclass-directive.md)) 到代码隐藏的合适的类。  
  
 值`x:Class`指令必须是一个字符串，指定完全限定的名称的类，但不包含任何程序集信息 (等效于<xref:System.Type.FullName%2A?displayProperty=nameWithType>)。 对于简单的应用程序，如果代码隐藏的构建这种方式 （在类级别的代码定义开始），可以忽略 CLR 命名空间信息。  
  
 页面或应用程序定义的代码隐藏文件必须包含的项目的生成已编译的应用程序，并涉及标记编译的代码文件中。 必须遵循 CLR 类的名称规则。 有关详细信息，请参阅[Framework 设计准则](../../standard/design-guidelines/index.md)。 默认情况下，代码隐藏类必须是`public`; 但是，可以通过使用而在不同的访问级别定义[X:classmodifier 指令](x-classmodifier-directive.md)。  
  
 此解释`x:Class`属性仅适用于基于 CLR 的 XAML 实现中，特别是到.NET Framework XAML 服务。 其他 XAML 实现的不基于 CLR 和未使用.NET Framework XAML 服务可能使用不同的分辨率公式用于连接 XAML 标记和备份运行时代码。 有关更多常规解释的详细信息`x:Class`，请参阅[ \[MS XAML\]](https://go.microsoft.com/fwlink/?LinkId=114525)。  
  
 在某个特定级别的体系结构的含义`x:Class`未在.NET Framework XAML 服务中。 这是因为.NET Framework XAML 服务未指定的 XAML 的标记和备份代码已连接的编程模型。 其他用法`x:Class`指令可能实现的特定框架所使用的编程模型或应用程序模型来定义如何连接 XAML 标记和基于 CLR 的代码隐藏。 每个框架都可以具有其自己实现某些行为或必须包含在生成环境中的特定组件的生成操作。 在框架中，生成操作还可随用于代码隐藏的特定 CLR 语言。  
  
## <a name="xclass-in-the-wpf-programming-model"></a>WPF 编程模型中的 x： 类  
 在 WPF 应用程序和 WPF 应用程序模型`x:Class`可以为任何 XAML 文件的根目录和正在编译的元素声明为属性 (其中 XAML 在 WPF 应用程序项目中使用包含`Page`生成操作)，或 <c4 1> <xref:System.Windows.Application> 编译的 WPF 应用程序的应用程序定义中的根。 声明`x:Class`页面根或应用程序根目录以外的元素上或在未编译的 WPF XAML 文件，会导致在编译时错误[!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)]和[!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)]WPF XAML 编译器。 有关的其他方面`x:Class`处理在 WPF 中，请参阅[的代码隐藏和 XAML 在 WPF 中的](../wpf/advanced/code-behind-and-xaml-in-wpf.md)。  
  
## <a name="xclass-for-windows-workflow-foundation"></a>x： 用于 Windows Workflow Foundation 类  
 对于 Windows Workflow Foundation，`x:Class`完全在 XAML，组成的自定义活动的类的名称或名称与代码隐藏的活动设计器的 XAML 页面分部类。  
  
## <a name="silverlight-usage-notes"></a>Silverlight Usage 备注。  
 `x:Class` 适用于 Silverlight 单独说明了。 有关详细信息，请参阅[XAML Namespace （x:）语言功能 (Silverlight)](https://go.microsoft.com/fwlink/?LinkId=199081)。  
  
## <a name="see-also"></a>请参阅
- [x:Subclass 指令](x-subclass-directive.md)
- [XAML 及 WPF 的自定义类](../wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [x:ClassModifier 指令](x-classmodifier-directive.md)
- [从 WPF 迁移到 System.Xaml 的类型](types-migrated-from-wpf-to-system-xaml.md)
