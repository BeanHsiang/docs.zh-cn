---
title: F# 类型
description: 了解有关在中使用的类型F#以及F#类型命名和描述。
ms.date: 05/16/2016
ms.openlocfilehash: bdbb89dc751970ac31fe102df009f0bff6388e52
ms.sourcegitcommit: db8b83057d052c1f9f249d128b08d4423af0f7c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2018
ms.locfileid: "33565575"
---
# <a name="f-types"></a>F# 类型

本主题介绍中使用的类型F#以及F#类型命名和描述。


## <a name="summary-of-f-types"></a>摘要的F#类型
某些类型被视为*基元类型*，如布尔类型`bool`和各种大小，其中包括的字节数和字符类型的整型和浮点类型。 中介绍了这些类型[基元类型](primitive-types.md)。

其他内置于语言的类型包括元组、 列表、 数组、 序列、 记录和可区分联合。 如果您具有与其他.NET 语言的体验，并且学习F#，您应阅读的主题的每个类型。 有关这些类型的详细信息的链接中包含[相关主题](https://msdn.microsoft.com/library/#rel)本主题的部分。 这些F#的特定类型都支持通用函数编程语言的编程样式。 许多这些类型具有关联中的模块F#支持对这些类型的常见操作的库。

函数类型包含有关参数类型和返回类型。

.NET Framework 是对象类型、 接口类型、 委托类型和其他人的源。 就像任何其他.NET 语言一样，可以定义自己的对象类型。

此外，F#代码可以定义别名，分别名为*类型缩写*，是可选的类型名称。 类型可能会在将来更改，并且想要避免更改取决于类型的代码时，可能会使用类型缩写。 或者，可以使用类型缩写作为一种类型，可以使代码更易于阅读和理解的友好名称。

F#提供记住函数式编程设计的有用的集合类型。 使用这些集合类型，可帮助您编写更功能在样式中的代码。 有关详细信息，请参阅[F#集合类型](fsharp-collection-types.md)。


## <a name="syntax-for-types"></a>类型的语法
在F#代码中，您通常必须编写出的类型的名称。 每个类型都有一个语法形式，并使用这些语法形式中的类型注释、 抽象方法声明、 委托声明、 签名和其他构造。 每当您声明中解释器的新程序构造，解释器将打印其类型的构造和语法的名称。 此语法可能只是用户定义类型的标识符或内置标识符等的`int`或`string`，但对于更复杂类型，语法更复杂。

下表显示了有关类型语法的各个方面F#类型。



|类型|类型语法|示例|
|----|-----------|--------|
|基元类型|*type-name*|`int`<br /><br />`float`<br /><br />`string`|
|聚合类型 （类、 结构、 联合、 记录、 枚举和等等）|*type-name*|`System.DateTime`<br /><br />`Color`|
|类型缩写|*类型缩写名称*|`bigint`|
|完全限定的类型|*namespaces.type 名称*<br /><br />或<br /><br />*modules.type 名称*<br /><br />或<br /><br />*namespaces.modules.type 名称*|`System.IO.StreamWriter`|
|array|*类型名称*[] 或<br /><br />*类型名称*数组|`int[]`<br /><br />`array<int>`<br /><br />`int array`|
|二维数组|*类型名称*[、]|`int[,]`<br /><br />`float[,]`|
|三维数组|*类型名称*[、]|`float[,,]`|
|tuple|*类型 name1* &#42; *类型 name2* ...|例如，`(1,'b',3)`具有类型 `int * char * int`|
|Generic Type — 泛型类型|*类型参数* *泛型类型名称*<br /><br />或<br /><br />*泛型类型名称*&lt;*类型参数列表*&gt;|`'a list`<br /><br />`list<'a>`<br /><br />`Dictionary<'key, 'value>`|
|构造类型 （具有提供的特定类型实参的泛型类型）|*类型实参* *泛型类型名称*<br /><br />或<br /><br />*泛型类型名称*&lt;*类型实参列表*&gt;|`int option`<br /><br />`string list`<br /><br />`int ref`<br /><br />`option<int>`<br /><br />`list<string>`<br /><br />`ref<int>`<br /><br />`Dictionary<int, string>`|
|只有一个参数的函数类型|*参数 type1*  - &gt; *返回类型*|该函数采用`int`，并返回`string`具有类型 `int -> string`|
|具有多个参数的函数类型|*参数 type1*  - &gt; *参数 type2*  - &gt; ...-&gt; *返回类型*|该函数采用`int`和一个`float`，并返回`string`具有类型 `int -> float -> string`|
|高阶函数作为参数|(*函数类型*)|`List.map` 具有类型 `('a -> 'b) -> 'a list -> 'b list`|
|委托|委托的*函数类型*|`delegate of unit -> int`|
|可变类型|#*类型名称*|`#System.Windows.Forms.Control`<br /><br />`#seq<int>`|

## <a name="related-topics"></a>相关主题


|主题|描述|
|-----|-----------|
|[基元类型](primitive-types.md)|介绍内置简单类型，例如整型、 布尔值类型和字符类型。|
|[Unit 类型](unit-type.md)|介绍`unit`类型中，键入，以包含一个值，将由 （）; 等效于`void`中C#并`Nothing`Visual Basic 中。|
|[元组](tuples.md)|介绍了元组类型、 包含分组中对、 三元组、 四重等任何类型的关联值的类型。|
|[选项](options.md)|介绍选项类型，该类型可能具有的值或为空。|
|[列表](lists.md)|介绍列表，它是元素的有序的、 不可变系列所有相同的类型。|
|[数组](arrays.md)|介绍数组，它有序集的相同类型的可变元素占用的内存的连续块并具有固定大小。|
|[序列](sequences.md)|说明序列类型，表示逻辑的一系列值;仅在必要时计算单个值。|
|[记录](records.md)|介绍了记录类型、 一个小型的已命名的值聚合。|
|[可区分联合](discriminated-unions.md)|介绍可区分联合类型的值可以是可能的类型的一组的任何一个的类型。|
|[函数](functions/index.md)|说明函数的值。|
|[类](classes.md)|介绍了类类型、 为.NET 引用类型对应的对象类型。 类类型才能包含成员、 属性、 实现的接口和基类型。|
|[结构](structures.md)|介绍`struct`类型、 对应于一个.NET 值类型的对象类型。 `struct`类型通常表示一个小型数据的聚合。|
|[接口](interfaces.md)|介绍接口类型，它们是表示一组的成员提供某种功能，但不包含数据的类型。 必须由要非常有用的对象类型实现接口类型。|
|[委托](delegates.md)|描述表示一个函数作为对象的委托类型。|
|[枚举](enumerations.md)|介绍枚举类型，其值属于一组命名的值。|
|[特性](attributes.md)|描述了属性，用来指定另一种类型的元数据。|
|[异常类型](exception-handling/exception-types.md)|介绍了异常，指定错误的信息。|
