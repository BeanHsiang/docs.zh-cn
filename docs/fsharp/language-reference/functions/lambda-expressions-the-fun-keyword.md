---
title: Lambda 表达式：Fun 关键字
description: 了解如何使用F#增添些乐趣关键字来定义 lambda 表达式，这是一个匿名函数。
ms.date: 05/16/2016
ms.openlocfilehash: 6ad15173bb8643bff330e3ca3823cba5d43ad445
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614452"
---
# <a name="lambda-expressions-the-fun-keyword-f"></a>Lambda 表达式：Fun 关键字 (F#)

`fun`关键字用于定义 lambda 表达式，即匿名函数。

## <a name="syntax"></a>语法

```fsharp
fun parameter-list -> expression
```

## <a name="remarks"></a>备注

*参数列表*通常包含的名称和 （可选） 参数的类型。 一般来说，*参数列表*可以是组合的任何F#模式。 有关可能模式的完整列表，请参阅[模式匹配](../pattern-matching.md)。 有效参数列表包含下面的示例。

```fsharp
// Lambda expressions with parameter lists.
fun a b c -> ...
fun (a: int) b c -> ...
fun (a : int) (b : string) (c:float) -> ...

// A lambda expression with a tuple pattern.
fun (a, b) -> …

// A lambda expression with a list pattern.
fun head :: tail -> …
```

*表达式*是其中的最后一个表达式会生成一个返回值的函数的正文。 有效的 lambda 表达式的示例包括：

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet301.fs)]

## <a name="using-lambda-expressions"></a>使用 Lambda 表达式

当你想要在列表或其他集合上执行操作并想要避免额外的工作的定义函数时，lambda 表达式时特别有用。 许多F#库函数采用函数值作为参数，并可能会特别方便，可以在这些情况下使用 lambda 表达式。 下面的代码将 lambda 表达式应用于列表中的元素。 在这种情况下，匿名函数将 1 添加到列表中的每个元素。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet302.fs)]

## <a name="see-also"></a>请参阅

- [函数](index.md)