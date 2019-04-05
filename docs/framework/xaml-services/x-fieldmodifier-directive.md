---
title: x:FieldModifier 指令
ms.date: 03/30/2017
helpviewer_keywords:
- FieldModifier attribute in XAML [XAML Services]
- x:FieldModifier attribute [XAML Services]
- XAML [XAML Services], x:FieldModifier attribute
ms.assetid: ed427cd4-2f35-4d24-bd2f-0fa7b71ec248
ms.openlocfilehash: 27ff9d027f5ff5155543097b7f0f0c2839387fe5
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58042449"
---
# <a name="xfieldmodifier-directive"></a>x:FieldModifier 指令
修改 XAML 编译行为，以便与定义的已命名的对象引用的字段<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>而不是访问<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>默认行为。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```xaml  
<object x:FieldModifier="Public".../>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|*Public*|传递以指定确切的字符串<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>与<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>各不相同，具体取决于使用的代码隐藏编程语言。 请参阅“备注”。|  
  
## <a name="dependencies"></a>依赖项  
 如果使用 XAML 生产`x:FieldModifier`任意位置，该 XAML 生产的根元素必须声明[X:class 指令](x-class-directive.md)。  
  
## <a name="remarks"></a>备注  
 `x:FieldModifier` 不相关的声明的类或其成员的常规访问级别。 如果是 XAML 生产的一部分的特定 XAML 对象处理时，并将成为应用程序的对象图中可以访问的对象，此选项仅适用于 XAML 处理行为。 默认情况下，此类对象的字段引用将保持私有，以防止控件使用者直接修改的对象图。 相反，控件使用者应使用标准模式的情况下启用的编程模型，如通过获取布局根、 子元素集合，专用的公共属性，修改对象图形等。  
  
 值为`x:FieldModifier`属性因编程语言，并在特定框架中它的用途而异。 要使用的字符串取决于如何实现每种语言及其<xref:System.CodeDom.Compiler.CodeDomProvider>和类型转换器，它将返回定义的含义<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>和<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>，以及该语言是否区分大小写。  
  
-   对于 C#，要传递的用于指定的字符串<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>是`public`。  
  
-   用于 Microsoft Visual Basic.NET，要传递的用于指定的字符串<xref:System.Reflection.TypeAttributes.Public?displayProperty=nameWithType>是`Public`。  
  
-   有关[!INCLUDE[TLA2#tla_cppcli](../../../includes/tla2sharptla-cppcli-md.md)]，XAML 没有目标当前存在; 因此，要传递的字符串是不确定。  
  
 此外可以指定<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>(`internal`中C#， `Friend` Visual Basic 中) 但指定<xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType>并不常见因为`NotPublic`因为该行为已是默认值。  
  
 <xref:System.Reflection.TypeAttributes.NotPublic?displayProperty=nameWithType> 是默认行为，因为它不是很频繁编译 XAML 的程序集之外的代码需要访问 XAML 创建的元素。 WPF 安全体系结构以及 XAML 编译行为将声明为公共，存储元素实例的字段，除非专门设置`x:FieldModifier`以允许公共访问。  
  
 `x:FieldModifier` 带有的元素才[X:name 指令](x-name-directive.md)因为该名称用于引用后它是公共字段。  
  
 默认情况下，根元素的分部类是公共的则但是，您可以通过使其非公共使用[X:classmodifier 指令](x-classmodifier-directive.md)。 [X:classmodifier 指令](x-classmodifier-directive.md)还会影响根元素类的实例的访问级别。 将两者放入`x:Name`并`x:FieldModifier`根元素，但这仅生成公共字段副本的根元素，具有真正的根元素类访问级别仍受[X:classmodifier 指令](x-classmodifier-directive.md)。  
  
## <a name="see-also"></a>请参阅
- [XAML 及 WPF 的自定义类](../wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [WPF 中的代码隐藏和 XAML](../wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [x:Name 指令](x-name-directive.md)
- [Building a WPF Application (WPF)](../wpf/app-development/building-a-wpf-application-wpf.md)（生成 WPF 应用程序 (WPF)）
- [x:ClassModifier 指令](x-classmodifier-directive.md)
