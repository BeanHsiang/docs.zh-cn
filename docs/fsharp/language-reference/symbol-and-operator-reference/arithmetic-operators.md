---
title: 算术运算符
description: 了解有关中可用的算术运算符F#编程语言。
ms.date: 04/04/2018
ms.openlocfilehash: 826f334125a542855bf2fda43465618403d49d4c
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614579"
---
# <a name="arithmetic-operators"></a>算术运算符

本主题介绍中可用的算术运算符F#语言。

## <a name="summary-of-binary-arithmetic-operators"></a>二进制算术运算符的摘要

下表总结了可用于未装箱的整型和浮点类型的二进制算术运算符。

|二元运算符|备注|
|---------------|-----|
|`+` (此外，加上)|未选中状态。 数字加在一起时的可能的溢出条件和的总和超出了类型支持的最大绝对值。|
|`-` (减法、 减号)|未选中状态。 可能的下溢条件时减去无符号的类型，或太小，无法由类型表示浮点值时。|
|`*` (乘号）|未选中状态。 可能的溢出条件时两个数相乘的积超过类型支持的最大绝对值。|
|`/` （除号）|除数为零的原因<xref:System.DivideByZeroException>对于整型类型。 对于浮点类型，被零除为您提供了特殊的浮点值`+Infinity`或`-Infinity`。 太小，无法由类型表示的浮点数时，也是有可能的下溢条件。|
|`%` （剩余部分、 rem）|返回除法运算的余数。 结果的符号是第一个操作数的符号相同。|
|`**` （幂的运算求幂）|可能的溢出条件时结果超出了最大绝对值的类型。<br /><br />求幂运算符仅适用于浮点类型。|

## <a name="summary-of-unary-arithmetic-operators"></a>一元算术运算符的摘要

下表总结了可用于整型和浮点类型的一元算术运算符。

|一元运算符|说明|
|--------------|-----|
|`+` （正）|可以应用于任何算术表达式。 不会更改值的符号。|
|`-` （求反，负）|可以应用于任何算术表达式。 更改值的符号。|

在溢出或下溢的整型类型的行为是环绕在周围。 这将导致不正确的结果。 整数溢出是潜在的严重问题，可能会导致安全问题时软件不编写要为其帐户。 如果这是你的应用程序的一个问题，请考虑使用中的选中的运算符`Microsoft.FSharp.Core.Operators.Checked`。

## <a name="summary-of-binary-comparison-operators"></a>二进制比较运算符的摘要

下表显示了适用于整型和浮点类型的二进制比较运算符。 这些运算符的返回值类型`bool`。

浮点数应永远不会直接比较相等，因为 IEEE 浮点表示形式不支持完全相等运算。 可以轻松验证通过检查的代码是相等的两个数字实际上可能具有不同的位表示形式。

|运算符|说明|
|--------|-----|
|`=` （等于）|这不是赋值运算符。 它仅用于比较。 这是泛型的运算符。|
|`>` （大于）|这是泛型的运算符。|
|`<` （小于）|这是泛型的运算符。|
|`>=` (大于或等于)|这是泛型的运算符。|
|`<=` (小于或等于)|这是泛型的运算符。|
|`<>` （不等于）|这是泛型的运算符。|

## <a name="overloaded-and-generic-operators"></a>运算符重载和一般运算符

本主题中讨论的运算符的所有中定义**Microsoft.FSharp.Core.Operators**命名空间。 某些运算符使用的静态解析的类型参数定义。 这意味着每个适用于该运算符的特定类型的单个定义。 属于此类别的所有一元和二元算术和按位运算符。 比较运算符都是泛型方法，并且因此能够使用任何类型，不只是基元算术类型。 可区分的联合和记录类型具有其自己的自定义实现生成的F#编译器。 类类型，可使用该方法<xref:System.Object.Equals%2A>。

泛型运算符都是可自定义。 若要自定义比较函数，请重写<xref:System.Object.Equals%2A>若要提供您自己的自定义的相等性比较，并实现<xref:System.IComparable>。 <xref:System.IComparable?displayProperty=nameWithType>接口有一个单一的方法，<xref:System.IComparable.CompareTo%2A>方法。

## <a name="operators-and-type-inference"></a>运算符和类型推理

在表达式中运算符的用法约束上该运算符的类型推理。 此外，运算符的使用可防止自动泛化，因为使用运算符表示算术类型。 如果没有任何其他信息，F#编译器将推断`int`作为算术表达式的类型。 通过指定另一种类型，可以重写此行为。 因此参数类型和返回类型`function1`下面的代码中被推断为`int`，但为类型`function2`被推断为`float`。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3501.fs)]

## <a name="see-also"></a>请参阅

- [符号和运算符参考](index.md)
- [运算符重载](../operator-overloading.md)
- [位运算符](bitwise-operators.md)
- [布尔运算符](boolean-operators.md)