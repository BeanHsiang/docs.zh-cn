---
title: 强制转换和转换
description: 了解如何F#编程语言提供的各种基元类型之间的算术转换的转换运算符。
ms.date: 05/16/2016
ms.openlocfilehash: 2a12d48106a267edfc67c9e7b3d3a7bd41d8261c
ms.sourcegitcommit: 3d0c29b878f00caec288dfecb3a5c959de5aa629
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655980"
---
# <a name="casting-and-conversions-f"></a>强制转换和转换 (F#)

本主题介绍了类型转换的F#。

## <a name="arithmetic-types"></a>算术类型

F#提供转换运算符的各种基元类型之间的算术转换如之间的整数和浮点类型。 整型和 char 转换运算符具有选中和取消选中窗体;浮点运算符和`enum`转换运算符不这样做。 取消选中窗体中定义`Microsoft.FSharp.Core.Operators`并选中窗体中定义`Microsoft.FSharp.Core.Operators.Checked`。 选中窗体溢出检查，并生成运行时异常，如果生成的值超出了目标类型的限制。

每个运算符具有名称与目标类型的名称相同。 例如，在下面的代码，在其中的类型已显式批注，`byte`显示有两个不同的含义。 第一个匹配项是类型，第二个是转换运算符。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4401.fs)]

下表显示了在中定义的转换运算符F#。

|运算符|描述|
|--------|-----------|
|`byte`|将转换为字节，8 位无符号类型。|
|`sbyte`|将转换为有符号字节。|
|`int16`|将转换为 16 位有符号整数。|
|`uint16`|将转换为 16 位无符号整数。|
|`int32, int`|将转换为 32 位有符号整数。|
|`uint32`|将转换为 32 位无符号整数。|
|`int64`|将转换为 64 位有符号整数。|
|`uint64`|将转换为 64 位无符号整数。|
|`nativeint`|将转换为本机整数。|
|`unativeint`|将转换为无符号本机整数。|
|`float, double`|将转换为 64 位双精度 IEEE 浮点数。|
|`float32, single`|将转换为 32 位单精度 IEEE 浮点数。|
|`decimal`|将转换为`System.Decimal`。|
|`char`|将转换为`System.Char`，Unicode 字符。|
|`enum`|将转换为枚举类型。|

除了内置基元类型，可以实现的类型与使用这些运算符`op_Explicit`或`op_Implicit`的带有适当签名方法。 例如，`int`转换运算符适用于任何类型，它提供一种静态方法`op_Explicit`用于采用类型作为参数并返回`int`。 作为一般规则无法由返回类型重载方法一个特殊的例外，你可以这样做`op_Explicit`和`op_Implicit`。

## <a name="enumerated-types"></a>枚举的类型

`enum`运算符是采用一个表示的类型的类型参数的泛型运算符`enum`将转换为。 将转换为枚举类型，类型推理会尝试确定的类型`enum`想要将转换为。 在下面的示例中，变量`col1`未显式批注，但其类型推断从更高版本的相等性测试。 因此，编译器可以推断出要转换为`Color`枚举。 或者，你可以提供一个类型批注，如同`col2`在下面的示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4402.fs)]

您可以显式指定目标枚举类型，作为类型参数，如以下代码所示：

```fsharp
let col3 = enum<Color> 3
```

请注意枚举转换工作，仅当枚举的基础类型是与要转换的类型兼容。 在下面的代码，则转换失败由于之间不匹配编译`int32`和`uint32`。

```fsharp
// Error: types are incompatible
let col4 : Color = enum 2u
```

有关详细信息，请参阅[枚举](enumerations.md)。

## <a name="casting-object-types"></a>强制转换对象类型

类型的对象层次结构之间的转换是面向对象的编程的基础。 有两种基本类型的转换： 向上转换） 和向下转换）。 强制转换的层次结构表示强制转换为基对象引用是派生的对象引用。 此类强制转换是能保证有效，前提是在派生类的继承层次结构中的类的基类。 按层次结构，从基对象引用为派生的对象引用，强制转换成功，仅当该对象实际上是正确的目标 （派生） 类型或派生自目标类型的类型的实例。

F#提供的这些类型的转换运算符。 `:>`层次结构，向上转换运算符和`:?>`沿层次结构将转换运算符。

### <a name="upcasting"></a>向上转换

在许多面向对象语言中，向上转换是隐式;在F#，这些规则略有不同。 当你将参数传递到方法的对象类型上时，将自动应用向上转换。 但是，对于在模块中的 let 绑定函数，向上转换不是自动的除非参数类型被声明为灵活的类型。 有关详细信息，请参阅[可变类型](flexible-Types.md)。

`:>`运算符执行静态强制转换，这意味着在编译时确定转换是否成功。 如果使用的强制转换`:>`编译成功，它是有效的转换，在运行时有无故障的可能性。

此外可以使用`upcast`运算符来执行此类转换。 以下表达式指定层次结构向上转换：

```fsharp
upcast expression
```

当使用向上转换运算符时，编译器将尝试推断上下文中将转换为的类型。 如果编译器无法确定目标类型，编译器会报告错误。

### <a name="downcasting"></a>向下转换

`:?>`运算符执行动态强制转换，这意味着在运行时确定转换是否成功。 使用强制转换`:?>`运算符不检查在编译时; 但在运行时，尝试将强制转换为指定的类型。 如果对象是与目标类型兼容，强制转换会成功。 如果对象不是与目标类型兼容的运行时将引发`InvalidCastException`。

此外可以使用`downcast`运算符来执行动态类型转换。 以下表达式指定沿层次结构从程序上下文中推断出的类型的转换：

```fsharp
downcast expression
```

同样适用于`upcast`运算符，如果编译器无法推断特定的目标类型从上下文，它将报告错误。

下面的代码演示如何使用`:>`和`:?>`运算符。 该代码演示`:?>`您知道，转换将失败，因为它会引发，最好使用运算符`InvalidCastException`如果转换失败。 如果不知道，转换会成功，使用的类型测试`match`表达式是更好的因为它可以避免生成异常的开销。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4403.fs)]

因为泛型运算符`downcast`和`upcast`依赖类型推断来确定自变量和返回类型，在上面的代码，您可以替换

```fsharp
let base1 = d1 :> Base1
```

替换为

```fsharp
let base1 = upcast d1
```

在上面的代码中的参数类型和返回类型是`Derived1`和`Base1`分别。

类型测试的详细信息，请参阅[匹配表达式](match-Expressions.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
