---
title: 对象表达式
description: 了解如何使用F#对象表达式时您想要避免额外的代码和开销所需创建一个新命名类型。
ms.date: 02/08/2019
ms.openlocfilehash: c00b2e329a97b86ec2c8c84c143d2aa199875442
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56091664"
---
# <a name="object-expressions"></a>对象表达式

*对象表达式*是表达式，它创建动态创建的匿名对象类型的新实例可基于现有基类型、 接口或接口集。

## <a name="syntax"></a>语法

```fsharp
// When typename is a class:
{ new typename [type-params]arguments with
    member-definitions
    [ additional-interface-definitions ]
}
// When typename is not a class:
{ new typename [generic-type-args] with
    member-definitions
    [ additional-interface-definitions ]
}
```

## <a name="remarks"></a>备注

在上述语法中， *typename*表示现有的类类型或接口类型。 *类型-params*介绍了可选的泛型类型参数。 *自变量*仅用于类类型，需要构造函数参数。 *成员定义*替代基类方法，或从基类或接口的抽象方法的实现。

下面的示例演示了多种不同类型的对象表达式。

```fsharp
// This object expression specifies a System.Object but overrides the
// ToString method.
let obj1 = { new System.Object() with member x.ToString() = "F#" }
printfn "%A" obj1

// This object expression implements the IFormattable interface.
let delimiter(delim1: string, delim2: string, value: string) =
    { new System.IFormattable with
        member x.ToString(format: string, provider: System.IFormatProvider) =
            if format = "D" then
                delim1 + value + delim2
            else
                value }

let obj2 = delimiter("{","}", "Bananas!");

printfn "%A" (System.String.Format("{0:D}", obj2))

// This object expression implements multiple interfaces.
type IFirst =
  abstract F : unit -> unit
  abstract G : unit -> unit

type ISecond =
  inherit IFirst
  abstract H : unit -> unit
  abstract J : unit -> unit

// This object expression implements an interface chain.
let implementer() =
    { new ISecond with
        member this.H() = ()
        member this.J() = ()
      interface IFirst with
        member this.F() = ()
        member this.G() = () }
```

## <a name="using-object-expressions"></a>使用对象表达式

当你想要避免额外的代码和创建所需的新命名类型的开销时，您可以使用对象表达式。 如果您使用对象表达式在程序中创建的类型的数量降至最低，可以减少代码的行数，并防止不必要的迅速普及的类型。 而不是创建多个类型只是为了处理特定情况下，可以使用自定义现有类型或为手头的特定情况提供适当的接口实现的对象表达式。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
