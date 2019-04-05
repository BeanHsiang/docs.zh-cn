---
title: 断言
description: 了解如何使用 assert 表达式作为一种调试功能测试中的表达式F#编程语言。
ms.date: 05/16/2016
ms.openlocfilehash: c2d97386e87e9b915da490a78fff9aedb9def616
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610198"
---
# <a name="assertions"></a>断言

`assert`表达式是一个可用于测试表达式的调试功能。 在调试模式中遇到故障时，断言将生成一个系统错误对话框。

## <a name="syntax"></a>语法

```fsharp
assert condition
```

## <a name="remarks"></a>备注

`assert`表达式具有类型`bool -> unit`。

在上述语法中，*条件*表示是要测试的布尔表达式。 如果表达式计算结果为`true`，执行将继续不受影响。 如果其计算结果为`false`，则会生成系统的错误对话框。 错误对话框中已包含的字符串的标题**断言失败**。 对话框中包含指示出现了断言失败的堆栈跟踪。

在调试模式下; 编译时，才会启用断言检查也就是说，如果常量`DEBUG`定义。 在项目系统中，默认情况下，`DEBUG`常量在调试配置中而不是在发布配置定义。

不能通过使用捕获断言失败错误F#异常处理。

> [!NOTE]
> `assert`函数将解析为<xref:System.Diagnostics.Debug.Assert*?displayProperty=nameWithType>。

## <a name="example"></a>示例

下面的代码示例演示如何使用`assert`表达式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet5401.fs)]

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)