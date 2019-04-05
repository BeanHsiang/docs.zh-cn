---
title: 构造函数
description: 了解如何定义和使用中的构造函数F#创建和初始化类和结构的对象。
ms.date: 05/16/2016
ms.openlocfilehash: 34989e2877b29f6f9fe1f6cc05e3fd7c90a1306a
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612070"
---
# <a name="constructors"></a>构造函数

本主题介绍如何定义和使用构造函数来创建和初始化类和结构的对象。

## <a name="construction-of-class-objects"></a>类对象的构造

类类型的对象具有构造函数。 有两种类型的构造函数。 一个是主构造函数，其参数的类型名称之后出现在括号内。 使用指定另一个可选的附加构造函数`new`关键字。 任何此类其他构造函数必须调用主构造函数。

主构造函数包含`let`和`do`类定义开头显示的绑定。 一个`let`绑定声明的私有字段和方法的类;`do`绑定执行代码。 有关详细信息`let`绑定中类构造函数，请参阅[`let`类中的绑定](let-bindings-in-classes.md)。 有关详细信息`do`绑定中的构造函数，请参阅[`do`类中的绑定](do-bindings-in-classes.md)。

无论你想要调用的构造函数是主构造函数或另一个构造函数，可以通过使用创建对象`new`表达式，带或不带可选`new`关键字。 您初始化您的对象以及构造函数参数，通过列出顺序中的自变量和通过以逗号分隔并括在括号中，或通过在括号中使用命名的参数和值。 您还可以设置属性的对象上的对象的构造期间使用的属性名称并分配值，就像您使用名为构造函数自变量。

以下代码演示了具有一个构造函数和创建对象的各种方法的类。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet3501.fs)]

输出如下所示。

```console
Initialized object that has coordinates (1, 2, 3)
Initialized object that has coordinates (4, 5, 6)
Initialized object that has coordinates (7, 8, 9)
Initialized object that has coordinates (0, 0, 0)
```

## <a name="construction-of-structures"></a>构造的结构

结构按照类的所有规则。 因此，可以具有主构造函数，并可以使用来提供其他构造函数`new`。 但是，没有结构和类之间的一个重要区别： 结构可以具有默认构造函数 （即，一个不带任何参数），即使没有主构造函数定义。 默认构造函数初始化为默认值为该类型，通常为零或其等效的所有字段。 为结构定义任何构造函数必须具有至少一个参数，以便使用默认构造函数不冲突。

此外，结构通常具有通过使用创建的字段`val`关键字; 类还可以具有这些字段。 结构和类具有使用定义的字段的`val`关键字可以也在中初始化其他构造函数通过使用记录表达式，如下面的代码中所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet3502.fs)]

有关详细信息，请参阅[显式字段：`val`关键字](explicit-fields-the-val-keyword.md)。

## <a name="executing-side-effects-in-constructors"></a>在构造函数中执行的负面影响

在类中的主构造函数可以执行中的代码`do`绑定。 但是，如果您需要在另一个构造函数，而不执行代码`do`绑定？ 若要执行此操作，应使用`then`关键字。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet3503.fs)]

主构造函数的副作用仍能执行。 因此，输出如下所示。

```console
Created a person object.
Created a person object.
Created an invalid person object.
```

## <a name="self-identifiers-in-constructors"></a>在构造函数中的自我标识符

在其他成员提供每个成员的定义中的当前对象的名称。 此外可以将自我标识符的类定义的第一行上使用`as`紧跟构造函数参数的关键字。 下面的示例说明了此语法。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet3504.fs)]

在其他构造函数，您还可以定义自我标识符放`as`子句之后的构造函数参数。 下面的示例说明了此语法。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet3505.fs)]

尝试之前已完全定义使用一个对象，则会出现问题。 因此，使用自我标识符会导致编译器发出警告并插入其他检查，以确保该对象初始化之前不会访问对象的成员。 只应使用中的自我标识符`do`绑定的主构造函数，或之后`then`其他构造函数中的关键字。

自我标识符的名称不一定要`this`。 它可以是任何有效的标识符。

## <a name="assigning-values-to-properties-at-initialization"></a>将值分配给在初始化的属性

可以通过追加格式的赋值的列表中的初始化代码的类对象的属性分配值`property = value`到一个构造函数的参数列表。 下面的代码示例对此进行了演示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

前面的代码中的以下版本说明了普通自变量、 可选参数和一个构造函数调用中的属性设置的组合。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet3507.fs)]

## <a name="constructors-in-inherited-class"></a>中继承的类的构造函数

从具有一个构造函数的基类继承时，必须在继承子句中指定其自变量。 有关详细信息，请参阅[构造函数和继承](../inheritance.md#constructors-and-inheritance)。

## <a name="static-constructors-or-type-constructors"></a>静态构造函数或类型构造函数

除了指定代码用于创建对象，静态`let`和`do`绑定可以在执行之前首先使用的类型来执行初始化在类型级别的类类型中编写。 有关详细信息，请参阅[`let`类中的绑定](let-bindings-in-classes.md)并[`do`类中的绑定](do-bindings-in-classes.md)。

## <a name="see-also"></a>请参阅

- [成员](index.md)