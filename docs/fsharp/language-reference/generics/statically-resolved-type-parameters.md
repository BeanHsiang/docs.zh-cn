---
title: 静态解析的类型参数
description: 了解如何使用F#静态解析的类型参数，它将被替换为实际类型在编译时而不是在运行时。
ms.date: 05/16/2016
ms.openlocfilehash: 9ad23a881e644dfe2bccd56fa04d3c219b51cf7d
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614085"
---
# <a name="statically-resolved-type-parameters"></a>静态解析的类型参数

一个*静态解析的类型参数*是在编译时而不是在运行时替换为实际类型的类型参数。 它们的前面有一个插入符号 (^) 符号。

## <a name="syntax"></a>语法

```
ˆtype-parameter
```

## <a name="remarks"></a>备注

在F#语言中，有两种不同的类型参数。 第一个类型为标准的泛型类型参数。 这些类型由撇号 （'），作为 in 参数指示`'T`和`'U`。 它们等效于其他.NET Framework 语言中的泛型类型参数。 另外一种类型是静态解析并由一个插入符号，如`^T`和`^U`。

静态解析的类型参数是主要适用于与约束，可用于指定类型参数必须为可具有的特定成员的成员约束一起使用。 没有办法使用常规的泛型类型参数创建这种类型的约束。

下表总结了两种类型的类型参数之间的异同。

|功能|泛型|静态解析的|
|-------|-------|-------------------|
|语法|`'T`， `'U`|`^T`， `^U`|
|解决时间|运行时|编译时间|
|成员约束|不能与成员约束一起使用。|可以与成员约束一起使用。|
|代码生成|使用标准的泛型类型参数的类型 （或方法） 会导致单个泛型类型或方法的生成。|生成多个实例化的类型和方法，每个类型的需要。|
|与类型一起使用|可以在类型上使用。|不能在类型上使用。|
|使用内联函数|不是。 内联函数不能使用标准的泛型类型参数进行参数化。|可以。 静态解析的类型参数不能用于函数或不是内联的方法。|

许多F#核心库功能，尤其是运算符，具有静态解析的类型参数。 这些函数和运算符将以内联方式，并导致数值计算的高效的代码生成。

内联方法和函数，使用运算符，或使用其他具有静态解析的类型参数的函数还可以使用静态解析的类型参数本身。 通常情况下，类型推理来推断这类内联函数具有静态解析的类型参数。 下面的示例演示为具有静态解析的类型参数推断出的运算符定义。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-3/snippet401.fs)]

解析的类型的`(+@)`的同时使用基于`(+)`和`(*)`，这两个的这会导致类型推理来推断成员的静态解析的类型参数的约束。 解析的类型，如中所示F#解释器，如下所示。

```fsharp
^a -> ^c -> ^d
when (^a or ^b) : (static member ( + ) : ^a * ^b -> ^d) and
(^a or ^c) : (static member ( * ) : ^a * ^c -> ^b)
```

输出如下所示。

```
2
1.500000
```

从F#4.1，您还可以静态解析的类型的参数签名中指定具体的类型名称。  在以前版本的语言，类型名称实际上无法由编译器推断出，但无法实际指定的签名中。  在F#4.1，您还可以在静态解析的类型的参数签名中指定具体的类型名称。 以下是一个示例：

```fsharp
let inline konst x _ = x

type CFunctor() = 
    static member inline fmap (f: ^a -> ^b, a: ^a list) = List.map f a
    static member inline fmap (f: ^a -> ^b, a: ^a option) =
        match a with
        | None -> None
        | Some x -> Some (f x)

    // default implementation of replace
    static member inline replace< ^a, ^b, ^c, ^d, ^e when ^a :> CFunctor and (^a or ^d): (static member fmap: (^b -> ^c) * ^d -> ^e) > (a, f) =
        ((^a or ^d) : (static member fmap : (^b -> ^c) * ^d -> ^e) (konst a, f))

    // call overridden replace if present
    static member inline replace< ^a, ^b, ^c when ^b: (static member replace: ^a * ^b -> ^c)>(a: ^a, f: ^b) =
        (^b : (static member replace: ^a * ^b -> ^c) (a, f))

let inline replace_instance< ^a, ^b, ^c, ^d when (^a or ^c): (static member replace: ^b * ^c -> ^d)> (a: ^b, f: ^c) =
        ((^a or ^c): (static member replace: ^b * ^c -> ^d) (a, f))

// Note the concrete type 'CFunctor' specified in the signature
let inline replace (a: ^a) (f: ^b): ^a0 when (CFunctor or  ^b): (static member replace: ^a *  ^b ->  ^a0) =
    replace_instance<CFunctor, _, _, _> (a, f)
```

## <a name="see-also"></a>请参阅

- [泛型](index.md)
- [类型推断](../type-inference.md)
- [自动泛化](automatic-generalization.md)
- [约束](constraints.md)
- [内联函数](../functions/inline-functions.md)