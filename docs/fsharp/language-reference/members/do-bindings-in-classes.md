---
title: 类中的 do 绑定
description: 了解如何使用F#do 中的类定义，当构造对象或首次使用该类型时将执行操作的绑定。
ms.date: 05/16/2016
ms.openlocfilehash: 0ddf2b5ca458d0950c2e07bf2c37c205877e2173
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613110"
---
# <a name="do-bindings-in-classes"></a>类中的 do 绑定

一个`do`绑定类定义中的执行操作，当构造对象或时，对于静态`do`绑定，类型首次使用时。

## <a name="syntax"></a>语法

```fsharp
[static] do expression
```

## <a name="remarks"></a>备注

一个`do`一起使用或者之后，会显示绑定`let`绑定类定义中的成员定义之前。 尽管`do`关键字是可选的`do`绑定在模块级别，它不是可选的`do`类定义中的绑定。

有关构造的每个对象的任何给定类型，非静态`do`绑定和非静态`let`类定义中出现的顺序会执行绑定。 多个`do`绑定可以出现在一个类型中。 非静态`let`绑定和非静态`do`绑定将成为主构造函数的主体。 中非静态的代码`do`主构造函数参数和任何值或函数中定义的绑定节可以引用`let`绑定部分。

非静态`do`绑定可以访问类的成员，只要类具有定义的自我标识符`as`类标题，并，只要这些成员的所有使用都限定为类的自我标识符中的关键字。

因为`let`绑定将初始化一个类，这通常是为保证成员正常工作所必需的私有字段`do`绑定通常置于后`let`绑定中的代码的因此`do`绑定可以执行完全初始化的对象。 如果你的代码尝试使用成员初始化完成之前，将引发 InvalidOperationException。

静态`do`绑定可以引用静态成员或字段的封闭类，但不是实例成员或字段。 静态`do`绑定将成为类，该类可保证执行之前先使用类的静态初始值设定项的一部分。

属性被忽略的`do`中类型的绑定。 如果属性是必需执行中的代码的`do`绑定，它必须将应用于主构造函数。

在下面的代码中，类具有一个静态`do`绑定和非静态`do`绑定。 该对象具有两个参数的构造函数`a`并`b`，和两个私有字段中定义`let`类的绑定。 此外定义了两个属性。 所有这些处于作用域内非静态`do`绑定部分中，通过将所有这些值输出的行所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3101.fs)]

输出如下所示。

```console
Initializing MyType.
Initializing object 1 2 2 4 8 16
```

## <a name="see-also"></a>请参阅

- [成员](index.md)
- [类](../classes.md)
- [构造函数](constructors.md)
- [类中的 `let` 绑定](let-bindings-in-classes.md)
- [`do` 绑定](../functions/do-Bindings.md)