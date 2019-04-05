---
title: 约束
description: 了解如何F#应用于泛型类型参数，以在泛型类型或函数中指定的类型参数的要求的约束。
ms.date: 05/16/2016
ms.openlocfilehash: b253ce50707512a0d46c41bba2dde34adcc24d0e
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612226"
---
# <a name="constraints"></a>约束

本主题介绍可应用于泛型约束类型参数，以在泛型类型或函数中指定的类型参数的要求。

## <a name="syntax"></a>语法

```fsharp
type-parameter-list when constraint1 [ and constraint2]
```

## <a name="remarks"></a>备注

有几个不同的约束可用于限制可在泛型类型的类型。 下表列出并描述这些约束。

|约束|语法|描述|
|----------|------|-----------|
|类型约束|*类型参数*:&gt; *类型*|提供的类型必须等于或派生从指定的类型，或者，如果该类型是接口，提供的类型必须实现接口。|
|Null 约束|*类型参数*: null|提供的类型必须支持 null 字面值。 这包括所有的.NET 对象类型而非F#列表、 元组、 函数、 类、 记录或联合类型。|
|显式成员约束|[（]*类型参数*[or...或*类型参数*)]: (*成员签名*)|在至少其中一个提供的类型参数必须具有指定的签名; 的成员不适合公共使用。 成员必须要么显式定义为显式成员约束的有效目标类型或隐式类型扩展的一部分。|
|构造函数约束|*类型参数*: (新： 单元-&gt; )|提供的类型必须具有默认构造函数。|
|值类型约束|： 结构|提供的类型必须是一个.NET 值类型。|
|引用类型约束|： 不结构|提供的类型必须是.NET 引用类型。|
|枚举类型约束|： 枚举&lt;*基础类型*&gt;|提供的类型必须为枚举的类型具有指定的基础类型;不适合公共使用。|
|委托约束|： 委托&lt;*元组参数类型*，*返回类型*&gt;|提供的类型必须为委托类型具有指定的参数和返回值;不适合公共使用。|
|比较约束|： 比较|提供的类型必须支持比较。|
|相等约束|： 是否相等|提供的类型必须支持相等性。|
|非托管的约束|： 非托管|提供的类型必须是一个非托管的类型。 非托管的类型都是任一特定基元类型 (`sbyte`， `byte`， `char`， `nativeint`， `unativeint`， `float32`， `float`， `int16`， `uint16`， `int32`， `uint32`， `int64`， `uint64`，或`decimal`)，枚举类型`nativeptr<_>`，或其字段都为非托管的类型的非泛型结构。|

您必须添加约束，当你的代码必须使用一种功能，一般情况下是可在约束类型而不是在类型上时。 例如，如果你使用类型约束指定类类型，可以使用任何一种泛型函数或类型中的类的方法。

指定约束有时需要写入时，是类型参数显式，因为不受约束，编译器具有无法验证您使用的功能将可用于在运行时类型可能会提供任何类型参数。

在中使用的最常见约束F#代码是指定基类或接口的类型约束。 其他约束或者使用由F#库来实现某些功能，如显式成员约束，它用于实现的运算符重载算术运算符，由你或由主要是因为F#支持公共语言运行时支持的约束的完整集合。

在类型推理过程中，某些约束会自动由编译器推断。 例如，如果您使用`+`在函数中的运算符，编译器将推断变量类型的表达式中使用的显式成员约束。

以下代码演示了一些约束声明。

```fsharp
// Base Type Constraint
type Class1<'T when 'T :> System.Exception> =
class end

// Interface Type Constraint
type Class2<'T when 'T :> System.IComparable> = 
class end

// Null constraint
type Class3<'T when 'T : null> =
class end

// Member constraint with static member
type Class4<'T when 'T : (static member staticMethod1 : unit -> 'T) > =
class end

// Member constraint with instance member
type Class5<'T when 'T : (member Method1 : 'T -> int)> =
class end

// Member constraint with property
type Class6<'T when 'T : (member Property1 : int)> =
class end

// Constructor constraint
type Class7<'T when 'T : (new : unit -> 'T)>() =
member val Field = new 'T()

// Reference type constraint
type Class8<'T when 'T : not struct> =
class end

// Enumeration constraint with underlying value specified
type Class9<'T when 'T : enum<uint32>> =
class end

// 'T must implement IComparable, or be an array type with comparable
// elements, or be System.IntPtr or System.UIntPtr. Also, 'T must not have
// the NoComparison attribute.
type Class10<'T when 'T : comparison> =
class end

// 'T must support equality. This is true for any type that does not
// have the NoEquality attribute.
type Class11<'T when 'T : equality> =
class end

type Class12<'T when 'T : delegate<obj * System.EventArgs, unit>> =
class end

type Class13<'T when 'T : unmanaged> =
class end

// Member constraints with two type parameters
// Most often used with static type parameters in inline functions
let inline add(value1 : ^T when ^T : (static member (+) : ^T * ^T -> ^T), value2: ^T) =
value1 + value2

// ^T and ^U must support operator +
let inline heterogenousAdd(value1 : ^T when (^T or ^U) : (static member (+) : ^T * ^U -> ^T), value2 : ^U) =
value1 + value2

// If there are multiple constraints, use the and keyword to separate them.
type Class14<'T,'U when 'T : equality and 'U : equality> =
class end
```

## <a name="see-also"></a>请参阅

- [泛型](index.md)
- [约束](constraints.md)