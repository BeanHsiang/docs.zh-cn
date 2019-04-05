---
title: 度量单位
description: 了解如何浮点和的有符号整数值F#可以具有关联的度量值，这些信息通常用于指示长度、 卷和大容量单位。
ms.date: 05/16/2016
ms.openlocfilehash: 935dbff3545f92736ce8c51de86a168429dc194f
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610978"
---
# <a name="units-of-measure"></a>度量单位

浮点数和的有符号整数值F#可以具有关联的单元的度量值，这些信息通常用于指示长度、 卷、 大容量，等等。 通过使用个单位的数量，使编译器无法验证算术关系具有正确的单位，从而有助于防止出现编程错误。

## <a name="syntax"></a>语法

```fsharp
[<Measure>] type unit-name [ = measure ]
```

## <a name="remarks"></a>备注

上述语法中定义*单元名称*作为一个单元的度量值。 可选部分用于定义新的度量值根据以前定义的单位。 例如，以下行定义度量值`cm`（厘米）。

```fsharp
[<Measure>] type cm
```

下面的行定义度量值`ml`（毫升） 为立方厘米 (`cm^3`)。

```fsharp
[<Measure>] type ml = cm^3
```

在上述语法中，*度量值*是涉及到单元的公式。 在涉及单元的公式，（正值和负值） 支持整数幂，单位之间的空格指示两个单位的产品`*`还表示的单位，产品和`/`指示的单位的商。 对于相应的单元，可以使用负的整数幂或`/`，该值指示分子和分母的单元公式之间的分隔。 在分母中的多个单元应由括号括起来。 用后的空格分隔的单位`/`被解释为属于分母，但后面的任何单位`*`将被解释为分子的一部分。

在单元表达式中，可以单独以指示纲数量，或者与其他单位，例如分子，可以使用 1。 例如，速率的单位将写为`1/s`，其中`s`表示秒。 在单元公式中不使用括号。 不到单元的公式; 中指定数值转换常量但是，可以单独定义单位使用的转换常量和单元检查计算中使用它们。

表示同一事物的单元公式可以用不同的等效方法。 因此，编译器将转换形式一致，这将负数幂倒数、 组单位转换为单一的分子和分母，并按字母顺序排列的分子和分母中的单元为单位的公式。

例如，单元公式`kg m s^-2`并`m /s s * kg`将转换为`kg m/s^2`。

浮点表达式中使用度量的单位。 使用浮点数与关联的单元的度量值将添加另一个级别的类型安全，并有助于避免使用弱类型化的浮点数时可能出现在公式中的单元不匹配错误。 如果您编写的浮点使用单位的点表达式，必须与匹配表达式中的单元。

下面的示例中所示，你可以批注文本与中尖括号内的单元公式。

```fsharp
1.0<cm>
55.0<miles/hour>
```

您不要将数和尖括号; 之间有空格但是，如包含的文本后缀`f`，如下面的示例。

```fsharp
// The f indicates single-precision floating point.
55.0f<miles/hour>
```

此类批注更改文字的类型从其基元类型 (如`float`) 为划分维度的类型，如`float<cm>`或在这种情况下， `float<miles/hour>`。 单位批注`<1>`指示纲数量和其类型是等效于没有单元参数的基元类型。

是浮点数或带符号整型类型以及额外的单位批注，在括号中指示的测量单位的类型。 因此，当你编写从转换的类型时，才`g`（元语法） 到`kg`（千克） 描述的类型，如下所示。

```fsharp
let convertg2kg (x : float<g>) = x / 1000.0<g/kg>
```

度量单位用于检查的编译时间单位，但不是会保留在运行时环境。 因此，它们不会影响性能。

度量单位可以应用于任何类型，而不仅仅浮点类型;但是，唯一的浮点类型，已签名的整型类型和十进制类型确定了维度的支持数量。 因此，它仅有意义使用基元类型和包含这些基元类型的聚合的度量单位。

下面的示例演示如何使用度量单位。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6901.fs)]

下面的代码示例说明了如何将从纲浮点数转换为划分维度的浮点值。 您只需与 1.0 相乘，将维度应用于 1.0。 可以将此抽象到所示的函数`degreesFahrenheit`。

此外，当将划分维度的值传递到期望纲浮点数的函数中，则必须取消扩展单位或强制转换为`float`通过使用`float`运算符。 在此示例中，您除以`1.0<degC>`的参数`printf`因为`printf`需要纲数量。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6902.fs)]

下面的示例会话显示的输出和此代码的输入。

```
Enter a temperature in degrees Fahrenheit.
90
That temperature in degrees Celsius is    32.22.
```

## <a name="using-generic-units"></a>使用泛型单位

对具有关联的单元的度量值的数据，可以编写运行的泛型函数。 您为此，指定一个类型与泛型单元一起作为一个类型参数，如下面的代码示例中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6903.fs)]

## <a name="creating-aggregate-types-with-generic-units"></a>使用泛型单位创建聚合类型

下面的代码演示如何创建单个浮动点具有的值都是泛型方法的单元组成的聚合类型。 这使单个类型来创建适用于各种单位。 此外，泛型单位可以通过确保泛型类型具有一组单元相同的泛型类型具有一组不同的单元与不同的类型保留类型安全。 此技术的基础是`Measure`特性可以应用于类型参数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6904.fs)]

## <a name="units-at-runtime"></a>在运行时的单位

度量单位用于静态类型检查。 浮点值编译时，将消除的度量单位，以便在运行时的单位是丢失。 因此，任何尝试实现取决于在运行时检查单元的功能是不可能。 例如，实现`ToString`函数来打印出单位不能。

## <a name="conversions"></a>转换

要转换具有单位的类型 (例如， `float<'u>`) 到一个没有单元的类型，可以使用标准的转换函数。 例如，可以使用`float`将转换为`float`不具有单元，如下面的代码中所示的值。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6905.fs)]

若要将无单位的值转换为具有单元的值，可以用适当的单位乘以 1 或 1.0 进行批注的值。 但是，为编写的互操作性层，也有一些可用于与单元将无单位值转换为值的显式函数。 这些对象位于[Microsoft.FSharp.Core.LanguagePrimitives](https://msdn.microsoft.com/library/69d08ac5-5d51-4c20-bf1e-850fd312ece3)模块。 例如，若要从无单位转换`float`到`float<cm>`，使用[FloatWithMeasure](https://msdn.microsoft.com/library/69520bc7-d67b-46b8-9004-7cac9646b8d9)，如下面的代码中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6906.fs)]

## <a name="units-of-measure-in-the-f-core-library"></a>中的度量单位F#核心库

单元库现已推出`FSharp.Data.UnitSystems.SI`命名空间。 它包括这两个符号形式的 SI 单位 (如`m`测定仪) 中`UnitSymbols`子命名空间和其完整名称 (如`meter`测定仪) 中`UnitNames`子命名空间。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)