---
title: 数组
description: 了解如何创建和使用中的数组F#编程语言。
ms.date: 05/16/2016
ms.openlocfilehash: 9670f2a61ed5c254493806501120552be9caecdf
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53614553"
---
# <a name="arrays"></a>数组

> [!NOTE]
> API 参考链接将转至 MSDN。  Docs.microsoft.com API 参考尚未完成。

数组是连续数据元素的所有相同类型的固定大小、 从零开始的可变集合。

## <a name="creating-arrays"></a>创建数组

可以多种方式来创建数组。 可以通过列出之间的连续值来创建小型数组`[|`和`|]`用分号分隔，如以下示例所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet1.fs)]

此外可以将每个元素放置在单独的行，在其中是可选的用例的分号分隔符。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet2.fs)]

数组元素的类型推断出使用的文本，并且必须一致。 下面的代码导致错误，因为 1.0 是一个浮点数和 2 和 3 都是整数。

```fsharp
// Causes an error.
// let array2 = [| 1.0; 2; 3 |]
```

序列表达式还可用于创建数组。 下面是一个示例，创建从 1 到 10 的整数的平方值的数组。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet3.fs)]

若要创建一个数组，其中所有元素都初始化为零，请使用`Array.zeroCreate`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet4.fs)]

## <a name="accessing-elements"></a>访问元素

可以通过使用点运算符访问数组元素 (`.`) 和方括号 (`[`和`]`)。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet5.fs)]

数组索引从 0 开始。

此外可以使用切片表示法，可用于指定子数组的范围来访问数组元素。 下面是示例切片表示法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet51.fs)]

使用切片表示法时，创建数组的新副本。

## <a name="array-types-and-modules"></a>数组类型和模块

所有的类型F#数组是.NET Framework 类型<xref:System.Array?displayProperty=nameWithType>。 因此，F#数组支持中提供的所有功能<xref:System.Array?displayProperty=nameWithType>。

库模块[ `Microsoft.FSharp.Collections.Array` ](https://msdn.microsoft.com/library/0cda8040-9396-40dd-8dcd-cf48542165a1)支持对一维数组的操作。 模块`Array2D`， `Array3D`，和`Array4D`包含分别支持针对数组的两个、 三种类型和四个维度的操作的函数。 创建数组的秩大于四使用<xref:System.Array?displayProperty=nameWithType>。

### <a name="simple-functions"></a>简单的函数

[`Array.get`](https://msdn.microsoft.com/library/dd93e85d-7e80-4d76-8de0-b6d45bcf07bc) 获取一个元素。 [`Array.length`](https://msdn.microsoft.com/library/0d775b6a-4a8f-4bd1-83e5-843b3251725f) 提供了数组的长度。 [`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790) 将元素设置为指定的值。 下面的代码示例演示如何使用这些函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet9.fs)]

输出如下所示。

```
0 1 2 3 4 5 6 7 8 9
```

### <a name="functions-that-create-arrays"></a>创建数组的函数

多个函数创建而无需现有数组的数组。 [`Array.empty`](https://msdn.microsoft.com/library/c3694b92-1c16-4c54-9bf2-fe398fadce32) 创建不包含任何元素的新数组。 [`Array.create`](https://msdn.microsoft.com/library/e848c8d6-1142-4080-9727-8dacc26066be) 创建指定大小的数组，并将所有元素都设置为提供的值。 [`Array.init`](https://msdn.microsoft.com/library/ee898089-63b0-40aa-910c-5ae7e32f6665) 创建一个数组，给定一个维度和用于生成元素的函数。 [`Array.zeroCreate`](https://msdn.microsoft.com/library/fa5b8e7a-1b5b-411c-8622-b58d7a14d3b2) 创建在其中所有元素将都初始化为数组的类型的零个值的数组。 下面的代码演示了这些函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet91.fs)]

输出如下所示。

```
Length of empty array: 0
Area of floats set to 5.0: [|5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0; 5.0|]
Array of squares: [|0; 1; 4; 9; 16; 25; 36; 49; 64; 81|]
```

[`Array.copy`](https://msdn.microsoft.com/library/9d0202f1-1ea0-475e-9d66-4f8ccc3c5b5f) 创建一个新数组，其中包含从现有数组复制的元素。 请注意，该副本是浅表副本，这意味着如果元素类型是引用类型，则复制仅引用，不是基础对象。 下面的代码示例阐释了这一点。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet11.fs)]

上述代码的输出如下所示：

```
[|Test1; Test2; |]
[|; Test2; |]
```

将字符串`Test1`仅在第一个数组中出现，因为创建新元素的操作将覆盖在引用`firstArray`但不会影响中仍存在一个空字符串的原始引用`secondArray`。 字符串`Test2`出现在这两个数组中，因为`Insert`上的操作<xref:System.Text.StringBuilder?displayProperty=nameWithType>类型会影响基础<xref:System.Text.StringBuilder?displayProperty=nameWithType>对象，在这两个数组中引用该对象。

[`Array.sub`](https://msdn.microsoft.com/library/40fb12ba-41d7-4ef0-b33a-56727deeef9d) 从数组的子范围生成新数组。 提供的起始索引和长度的指定子范围。 以下代码演示了 `Array.sub` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet12.fs)]

该输出显示子数组从元素 5 开始，并且包含 10 个元素。

```
[|5; 6; 7; 8; 9; 10; 11; 12; 13; 14|]
```
[`Array.append`](https://msdn.microsoft.com/library/08836310-5036-4474-b9a2-2c73e2293911) 通过组合两个现有数组来创建一个新数组。

下面的代码演示**Array.append**。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet13.fs)]

上述代码的输出如下所示。

```
[|1; 2; 3; 4; 5; 6|]
```

[`Array.choose`](https://msdn.microsoft.com/library/f5c8a5e2-637f-44d4-b35c-be96a6618b09) 选择要包含在一个新数组中的数组的元素。 下面的代码演示`Array.choose`。 请注意，该数组的元素类型不必与选项类型中返回的值的类型匹配。 在此示例中，元素类型是`int`且选项为多项式函数的结果`elem*elem - 1`，一个浮点数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet14.fs)]

上述代码的输出如下所示。

```
[|3.0; 15.0; 35.0; 63.0; 99.0|]
```

[`Array.collect`](https://msdn.microsoft.com/library/c3b60c3b-9455-48c9-bc2b-e88f0434342a) 对现有数组的每个数组元素运行指定的函数收集函数生成的元素并将它们合并到新数组。 下面的代码演示`Array.collect`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet15.fs)]

上述代码的输出如下所示。

```
[|0; 1; 0; 1; 2; 3; 4; 5; 0; 1; 2; 3; 4; 5; 6; 7; 8; 9; 10|]
```

[`Array.concat`](https://msdn.microsoft.com/library/f7219b79-1ec8-4a25-96b1-edbedb358302) 采用一系列数组并将它们合并到单个数组。 下面的代码演示`Array.concat`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet16.fs)]

上述代码的输出如下所示。

```
[|(1, 1, 1); (1, 2, 2); (1, 3, 3); (2, 1, 2); (2, 2, 4); (2, 3, 6); (3, 1, 3);
(3, 2, 6); (3, 3, 9)|]
```

[`Array.filter`](https://msdn.microsoft.com/library/b885b214-47fc-4639-9664-b8c183a39ede) 使用布尔条件函数并生成只包含这些元素从输入条件为 true 的数组的新数组。 下面的代码演示`Array.filter`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet17.fs)]

上述代码的输出如下所示。

```
[|2; 4; 6; 8; 10|]
```

[`Array.rev`](https://msdn.microsoft.com/library/1bbf822c-763b-4794-af21-97d2e48ef709) 通过颠倒现有数组的顺序生成一个新数组。 下面的代码演示`Array.rev`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet18.fs)]  

上述代码的输出如下所示。

```
"Hello world!"
```

您可以方便地组合数组模块中的函数，用于转换数组，通过使用管道运算符 (`|>`)，如以下示例所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet19.fs)]

输出为

```
[|100; 36; 16; 4|]
```

### <a name="multidimensional-arrays"></a>多维数组

可以创建多维数组，但没有用于编写多维数组文本语法。 使用运算符[ `array2D` ](https://msdn.microsoft.com/library/1d52503d-2990-49fc-8fd3-6b0e508aa236)从一系列数组元素的序列创建数组。 这些序列可以是数组或列表文本。 例如，以下代码创建一个二维数组。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet20.fs)]

此外可以使用函数[ `Array2D.init` ](https://msdn.microsoft.com/library/9de07e95-bc21-4927-b5b4-08fdec882c7b)来初始化数组的两个维度和类似函数是可用于三个和四个维度的数组。 这些函数采用一个用于创建元素的函数。 若要创建一个二维数组，其中包含元素设置为初始值而不是指定一个函数，请使用[ `Array2D.create` ](https://msdn.microsoft.com/library/36c9d980-b241-4a20-bc64-bcfa0205d804)函数，这也是可用于数组最多四个维度。 下面的代码示例首先演示如何创建包含所需的元素的数组的数组，然后使用`Array2D.init`生成所需的二维数组。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet21.fs)]

最多级别 4 的数组支持数组索引和切片语法。 当多个维度中指定索引时，则使用逗号分隔索引，如下面的代码示例中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet22.fs)]

二维数组的类型编写方式为`<type>[,]`(例如， `int[,]`， `double[,]`)，和三维数组的类型被写为`<type>[,,]`，等有关的更高维数的数组。

可用于一维数组的函数的一个子集也是可用于多维数组。 有关详细信息，请参阅[ `Collections.Array Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array-module-%5bfsharp%5d)， [ `Collections.Array2D Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array2d-module-%5bfsharp%5d)， [ `Collections.Array3D Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array3d-module-%5bfsharp%5d)，并[ `Collections.Array4D Module` ](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.array4d-module-%5bfsharp%5d)。

### <a name="array-slicing-and-multidimensional-arrays"></a>数组切片和多维数组

在二维数组 （矩阵） 中，你可以通过指定范围并使用通配符提取子矩阵 (`*`) 字符指定整行或列。

```fsharp
/ Get rows 1 to N from an NxM matrix (returns a matrix):
matrix.[1.., *]

// Get rows 1 to 3 from a matrix (returns a matrix):
matrix.[1..3, *]

// Get columns 1 to 3 from a matrix (returns a matrix):
matrix.[*, 1..3]

// Get a 3x3 submatrix:
matrix.[1..3, 1..3]
```

在F#3.1 中，可以将多维数组分解为相同或更低维度的子数组。 例如，可以通过指定的单个行或列从矩阵获得一个向量。

```fsharp
// Get row 3 from a matrix as a vector:
matrix.[3, *]

// Get column 3 from a matrix as a vector:
matrix.[*, 3]
```

您可以使用此切片语法以实施元素访问运算符和重载的类型`GetSlice`方法。 例如，以下代码创建包装的矩阵类型F#2D 数组实现项属性为数组编制索引，提供支持，并实现了三个版本的`GetSlice`。 如果矩阵类型，可作为模板使用此代码，可以使用本部分介绍的所有切片操作。

```fsharp
type Matrix<'T>(N: int, M: int) =
    let internalArray = Array2D.zeroCreate<'T> N M

    member this.Item
        with get(a: int, b: int) = internalArray.[a, b]
        and set(a: int, b: int) (value:'T) = internalArray.[a, b] <- value

    member this.GetSlice(rowStart: int option, rowFinish : int option, colStart: int option, colFinish : int option) =
        let rowStart = 
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish =
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        let colStart = 
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish = 
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[rowStart..rowFinish, colStart..colFinish]

    member this.GetSlice(row: int, colStart: int option, colFinish: int option) =
        let colStart = 
            match colStart with
            | Some(v) -> v
            | None -> 0
        let colFinish = 
            match colFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(1) - 1
        internalArray.[row, colStart..colFinish]

    member this.GetSlice(rowStart: int option, rowFinish: int option, col: int) =
        let rowStart = 
            match rowStart with
            | Some(v) -> v
            | None -> 0
        let rowFinish = 
            match rowFinish with
            | Some(v) -> v
            | None -> internalArray.GetLength(0) - 1
        internalArray.[rowStart..rowFinish, col]

module test =
    let generateTestMatrix x y =
        let matrix = new Matrix<float>(3, 3)
        for i in 0..2 do
            for j in 0..2 do
                matrix.[i, j] <- float(i) * x - float(j) * y
        matrix

    let test1 = generateTestMatrix 2.3 1.1
    let submatrix = test1.[0..1, 0..1]
    printfn "%A" submatrix

    let firstRow = test1.[0,*]
    let secondRow = test1.[1,*]
    let firstCol = test1.[*,0]
    printfn "%A" firstCol
```

### <a name="boolean-functions-on-arrays"></a>对数组的布尔函数

函数[ `Array.exists` ](https://msdn.microsoft.com/library/8e47ad6c-c065-4876-8cb4-ec960ec3e5c9)并[ `Array.exists2` ](https://msdn.microsoft.com/library/2e384a6a-f99d-4e23-b677-250ffbc1dd8e)分别测试在一个或两个数组中的元素。 这些函数采用一个测试函数，并返回`true`如果不存在元素 (或元素对`Array.exists2`) 满足条件。

下面的代码演示如何使用`Array.exists`和`Array.exists2`。 在这些示例中，通过应用的自变量，在这些情况下，函数参数之一来创建新函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet23.fs)]

上述代码的输出如下所示。

```
true
false
false
true
```

同样，该函数[ `Array.forall` ](https://msdn.microsoft.com/library/d88f2cd0-fa7f-45cf-ac15-31eae9086cc4)测试一个数组以确定每个元素是否满足某个布尔条件。 变体[ `Array.forall2` ](https://msdn.microsoft.com/library/c68f61a1-030c-4024-b705-c4768b6c96b9)通过使用布尔函数的长度相等的两个数组元素执行相同操作。 下面的代码演示如何使用这些函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet24.fs)]

这些示例的输出如下所示。

```
false
true
true
false
```

### <a name="searching-arrays"></a>搜索数组

[`Array.find`](https://msdn.microsoft.com/library/db6d920a-de19-4520-85a4-d83de77c1b33) 采用一个布尔函数，并返回函数为其返回的第一个元素`true`，或引发<xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType>如果找到不满足条件的元素。 [`Array.findIndex`](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f) 类似于`Array.find`，只不过它将返回而不是元素本身的元素的索引。

下面的代码使用`Array.find`和`Array.findIndex`要查找的正方形和完美的多维数据集的数字。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet25.fs)]

输出如下所示。

```
The first element that is both a square and a cube is 64 and its index is 62.
```

[`Array.tryFind`](https://msdn.microsoft.com/library/7bd65f6c-df77-454c-ac3a-6f7baecec9d9) 就像`Array.find`，只不过其结果是一个选项类型，并且它将返回`None`如果未找到的元素。 `Array.tryFind` 应使用而不是`Array.find`时您不知道数组中是否有匹配的元素。 同样， [ `Array.tryFindIndex` ](https://msdn.microsoft.com/library/da82f7fe-95e9-4fd5-a924-cd3c9d10618a)类似于[ `Array.findIndex` ](https://msdn.microsoft.com/library/5ae3a8f9-7b8f-44ea-a740-d5700f4d899f)只不过选项类型为返回值。 如果未找到的元素，则选择是`None`。

以下代码演示了 `Array.tryFind` 的用法。 此代码依赖于前面的代码。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet26.fs)]

输出如下所示。

```
Found an element: 1
Found an element: 729
```

使用[ `Array.tryPick` ](https://msdn.microsoft.com/library/72d45f85-037b-43a9-97fd-17239f72713e)当需要进行转换除了查找它的元素。 结果是函数为其返回作为选项值，转换后的元素的第一个元素或`None`如果不找到任何此类元素。

以下代码显示了 `Array.tryPick` 的用法。 在这种情况下，而不是 lambda 表达式，来简化代码，定义其他几个本地帮助器函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet27.fs)]

输出如下所示。

```
Found an element 1 with square root 1 and cube root 1.
Found an element 64 with square root 8 and cube root 4.
Found an element 729 with square root 27 and cube root 9.
Found an element 4096 with square root 64 and cube root 16.
```

### <a name="performing-computations-on-arrays"></a>对数组执行计算

[ `Array.average` ](https://msdn.microsoft.com/library/7029f2b9-91ea-41cb-be1b-466a5a0db20e)函数返回数组中的每个元素的平均值。 它被限制为支持整除的一个整数，其中包括浮点型，但不是整型类型的元素类型。 [ `Array.averageBy` ](https://msdn.microsoft.com/library/e9d64609-06a3-48f0-bc07-226ab0f85c54)函数返回的每个元素调用函数的结果的平均值。 对于整型类型的数组，可以使用`Array.averageBy`函数将每个元素转换为浮点型以便进行计算。

使用[ `Array.max` ](https://msdn.microsoft.com/library/f03fbda0-fce6-40e2-a85d-79c9d81f710b)或[ `Array.min` ](https://msdn.microsoft.com/library/d6b3da5f-bac0-4355-9846-4b72d95bc3fd)若要获取的最大或最小元素，如果元素类型支持它。 同样， [ `Array.maxBy` ](https://msdn.microsoft.com/library/18dbe7c5-482e-4766-8e01-12a76f847045)并[ `Array.minBy` ](https://msdn.microsoft.com/library/24091583-be78-4cc9-9fab-de6d7506af4f)允许功能首次执行，而可能是以转换为支持比较的类型。

[`Array.sum`](https://msdn.microsoft.com/library/4ffdb8c8-cd94-4b0b-9e5c-a7c9c17963c2) 添加一个数组的元素和[ `Array.sumBy` ](https://msdn.microsoft.com/library/41698ba6-1adc-4169-8cc5-7a0e3f8de56b)对每个元素调用一个函数并将结果相加。

若要执行的函数对数组中每个元素，但不存储返回值，请使用[ `Array.iter` ](https://msdn.microsoft.com/library/94eba0f1-ecd7-459f-b89f-ed2a2923e516)。 对于涉及长度相等的两个数组的函数，使用[ `Array.iter2` ](https://msdn.microsoft.com/library/018aa9b9-f186-4142-be8a-a62462794fdc)。 如果还需要保留的函数的结果的数组，使用[ `Array.map` ](https://msdn.microsoft.com/library/38cbe824-0480-47be-85fd-df3afdd97a45)或[ `Array.map2` ](https://msdn.microsoft.com/library/bb7aafe8-4a1f-45b9-92fc-1af9eafbea5c)，一次作用于两个数组。

变体[ `Array.iteri` ](https://msdn.microsoft.com/library/8bbe2ed4-ada7-4906-ac3e-cb09f9db6486)并[ `Array.iteri2` ](https://msdn.microsoft.com/library/c041b91f-6080-45b7-867b-2ed983a90405)允许要在计算中的元素的索引; 同样适用于[ `Array.mapi` ](https://msdn.microsoft.com/library/f7e45994-b0a1-49e6-8fb5-5641cea8fde4)并[ `Array.mapi2` ](https://msdn.microsoft.com/library/5edb33d2-47da-44e1-9290-40c00c47d5b0)。

函数[ `Array.fold` ](https://msdn.microsoft.com/library/5ed9dd3b-3694-4567-94d0-fd9a24474e09)， [ `Array.foldBack` ](https://msdn.microsoft.com/library/1121a453-dead-4711-a0ca-cc147752989c)， [ `Array.reduce` ](https://msdn.microsoft.com/library/fd62a985-89fe-4f49-a9d4-0c808ac6749d)， [ `Array.reduceBack` ](https://msdn.microsoft.com/library/4fdd4cbe-2238-4c5c-b286-597a7e9036f9)， [`Array.scan` ](https://msdn.microsoft.com/library/f6893608-9146-450d-9ebb-a0016803fbb0)，并[ `Array.scanBack` ](https://msdn.microsoft.com/library/7610f406-7a5c-41db-a0ca-8e2a2a4826ad)执行涉及数组的所有元素的算法。 同样，变体[ `Array.fold2` ](https://msdn.microsoft.com/library/5c845087-d041-476e-8cc4-53ae6849ef79)并[ `Array.foldBack2` ](https://msdn.microsoft.com/library/aa51b405-df20-4c51-9998-a6530f7db862)对两个数组执行计算。

用于执行计算这些函数对应的函数中的同名[List 模块](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)。 有关用法示例，请参阅[列出了](lists.md)。

### <a name="modifying-arrays"></a>修改数组

[`Array.set`](https://msdn.microsoft.com/library/847edc0d-4dc5-4a39-98c7-d4320c60e790) 将元素设置为指定的值。 [`Array.fill`](https://msdn.microsoft.com/library/c83c9886-81d9-44f9-a195-61c7b87f7df2) 设置为指定的值数组中的一系列元素。 下面的代码提供的示例`Array.fill`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/arrays/snippet28.fs)]

输出如下所示。

```
[|1; 2; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 0; 23; 24; 25|]
```

可以使用[ `Array.blit` ](https://msdn.microsoft.com/library/675e13e4-7fb9-4e0d-a5be-a112830de667)将一个数组的子部分复制到另一个数组。

### <a name="converting-to-and-from-other-types"></a>转换到和从其他类型

[`Array.ofList`](https://msdn.microsoft.com/library/e7225239-f561-45a4-b0b5-69a1cdcae78b) 从列表创建数组。 [`Array.ofSeq`](https://msdn.microsoft.com/library/6bedf5e0-4b22-46da-b09c-6aa09eff220c) 从序列创建数组。 [`Array.toList`](https://msdn.microsoft.com/library/4deff724-0be4-4688-92e7-9d67a1097786) 并[ `Array.toSeq` ](https://msdn.microsoft.com/library/ac28dbab-406c-4fe0-ab08-c1ce5e247af4)从数组类型转换为这些其他集合类型。

### <a name="sorting-arrays"></a>对数组进行排序

使用[ `Array.sort` ](https://msdn.microsoft.com/library/c6679075-e7eb-463c-9be5-c89be140c312)若要通过使用泛型比较函数对数组进行排序。 使用[ `Array.sortBy` ](https://msdn.microsoft.com/library/144498dc-091d-4575-a229-c0bcbd61426b)为了指定生成一个值的函数，称为*密钥*，以通过使用泛型比较函数基于该键进行排序。 使用[ `Array.sortWith` ](https://msdn.microsoft.com/library/699d3638-4244-4f42-8496-45f53d43ce95)如果想要提供自定义比较函数。 `Array.sort``Array.sortBy`，和`Array.sortWith`所有返回一个新数组，为已排序的数组。 变体[ `Array.sortInPlace` ](https://msdn.microsoft.com/library/36f39947-8a88-4823-9e9b-e9d838d292e0)， [ `Array.sortInPlaceBy` ](https://msdn.microsoft.com/library/7fb9d2dd-d461-4c67-8b43-b5c59fc12c3f)，以及[ `Array.sortInPlaceWith` ](https://msdn.microsoft.com/library/454f9e11-972d-47a6-a854-8031cb0c7b0b)修改现有而不是返回一个新数组。

### <a name="arrays-and-tuples"></a>数组和元组

函数[ `Array.zip` ](https://msdn.microsoft.com/library/23e086b8-b266-4db2-8b68-e88e6a8e2187)并[ `Array.unzip` ](https://msdn.microsoft.com/library/a529b47c-2e2b-4f79-ad44-c578432d2f48)将元组对的数组转换为元组的数组，反之亦然。 [`Array.zip3`](https://msdn.microsoft.com/library/1745744a-d2ca-4c3e-b825-3f15d9f4000d) 并[ `Array.unzip3` ](https://msdn.microsoft.com/library/bc3e6db0-f334-444f-8c30-813942880677)是类似，只不过它们使用的三个元素的元组或三个数组的元组。

## <a name="parallel-computations-on-arrays"></a>对数组的并行计算

该模块[ `Array.Parallel` ](https://msdn.microsoft.com/library/60f30b77-5af4-4050-9a5c-bcdb3f5cbb09)包含用于对数组执行并行计算的函数。 此模块不可用在面向.NET Framework 版本 4 之前的版本的应用程序中。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [F# 类型](fsharp-types.md)