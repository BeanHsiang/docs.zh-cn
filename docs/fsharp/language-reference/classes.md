---
title: 类
description: 了解如何F#类是表示可以具有属性、 方法和事件的对象的类型。
ms.date: 05/16/2016
ms.openlocfilehash: 6bf838e98acecb89436d3e87809d9eb6da0c66d5
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53611173"
---
# <a name="classes"></a>类

*类*是表示可以具有属性、 方法和事件的对象类型。

## <a name="syntax"></a>语法

```fsharp
// Class definition:
type [access-modifier] type-name [type-params] [access-modifier] ( parameter-list ) [ as identifier ] =
[ class ]
[ inherit base-type-name(base-constructor-args) ]
[ let-bindings ]
[ do-bindings ]
member-list
...
[ end ]
// Mutually recursive class definitions:
type [access-modifier] type-name1 ...
and [access-modifier] type-name2 ...
...
```

## <a name="remarks"></a>备注

类表示.NET 对象类型; 的基本说明类是支持面向对象的编程中的主类型概念F#。

在上述语法中，`type-name`是任何有效的标识符。 `type-params`介绍了可选的泛型类型参数。 它包含类型参数名称和括在尖括号中的约束 (`<`和`>`)。 有关详细信息，请参阅[泛型](generics/index.md)并[约束](generics/constraints.md)。 `parameter-list`介绍构造函数参数。 第一个访问修饰符与类型;第二个与主构造函数。 在这两种情况下，默认值是`public`。

使用指定的类的基类`inherit`关键字。 必须提供基类构造函数的参数，在括号中。

声明字段或函数值是通过使用该类的局部`let`绑定，并且必须遵循的一般规则`let`绑定。 `do-bindings`部分包含用于构造对象时执行的代码。

`member-list`包含其他构造函数、 实例和静态方法声明、 接口声明、 抽象的绑定，以及属性和事件声明。 中介绍了这些[成员](members/index.md)。

`identifier` ，可使用可选`as`关键字会为命名实例变量或自我标识符，可用于在类型定义中引用的类型的实例。 有关详细信息，请参阅本主题后面的部分自我标识符。

关键字`class`和`end`标记开头和末尾定义是可选的。

递归类型，它们是相互引用的类型，以及已加入的相互`and`一样相互递归函数是关键字。 有关示例，请参阅部分相互递归类型。

## <a name="constructors"></a>构造函数

构造函数是可创建类类型的实例的代码。 类构造函数中稍有不同工作F#不是它们在其他.NET 语言中执行操作。 在F#类中，始终是主构造函数中所述该形参的实参`parameter-list`后面的类型名称，其正文组成`let`(和`let rec`) 在类声明开头的绑定和`do`遵循的绑定。 在主构造函数的参数是在类声明整个范围内。

可以使用添加其他构造函数`new`关键字添加成员，按如下所示：

`new`(`argument-list`) = `constructor-body`

新的构造函数的主体必须调用主构造函数指定的类声明的顶部。

下面的示例说明了这一概念。 在下面的代码，`MyClass`具有两个构造函数，主构造函数采用两个参数和另一个构造函数不采用任何参数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2401.fs)]

## <a name="let-and-do-bindings"></a>let 和 do 绑定

`let`和`do`类定义中的绑定窗体中的主类构造函数的正文，因此它们运行时创建的类实例。 如果`let`绑定是一个函数，则将它编译为一个成员。 如果`let`绑定是一个值，不用于在任何函数或成员，则将它编译到一个变量中的本地构造函数。 否则，它被编译到类的字段。 `do`遵循的表达式被编译到主构造函数和执行每个实例的初始化代码。 其他所有构造函数始终调用主构造函数，因为`let`绑定和`do`绑定始终执行而不考虑其调用构造函数。

创建的字段`let`绑定可以访问在整个方法和类的属性; 但是，它们不能从访问静态方法，即使这些静态方法采用实例变量作为参数。 它们不能通过使用自我标识符，如果存在访问。

## <a name="self-identifiers"></a>自我标识符

一个*自我标识符*是表示当前实例的名称。 自我标识符类似于`this`C# 或 c + + 中的关键字或`Me`在 Visual Basic 中。 您可以在两种不同的方式，具体取决于是否想要在作用域为整个类定义或只是单个方法中的自助标识符定义自我标识符。

若要定义整个类自我标识符，请使用`as`构造函数参数的右括号后的关键字列表，并指定标识符名称。

若要定义的自我标识符只是一种方法，提供在成员声明中，只需在方法名称和句点 （.） 作为分隔符之前的自我标识符。

下面的代码示例说明了创建自我标识符的两种方法。 在第一行`as`关键字用于定义自我标识符。 在第五个行中，标识符`this`用于定义其作用域仅限于方法自我标识符`PrintMessage`。

```fsharp
type MyClass2(dataIn) as self =
    let data = dataIn
    do
        self.PrintMessage()
    member this.PrintMessage() =
        printf "Creating MyClass2 with Data %d" data
```

与在其他.NET 语言中，您可以命名自我标识符随意;您不限于名称如`self`， `Me`，或`this`。

使用声明的自我标识符`as`关键字未初始化之前后`let`会执行绑定。 因此，它不能用在`let`绑定。 可以使用中的自我标识符`do`绑定部分。

## <a name="generic-type-parameters"></a>泛型类型参数

在尖括号中指定泛型类型参数 (`<`和`>`)，在标识符后跟可用一个单引号的窗体中。 由逗号分隔多个泛型类型参数。 泛型类型参数是在整个声明范围内。 下面的代码示例演示如何指定泛型类型参数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2403.fs)]

使用类型时，会被推断类型参数。 在下面的代码中，推断出的类型是元组序列。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet24031.fs)]

## <a name="specifying-inheritance"></a>指定继承

`inherit`子句标识直接基类，如果有的话。 在F#中，只有一个直接基类允许。 一个类实现的接口不会考虑基类。 接口中讨论[接口](Interfaces.md)主题。

您可以访问的方法和属性的基类派生类中使用的语言关键字`base`作为标识符后, 跟一个句点 （.） 和成员的名称。

有关详细信息，请参阅[继承](inheritance.md)。

## <a name="members-section"></a>成员部分

可以在本部分中定义静态或实例方法、 属性、 接口实现、 抽象成员，事件声明和其他构造函数。 允许和执行操作的绑定不能出现在本部分中。 因为可以将成员添加到的各种F#类型的类，除了他们讨论了在单独主题中，[成员](members/index.md)。

## <a name="mutually-recursive-types"></a>相互递归类型

在定义以循环方式相互引用的类型时，您将排列在一起的类型定义通过使用`and`关键字。 `and`关键字将替换`type`上除外，如下所示的第一个定义的关键字。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2404.fs)]

输出是当前目录中的所有文件的列表。

## <a name="when-to-use-classes-unions-records-and-structures"></a>何时使用类、 联合、 记录和结构

给定类型可供选择的多样性，需要充分了解什么每种类型专为以选择特定的情况下的相应类型。 类旨在供在面向对象的编程上下文中使用。 面向对象的编程是为.NET Framework 编写的应用程序中使用的主流模式。 如果在F#代码必须与.NET Framework 或另一个面向对象的库，紧密合作，尤其是当您必须扩展从诸如 UI 库之类的面向对象的类型系统，和类可能适当。

如果您不紧密地与代码交互操作的面向对象的或者您编写的是自包含且因此频繁交互，面向对象的代码从受保护的代码，您应该考虑使用记录和可区分联合。 单一的精心构思的可区分的联合，以及合适的模式匹配的代码中，通常可用作对象层次结构的更简单的替代。 有关可区分联合的详细信息，请参阅[可区分联合](discriminated-unions.md)。

记录具有的优点是比类更简单，但记录将不适用时的一种类型的需求超过可完成的简单性。 记录是基本上简单值的聚合，而无需单独的构造函数可以执行自定义操作的、 不包含隐藏字段，且无继承或接口实现。 虽然属性和方法等的成员可以添加到记录，以使其行为更复杂，存储在一条记录中的字段仍是值的简单聚合。 有关记录的详细信息，请参阅[记录](records.md)。

结构也是有用的少量聚合数据，但它们不同于类和记录，它们是.NET 值类型。 类和记录是.NET 引用类型。 值类型和引用类型的语义不同，是按值传递值类型。 这意味着它们进行复制时作为参数传递或从函数返回位的位。 它们是也存储在堆栈上或者，如果将其用作字段，则嵌入在父对象而不是存储在堆上其自己单独的位置。 因此，结构是适用于经常访问的数据访问堆的系统开销问题时。 有关结构的详细信息，请参阅[结构](structures.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [成员](members/index.md)
- [继承](inheritance.md)
- [接口](interfaces.md)