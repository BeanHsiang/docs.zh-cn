---
title: 运算符重载
description: 了解如何重载算术运算符的类或记录类型中并在全局级别的F#。
ms.date: 05/16/2016
ms.openlocfilehash: c4b52b02522b750aa55ca6cf4097295e35ab1739
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610757"
---
# <a name="operator-overloading"></a>运算符重载

本主题介绍如何重载算术运算符在类或记录类型，并在全局级别。

## <a name="syntax"></a>语法

```fsharp
// Overloading an operator as a class or record member.
static member (operator-symbols) (parameter-list) =
    method-body
// Overloading an operator at the global level
let [inline] (operator-symbols) parameter-list = function-body
```

## <a name="remarks"></a>备注

在上述语法中，*运算符符号*是之一`+`， `-`， `*`， `/`， `=`，依次类推。 *参数列表*该运算符中的常用语法中显示的顺序指定操作数。 *方法主体*构造生成的值。

运算符重载的运算符必须是静态的。 运算符重载的一元运算符，如`+`并`-`，必须使用波形符 (`~`) 中*运算符符号*以指示运算符是一元运算符而不是二元运算符，如中所示下面的声明。

```fsharp
static member (~-) (v : Vector)
```

下面的代码演示一个仅包含两个运算符的矢量类，其中的一个运算符用于一元负运算，而另一个运算符用于标量乘法运算。 在示例中，因为无论矢量和标量出现的顺序必须适用运算符需要用于标量乘法的两个重载。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4001.fs)]

## <a name="creating-new-operators"></a>创建新的运算符

您可以重载所有标准运算符，但还可以创建新的运算符的某些字符序列。 允许的运算符字符是`!`， `%`， `&`， `*`， `+`， `-`， `.`， `/`， `<`， `=`， `>`， `?`， `@`， `^`， `|`，并`~`。 `~`字符具有特殊意义的一元运算符，并不是运算符字符序列的一部分。 并非所有运算符可以都进行一元。

具体取决于您使用的确切字符序列，您的运营商将具有特定优先级和结合性。 关联性到右还是从右到左可以既保留并出现在不带括号的序列中的相同级别的优先级的运算符时，将使用。

运算符字符`.`不会影响优先级，以便例如，如果你想要定义自己的具有相同的优先级和结合性作为普通乘法的乘法版本，您可以创建的运算符，如`.*`.

只有运算符`?`并`?<-`可能与启动`?`。

表中的所有运算符的优先顺序显示了F#中可以找到[符号和运算符参考](symbol-and-operator-reference/index.md)。

## <a name="overloaded-operator-names"></a>重载的运算符名称

当F#编译器将编译运算符表达式，它将生成具有该运算符将编译器生成的名称的方法。 这是在 Microsoft 中间语言 (MSIL) 的方法和反射和 IntelliSense 中显示的名称。 您不通常需要使用这些名称在F#代码。

下表显示了标准运算符和其相应的生成名称。

|运算符|生成的名称|
|--------|--------------|
|`[]`|`op_Nil`|
|`::`|`op_Cons`|
|`+`|`op_Addition`|
|`-`|`op_Subtraction`|
|`*`|`op_Multiply`|
|`/`|`op_Division`|
|`@`|`op_Append`|
|`^`|`op_Concatenate`|
|`%`|`op_Modulus`|
|`&&&`|`op_BitwiseAnd`|
|<code>&#124;&#124;&#124;</code>|`op_BitwiseOr`|
|`^^^`|`op_ExclusiveOr`|
|`<<<`|`op_LeftShift`|
|`~~~`|`op_LogicalNot`|
|`>>>`|`op_RightShift`|
|`~+`|`op_UnaryPlus`|
|`~-`|`op_UnaryNegation`|
|`=`|`op_Equality`|
|`<=`|`op_LessThanOrEqual`|
|`>=`|`op_GreaterThanOrEqual`|
|`<`|`op_LessThan`|
|`>`|`op_GreaterThan`|
|`?`|`op_Dynamic`|
|`?<-`|`op_DynamicAssignment`|
|<code>&#124;></code>|`op_PipeRight`|
|<code><&#124;</code>|`op_PipeLeft`|
|`!`|`op_Dereference`|
|`>>`|`op_ComposeRight`|
|`<<`|`op_ComposeLeft`|
|`<@ @>`|`op_Quotation`|
|`<@@ @@>`|`op_QuotationUntyped`|
|`+=`|`op_AdditionAssignment`|
|`-=`|`op_SubtractionAssignment`|
|`*=`|`op_MultiplyAssignment`|
|`/=`|`op_DivisionAssignment`|
|`..`|`op_Range`|
|`.. ..`|`op_RangeStep`|

其他此处未列出的运算符字符的组合可以用作运算符且具有通过串联下表中的每个字符的名称组成的名称。 例如，+ ！ 将成为`op_PlusBang`。

|运算符字符|name|
|------------------|----|
|`>`|`Greater`|
|`<`|`Less`|
|`+`|`Plus`|
|`-`|`Minus`|
|`*`|`Multiply`|
|`/`|`Divide`|
|`=`|`Equals`|
|`~`|`Twiddle`|
|`%`|`Percent`|
|`.`|`Dot`|
|`&`|`Amp`|
|<code>&#124;</code>|`Bar`|
|`@`|`At`|
|`^`|`Hat`|
|`!`|`Bang`|
|`?`|`Qmark`|
|`(`|`LParen`|
|`,`|`Comma`|
|`)`|`RParen`|
|`[`|`LBrack`|
|`]`|`RBrack`|

## <a name="prefix-and-infix-operators"></a>前缀和中缀运算符

*前缀*运算符应放置在一个或操作数，类似于函数前面。 *中缀*运算符应放置在两个操作数之间。

只有某些运算符可以用作前缀运算符。 一些运算符始终是前缀运算符，其他人可以为中缀或前缀，并且其余部分始终中缀运算符。 除了 `!` 之外，以 `!=` 开头的运算符以及运算符 `~` 或 `~` 的重复序列始终为前缀运算符。 运算符`+`， `-`， `+.`， `-.`， `&`， `&&`， `%`，和`%%`可以是前缀运算符或中缀运算符。 你通过添加从中缀版本区分这些运算符的前缀版本`~`前缀运算符定义它时开始处。 `~`时仅在定义它时使用运算符，不使用。

## <a name="example"></a>示例

下面的代码演示如何使用运算符重载来实现部分类型。 由分子和分母表示一小部分。 该函数`hcf`用于确定最高常见因素，它用于减少小数部分。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4002.fs)]

**输出：**

```
3/4 + 1/2 = 5/4
3/4 - 1/2 = 1/4
3/4 * 1/2 = 3/8
3/4 / 1/2 = 3/2
3/4 + 1 = 7/4
```

## <a name="operators-at-the-global-level"></a>在全局级别的运算符

此外可以定义在全局级别的运算符。 下面的代码定义一个运算符`+?`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4003.fs)]

上面的代码的输出是`12`。

因为的作用域的规则，您可以重新定义这种方式中的正则算术运算符F#指示新定义的运算符的优先于内置运算符。

关键字`inline`通常会与全局运算符，这通常是最好集成到调用代码的较小函数使用。 制定运算符函数内联还使他们能够使用静态解析的类型参数，以生成静态解析的泛型代码。 有关详细信息，请参阅[内联函数](functions/inline-functions.md)并[静态解析的类型参数](generics/statically-resolved-type-parameters.md)。

## <a name="see-also"></a>请参阅

- [成员](members/index.md)