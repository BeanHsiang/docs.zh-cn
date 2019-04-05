---
title: 匹配表达式
description: 了解如何F#匹配表达式提供的表达式与一组模式的比较结果为基础的分支控制。
ms.date: 04/19/2018
ms.openlocfilehash: 8972cc012d2746cb720eeed1acee403948941425
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53611563"
---
# <a name="match-expressions"></a>匹配表达式

`match`表达式提供的表达式与一组模式的比较结果为基础的分支控制。

## <a name="syntax"></a>语法

```fsharp
// Match expression.
match test-expression with
| pattern1 [ when condition ] -> result-expression1
| pattern2 [ when condition ] -> result-expression2
| ...

// Pattern matching function.
function
| pattern1 [ when condition ] -> result-expression1
| pattern2 [ when condition ] -> result-expression2
| ...
```

## <a name="remarks"></a>备注

模式匹配表达式允许基于与一组模式的测试表达式比较复杂的分支。 在中`match`表达式中，*测试表达式*中打开，并找到匹配项，相应与每个模式进行比较*结果表达式*计算和生成的值是返回与匹配表达式的值。

模式匹配上一个语法中所示的函数是在哪种模式匹配是立即对自变量执行一个 lambda 表达式。 等效于以下模式匹配函数，在上述语法中所示。

```fsharp
fun arg ->
    match arg with
    | pattern1 [ when condition ] -> result-expression1
    | pattern2 [ when condition ] -> result-expression2
    | ...
```

有关 lambda 表达式的详细信息，请参阅[Lambda 表达式：`fun`关键字](functions/lambda-expressions-the-fun-keyword.md)。

整个组模式应涵盖输入变量的所有可能的匹配项。 通常，您可以使用通配符模式 (`_`) 作为要匹配任何以前不匹配的输入的值的最后一个模式。

下面的代码演示了几种在其中`match`使用表达式。 引用和可用的所有可能模式的示例，请参阅[模式匹配](pattern-matching.md)。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4601.fs)]

## <a name="guards-on-patterns"></a>模式的先决条件

可以使用`when`子句来指定该变量必须满足与模式匹配的附加条件。 这样的子句被称为*防止*。 后面的表达式`when`除非与先决条件关联的模式进行匹配，则不会评估关键字。

下面的示例演示如何使用临界指定变量模式的数值范围。 请注意多个条件将结合使用布尔运算符。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4602.fs)]

请注意，由于不能在模式中使用文本之外的值，因此您必须使用`when`子句有部分输入与某个值进行比较。 以下代码所示：

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet4603.fs)]

请注意，当联合模式受防护，临界适用于**所有**的模式，而不仅仅是最后一个。 例如，给定以下代码，临界`when a > 12`同时适用于`A a`和`B a`:

```fsharp
type Union =
    | A of int
    | B of int

let foo() =
    let test = A 42
    match test with
    | A a
    | B a when a > 41 -> a // the guard applies to both patterns
    | _ -> 1

foo() // returns 42
```

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [活动模式](active-patterns.md)
- [模式匹配](pattern-matching.md)