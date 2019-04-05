---
title: 命名空间
description: 了解如何F#命名空间，可将代码组织到相关的功能区域，通过它可以将名称附加到的程序元素分组。
ms.date: 12/08/2018
ms.openlocfilehash: 526d7a07e4804751811c15fa91b0c74c1954d591
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613435"
---
# <a name="namespaces"></a>命名空间

命名空间，可以将代码组织到相关的功能区域，通过它可以将名称附加一组F#的程序元素。 命名空间是在通常顶级元素F#文件。

## <a name="syntax"></a>语法

```fsharp
namespace [rec] [parent-namespaces.]identifier
```

## <a name="remarks"></a>备注

如果你想要将代码放入一个命名空间，文件中的第一个声明必须声明命名空间。 然后将整个文件的内容会成为该命名空间的一部分，提供任何其他命名空间声明不存在更多的文件中。 如果是这种情况，然后被视为下一步的命名空间声明之前的所有代码可在第一个命名空间中。

命名空间不能直接包含的值和函数。 相反，必须在模块中，包含值和函数以及模块包含命名空间中。 命名空间可以包含类型和模块。

XML 文档注释可以声明一个命名空间，上面，但它们将被忽略。 编译器指令还可以上述命名空间声明。

命名空间可以显式声明命名空间关键字，或隐式声明模块时。 若要显式声明命名空间，请使用命名空间关键字后跟的命名空间名称。 下面的示例演示声明一个命名空间的代码文件`Widgets`的类型和该命名空间中提供的模块。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6406.fs)]

如果该文件的全部内容都位于一个模块，还可以声明命名空间隐式使用`module`关键字并提供完全限定的模块名称中的新命名空间名称。 下面的示例演示一个文件，其中声明一个命名空间`Widgets`和模块`WidgetsModule`，其中包含一个函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6401.fs)]

下面的代码是等效于上述代码中，但该模块是一个本地模块声明。 在这种情况下，命名空间必须出现在各自的行。

[!code-fsharp[Main](../../../samples/snippets/fsharp/namespaces/snippet6402.fs)]

如果在同一文件中一个或多个命名空间中需要多个模块，则必须使用本地模块声明。 当使用本地模块声明时，不能在模块声明中使用的限定命名空间。 下面的代码显示了具有命名空间声明和两个本地模块声明的文件。 在这种情况下，这些模块直接包含在该命名空间。没有任何文件具有相同名称的隐式创建的模块。 任何其他代码在文件中，如`do`绑定，因此需要限定模块成员位于命名空间中但不是在的内部模块`widgetFunction`通过使用模块名称。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6403.fs)]

此示例的输出如下所示。

```fsharp
Module1 10 20
Module2 5 6
```

有关详细信息，请参阅[模块](modules.md)。

## <a name="nested-namespaces"></a>嵌套的命名空间

在创建嵌套的命名空间时，必须完全限定它。 否则，您创建新的顶级命名空间。 命名空间声明中将忽略缩进。

下面的示例演示如何声明嵌套的命名空间。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6404.fs)]

## <a name="namespaces-in-files-and-assemblies"></a>中的文件和程序集的命名空间

命名空间可以跨多个文件中的单个项目或编译。 术语*命名空间片段*介绍包含在一个文件中的命名空间的一部分。 命名空间还可以跨多个程序集。 例如，`System`命名空间中包含整个.NET Framework，也不能跨越多个程序集包含多个嵌套的命名空间。

## <a name="global-namespace"></a>全局 Namespace

使用预定义的命名空间`global`将名称放在.NET 顶级命名空间。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6407.fs)]

您还可以使用全局若要引用的顶级的.NET 命名空间，例如，若要解决与其他命名空间的名称冲突。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet6408.fs)]

## <a name="recursive-namespaces"></a>递归命名空间

此外可以为递归，从而允许所有包含的代码要相互递归声明命名空间。  这是通过`namespace rec`。 使用`namespace rec`可以缓解一些烦恼无法编写类型和模块之间相互引用代码中的。 以下是此示例：

```fsharp
namespace rec MutualReferences

type Orientation = Up | Down
type PeelState = Peeled | Unpeeled

// This exception depends on the type below.
exception DontSqueezeTheBananaException of Banana

type BananaPeel() = class end

type Banana(orientation : Orientation) =
    member val IsPeeled = false with get, set
    member val Orientation = orientation with get, set
    member val Sides: PeelState list = [ Unpeeled; Unpeeled; Unpeeled; Unpeeled] with get, set

    member self.Peel() = BananaHelpers.peel self // Note the dependency on the BananaHelpers module.
    member self.SqueezeJuiceOut() = raise (DontSqueezeTheBananaException self) // This member depends on the exception above.

module BananaHelpers =
    let peel (b: Banana) =
        let flip (banana: Banana) =
            match banana.Orientation with
            | Up -> 
                banana.Orientation <- Down
                banana
            | Down -> banana

        let peelSides (banana: Banana) =
            banana.Sides
            |> List.map (function
                         | Unpeeled -> Peeled
                         | Peeled -> Peeled)

        match b.Orientation with
        | Up ->   b |> flip |> peelSides
        | Down -> b |> peelSides
```

请注意，异常`DontSqueezeTheBananaException`和类`Banana`两者相互引用。  此外，模块`BananaHelpers`和类`Banana`也相互引用。 这不是可能表示F#如果你删除`rec`关键字从`MutualReferences`命名空间。

此功能也仅适用于顶级[模块](modules.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [模块](modules.md)
- [F#RFC FS-1009-允许通过在文件中的较大范围的相互引用类型和模块](https://github.com/fsharp/fslang-design/blob/master/FSharp-4.1/FS-1009-mutually-referential-types-and-modules-single-scope.md)