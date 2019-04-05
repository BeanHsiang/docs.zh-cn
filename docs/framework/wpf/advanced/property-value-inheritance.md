---
title: 属性值继承
ms.date: 03/30/2017
helpviewer_keywords:
- inheritance [WPF], property values
- value inheritance [WPF]
- properties [WPF], value inheritance
ms.assetid: d7c338f9-f2bf-48ed-832c-7be58ac390e4
ms.openlocfilehash: 64cafbe2f6044c83600ef227608dee24b29e3943
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57359870"
---
# <a name="property-value-inheritance"></a>属性值继承
属性值继承是 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 属性系统的一项功能。 属性值继承使元素树中的子元素可以从父元素获取特定属性的值，并继承该值，就如同它是在最近的父元素中任意位置设置的一样。 父元素可能也已通过属性值继承获得了其值，因此系统有可能一直递归到页面根。 属性值继承不是默认属性系统行为；属性必须用特定的元数据设置来建立，以便使该属性对子元素启动属性值继承。  
  

  
<a name="Property_Value_Inheritance_is_Containment_Inheritance"></a>   
## <a name="property-value-inheritance-is-containment-inheritance"></a>属性值继承是内含继承  
 此处作为术语的“继承”与类型和常规的面向对象的编程中提到的继承并非完全相同的概念，后者指派生类从其基类继承成员定义。 继承的这一含义在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中也适用：当在代码中用作元素且公开为成员时，各基类中定义的属性将公开为 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 派生类的特性。 属性值继承则是关于属性值如何基于元素树中的父子关系从一个元素继承到另一个元素。 如果在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记中定义应用程序时将元素嵌套在其他元素中，则该元素树在此种情况下最直接可见。 还可以通过向其他对象的指定集合中添加对象来以编程方式创建对象树，在运行时，属性值继承在完成树中以相同方式工作。  
  
<a name="Practical_Applications_of_Property_Value_Inheritance"></a>   
## <a name="practical-applications-of-property-value-inheritance"></a>属性值继承的实际应用  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA#tla_api#plural](../../../../includes/tlasharptla-apisharpplural-md.md)] 包括几个启用属性继承的属性。 通常，使用这些属性的情况是当涉及到一个属性，每页可以仅对该属性设置一次，但是该属性还是某个基元素类的成员，因此还存在于大多数子元素中。 例如，<xref:System.Windows.FrameworkElement.FlowDirection%2A>属性控制哪个方向流动内容应提供程序并在页面上的排列。 通常做法是在所有子元素中以一致的方式处理文本流概念。 如果用户或环境操作因某种原因在元素树的某一层重置了流方向，则流方向通常会在整个树中重置。 当<xref:System.Windows.FrameworkElement.FlowDirection%2A>属性进行继承，值仅需要设置或重置的每个页面在应用程序中需要演示的元素树中级别的一次。 即使是最初的默认值也将按照这种方式继承。 在需有意混用流方向的极罕见情况下，属性值继承模型也仍允许个别元素重置该值。  
  
<a name="Making_a_Custom_Property_Inheritable"></a>   
## <a name="making-a-custom-property-inheritable"></a>使自定义属性可继承  
 通过更改自定义属性的元数据，还可以使自己的自定义属性可继承。 但是，请注意，将属性指定为可继承需要考虑到性能问题。 如果该属性没有已建立的本地值或通过样式、模板或数据绑定获取的值，则可继承的属性会将赋予它的属性值提供给逻辑树中的所有子元素。  
  
 为了让属性参与值继承，请按照[注册附加属性](how-to-register-an-attached-property.md)中所述创建自定义附加属性。 注册元数据属性 (<xref:System.Windows.FrameworkPropertyMetadata>) 并在该元数据内的选项设置中指定"Inherits"选项。 同时确保该属性已建立了默认值，因为该值现将继承。 尽管已将该属性注册为附加属性，可能还需像对“非附加”依赖项属性一样，为所有者类型上的 get/set 访问创建属性“包装”。 这样做之后，可继承的属性可以设置所有者类型或派生的类型上使用直接属性包装或它可以在任何使用附加的属性语法设置<xref:System.Windows.DependencyObject>。  
  
 附加的属性是从概念上讲类似于全局属性;您可以检查任何值<xref:System.Windows.DependencyObject>并获取有效结果。 附加属性的典型方案是在子元素上设置属性值和该方案会更为有效，如果有问题的属性是将始终作为附加属性的每个元素隐式存在一个附加的属性 (<xref:System.Windows.DependencyObject>) 在树中。  
  
> [!NOTE]
>  尽管属性值继承看起来对非附加依赖项属性有效，但通过运行时树中特定元素边界的非附加属性的继承行为并未定义。 始终使用<xref:System.Windows.DependencyProperty.RegisterAttached%2A>来注册您在其中指定的属性<xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>元数据中。  
  
<a name="InheritanceContext"></a>   
## <a name="inheriting-property-values-across-tree-boundaries"></a>跨树边界继承属性值  
 属性继承通过遍历元素树来工作。 此树通常与逻辑树并行。 但是，每当您包括 WPF 核心级别对象中的标记，用于定义元素树，如<xref:System.Windows.Media.Brush>，已创建一个不连续的逻辑树。 真正的逻辑树不会从概念上讲扩展通过<xref:System.Windows.Media.Brush>，因为逻辑树是 WPF 框架级别概念。 您可以看到这反映在结果中使用的方法时<xref:System.Windows.LogicalTreeHelper>。 但是，属性值继承可填补此间隙逻辑树中的，并且只要可继承的属性注册为附加的属性，而且没有有意的继承阻止边界可以仍可通过继承的值，(例如<xref:System.Windows.Controls.Frame>) 遇到。  
  
## <a name="see-also"></a>请参阅
- [依赖属性元数据](dependency-property-metadata.md)
- [附加属性概述](attached-properties-overview.md)
- [依赖项属性值优先级](dependency-property-value-precedence.md)
