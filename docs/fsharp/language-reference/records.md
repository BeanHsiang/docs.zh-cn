---
title: 记录
description: 了解如何F#记录表示已命名的值，可选择包含成员的简单聚合。
ms.date: 05/16/2016
ms.openlocfilehash: a499755383654ddaf76af12776ee93f27834b7b0
ms.sourcegitcommit: 3d0c29b878f00caec288dfecb3a5c959de5aa629
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53656136"
---
# <a name="records"></a>记录

记录表示已命名值的简单聚合，可选择包含成员。  从F#4.1，它们可以是结构或引用类型。  它们是默认情况下引用类型。

## <a name="syntax"></a>语法

```fsharp
[ attributes ]
type [accessibility-modifier] typename =
    { [ mutable ] label1 : type1;
      [ mutable ] label2 : type2;
      ... }
    [ member-list ]
```

## <a name="remarks"></a>备注

在上述语法中， *typename*是记录类型的名称*label1*并*label2*都是名称的值，称为*标签*，并*type1*并*type2*是这些值的类型。 *成员列表中*是成员的类型的可选列表。  可以使用`[<Struct>]`属性来创建结构记录而不是它是引用类型的记录。

以下是一些示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1901.fs)]

单独的行上的每个标签时，分号是可选的。

可以在名为的表达式中设置值*记录表达式*。 编译器将推断的类型使用 （如果足够不同于其他记录类型的标签） 的标签。 大括号 （{}） 括住记录表达式。 下面的代码演示初始化含有三个浮点元素带有标签的记录的记录表达式`x`，`y`和`z`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1907.fs)]

如果可能还具有相同标签的另一种类型，则不要使用缩写形式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1903.fs)]

最近声明的类型的标签优先于那些以前声明的类型，因此，在上述示例中，`mypoint3D`被推断为`Point3D`。 您可以显式指定记录类型，如以下代码所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1908.fs)]

可以就像类类型的记录类型的定义方法。

## <a name="creating-records-by-using-record-expressions"></a>使用记录表达式创建记录

可以通过使用记录中定义的标签初始化记录。 一个表达式，此方式被称为*记录表达式*。 使用大括号括住记录表达式并使用分号作为分隔符。

下面的示例演示如何创建一条记录。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1904.fs)]

最后一个字段中记录表达式和类型定义中后面的分号是可选的而不考虑字段是否都在同一行。

创建一条记录时，必须提供每个字段的值。 不能引用任何字段的初始化表达式中的其他字段的值。

在下面的代码的类型`myRecord2`推断出的字段的名称。 （可选） 可以显式指定类型名称。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

如果您需要复制现有记录，并可能更改的某些字段值，可记录构造的另一种形式。 以下代码行阐释了这一点。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

这种形式的记录表达式称为*复制和更新记录表达式*。

记录是不可变的默认设置。但是，您可以轻松创建已修改的记录，通过使用复制和更新表达式。 您还可显式指定可变字段。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1909.fs)]

不要将用于记录字段的 DefaultValue 特性。 更好的方法是定义具有初始化的字段的记录的默认实例为默认值然后使用复制和更新记录表达式来设置不同于默认值的任何字段。

```fsharp
// Rather than use [<DefaultValue>], define a default record.
type MyRecord =
    { Field1 : int
      Field2 : int }

let defaultRecord1 = { Field1 = 0; Field2 = 0 }
let defaultRecord2 = { Field1 = 1; Field2 = 25 }

// Use the with keyword to populate only a few chosen fields
// and leave the rest with default values.
let rr3 = { defaultRecord1 with Field2 = 42 }
```

## <a name="creating-mutually-recursive-records"></a>创建相互递归记录

一段时间时创建一条记录，你可能想让它取决于你想要定义之后的另一种类型。 除非定义记录类型是互斥的递归，这是一个编译错误。

定义相互递归记录通过`and`关键字。 这样可将 2 个或更多记录类型链接在一起。

例如，下面的代码定义`Person`和`Address`为相互递归类型：

```fsharp
// Create a Person type and use the Address type that is not defined
type Person =
  { Name: string
    Age: int
    Address: Address }
// Define the Address type which is used in the Person record
and Address =
  { Line1: string
    Line2: string
    PostCode: string }
```

如果要定义前面的示例，而无需`and`关键字，则它将无法编译。 `and`关键字是所必需的相互递归定义。

## <a name="pattern-matching-with-records"></a>使用记录的模式匹配

记录可以与模式匹配一起使用。 可以显式指定某些字段，并为匹配项时将分配其他字段所提供的变量。 下面的代码示例阐释了这一点。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1910.fs)]

此代码的输出如下所示。

```
Point is at the origin.
Point is on the x-axis. Value is 100.000000.
Point is at (10.000000, 0.000000, -1.000000).
```

## <a name="differences-between-records-and-classes"></a>记录与类之间的差异

记录字段与类不同，因为它们会自动公开为属性，并且它们是用于创建和复制的记录。 记录构造也不同于类构造。 在一个记录类型，不能定义构造函数。 相反，本主题中所述的构造语法适用。 类具有构造函数参数、 字段和属性之间没有直接关系。

与联合和结构类型，类似记录具有结构相等性语义。 类具有引用相等性语义。 下面的代码示例展示了此操作。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1911.fs)]

此代码的输出如下所示：

```
The records are equal.
```

如果您编写与类相同的代码，因为两个值表示堆上的两个对象，并且仅地址进行比较，两个类对象将不相等 (除非类类型重写`System.Object.Equals`方法)。

如果需要引用相等性的记录，将属性添加`[<ReferenceEquality>]`记录上方。

## <a name="see-also"></a>请参阅

- [F# 类型](fsharp-types.md)
- [类](classes.md)
- [F# 语言参考](index.md)
- [引用相等性](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.referenceequalityattribute-class-%5bfsharp%5d)
- [模式匹配](pattern-matching.md)
