---
title: 结构
description: 了解如何F#结构，紧凑对象类型通常比用于具有少量数据且行为简单类型的类更有效。
ms.date: 05/16/2016
ms.openlocfilehash: c091dc91765d6e828426de21e9bc5f79bfdebc6c
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612148"
---
# <a name="structures"></a>结构

一个*结构*是一种紧凑对象类型，可以是比具有少量的数据且行为简单的类型的类更有效。

## <a name="syntax"></a>语法

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    struct
        type-definition-elements-and-members
    end
// or
[ attributes ]
[<StructAttribute>]
type [accessibility-modifier] type-name =
    type-definition-elements-and-members
```

## <a name="remarks"></a>备注

结构是否*值类型*，这意味着它们直接对堆栈中，或将其用作时存储字段或数组元素内联在父类型。 与类和记录不同，结构具有按值传递语义。 这意味着它们主要用于经常访问和复制的少量聚合数据。

在前面的语法中，将显示两个窗体。 第一个窗体不是轻量级语法，但其仍然经常使用，因为当使用 `struct` 和 `end` 关键字时，你可以忽略第二个窗体中出现的 `StructAttribute` 特性。 你可以将 `StructAttribute` 缩写为 `Struct`。

*类型的定义的元素-和-成员*在上述语法中表示成员声明和定义。 结构可以具有构造函数以及可变和不可变字段，并且可以声明成员和接口实现。 有关详细信息，请参阅[成员](members/index.md)。

结构不能参与继承、不能包含 `let` 或 `do` 绑定、不能以递归方式包含其自身类型的字段（但可以包含引用其自身类型的引用单元格）。

由于结构不允许 `let` 绑定，你必须通过使用 `val` 关键字在结构中声明字段。 `val` 关键字定义字段及其类型，但不允许初始化。 相反，`val` 声明会初始化零或 null。 因此，具有隐式构造函数（即，在声明中的结构名称后直接给定参数）的结构要求使用 `val` 特性批注 `DefaultValue` 声明。 具有定义构造函数的结构仍支持零初始化。 因此，`DefaultValue` 特性是此类零值对字段有效的声明。 由于此类型上不允许 `let` 和 `do` 绑定，结构的隐式构造函数不执行任何操作，但所传入的隐式构造函数参数值作为私有字段提供。

显式构造函数可能涉及字段值的初始化。 当你的结构具有显式构造函数时，它仍支持零初始化；但是，由于它与显式构造函数冲突，请勿在 `DefaultValue` 声明上使用 `val` 特性。 有关详细信息`val`声明，请参阅[显式字段：`val`关键字](members/explicit-fields-the-val-keyword.md)。

结构上允许特性和可访问性修饰符，并遵循与其他类型相同的规则。 有关详细信息，请参阅[特性](attributes.md)并[访问控制](access-control.md)。

以下代码示例说明结构定义。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2501.fs)]

## <a name="byreflike-structs"></a>ByRefLike 结构

您可以定义自己的结构，可以遵循`byref`-如语义： 请参阅[Byref](byrefs.md)有关详细信息。 这通过<xref:System.Runtime.CompilerServices.IsByRefLikeAttribute>属性：

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsByRefLike` 并不意味着`Struct`。 必须同时出现在类型上。

一个"`byref`-如"结构中的F#是绑定堆栈的值类型。 它永远不会分配托管堆上。 一个`byref`-像结构可用于高效的编程中，因为它强制实施强检查有关生存期和非捕获组。 中的规则：

* 它们可用作函数参数、 方法参数、 局部变量、 方法返回。
* 它们不能是静态或实例的类或常规结构的成员。
* 不能通过任何闭包构造捕获它们 (`async`方法或 lambda 表达式)。
* 它们不能用作泛型参数。

尽管这些规则非常强限制使用，但它们这样做是为了满足这一承诺的高性能计算以安全方式。

## <a name="readonly-structs"></a>只读结构

你可以批注与结构<xref:System.Runtime.CompilerServices.IsReadOnlyAttribute>属性。 例如：

```fsharp
[<IsReadOnly; Struct>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsReadOnly` 并不意味着`Struct`。 你必须添加具有`IsReadOnly`结构。

此属性的使用发出元数据让F#和C#知道会将其视为`inref<'T>`并`in ref`分别。

定义 readonly 结构内的可变值将产生错误。

## <a name="struct-records-and-discriminated-unions"></a>结构记录和可区分的联合

可以表示[记录](records.md)并[可区分联合](discriminated-unions.md)为与结构`[<Struct>]`属性。  请参阅每个文章，了解详细信息。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [类](classes.md)
- [记录](records.md)
- [成员](members/index.md)