---
title: 模块
description: 了解如何F#模块是一组F#中的代码，例如值、 类型和函数值，F#程序。
ms.date: 04/24/2017
ms.openlocfilehash: 9e5bef4ffe3301a69bbe32483625652d988f8a35
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53611108"
---
# <a name="modules"></a>模块

在上下文中的F#语言中，*模块*是一组F#中的代码，例如值、 类型和函数值，F#程序。 对模块中的代码进行分组有助于将相关代码放在一起，并有助于避免程序中的名称冲突。

## <a name="syntax"></a>语法

```fsharp
// Top-level module declaration.
module [accessibility-modifier] [qualified-namespace.]module-name
declarations
// Local module declaration.
module [accessibility-modifier] module-name =
    declarations
```

## <a name="remarks"></a>备注

F#模块是一组F#的代码如类型、 值、 函数值和中的代码构造`do`绑定。 它只包含静态成员的公共语言运行时 (CLR) 类作为实现。 有两种类型的模块声明，具体取决于该模块中是否包含整个文件： 顶级模块声明和本地模块声明。 顶级模块声明模块中包括整个文件。 顶级模块声明可以显示仅为一个文件中的第一个声明。

在顶级模块声明，可选的语法*限定命名空间*是包含该模块的嵌套命名空间名称的序列。 限定命名空间不需要声明过。

无需缩进顶级模块中的声明。 您无需缩进本地模块中的所有声明。 在本地模块声明中，仅在该模块声明下缩进的声明是模块的一部分。

如果代码文件开头不为顶级模块声明或命名空间声明，作为该文件，而无需扩展，具有相同名称的隐式创建的顶级模块的一部分的文件，包括任何本地模块的全部内容与第一个字母转换为大写。 例如，考虑下面的文件。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6601.fs)]

此文件将进行编译，因为如果以这种方式编写：

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6602.fs)]

如果在文件中有多个模块，则必须为每个模块使用本地模块声明。 如果封闭命名空间声明，这些模块是封闭命名空间的一部分。 如果未声明的封闭命名空间，模块将成为隐式创建顶级模块的一部分。 下面的代码示例显示了包含多个模块的代码文件。 编译器隐式创建一个名为顶级模块`Multiplemodules`，并`MyModule1`和`MyModule2`嵌套在顶级的该模块中。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6603.fs)]

如果有多个文件在项目中或在单个编译时，或者如果要构建一个库，则必须包含命名空间声明或在文件顶部的模块声明。 F#编译器仅确定模块名称隐式时在项目或编译命令行中，只有一个文件且要创建应用程序。

*可访问性修饰符*可以是以下之一： `public`， `private`， `internal`。 有关详细信息，请参阅[访问控制](access-control.md)。 默认值为 public。

## <a name="referencing-code-in-modules"></a>引用的模块中的代码

在从另一个模块引用的函数、 类型和值时，必须使用限定的名称或打开模块。 如果使用限定的名称，必须指定命名空间、 模块和所需的程序元素的标识符。 按如下所示带有圆点 （.） 分隔每个部分的限定的路径。

`Namespace1.Namespace2.ModuleName.Identifier`

您可以打开该模块或一个或多个命名空间来简化代码。 有关打开命名空间和模块的详细信息，请参阅[导入声明：`open`关键字](import-declarations-the-open-keyword.md)。

下面的代码示例显示了顶级模块包含到文件末尾的所有代码。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6604.fs)]

若要从另一个文件，同一项目中使用此代码，可以使用限定的名称或打开该模块，然后使用函数，如以下示例所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6605.fs)]

## <a name="nested-modules"></a>嵌套的模块

可以嵌套模块。 内部模块必须于外部模块声明，以指示它们是内部模块，而不是新模块缩进。 例如，比较以下两个示例。 模块`Z`是一个内部模块，在下面的代码。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6607.fs)]

但模块`Z`是模块的同级`Y`在下面的代码。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6608.fs)]
模块`Z`也是下面的代码中的同级模块，因为它不会就模块中的其他声明缩进`Y`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6609.fs)]
最后，如果外部模块不包含任何声明，并且后面紧跟另一个模块声明，新的模块声明被假定为一个内部模块，但编译器会警告你如果第二个模块定义不会缩进贯彻比第一个。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6610.fs)]
若要消除此警告，缩进内部模块。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6611.fs)]
如果你想要在单个外部模块中的文件中的所有代码，您都需要使用内部模块外部模块不需要等号，并声明，包括任何内部模块声明，在外部模块中经历的无需将缩进。 内部模块声明中的声明无需进行缩进。 下面的代码演示此用例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/modules/snippet6612.fs)]

## <a name="recursive-modules"></a>递归模块

F#4.1 中引入了允许的所有包含的代码要相互递归的模块的概念。  这是通过`module rec`。  使用`module rec`可以缓解一些烦恼无法编写类型和模块之间相互引用代码中的。  以下是此示例：

```fsharp
module rec RecursiveModule =
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

请注意，异常`DontSqueezeTheBananaException`和类`Banana`两者相互引用。  此外，模块`BananaHelpers`和类`Banana`也相互引用。  这就不可能在 expressF#如果你删除`rec`关键字从`RecursiveModule`模块。

此功能，还可以在[命名空间](namespaces.md)与F#4.1。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [命名空间](namespaces.md)
- [F#RFC FS-1009-允许通过在文件中的较大范围的相互引用类型和模块](https://github.com/fsharp/fslang-design/blob/master/FSharp-4.1/FS-1009-mutually-referential-types-and-modules-single-scope.md)