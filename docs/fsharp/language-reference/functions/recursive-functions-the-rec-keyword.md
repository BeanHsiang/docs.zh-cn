---
title: 递归函数：Rec 关键字
description: 了解如何F#rec 关键字用于与 let 关键字定义的递归函数。
ms.date: 05/16/2016
ms.openlocfilehash: 9f9c7e1a4468de9551b3852d0e7b4381025b2699
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612902"
---
# <a name="recursive-functions-the-rec-keyword"></a>递归函数：Rec 关键字

`rec`一起使用关键字`let`关键字来定义的递归函数。

## <a name="syntax"></a>语法

```fsharp
// Recursive function:
let rec function-nameparameter-list =
function-body

// Mutually recursive functions:
let rec function1-nameparameter-list =
function1-body
and function2-nameparameter-list =
function2-body
...
```

## <a name="remarks"></a>备注

递归函数，调用本身，这些函数中显式标识F#语言。 这使正在定义的标识符可在函数的作用域中。

以下代码演示了递归函数，用于计算*n*<sup>th</sup>斐波纳契数。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet4001.fs)]

> [!NOTE]
> 在实践中，上面这类代码是一种浪费的内存和处理器时间，因为它涉及的以前计算的值重新计算。

方法是隐式类型; 中递归无需添加`rec`关键字。 类中的 let 的绑定不是隐式递归。

## <a name="mutually-recursive-functions"></a>相互递归函数

函数是有时*相互递归*，这意味着调用形成了循环，其中一个函数调用另一个后者又调用第一个具有任意数量的调用之间。 您必须在一个一起定义此类函数`let`使用的绑定`and`关键字来将它们链接在一起。

下面的示例演示两个相互递归函数。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet4002.fs)]

## <a name="see-also"></a>请参阅

- [函数](index.md)