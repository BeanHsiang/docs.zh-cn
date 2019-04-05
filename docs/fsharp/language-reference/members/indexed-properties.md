---
title: 索引属性
description: 了解如何在中的索引属性F#，这允许对有序数据的类似数组的访问。
ms.date: 10/17/2018
ms.openlocfilehash: bc330641c451973ddefa0a34fe6e757a808f6cb7
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57678600"
---
# <a name="indexed-properties"></a>索引属性

在定义类，用于对有序数据提取时，有时可能很有帮助，而无需公开基础的实现提供对该数据的索引的访问。 这通过`Index`成员。

## <a name="syntax"></a>语法

```fsharp
// Indexed property that has both get and set defined.
member self-identifier.Index
    with get(index-values) =
        get-member-body
    and set index-values values-to-set =
        set-member-body

// Indexed property with get only
member self-identifier.Index
    with get(index-values) =
        get-member-body

// Indexed property that has set only.
member self-identifier.Index
    with set index-values values-to-set =
        set-member-body
```

## <a name="remarks"></a>备注

上述语法中的窗体演示如何定义具有这两者的索引的属性`get`和一个`set`方法中，有`get`方法，或具有`set`方法仅。 此外可以将两者合并为仅限获取和组，所示的语法所示的语法，并生成具有 get 和 set 的属性。 这后一种形式，可将不同的可访问性修饰符和属性放在 get 和 set 方法。

使用名称`Item`，编译器会将属性视为默认索引属性。 一个*的默认索引属性*是一个属性，可以访问的对象实例上使用的类似数组的语法。 例如，如果`o`是用于定义此属性，该语法的类型的对象`o.[index]`用于访问属性。

用于访问非默认索引的属性的语法是提供属性和中括号内，就像常规成员的索引的名称。 例如，如果上的属性`o`称为`Ordinal`，您编写`o.Ordinal(index)`来访问它。

无论使用哪种形式，应始终使用扩充窗体上的索引属性的集方法。 扩充函数有关的信息，请参阅[函数](../functions/index.md)。

## <a name="example"></a>示例

下面的代码示例演示定义和使用的默认和非默认索引的属性具有 get 和 set 方法。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet3301.fs)]

## <a name="output"></a>输出

```console
ONE two three four five six seven eight nine ten
ONE first two second three third four fourth five fifth six 6th
seven seventh eight eighth nine ninth ten tenth
```

## <a name="indexed-properties-with-multiple-index-values"></a>具有多个索引值的索引的属性

索引的属性可以具有多个索引值。 在这种情况下，值是逗号分隔时使用的属性。 在此类属性中的 set 方法必须具有两个扩充的参数，其中第一个是包含密钥的元组，其中第二个是要设置的值。

下面的代码演示如何将具有多个索引值的索引属性。

```fsharp
open System.Collections.Generic

/// Basic implementation of a sparse matrix based on a dictionary
type SparseMatrix() =
    let table = new Dictionary<(int * int), float>()
    member __.Item
        // Because the key is comprised of two values, 'get' has two index values
        with get(key1, key2) = table.[(key1, key2)]

        // 'set' has two index values and a new value to place in the key's position
        and set (key1, key2) value = table.[(key1, key2)] <- value

let sm = new SparseMatrix()
for i in 1..1000 do
    sm.[i, i] <- float i * float i
```

## <a name="see-also"></a>请参阅

- [成员](index.md)
