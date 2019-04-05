---
title: x:Arguments 指令
ms.date: 03/30/2017
helpviewer_keywords:
- x:Arguments directive [XAML Services]
- Arguments directive in XAML [XAML Services]
- XAML [XAML Services], x:Arguments directive
ms.assetid: 87cc10b0-b610-4025-b6b0-ab27ca27c92e
ms.openlocfilehash: 351974786b9f4748499279d29202e2051d9268fd
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58043337"
---
# <a name="xarguments-directive"></a>x:Arguments 指令
打包构造参数为 XAML 中的对象元素声明非默认构造函数或工厂方法对象声明。  
  
## <a name="xaml-element-usage-nondefault-constructor"></a>XAML 元素用法 （非默认构造函数）  
  
```  
<object ...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## <a name="xaml-element-usage-factory-method"></a>XAML 元素用法 （工厂方法）  
  
```  
<object x:FactoryMethod="methodName"...>  
  <x:Arguments>  
    oneOrMoreObjectElements  
  </x:Arguments>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`oneOrMoreObjectElements`|指定要传递到支持非默认构造函数或工厂方法参数的一个或多个对象元素。<br /><br /> 典型用法是使用对象元素内的初始化文本指定的实际自变量值。 请参阅示例部分。<br /><br /> 元素的顺序很重要。 在顺序中的 XAML 类型必须与类型匹配，并键入后备构造函数或工厂方法重载的顺序。|  
|`methodName`|应能处理任何工厂方法的名称`x:Arguments`参数。|  
  
## <a name="dependencies"></a>依赖项  
 `x:FactoryMethod` 作用域和行为可以修改其中`x:Arguments`适用。  
  
 如果没有`x:FactoryMethod`指定，则`x:Arguments`适用于后备构造函数的备用 （非默认值） 签名。  
  
 如果`x:FactoryMethod`指定，则`x:Arguments`适用于命名方法的重载。  
  
## <a name="remarks"></a>备注  
 XAML 2006 可支持通过初始化文本的非默认初始化。 但是，初始化文本构造方法的实际应用受到限制。 初始化文本视为单个文本字符串;因此，除非可以分析自定义信息项和自定义分隔符的字符串的构造行为定义的类型转换器，否则它只添加单个参数初始化的功能。 此外，对象逻辑的文本字符串可能是给定的 XAML 分析器的本机默认类型转换器处理，则返回 true 字符串以外的其他基元。  
  
 `x:Arguments` XAML 使用情况不是属性元素用法在典型意义上，因为指令的标记不会引用包含对象元素的类型。 它更像是其他指令如`x:Code`其中元素 demarks 标记应解释为子内容的默认值以外的范围。 在这种情况下，每个对象元素的 XAML 类型进行通信，XAML 分析器用于确定哪些特定构造函数工厂方法签名参数类型中，信息`x:Arguments`正尝试使用情况进行引用。  
  
 `x:Arguments` 为对象元素正在构造必须位于任何其他属性元素、 内容、 内部文本或对象元素的初始化字符串。 中的对象元素`x:Arguments`可以包括属性和初始化字符串，允许通过该 XAML 类型和其后备构造函数或工厂方法的方式。 对于对象或参数，可以指定自定义 XAML 类型或通过引用建立的前缀映射为默认 XAML 命名空间之外的 XAML 类型。  
  
 XAML 处理器使用以下准则来确定自变量中的指定`x:Arguments`应该用于构造对象。 如果`x:FactoryMethod`信息进行比较的指定与指定`x:FactoryMethod`(请注意，值`x:FactoryMethod`是方法名称和命名的方法可以具有重载。 如果`x:FactoryMethod`未指定，则信息进行比较的对象的所有公共构造函数重载组。 XAML 处理逻辑然后进行比较的参数数目，并选择匹配的参数数量的重载。 如果多个匹配项，XAML 处理器应比较基于提供的对象元素的 XAML 类型的参数的类型。 如果仍多个匹配项，XAML 处理器行为未定义。 如果`x:FactoryMethod`指定，但该方法无法解析，XAML 处理器应引发异常。  
  
 XAML 特性用法`<x:Arguments>string</x:Arguments>`技术上是可行。 但是，这提供无法通过初始化文本和类型转换器，否则完成什么以外的任何功能，并使用此语法不是 XAML 2009 工厂方法功能的设计意图。  
  
## <a name="examples"></a>示例  
 下面的示例演示非默认构造函数签名，然后的 XAML 用法`x:Arguments`访问该签名。  
  
```csharp  
public class Food {  
    private string _name;  
    private Int32 _calories;  
    public Food(string name, Int32 calories) {  
        _name=name;  
        _calories=calories;  
    }  
}  
```  
  
```xaml  
<my:Food>  
    <x:Arguments>  
        <x:String>Apple</x:String>  
        <x:Int32>150</x:Int32>  
    </x:Arguments>  
</my:Food>  
```  
  
 下面的示例演示一个目标工厂方法签名，然后的 XAML 用法`x:Arguments`访问该签名。  
  
```csharp  
public Food TryLookupFood(string name)  
{  
  switch (name) {  
    case "Apple": return new Food("Apple",150);  
    case "Chocolate": return new Food("Chocolate",200);  
    case "Cheese": return new Food("Cheese", 450);  
    default: {return new Food(name,0);  
  }  
}  
```  
  
```xaml  
<my:Food x:FactoryMethod="TryLookupFood">  
    <x:Arguments>  
        <x:String>Apple</x:String>  
    </x:Arguments>  
</my:Food>  
```  
  
## <a name="see-also"></a>请参阅
- [定义与 .NET Framework XAML 服务一起使用的自定义类型](defining-custom-types-for-use-with-net-framework-xaml-services.md)
- [XAML 概述 (WPF)](../wpf/advanced/xaml-overview-wpf.md)
