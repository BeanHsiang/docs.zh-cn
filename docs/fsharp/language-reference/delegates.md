---
title: 委托
description: 了解如何在使用中的委托F#。
ms.date: 05/16/2016
ms.openlocfilehash: 772685488b7caef92123979d817929c631248afb
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612889"
---
# <a name="delegates"></a>委托

一个委托作为一个对象表示一个函数调用。 在F#，你通常应使用函数的值来表示作为一类值; 函数但是，委托在.NET Framework 中使用，因此时，需要与所希望的 Api 进行互操作。 可能还会使用它们时从其他.NET Framework 语言创作库设计用于使用。

## <a name="syntax"></a>语法

```fsharp
type delegate-typename = delegate of type1 -> type2
```

## <a name="remarks"></a>备注

在上述语法中，`type1`表示的参数类型和`type2`表示返回类型。 由自变量类型`type1`会自动进行扩充。 这表明，如果目标函数的参数会进行扩充，使用元组形式的此类型和已在元组形式的参数的带括号的元组。 自动科中删除一组括号，离开匹配的目标方法的元组参数。 请参阅中每种情况下应使用的语法的代码示例。

可以将委托附加到F#函数的值以及静态或实例方法。 F#可以直接作为要委托构造函数自变量传递函数值。 对于静态方法，使用的类和方法名称构造委托。 对于实例方法，需要提供的对象实例和一个自变量中的方法。 在这两种情况下，成员访问运算符 (`.`) 使用。

`Invoke`委托类型的方法调用封装的函数。 此外，还可以引用不带括号的 Invoke 方法名称作为函数值传递委托。

下面的代码演示用于创建表示在类中的各种方法的委托的语法。 具体取决于的方法是静态方法或实例方法，以及是否有元组形式或扩充窗体中的自变量，声明和赋值委托语法是稍有不同。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4201.fs)]

下面的代码显示了一些可以在使用委托的不同方法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4202.fs)]

前面的代码示例的输出如下所示。

```console
aaaaa
bbbbb
ccccc
[|"aaa"; "bbb"|]
```

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [参数和自变量](parameters-and-arguments.md)
- [事件](members/events.md)