---
title: let 绑定
description: 了解如何使用F#let 绑定，将一个标识符关联的值或函数。
ms.date: 05/16/2016
ms.openlocfilehash: 45de82acf6f4423698cd8037266968e023f40dcb
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612668"
---
# <a name="let-bindings"></a>let 绑定

一个*绑定*标识符相关联的值或函数。 您使用`let`关键字将绑定到值或函数的名称。

## <a name="syntax"></a>语法

```fsharp
// Binding a value:
let identifier-or-pattern [: type] =expressionbody-expression
// Binding a function value:
let identifier parameter-list [: return-type ] =expressionbody-expression
```

## <a name="remarks"></a>备注

`let`关键字用于绑定表达式来定义值或函数值的一个或多个名称。 最简单的形式`let`表达式将一个名称，如下所示绑定到一个简单的值。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1101.fs)]

如果使用新行分隔标识符中的表达式，必须缩进每一行的表达式，如以下代码所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1102.fs)]

而不是只是一个名称，可以指定包含名称的模式，例如，一个元组，如下面的代码中所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1103.fs)]

*正文表达式*是在其中使用这些名称的表达式。 主体表达式出现在其自己的行，缩进到行向上完全的第一个字符`let`关键字：

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1104.fs)]

一个`let`绑定可以出现在模块级别，类类型的定义中或在本地作用域，例如函数定义。 一个`let`在顶层模块中或在类类型的绑定不需要具有正文表达式，但在其他作用域级别，正文表达式是必需。 绑定的名称是可用的定义，但不是能在之前的时间点后`let`绑定将出现，如下面的代码中所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1105.fs)]

## <a name="function-bindings"></a>函数绑定

函数绑定遵循值绑定的规则，只不过函数的绑定包括函数名称和参数，如下面的代码中所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1106.fs)]

一般情况下，参数是模式，例如元组模式：

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1107.fs)]

一个`let`绑定表达式的计算结果为最后一个表达式的值。 因此，在下面的代码示例的值`result`计算得出`100 * function3 (1, 2)`，其计算结果为`300`。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1109.fs)]

有关详细信息，请参阅[函数](index.md)。

## <a name="type-annotations"></a>类型批注

可以通过包括所有括在括号中的类型名称后跟一个冒号 （:） 指定为参数的类型。 此外可以通过在最后一个参数的后面追加冒号和类型指定的返回值的类型。 完整类型批注`function1`，作为参数类型的整数，是不可能按如下所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1108.fs)]

类型推理时没有显式类型参数，用于确定函数的参数的类型。 这可能包括自动泛化参数用作泛型类型。

有关详细信息，请参阅[自动泛化](../generics/automatic-generalization.md)并[类型推理](../type-inference.md)。

## <a name="let-bindings-in-classes"></a>类中的 let 绑定

一个`let`绑定可以出现在类类型，但不是在结构或记录类型。 若要使用的类类型中的 let 绑定，类必须具有主构造函数。 构造函数参数必须出现在类定义中的类型名称之后。 一个`let`中的类类型的绑定定义私有字段和成员的类类型的并连同`do`在类型中，绑定窗体类型的主构造函数的代码。 下面的代码示例显示了一个类`MyClass`私有字段具有`field1`和`field2`。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1110.fs)]

作用域`field1`和`field2`仅限于在其中声明它们的类型。 有关详细信息，请参阅[`let`类中的绑定](../members/let-bindings-in-classes.md)并[类](../classes.md)。

## <a name="type-parameters-in-let-bindings"></a>中的类型参数的 let 绑定

一个`let`在模块级别，在类型中，或在计算表达式中的绑定可以具有显式类型参数。 中的 let 绑定表达式，例如在函数定义中，不能有类型参数。 有关详细信息，请参阅[泛型](../generics/index.md)。

## <a name="attributes-on-let-bindings"></a>上的属性的 let 绑定

属性可应用于顶级`let`绑定在模块中，如下面的代码中所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet1111.fs)]

## <a name="scope-and-accessibility-of-let-bindings"></a>作用域和辅助功能的 Let 绑定

使用 let 绑定声明的实体的作用域被限制到部分包含的绑定出现后 （如函数、 模块、 文件或类） 作用域。 因此，可以认为 let 的绑定到作用域中引入了一个名称。 在模块中，let 绑定值或函数都可以访问客户端的一个模块，只要该模块是可访问，因为在模块中的 let 的绑定会编译到模块的公共函数。 与此相反，在类中的 let 的绑定是私有的类。

通常情况下，模块中的函数必须由时使用的客户端代码的模块的名称限定。 例如，如果一个模块`Module1`有一个函数`function1`，用户将指定`Module1.function1`来引用该函数。

模块的用户可使用导入声明不按模块名称限定的情况下使该模块中的函数可供使用。 在刚刚提到的示例中，模块的用户可以在这种情况下打开模块通过使用导入声明开放`Module1`和之后是指`function1`直接。

```fsharp
module Module1 =
    let function1 x = x + 1.0

module Module2 =
    let function2 x =
        Module1.function1 x

open Module1

let function3 x =
    function1 x
```

某些模块具有属性[RequireQualifiedAccess](https://msdn.microsoft.com/library/8b9b6ade-0471-4413-ac5d-638cd0de5f15)，这意味着，必须使用的模块的名称限定它们公开的函数。 例如，F#列表模块具有此属性。

模块和访问控制的详细信息，请参阅[模块](../modules.md)并[访问控制](../access-control.md)。

## <a name="see-also"></a>请参阅

- [函数](index.md)
- [类中的 `let` 绑定](../members/let-bindings-in-classes.md)