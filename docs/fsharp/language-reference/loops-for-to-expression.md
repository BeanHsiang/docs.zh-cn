---
title: 循环：for...to 表达式
description: 请参阅如何F#数据类型...为表达式用于在循环中循环访问一系列循环变量的值。
ms.date: 05/16/2016
ms.openlocfilehash: 041e98fa4bcc140aa3cd699f6ed35bf52c8b4175
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612317"
---
# <a name="loops-forto-expression"></a>循环：for...to 表达式

`for...to`表达式用于在循环中循环访问一系列循环变量的值。

## <a name="syntax"></a>语法

```fsharp
for identifier = start [ to | downto ] finish do
    body-expression
```

## <a name="remarks"></a>备注

标识符的类型推断的类型从*启动*并*完成*表达式。 这些表达式的类型必须是 32 位整数。

尽管从技术上讲一个表达式，但`for...to`更像是命令性编程语言中的传统语句。 返回类型*正文表达式*必须是`unit`。 下面的示例演示的各种用法`for...to`表达式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5101.fs)]

上述代码的输出结果如下。

```
1 2 3 4 5 6 7 8 9 10
10 9 8 7 6 5 4 3 2 1
2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18
```

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [循环：`for...in` 表达式](loops-for-in-expression.md)
- [循环：`while...do` 表达式](loops-while-do-expression.md)