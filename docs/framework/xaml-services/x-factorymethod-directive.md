---
title: x:FactoryMethod 指令
ms.date: 03/30/2017
helpviewer_keywords:
- XAML. x:FactoryMethod directive [XAML Services]
- FactoryMethod directive in XAML [XAML Services]
- x:FactoryMethod directive [XAML Services]
ms.assetid: 829bcbdf-5318-4afb-9a03-c310e0d2f23d
ms.openlocfilehash: cb78514540f5f44b07b1fdd16283d26c647a3ac4
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58034540"
---
# <a name="xfactorymethod-directive"></a>x:FactoryMethod 指令
指定应使用 XAML 处理器正在解析其后备类型后初始化对象的构造函数以外的方法。  
  
## <a name="xaml-attribute-usage-no-xarguments"></a>XAML 特性用法，任何 x： 参数  
  
```  
<object x:FactoryMethod="methodname"...>  
  ...  
</object>  
```  
  
## <a name="xaml-attribute-usage-xarguments-as-elements"></a>XAML 特性用法，作为元素的 x： 参数  
  
```  
<object x:FactoryMethod="methodname"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`methodname`|XAML 处理器调用以初始化为指定的实例的方法的字符串方法名称`object`。 请参阅“备注”。|  
|`oneOrMoreObjectElements`|指定工厂方法参数的对象的一个或多个对象元素。 顺序很重要;它表示在其中应将参数传递给工厂方法的顺序。|  
  
## <a name="remarks"></a>备注  
 如果`methodname`是实例方法，不能限定。  
  
 支持为工厂方法的静态方法。 如果`methodname`是一种静态方法，`methodname`作为提供*typeName*。*methodName*组合，其中*typeName*命名定义的静态工厂方法的类。 *typeName*可以是如果引用类型中映射 xmlns 前缀限定。 *typeName*可以是与不同的类型`typeof(object)`。  
  
 工厂方法必须声明支持相关的对象元素的类型的公共方法。  
  
 工厂方法必须返回可分配给相关对象的实例。 工厂方法应永远不会返回 null。  
  
 `x:Arguments` 对与最匹配的工厂方法的签名的原则进行操作。 首先，匹配计算的参数计数。 如果没有参数计数为多个可能的匹配项，参数类型为检测计算和最佳匹配项。 如果仍二义性评估此阶段完成之后，XAML 处理器行为是未定义。  
  
 `x:FactoryMethod`元素用法不是属性元素用法在典型意义上，因为指令的标记不会引用包含对象元素的类型。 它预期该元素使用情况并不常见比属性用法。 `x:Arguments` （属性或元素用法） 可用于沿`x:FactoryMethod`元素使用情况，但这并没有专门显示使用情况部分中。  
  
 `x:FactoryMethod` 如某个元素必须位于任何其他属性元素之前，必须在任何之前`x:Arguments`还作为元素，提供，并且必须在之前的任何内容/内部文本/初始化文本。  
  
## <a name="see-also"></a>请参阅
- [x:Arguments 指令](x-arguments-directive.md)
