---
title: 类、结构和接口的名称
ms.date: 10/22/2008
helpviewer_keywords:
- type names, guidelines
- classes [.NET Framework], names
- enumerations [.NET Framework], names
- names [.NET Framework], interfaces
- common type names
- names [.NET Framework], type names
- names [.NET Framework], classes
- interfaces [.NET Framework], names
- generic type parameters
ms.assetid: 87a4b0da-ed64-43b1-ac43-968576c444ce
author: KrzysztofCwalina
ms.openlocfilehash: c0790cd20daf859ec81e2252dc9bce46673daf90
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54621820"
---
# <a name="names-of-classes-structs-and-interfaces"></a>类、结构和接口的名称
以下命名准则适用于常规类型命名。  
  
 **✓ 务必**通过使用 PascalCasing，用名词或名词短语命名类和结构。  
  
 这将类型名称与使用谓词短语命名的方法区分开来。  
  
 **✓ 务必**使用形容词短语命名接口，或偶尔用名词或名词短语命名接口。  
  
 应少使用名词和名词短语，它们可能会指示类型为抽象类而非接口。  
  
 **X 不要**给类名加前缀（例如，"C"）。  
  
 **✓ 考虑**使用基类的名称作为派生类名称的结尾部分。  
  
 这样可让名称非常易读，并清楚体现了关系。 代码中的相关例子有：`ArgumentOutOfRangeException`，这是一种 `Exception`，还有 `SerializableAttribute`，这是一种 `Attribute`。 但是，在应用此准则时，务必应进行合理判断；例如，`Button` 类是一种 `Control` 事件，尽管其名称中并未出现 `Control`。  
  
 **✓ 务必**在接口名称前加上字母 I 作为前缀，以指示该类型是接口。  
  
 例如，`IComponent`（描述性名词），`ICustomAttributeProvider`（名词短语）和 `IPersistable`（形容词）是合适的接口名称。与其他类型名称一样，应避免使用缩略形式。 与其他类型名称，避免缩写。  
  
 **✓ 务必**确保在定义类和接口对时，类名称和接口名称的区别仅在于 "I" 前缀，其中类是接口的标准实现。  
  
## <a name="names-of-generic-type-parameters"></a>泛型类型参数的名称  
 .NET Framework 2.0 中增添了泛型。 此功能引入了一种新的标识符称为*类型参数*。  
  
 **✓ 务必**使用描述性名称命名泛型参数，除非单字母名称可完整体现要传达的含义且描述性名称意义不大。  
  
 **✓ 考虑**使用 `T` 作为具有一个单字母类型参数的类型的类型参数名称。  
  
```  
public int IComparer<T> { ... }  
public delegate bool Predicate<T>(T item);  
public struct Nullable<T> where T:struct { ... }  
```  
  
 **✓ 务必**使用 `T` 作为描述性类型参数名称的前缀。  
  
```  
public interface ISessionChannel<TSession> where TSession : ISession {  
    TSession Session { get; }  
}  
```  
  
 **✓ 考虑**在参数名称中体现出对该类型参数设置的约束。  
  
 例如，被限制为 `ISession` 的参数可能名为 `TSession`。  
  
## <a name="names-of-common-types"></a>常见类型的名称  
 **✓ 务必**在命名从某些 .NET Framework 类型派生的类型或在实现某些 .NET Framework 类型时，遵循下表所述准则。  
  
|基类型|派生的实现类型准则|  
|---------------|------------------------------------------|  
|`System.Attribute`|**✓ 务必**为自定义属性类的名称添加后缀 "Attribute"。|  
|`System.Delegate`|**✓ 务必**向事件中所用委托的名称中添加后缀 "EventHandler"。<br /><br /> **✓ 务必**在用作事件处理程序的委托以外的委托名称中添加后缀 "Callback"。<br /><br /> **X 不要**将后缀 "Delegate" 添加到委托。|  
|`System.EventArgs`|**✓ 务必**添加后缀 "EventArgs"。|  
|`System.Enum`|**X 不要**从此类派生；而是使用所用语言支持的关键字；例如，在 C# 中，使用关键字 `enum`。<br /><br /> **X 不要**添加后缀 "Enum" 或 "Flag"。|  
|`System.Exception`|**✓ 务必**添加后缀 "Exception"。|  
|`IDictionary` <br /> `IDictionary<TKey,TValue>`|**✓ 务必**添加后缀 "Dictionary"。 请注意，`IDictionary` 是一种特定类型的集合，但此准则优先于后面更宽泛的集合准则。|  
|`IEnumerable` <br /> `ICollection` <br /> `IList` <br /> `IEnumerable<T>` <br /> `ICollection<T>` <br /> `IList<T>`|**✓ 务必**添加后缀 "Collection"。|  
|`System.IO.Stream`|**✓ 务必**添加后缀 "Stream"。|  
|`CodeAccessPermission IPermission`|**✓ 务必**添加后缀 "Permission"。|  
  
## <a name="naming-enumerations"></a>命名枚举  
 一般情况下，枚举类型（也称为枚举）的名称应遵循标准的类型命名规则（PascalCasing 等）。 但还有专用于枚举的其他准则。  
  
 **✓ 务必**为枚举使用单数形式的类型名称，除非枚举值是位域。  
  
 **✓ 务必**为值为位域的枚举使用复数形式的类型名称，这类枚举也称为标志枚举。  
  
 **X 不要**在枚举类型名称中使用 "Enum" 作为后缀。  
  
 **X 不要**在枚举类型名称中使用 "Flag" 或 "Flags" 作为后缀。  
  
 **X 不要**在枚举值名称中使用前缀（例如，对 ADO 枚举使用 "ad”，对富文本枚举使用 "rtf" 等）。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [命名规则](../../../docs/standard/design-guidelines/naming-guidelines.md)
