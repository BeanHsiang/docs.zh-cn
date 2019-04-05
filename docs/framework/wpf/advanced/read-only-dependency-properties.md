---
title: 只读依赖项属性
ms.date: 03/30/2017
helpviewer_keywords:
- dependency properties [WPF], read-only
- read-only dependency properties [WPF]
ms.assetid: f23d6ec9-3780-4c09-a2ff-b2f0a2deddf1
ms.openlocfilehash: 9aeeab95342bce94c53e89229003f55009118f96
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378998"
---
# <a name="read-only-dependency-properties"></a>只读依赖项属性
本主题介绍只读依赖属性，包括现有只读依赖属性、创建自定义只读依赖属性的方案和技术。  
  

  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>系统必备  
 本主题假定你了解实现依赖属性的基本方案，以及如何将元数据应用于自定义依赖属性。 有关上下文，请参阅[自定义依赖属性](custom-dependency-properties.md)和[依赖属性元数据](dependency-property-metadata.md)。  
  
<a name="existing"></a>   
## <a name="existing-read-only-dependency-properties"></a>现有只读依赖属性  
 在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 框架中定义的某些依赖属性是只读的。 指定只读依赖属性的一般原因如下：这些属性应该用于状态确定，但是有多种因素影响该状态，从用户界面设计的角度看，仅将属性设置为该状态并不能达到预期的效果。 例如，属性<xref:System.Windows.UIElement.IsMouseOver%2A>实际上只显示从鼠标输入确定的状态。 任何通过避开实际的鼠标输入以编程方式设置此值的尝试都是不可预期的，并将导致不一致。  
  
 由于其不可设置性，只读依赖属性不适用于依赖属性通常为其提供一个解决方案（即：数据绑定，直接样式化为某个值、验证、动画和继承）的多种方案。 尽管不可设置，但只读依赖属性仍具有一些由属性系统中的依赖属性支持的其他功能。 只读依赖属性仍可以用作样式中的属性触发器，这是其他功能中最重要的功能。 无法使用常规的 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性启用触发器；必须使用依赖属性才行。 前面提到<xref:System.Windows.UIElement.IsMouseOver%2A>属性是一个最好的例子，它可能是非常有用，可以定义一个控件的样式，其中，某些方案的背景、 前景或类似内复合元素的属性等的可见属性用户将鼠标悬停在控件的某些定义区域时，会更改控件。 只读依赖属性中的更改还可以由属性系统的固有失效进程检测并报告，这实际上是在内部支持属性触发器功能。  
  
<a name="new"></a>   
## <a name="creating-custom-read-only-dependency-properties"></a>创建自定义只读依赖属性  
 请务必阅读上一节中有关只读依赖属性为何不适用于许多典型依赖属性方案的内容。 但是如果有适当的方案，可能需要创建自己的只读依赖属性。  
  
 创建只读依赖属性的大多数过程与[自定义依赖属性](custom-dependency-properties.md)和[实现依赖属性](how-to-implement-a-dependency-property.md)主题中介绍的过程相同。 但有三个重要的差异：  
  
-   当注册属性，调用<xref:System.Windows.DependencyProperty.RegisterReadOnly%2A>方法而非普通<xref:System.Windows.DependencyProperty.Register%2A>属性注册的方法。  
  
-   实现 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]“包装器”属性时，请确保该包装器也没有设置的实现，以便在公开的公共包装器的只读状态中不存在不一致现象。  
  
-   由只读注册返回的对象是<xref:System.Windows.DependencyPropertyKey>而非<xref:System.Windows.DependencyProperty>。 仍应将该字段存储为成员，但通常不将其设置为类型的公共成员。  
  
 无论你具有什么专用字段或值，可使用你确定的任何逻辑来完全编写对只读依赖属性的支持。 但是，在最初或运行时逻辑过程中设置属性的最简单方法是使用属性系统的 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，而不是避开属性系统并直接设置专有支持字段。 具体而言，没有的签名<xref:System.Windows.DependencyObject.SetValue%2A>接受类型参数的<xref:System.Windows.DependencyPropertyKey>。 如何以及在何处设置此值以编程方式在应用程序逻辑中你如何可能想要设置的访问将影响<xref:System.Windows.DependencyPropertyKey>首次注册依赖属性时创建。 如果完全在专有类中处理此逻辑，或者如果要求从程序集的其他部分对其进行设置，可以在内部进行设置。 一种方法是调用<xref:System.Windows.DependencyObject.SetValue%2A>通知存储的属性值需要为其更改的类实例的相关事件的类事件处理程序中。 另一种方法是将绑定依赖关系属性在一起使用配对<xref:System.Windows.PropertyChangedCallback>和<xref:System.Windows.CoerceValueCallback>回调在注册过程中的这些属性的元数据的一部分。  
  
 因为<xref:System.Windows.DependencyPropertyKey>是专用容器，并不会传播由属性系统在代码之外，更好的安全设置比读写依赖属性具有只读依赖属性。 对于读写依赖属性，标识字段是显式或隐式公用的，因此该属性可广泛设置。 有关更多详细信息，请参阅[依赖属性的安全性](dependency-property-security.md)。  
  
## <a name="see-also"></a>请参阅
- [依赖项属性概述](dependency-properties-overview.md)
- [自定义依赖属性](custom-dependency-properties.md)
- [样式设置和模板化](../controls/styling-and-templating.md)
