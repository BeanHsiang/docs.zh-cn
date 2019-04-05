---
title: 切片 (F#)
description: 了解如何使用现有的切片F#数据类型以及如何定义其他数据类型的切片。
ms.date: 01/22/2019
ms.openlocfilehash: 1d8bb029ad18c8853ab58888959967ed279fb368
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675272"
---
# <a name="slices"></a>切片

在F#，切片是一种数据类型的子集。 若要将能够从数据类型执行切片，数据类型必须要么定义`GetSlice`方法中或在[键入扩展名](type-extensions.md)，它是在作用域。 本文介绍了如何获取切片从现有F#类型以及如何定义你自己。

切片是类似于[索引器](members/indexed-properties.md)，但而不是从基础数据结构生成单个值，它们会产生多个数据库。

F#当前具有对字符串、 列表、 数组和 2D 数组进行切片的内部函数支持。

## <a name="basic-slicing-with-f-lists-and-arrays"></a>使用基本切片F#列表和数组

生成切片的最常见的数据类型F#列表和数组。 下面的示例演示如何执行此操作的列表：

```fsharp
// Generate a list of 100 integers
let fullList = [ 1 .. 100 ]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullList.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullList.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullList.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

对数组进行切片就像对列表进行切片：

```fsharp
// Generate an array of 100 integers
let fullArray = [| 1 .. 100 |]

// Create a slice from indices 1-5 (inclusive)
let smallSlice = fullArray.[1..5]
printfn "Small slice: %A" smallSlice

// Create a slice from the beginning to index 5 (inclusive)
let unboundedBeginning = fullArray.[..5]
printfn "Unbounded beginning slice: %A" unboundedBeginning

// Create a slice from an index to the end of the list
let unboundedEnd = fullArray.[94..]
printfn "Unbounded end slice: %A" unboundedEnd
```

## <a name="slicing-multidimensional-arrays"></a>切片的多维数组

F#支持多维数组中的F#核心库。 与一维数组相同的多维数组的切片也很有用。 但是，引入了额外的维度要求略有不同的语法，以便您可以采取的特定行和列切片。

以下示例演示如何进行切片的二维数组：

```fsharp
// Generate a 3x3 2D matrix
let A = array2D [[1;2;3];[4;5;6];[7;8;9]]
printfn "Full matrix:\n %A" A

// Take the first row
let row0 = A.[0,*]
printfn "Row 0: %A" row0

// Take the first column
let col0 = A.[*,0]
printfn "Column 0: %A" col0

// Take all rows but only two columns
let subA = A.[*,0..1]
printfn "%A" subA

// Take two rows and all columns
let subA' = A.[0..1,*]
printfn "%A" subA'

// Slice a 2x2 matrix out of the full 3x3 matrix
let twoByTwo = A.[0..1,0..1]
printfn "%A" twoByTwo
```

F#核心库不会定义`GetSlice`三维数组。 如果你想要对那些或其他数组或多个维度进行切片，则必须定义`GetSlice`成员自己。

## <a name="defining-slices-for-other-data-structures"></a>定义其他数据结构的切片

F#核心库定义了针对一组有限的类型段。 如果你想要定义更多的数据类型的切片，就可以做到本身在类型定义中或在类型扩展中。

例如，下面是可以如何定义切片<xref:System.ArraySegment%601>类，以允许用于方便数据处理：

```fsharp
open System

type ArraySegment<'TItem> with
    member segment.GetSlice(?start, ?finish) =
        let start = defaultArg start 0
        let finish = defaultArg finish segment.Count
        ArraySegment(segment.Array, segment.Offset + start, finish - start)

let arr = ArraySegment [| 1 .. 10 |]
let slice = arr.[2..5] //[ 3; 4; 5]
```

### <a name="use-inlining-to-avoid-boxing-if-it-is-necessary"></a>使用内联，从而避免装箱，如有必要

如果你正在定义的实际结构类型的切片，我们建议您`inline``GetSlice`成员。 F#编译器会优化的可选参数，避免由于切片任何堆分配。 这是非常重要的如切片构造<xref:System.Span%601>，不能在堆上分配。

```fsharp
open System

type Span<'T> with
    // Note the 'inline' in the member definition
    member inline sp.GetSlice(startIdx, endIdx) =
        let s = defaultArg startIdx 0
        let e = defaultArg endIdx sp.Length
        sp.Slice(s, e)

let printSpan (sp: Span<int>) =
    let arr = sp.ToArray()
    printfn "%A" arr

let sp = [| 1; 2; 3; 4; 5 |].AsSpan()
printSpan sp.[0..] // [|1; 2; 3; 4; 5|]
printSpan sp.[..5] // [|1; 2; 3; 4; 5|]
printSpan sp.[0..3] // [|1; 2; 3|]
printSpan sp.[1..2] // |2; 3|]
```

## <a name="see-also"></a>请参阅

- [索引的属性](members/indexed-properties.md)
