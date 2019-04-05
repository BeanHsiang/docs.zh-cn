---
title: 继承
description: 了解如何指定F#使用继承关键字的继承关系。
ms.date: 05/16/2016
ms.openlocfilehash: 775ee52039caf4c4ab65f82fa21d4e536135a12a
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610133"
---
# <a name="inheritance"></a>继承

使用继承进行建模"是 a"关系或子类型化，在面向对象的编程。

## <a name="specifying-inheritance-relationships"></a>指定继承关系

使用指定继承关系`inherit`类声明中的关键字。 基本语法形式如以下示例所示。

```fsharp
type MyDerived(...) =
    inherit MyBase(...)
```

一个类可以有最多一个直接基类。 如果不执行操作通过使用指定的基类`inherit`类的关键字，隐式继承自`System.Object`。

## <a name="inherited-members"></a>继承的成员

如果一个类继承自另一个类，则方法和类的基类的成员可供派生类的用户就像直接成员的派生类。

任何的 let 绑定和构造函数参数是专用于一个类，因此，不能从派生类访问。

关键字`base`可在派生类中，并且引用的基的类实例。 它被当做自我标识符。

## <a name="virtual-methods-and-overrides"></a>虚方法和重写

虚方法 （和属性） 在某种程度上以不同方式处理F#与其他.NET 语言相比。 若要声明新的虚拟成员，请使用`abstract`关键字。 无论您是否提供的默认实现，该方法执行此操作。 因此在基类中虚方法的完整定义采用这种模式：

```fsharp
abstract member [method-name] : [type]

default [self-identifier].[method-name] [argument-list] = [method-body]
```

和此虚拟方法的重写派生类中采用这种模式：

```fsharp
override [self-identifier].[method-name] [argument-list] = [method-body]
```

如果省略基类中的默认实现，基类将成为一个抽象类。

下面的代码示例说明了新的虚拟方法的声明`function1`基类以及如何在派生类中重写它。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2601.fs)]

## <a name="constructors-and-inheritance"></a>构造函数和继承

必须在派生类中调用基类构造函数。 基类构造函数的参数的参数列表中显示`inherit`子句。 必须从提供给派生的类构造函数的参数确定所使用的值。

下面的代码显示了基类和派生的类中，其中派生的类调用基类构造函数中的继承子句：

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2602.fs)]

在多个构造函数的情况下可以使用下面的代码。 在派生的类构造函数的第一行是`inherit`子句中，和字段显示为与声明的显式字段`val`关键字。 有关详细信息，请参阅[显式字段：`val`关键字](members/explicit-fields-the-val-keyword.md)。

```fsharp
type BaseClass =
    val string1 : string
    new (str) = { string1 = str }
    new () = { string1 = "" }

type DerivedClass =
    inherit BaseClass

    val string2 : string
    new (str1, str2) = { inherit BaseClass(str1); string2 = str2 }
    new (str2) = { inherit BaseClass(); string2 = str2 }

let obj1 = DerivedClass("A", "B")
let obj2 = DerivedClass("A")
```

## <a name="alternatives-to-inheritance"></a>继承的替代方法

在需要稍作修改的一种类型的情况下，请考虑使用对象表达式作为继承的替代方法。 下面的示例演示如何使用对象表达式来创建新的派生的类型的替代方法：

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2603.fs)]

对象表达式的详细信息，请参阅[对象表达式](object-expressions.md)。

当你创建的对象层次结构时，请考虑使用而不继承的可区分的联合。 可区分的联合还可以共享通用的整体类型的不同对象的模型不同的行为。 单个可区分的联合通常无需多个次要变体的每个其他派生类。 有关可区分联合的信息，请参阅[可区分联合](discriminated-unions.md)。

## <a name="see-also"></a>请参阅

- [对象表达式](object-expressions.md)
- [F# 语言参考](index.md)