---
title: 方法
description: 了解如何F#方法是与用于公开和实现的功能和行为的对象和类型的类型相关联的函数。
ms.date: 05/16/2016
ms.openlocfilehash: 03150cc67f79bfde58cf27e4a9d4dfa9e9ff3f55
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614020"
---
# <a name="methods"></a>方法

一个*方法*是与类型相关联的函数。 在面向对象的编程中，使用方法来公开和实现的功能和行为的对象和类型。

## <a name="syntax"></a>语法

```fsharp
// Instance method definition.
[ attributes ]
member [inline] self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Static method definition.
[ attributes ]
static member [inline] method-name parameter-list [ : return-type ] =
    method-body

// Abstract method declaration or virtual dispatch slot.
[ attributes ]
abstract member method-name : type-signature

// Virtual method declaration and default implementation.
[ attributes ]
abstract member method-name : type-signature
[ attributes ]
default self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Override of inherited virtual method.
[ attributes ]
override self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Optional and DefaultParameterValue attributes on input parameters
[ attributes ]
[ modifier ] member [inline] self-identifier.method-name ([<Optional; DefaultParameterValue( default-value )>] input) [ : return-type ]
```

## <a name="remarks"></a>备注

在上述语法中，可以看到各种形式的方法声明和定义。 在较长的方法体，等号 （=） 后, 跟换行符和缩进整个方法主体。

特性可以应用于任何方法声明。 它们位于方法定义的语法，并且通常列在单独的行。 有关更多信息，请参阅[特性](../attributes.md)。

可以将方法标记为`inline`。 有关 `inline` 的信息，请参阅[内联函数](../functions/inline-functions.md)。

可以在类型; 中的递归使用的非内联的方法。无需显式使用`rec`关键字。

## <a name="instance-methods"></a>实例方法

实例方法声明具有`member`关键字和一个*自我标识符*后, 跟一个句点 （.） 的方法名称和参数。 对于这种情况`let`绑定，*参数列表*可以是一种模式。 通常情况下，则将括在圆括号中元组形式，这是方法方法的参数出现在方法F#及其在其他.NET Framework 语言中的创建时间。 但是，扩充的形式 （用空格分隔的参数） 也很常见，并且还支持其他模式。

下面的示例演示定义和使用非抽象实例方法。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3401.fs)]

在实例方法中，不要使用 let 的绑定定义的访问权限字段使用自我标识符。 访问其他成员和属性时，请使用自我标识符。

## <a name="static-methods"></a>静态方法

关键字`static`用于指定可以没有实例调用的方法，并且不相关联的对象实例。 否则，方法是实例方法。

下一节中的示例显示了使用声明的字段`let`关键字，使用声明的属性成员`member`关键字，并且使用声明的静态方法`static`关键字。

下面的示例演示定义和使用静态方法。 假定这些方法定义中`SomeType`上一节中的类。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3402.fs)]

## <a name="abstract-and-virtual-methods"></a>抽象方法和虚方法

关键字`abstract`指示一种方法都有一个虚拟调度和可能不具有在类中定义。 一个*虚拟调度槽*是面向对象的类型中的调用在运行时中用于查找虚函数在内部维护函数的表中的条目。 虚拟调度机制是实现的机制*多态性*，面向对象的编程的一个重要功能。 具有至少一个抽象方法没有定义的类是*抽象类*，这意味着该类的可以创建任何实例。 有关抽象类的详细信息，请参阅[抽象类](../abstract-classes.md)。

抽象方法声明不包括方法体。 相反，该方法的名称后跟一个冒号 （:） 和方法的类型签名。 一种方法的类型签名是您将鼠标指针悬停通过方法名称在 Visual Studio 代码编辑器中，除而无需参数名称时，intellisense 所示相同的。 当您正在以交互方式，解释器，fsi.exe，也会显示类型签名。 Out 参数后, 跟具有相应的分隔符的返回类型的类型的列表格式是一种方法的类型签名。 扩充的参数由分隔`->`分隔元组参数`*`。 返回值始终与通过参数分隔开来`->`符号。 可以使用括号，到组复杂的参数，例如，当函数类型是一个参数，或者用于指示当元组被视为单个参数而不是两个参数。

你还可以允许抽象方法默认定义通过添加到类定义并使用`default`关键字，如本主题中的语法块中所示。 同一类中都有一个定义一个抽象方法相当于其他.NET Framework 语言中的虚拟方法。 是否存在的定义，`abstract`关键字在类的虚函数表中创建一个新的调度槽。

无论是否基类实现其抽象方法，派生的类可以提供抽象方法的实现。 若要在派生类中实现一个抽象方法，定义在派生类中，除使用具有相同名称和签名的方法`override`或`default`关键字，并提供方法体。 关键字`override`和`default`意味着完全相同的目标。 使用`override`的新方法重写基类实现; 如果使用`default`时您创建与原始的抽象声明相同的类中实现。 不要使用`abstract`关键字上实现抽象基类中声明的方法的方法。

下面的示例演示一个抽象方法`Rotate`，其默认实现，.NET Framework 的虚方法的等效项。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3403.fs)]

下面的示例演示一个重写基类方法的派生的类。 在这种情况下，重写更改的行为，以便该方法不执行任何操作。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3404.fs)]

## <a name="overloaded-methods"></a>重载方法

重载的方法是在给定类型中具有相同名称但具有不同参数的方法。 在F#，而不是重载方法通常使用可选参数。 但是，重载的方法允许在语言中，参数是在元组形式中，不是扩充形式。

## <a name="optional-arguments"></a>可选实参

从F#4.1，您还可以使用默认参数值的可选参数在方法中。  这是为了便于与 C# 代码的互操作。  下面的示例演示了该语法：

```fsharp
// A class with a method M, which takes in an optional integer argument.
type C() =
    __.M([<Optional; DefaultParameterValue(12)>] i) = i + 1
```

请注意，为传入的值`DefaultParameterValue`必须与输入的类型匹配。  在上面的示例，它是`int`。  尝试将传递到一个非整数值`DefaultParameterValue`将导致编译错误。

## <a name="example-properties-and-methods"></a>示例:属性和方法

下面的示例包含具有字段、 私有函数、 属性和静态方法的示例的类型。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3406.fs)]

## <a name="see-also"></a>请参阅

- [成员](index.md)