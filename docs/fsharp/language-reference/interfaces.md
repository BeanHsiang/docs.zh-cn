---
title: 接口
description: 了解如何F#接口指定的其他类实现的相关成员集。
ms.date: 05/16/2016
ms.openlocfilehash: 85b5506d96c26be5e52670c0c62d27cae047d1a6
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610549"
---
# <a name="interfaces"></a>接口

*接口*指定其他类实现的相关成员的集。

## <a name="syntax"></a>语法

```fsharp
// Interface declaration:
[ attributes ]
type [accessibility-modifier] interface-name =
    [ interface ]     [ inherit base-interface-name ...]
    abstract member1 : [ argument-types1 -> ] return-type1
    abstract member2 : [ argument-types2 -> ] return-type2
    ...
[ end ]

// Implementing, inside a class type definition:
interface interface-name with
    member self-identifier.member1argument-list = method-body1
    member self-identifier.member2argument-list = method-body2

// Implementing, by using an object expression:
[ attributes ]
let class-name (argument-list) =
    { new interface-name with
        member self-identifier.member1argument-list = method-body1
        member self-identifier.member2argument-list = method-body2
        [ base-interface-definitions ]
    }
    member-list
```

## <a name="remarks"></a>备注

接口声明类似于类声明，只不过未实现成员。 相反，所有成员都是抽象的由关键字`abstract`。 抽象方法不提供方法体。 但是，可以通过包括单独定义的成员一起使用的方法提供默认实现`default`关键字。 执行此操作等效于在其他.NET 语言中的基类中创建的虚拟方法。 可以在实现该接口的类中重写此类的虚方法。

接口的默认可访问性是`public`。

您可以根据需要为每个方法参数提供一个名称使用常规F#语法：

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet24032.fs)]

在上面`ISprintable`示例中，`Print`方法具有单个类型的参数`string`同名`format`。

有两种方法来实现的接口： 通过使用对象表达式，并通过使用类类型。 在任一情况下，类类型或对象表达式为接口的抽象方法提供方法体。 实现是特定于每个类型实现接口。 因此，不同类型的接口方法可能彼此不同。

关键字`interface`和`end`，使用轻量语法时，用于标记的开始和结束的定义，将可选。 如果不使用这些关键字，编译器将尝试推断类型通过分析使用的构造是否是一个类或接口。 如果您定义一个成员，或使用其他类的语法，该类型将解释为一个类。

.NET 编码样式是开始使用大写的所有接口`I`。

## <a name="implementing-interfaces-by-using-class-types"></a>通过使用类类型实现接口

可通过使用类类型中实现一个或多个接口`interface`关键字，接口的名称和`with`关键字后, 跟接口成员定义，如下面的代码中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2801.fs)]

继承接口实现，因此任何派生的类无需重新实现它们。

## <a name="calling-interface-methods"></a>调用接口方法

可以仅通过该接口，不能通过类型实现接口的任何对象调用接口方法。 因此，可能向上转换为接口类型必须通过使用`:>`运算符或`upcast`为了调用这些方法的运算符。

若要调用接口方法具有类型的对象时`SomeClass`，如下面的代码中所示，必须将向上转换为接口类型的对象。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2802.fs)]

一种替代方法是在对象上的向上转换声明一个方法，并调用接口方法，如以下示例所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2803.fs)]

## <a name="implementing-interfaces-by-using-object-expressions"></a>通过使用对象表达式实现接口

对象表达式提供了一种快捷方法来实现接口。 不需要创建一个名为的类型，并只是想支持的接口方法，而无需任何其他方法的对象时很有用。 下面的代码说明了对象表达式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2804.fs)]

## <a name="interface-inheritance"></a>接口继承

接口可以从一个或多个基接口继承。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2805.fs)]

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [对象表达式](object-expressions.md)
- [类](classes.md)