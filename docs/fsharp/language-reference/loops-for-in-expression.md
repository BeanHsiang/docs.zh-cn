---
title: 循环：for...in 表达式
description: 请参阅如何F#数据类型...在表达式中循环构造用于循环访问的可枚举集合中的模式匹配。
ms.date: 05/16/2016
ms.openlocfilehash: adaf448a49cf53c63c41f9156d40ee5d1ad3caeb
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614398"
---
# <a name="loops-forin-expression"></a>循环：for...in 表达式

此循环构造用于循环访问的可枚举集合，如范围表达式、 序列、 列表、 数组或支持枚举的其他构造中的模式匹配。

## <a name="syntax"></a>语法

```fsharp
for pattern in enumerable-expression do
    body-expression
```

## <a name="remarks"></a>备注

`for...in`表达式可以比作`for each`其他.NET 语言中的语句因为它用于循环访问的可枚举集合中的值。 但是，`for...in`还支持模式匹配集合，而不仅仅是迭代不通过对整个集合。

可以指定的可枚举的表达式，作为可枚举集合，或通过使用`..`运算符，为上一种整型类型的范围。 可枚举集合包括列表、 序列、 数组、 集、 映射和等等。 实现的任何类型`System.Collections.IEnumerable`可用。

当使用表示范围`..`运算符，可以使用以下语法。

*启动*... *完成*

此外可以使用一种包括名为增量*跳过*，如下面的代码。

*启动*... *跳过*... *完成*

时使用整数范围和简单的计数器变量作为一种模式，典型的行为是计数器变量递增 1 上的每个迭代，但如果该范围包含跳过值，此计数器递增的 skip 值改为。

在模式匹配的值还可在正文的表达式。

下面的代码示例说明如何使用`for...in`表达式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5201.fs)]

输出如下所示。

```
1
5
100
450
788
```

下面的示例演示如何循环访问序列，以及如何使用元组模式而不是简单的变量。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5202.fs)]

输出如下所示。

```
1 squared is 1
2 squared is 4
3 squared is 9
4 squared is 16
5 squared is 25
6 squared is 36
7 squared is 49
8 squared is 64
9 squared is 81
10 squared is 100
```

下面的示例演示如何在简单的整数范围内循环。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5203.fs)]

Function1 的输出如下所示。

```
1 2 3 4 5 6 7 8 9 10
```

下面的示例演示如何循环访问一系列具有 skip 值为 2，其中包括每个其他元素的范围。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5204.fs)]

输出`function2`如下所示。

```
1 3 5 7 9
```

下面的示例演示如何使用字符范围。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5205.fs)]

输出`function3`如下所示。

```
a b c d e f g h i j k l m n o p q r s t u v w x y z
```

下面的示例演示如何使用反向迭代负的 skip 值。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5208.fs)]

输出`function4`如下所示。

```
10 9 8 7 6 5 4 3 2 1 ... Lift off!
```

开始和结束范围也可以是表达式，如函数，如以下代码所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5206.fs)]

输出`function5`与此输入如下所示。

```
2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18
```

下一个示例演示如何使用通配符字符 (\_) 元素在循环中的不需要时。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5207.fs)]

输出如下所示。

```
Number of elements in list1: 5
```

`Note` 可以使用`for...in`在序列表达式和其他计算表达式，这种情况下的自定义的版本`for...in`使用表达式。 有关详细信息，请参阅[序列](sequences.md)，[异步工作流](asynchronous-workflows.md)，并[计算表达式](computation-expressions.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [循环：`for...to` 表达式](loops-for-to-expression.md)
- [循环：`while...do` 表达式](loops-while-do-expression.md)