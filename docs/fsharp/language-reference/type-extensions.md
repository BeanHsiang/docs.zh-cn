---
title: 类型扩展
description: 了解如何F#类型扩展允许将新成员添加到以前定义的对象类型。
ms.date: 02/08/2019
ms.openlocfilehash: 69fb3b771b5334c5771f2ac75341b38c1dad5b90
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56092470"
---
# <a name="type-extensions"></a>类型扩展

类型扩展 (也称为_扩大_) 是一系列功能，让你将新成员添加到以前定义的对象类型。 三个功能是：

* 内部类型扩展
* 可选类型扩展
* 扩展方法

每个可用于不同方案和不同的权衡。

## <a name="syntax"></a>语法

```fsharp
// Intrinsic and optional extensions
type typename with
    member self-identifier.member-name =
        body
    ...

// Extension methods
open System.Runtime.CompilerServices

[<Extension>]
type Extensions() =
    [static] member self-identifier.extension-name (ty: typename, [args]) =
        body
    ...
```

## <a name="intrinsic-type-extensions"></a>内部类型扩展

内部类型扩展是一个类型扩展，扩展的用户定义的类型。

内部类型扩展必须在同一文件中定义**和**中相同的命名空间或模块是作为正在扩展的类型。 任何其他定义将导致其正在[可选类型扩展](type-extensions.md#optional-type-extensions)。

内部类型扩展有时是更简洁的方式来区分类型声明功能。 下面的示例演示如何定义内部类型扩展：

```fsharp
namespace Example

type Variant =
    | Num of int
    | Str of string
  
module Variant =
    let print v =
        match v with
        | Num n -> printf "Num %d" n
        | Str s -> printf "Str %s" s

// Add a member to Variant as an extension
type Variant with
    member x.Print() = Variant.print x
```

使用类型扩展，可单独的以下各项：

* 声明`Variant`类型
* 若要打印的功能`Variant`类，具体取决于其"形状"
* 用于访问对象样式使用的打印功能的方法`.`-表示法

这是一种替代方法上定义为成员的所有内容`Variant`。 虽然它不是功能的本质上是功能的更好的方法，它可以是功能的在某些情况下的更简洁表示形式。

内部类型扩展编译为它们增加时，会显示在类型上反射检查类型的类型的成员。

## <a name="optional-type-extensions"></a>可选类型扩展

可选类型扩展是类型的显示原始模块、 命名空间或要扩展的程序集外部的扩展。

可选类型扩展可用于扩展具有未定义自己的类型。 例如：

```fsharp
module Extensions

open System.Collections.Generic

type IEnumerable<'T> with
    /// Repeat each element of the sequence n times
    member xs.RepeatElements(n: int) =
        seq {
            for x in xs do
                for i in 1 .. n do
                    yield x
        }
```

现在可以访问`RepeatElements`如同它是的成员<xref:System.Collections.Generic.IEnumerable%601>只要`Extensions`模块打开您正处于作用域中。

可选扩展不显示在当反射检查时，扩展的类型。 可选扩展必须在模块中，并且时，它们仅在作用域中包含扩展的模块是打开的或者在作用域中的其他方面。

可选扩展成员将会编译成静态成员，为其对象实例隐式传递的第一个参数。 但是，它们的作用像是实例成员或根据它们的声明的静态成员。

可选扩展成员也看不到C#或 VB 的使用者。 因此，可以仅使用其他F#代码。

## <a name="generic-limitation-of-intrinsic-and-optional-type-extensions"></a>泛型的内部函数和可选类型扩展限制

它是可以受限类型变量的泛型类型上声明的类型扩展。 要求是类型的扩展声明的约束与声明的约束相匹配。

但是，即使约束匹配的声明的类型和类型扩展之间，有可能有一定比声明的类型的类型参数的不同要求的扩展成员正文推断出来的约束。 例如：

```fsharp
open System.Collections.Generic

// NOT POSSIBLE AND FAILS TO COMPILE!
//
// The member 'Sum' has a different requirement on 'T than the type IEnumerable<'T>
type IEnumerable<'T> with
    member this.Sum() = Seq.sum this
```

没有方法来获取此代码以使用可选类型扩展：

* 原样`Sum`成员都有不同的约束`'T`(`static member get_Zero`和`static member (+)`) 比类型扩展的定义。
* 修改类型扩展具有同一约束作为`Sum`将不再匹配上定义的约束`IEnumerable<'T>`。
* 更改`member this.Sum`到`member inline this.Sum`将产生错误类型约束不匹配。

所需的内容是"空间中浮动"，可以提供好像它们扩展类型的静态方法。 这是其中的扩展方法变得非常必要。

## <a name="extension-methods"></a>扩展方法

最后，扩展方法 (有时称为"C#样式扩展成员") 可以声明中F#作为类的静态成员方法。

扩展方法可用于当你希望将约束类型变量的泛型类型上定义扩展。 例如：

```fsharp
namespace Extensions

open System.Runtime.CompilerServices

[<Extension>]
type IEnumerableExtensions() =
    [<Extension>]
    static member inline Sum(xs: IEnumerable<'T>) = Seq.sum xs
```

使用时，此代码将使其看起来像`Sum`上定义<xref:System.Collections.Generic.IEnumerable%601>，但前提是`Extensions`已打开或在范围内。

## <a name="other-remarks"></a>其他备注

类型扩展还具有以下属性：

* 可以扩展任何可访问的类型。
* 可以定义内部函数和可选类型扩展_任何_成员类型，而不仅仅是方法。 因此扩展属性也有可能，例如。
* `self-identifier`令牌[语法](type-extensions.md#syntax)表示调用，就像普通成员的类型的实例。
* 扩展的成员可以是静态或实例成员。
* 在类型扩展的类型变量必须与匹配的声明类型的约束。

类型扩展还存在以下限制：

* 类型扩展不支持虚拟或抽象方法。
* 类型扩展不支持扩大作为替代方法。
* 不支持类型扩展[静态解析的类型参数](generics/statically-resolved-type-parameters.md)。
* 可选类型扩展不支持扩大作为构造函数。
* 不能在定义类型扩展[类型缩写，用](type-abbreviations.md)。
* 类型扩展不是有效的`byref<'T>`（尽管它们可以声明）。
* 类型扩展不是有效的属性 （但它们可以声明）。
* 可以定义重载具有相同名称的其他方法的扩展，但F#编译器提供了首选项设置为非扩展方法，如果调用不明确。

最后，如果多个内部类型扩展存在一种类型，所有成员必须都是唯一的。 对于可选类型扩展为同一类型的不同类型扩展中的成员可以具有相同的名称。 仅当客户端代码打开两个不同的作用域定义相同成员名称，则会出现多义性错误。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [成员](members/index.md)
