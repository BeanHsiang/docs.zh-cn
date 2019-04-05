---
title: 入口点
description: 了解如何将入口点设置为F#编译为可执行文件，正式开始执行的位置的程序。
ms.date: 05/16/2016
ms.openlocfilehash: 915ab17b9a4fc7fd4d0ae344cb273b1d348a02f1
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614335"
---
# <a name="entry-point"></a>入口点

本主题介绍的方法，用于将入口点设置为F#程序。

## <a name="syntax"></a>语法

```fsharp
[<EntryPoint>]
let-function-binding
```

## <a name="remarks"></a>备注

在上述语法中， *let 函数绑定*是中的函数的定义`let`绑定。

可执行文件正式开始执行时编译的程序入口点。 指定的入口点F#应用程序通过应用`EntryPoint`属性为该程序的`main`函数。 此函数 (使用创建的`let`绑定) 必须是最后一个已编译文件中的最后一个函数。 最后一个已编译的文件是项目中的最后一个文件或传递给命令行的最后一个文件。

入口点函数具有类型`string array -> int`。 在命令行上提供的参数传递给`main`字符串数组中的函数。 数组的第一个元素是第一个参数;可执行文件的名称不包含在数组中，因为它是其他一些语言中。 返回的值用作进程退出代码。 零通常指示成功;非零值指示错误。 特定含义的非零返回代码; 没有约定返回代码的含义是特定于应用程序。

下面的示例演示一个简单`main`函数。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/entry-point/snippet501.fs)]

使用命令行执行此代码时`EntryPoint.exe 1 2 3`，输出如下所示。

```console
Arguments passed to function : [|"1"; "2"; "3"|]
```

## <a name="implicit-entry-point"></a>隐式入口点

程序没有**入口点**显式指示的入口点，最后一个文件中的最高级别绑定，要编译的属性用作入口点。

## <a name="see-also"></a>请参阅

- [函数](index.md)
- [let 绑定](let-bindings.md)