---
title: 异常:try...with 表达式
description: 了解如何使用F#的 try...使用异常处理的表达式。
ms.date: 05/16/2016
ms.openlocfilehash: 742e0b595525c69b83a55682c3c8b9b650326ac7
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614423"
---
# <a name="exceptions-the-trywith-expression"></a>异常:try...with 表达式

本主题介绍`try...with`表达式，用于中的异常处理表达式F#语言。

## <a name="syntax"></a>语法

```fsharp
try
    expression1
with
| pattern1 -> expression2
| pattern2 -> expression3
...
```

## <a name="remarks"></a>备注

`try...with`表达式用于在中处理异常F#。 它相当于`try...catch`C# 中的语句。 在上述语法中的代码*expression1*可能会生成异常。 `try...with`表达式将返回一个值。 如果不引发任何异常，则整个表达式返回的值*expression1*。 如果引发异常，每个*模式*异常，以及相应的第一个匹配模式的反过来相比*表达式*，称为*异常处理程序*，则执行该分支，并总体表达式该异常处理程序中返回的表达式的值。 如果没有模式匹配，该异常将传播到调用堆栈，直到找到匹配的处理程序。 从异常处理程序中的每个表达式返回的值的类型必须匹配从中的表达式返回的类型`try`块。

通常情况下，还发生了错误的事实意味着没有有效的值可以返回的每个异常处理程序中的表达式。 常见模式是表达式的将是表达式的选项类型类型。 下面的代码示例说明了此模式。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5601.fs)]

异常可以是.NET 异常，也可以是F#异常。 您可以定义F#通过使用异常`exception`关键字。

可以使用各种模式要筛选的异常类型和其他条件;下表总结了选项。

|模式|描述|
|-------|-----------|
|:? *异常类型*|与指定的.NET 异常类型匹配。|
|:? *异常类型*作为*标识符*|匹配指定的.NET 异常类型，但为异常提供了一个命名的值。|
|*异常名称*(*自变量*)|匹配F#异常类型和绑定参数。|
|*identifier*|匹配任何异常并将名称绑定到的异常对象。 等效于 **:？作为 System.Exception**_标识符_|
|*标识符*时*条件*|如果条件为 true，则匹配的任何异常。|

## <a name="examples"></a>示例

下面的代码示例演示了使用各种异常处理程序模式。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5602.fs)]

> [!NOTE]
> `try...with`构造是从单独的表达式`try...finally`表达式。 因此，如果你的代码需要两`with`块和一个`finally`块中，必须将嵌套两个表达式。

> [!NOTE]
> 可以使用`try...with`在异步工作流和其他计算表达式，在这种情况下自定义的版本的`try...with`使用表达式。 有关详细信息，请参阅[异步工作流](../asynchronous-workflows.md)，并[计算表达式](../computation-expressions.md)。

## <a name="see-also"></a>请参阅

- [异常处理](index.md)
- [异常类型](exception-types.md)
- [异常：`try...finally`表达式](the-try-finally-expression.md)