---
title: XAML 2009 语言功能
ms.date: 03/30/2017
helpviewer_keywords:
- XAML 2009 [XAML Services]
- XAML [XAML Services], XAML 2009
ms.assetid: f6bb18d8-c86a-4549-8862-323e6b32a8dd
ms.openlocfilehash: 6de103d9b5b59ec1a47098e44e07ee95a3db166e
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58039567"
---
# <a name="xaml-2009-language-features"></a>XAML 2009 语言功能
XAML 2009 是新 XAML 语言功能的简写术语，其扩展现有的 XAML 语言规范。 XAML 2009 引入了几个新指令和结构。 其中包括[X:arguments 指令](x-arguments-directive.md); [X:factorymethod 指令](x-factorymethod-directive.md); [X:reference 标记扩展](x-reference-markup-extension.md); [X:typearguments 指令](x-typearguments-directive.md); 以及常见语言基元的内置类型 (例如`x:Char`)。  
  
<a name="xaml_2009_support_in_wpf_and_visual_studio"></a>   
## <a name="xaml-2009-support-in-wpf-and-visual-studio"></a>在 WPF 和 Visual Studio 中支持 XAML 2009  
 在 WPF 中，可以使用 XAML 2009 功能，但仅针对未进行 WPF 标记编译的 XAML。 标记编译的 XAML 以及 BAML 形式的 XAML 当前不支持 XAML 2009 语言关键字和功能。  
  
 请注意，在 WPF 中加载松散的 XAML 的现有技术也有可能受到 CLR 类型的安全和访问限制，该类型系统比标记编译的 XAML 更加严格。 有关更多信息，请参见 [安全性 (WPF)](../wpf/security-wpf.md) 或 [WPF 安全策略 — 平台安全性](../wpf/wpf-security-strategy-platform-security.md)。  
  
 XAML 2009 还引入了一些附加功能，可修改曾经的 XAML 2006 构造或修改基本标记窗体。  
  
### <a name="xkey-as-an-object-element"></a>X:key 作为对象元素  
 XAML 2009 可支持 `x:Key` 作为对象（具有对象元素值的属性元素）；但是 XAML 2006 仅支持 `x:Key` 作为属性。 请参阅 [x:Key Directive](x-key-directive.md)的“XAML 2009”一节。  
  
### <a name="xmlns-on-property-elements"></a>属性元素上的 xmlns  
 XAML 2009 可以支持属性元素上的 XAML 命名空间 (xmlns) 定义，而 XAML 2006 只支持对象元素上的 xmlns 定义。  
  
### <a name="event-attributes"></a>事件特性  
 对于由事件支持的特性，XAML 2006 会假定涉及到了标记编译并将事件提交给标记编译。 XAML 2009 支持类似标记扩展的标记窗体，其不同于事件布线，直至运行时解析/加载 XAML。 但是，WPF 应用程序和 WPF UI 的 XAML 方案通常不使用此功能。 WPF 和其 XAML 2006 实现使用在 <xref:System.Windows.UIElement> 级别定义的路由事件的事件处理程序布线组合及其标记编译器步骤，用于其众多事件特性处理。 标记编译器还预处理生成操作声明用于标记编译器的 XAML 中找到任何事件属性。  
  
## <a name="see-also"></a>请参阅
- [XAML 概述 (WPF)](../wpf/advanced/xaml-overview-wpf.md)
