---
title: Fixed 的关键字
description: 了解如何将 pin 到堆栈上的本地，以防止具有集合F#固定关键字。
ms.date: 04/24/2017
ms.openlocfilehash: 7fdf66560f3e2ab7584b00c7e4584d7f6c161858
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614324"
---
# <a name="the-fixed-keyword"></a>Fixed 的关键字

F#4.1 中引入了`fixed`关键字，以便您可以"固定"到堆栈上的本地，以防止其被收集或在垃圾回收期间移动。  它用于低级别的编程方案。

## <a name="syntax"></a>语法

```fsharp
use ptr = fixed expression
```

## <a name="remarks"></a>备注

这将扩展表达式，以允许提取一个指针，并将其绑定到会阻止正在收集或在垃圾回收期间移动名称的语法。  

通过固定的表达式中的指针`fixed`关键字将绑定到通过标识符`use`关键字。  此语义是类似于通过资源管理`use`关键字。  指针被固定在范围内，而超出范围后，它不再被固定。  `fixed` 不能使用上下文的外部`use`绑定。  必须为具有名称绑定指针`use`。

使用`fixed`必须在函数或方法中的表达式中执行。  它不能在脚本级别或模块级别范围内使用。

如所有指针代码，这是不安全的功能，将发出警告时使用。

## <a name="example"></a>示例

```fsharp
open Microsoft.FSharp.NativeInterop

type Point = { mutable X: int; mutable Y: int}

let squareWithPointer (p: nativeptr<int>) =
    // Dereference the pointer at the 0th address.
    let mutable value = NativePtr.get p 0

    // Perform some work
    value <- value * value

    // Set the value in the pointer at the 0th address.
    NativePtr.set p 0 value

let pnt = { X = 1; Y = 2 }
printfn "pnt before - X: %d Y: %d" pnt.X pnt.Y // prints 1 and 2

// Note that the use of 'fixed' is inside a function.
// You cannot fix a pointer at a script-level or module-level scope.
let doPointerWork() =
    use ptr = fixed &pnt.Y

    // Square the Y value
    squareWithPointer ptr
    printfn "pnt after - X: %d Y: %d" pnt.X pnt.Y // prints 1 and 4

doPointerWork()
```

## <a name="see-also"></a>请参阅

- [NativePtr 模块](https://msdn.microsoft.com/visualfsharpdocs/conceptual/nativeinterop.nativeptr-module-%5Bfsharp%5D)
