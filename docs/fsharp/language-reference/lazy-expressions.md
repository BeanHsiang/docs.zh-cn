---
title: 延迟表达式
description: 了解如何F#延迟表达式可以提高性能的应用程序和库。
ms.date: 03/13/2019
ms.openlocfilehash: 6d53d53093f4e93f53e1c956b94e2f1e4a1bbd55
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57853319"
---
# <a name="lazy-expressions"></a>延迟表达式

*延迟表达式*是不会立即开始，但改为在需要结果时计算的表达式。 这可以帮助提高代码的性能。

## <a name="syntax"></a>语法

```fsharp
let identifier = lazy ( expression )
```

## <a name="remarks"></a>备注

在上述语法中，*表达式*是仅时结果是必需的将计算的代码并*标识符*是将结果存储的值。 值为类型[ `Lazy<'T>` ](https://msdn.microsoft.com/library/b29d0af5-6efb-4a55-a278-2662a4ecc489)，其中的实际类型用于`'T`根据表达式的结果。

延迟表达式，可以通过限制仅需要结果时这种情况下对表达式的执行，从而提高性能。

若要强制执行的表达式，则调用方法`Force`。 `Force` 将导致执行要执行仅一次。 对后续调用`Force`返回相同的结果，但不是执行任何代码。

下面的代码演示使用延迟表达式以及如何使用`Force`。 在此代码的类型`result`是`Lazy<int>`，并`Force`方法将返回`int`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet73011.fs)]

延迟计算，但不是`Lazy`类型，还可用于序列。 有关详细信息，请参阅[序列](sequences.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [LazyExtensions 模块](https://msdn.microsoft.com/library/86671f40-84a0-402a-867d-ae596218d948)
