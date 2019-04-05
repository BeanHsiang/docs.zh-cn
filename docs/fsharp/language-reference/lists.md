---
title: 列表
description: 了解如何F#列出了相同类型的元素的有序的、 不可变序列。
ms.date: 05/16/2016
ms.openlocfilehash: cc4e292280cca0dca37f69cf5a46ec2822d08d5c
ms.sourcegitcommit: 3d0c29b878f00caec288dfecb3a5c959de5aa629
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53656331"
---
# <a name="lists"></a>列表

> [!NOTE]
> 本文中的 API 参考链接将转至 MSDN。  Docs.microsoft.com API 参考尚未完成。

F# 中的列表是一个有序的、不可变的同类型元素系列。 若要执行基本操作的列表上，使用中的函数[List 模块](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)。

## <a name="creating-and-initializing-lists"></a>创建和初始化列表

可以通过以下方式来定义列表：显式列出元素并用分号分隔各个元素，然后将这些元素用方括号括起来，如下面的代码行所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1301.fs)]

也可以在各个元素之间插入换行符，在这种情况下，分号是可选的。 当元素初始化表达式较长或你希望为每个元素包含一个注释时，后一种语法会产生可读性更高的代码。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet13011.fs)]

通常，所有列表元素都必须是同一类型。 但存在一种例外情况，即其元素被指定为基类型的列表中包含的元素可以是派生类型。 由于 `Button` 和 `CheckBox` 都派生自 `Control`，因此以下内容是可接受的。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet13012.fs)]

也可以使用由范围分隔符 (`..`) 分隔的整数所指示的范围来定义列表元素，如以下代码所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1302.fs)]

可使用一对中间不包含任何内容的方括号来指定空列表。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1304.fs)]

也可以使用序列表达式来创建列表。 请参阅[序列表达式](sequences.md#sequence-expressions)有关详细信息。 例如，以下代码创建一个从 1 到 10 的整数的平方值的列表。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1303.fs)]

## <a name="operators-for-working-with-lists"></a>用于处理列表的运算符

可以使用 `::` (cons) 运算符将元素附加到列表中。 如果 `list1` 为 `[2; 3; 4]`，则以下代码会将 `list2` 创建为 `[100; 2; 3; 4]`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1305.fs)]

可以使用 `@` 运算符来串联具有可兼容类型的列表，如以下代码所示。 如果 `list1` 为 `[2; 3; 4]`，且 `list2` 为 `[100; 2; 3; 4]`，则此代码会将 `list3` 创建为 `[2; 3; 4; 100; 2; 3; 4]`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1306.fs)]

中提供了用于对列表执行操作的函数[List 模块](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)。

由于 F# 中的列表是不可变的，因此任何修改操作都会生成新列表，而不是修改现有列表。

中列出了F#将作为单独链接的列表，这意味着，访问列表头的操作是 o （1），并且元素访问复杂度为 O (*n*)。

## <a name="properties"></a>Properties

列表类型支持以下属性：

|属性|类型|描述|
|--------|----|-----------|
|[Head](https://msdn.microsoft.com/library/5f9414fd-6bdb-470a-8b72-40016db30740)|`'T`|第一个元素。|
|[为空](https://msdn.microsoft.com/library/44406ecb-1918-4d32-b32a-ca1f69840386)|`'T list`|返回适合类型的空列表的静态属性。|
|[IsEmpty](https://msdn.microsoft.com/library/3ba087b2-2fc2-406d-b10a-cff6a19322da)|`bool`|如果列表不包含任何元素，则为 `true`。|
|[Item](https://msdn.microsoft.com/library/bdb2553a-0e54-4ff8-baed-ab1aac8f5dae)|`'T`|位于指定索引处（从零开始）的元素。|
|[长度](https://msdn.microsoft.com/library/25f715c8-9daa-4c4d-a6c7-26772f9dab4d)|`int`|元素数量。|
|[结尾](https://msdn.microsoft.com/library/2a6f8eb9-dc32-41aa-8b62-2baffaface91)|`'T list`|不带第一个元素的列表。|

以下是一些使用这些属性的示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1307.fs)]

## <a name="using-lists"></a>使用列表

利用列表进行编程，你可以使用少量代码来执行复杂的操作。 本节介绍针对列表的常见操作，这些操作对于函数编程很重要。

### <a name="recursion-with-lists"></a>利用列表进行递归

列表特别适合于递归编程技术。 假设要对列表的每个元素执行某个操作。 可以通过以下方式来实现递归：对列表头执行操作，然后再次将列表尾（一个更小的列表，它由不带第一个元素的原始列表组成）传递回下一级递归。

若要编写此类递归函数，可在模式匹配中使用 cons 运算符 (`::`)，以便将列表头与列表尾分离。

以下代码示例显示了如何使用模式匹配来实现对列表执行操作的递归函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet13071.fs)]

上面的代码非常适用于小型列表，但对于大型列表，它可能会溢出堆栈。 以下代码通过使用累加器参数（一种用于处理递归函数的标准技术）对该代码进行了改进。 使用累加器参数会使函数进行尾递归，这将节省堆栈空间。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet13072.fs)]

函数 `RemoveAllMultiples` 是一个递归函数，它采用两个列表。 第一个列表包含一些数字（将移除这些数字的倍数），第二个列表是要从中移除这些倍数数字的列表。 以下示例中的代码使用此递归函数来消除列表中的所有非质数，结果是得到一个质数列表。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1308.fs)]

输出如下所示：

```
Primes Up To 100:
[2; 3; 5; 7; 11; 13; 17; 19; 23; 29; 31; 37; 41; 43; 47; 53; 59; 61; 67; 71; 73; 79; 83; 89; 97]
```

## <a name="module-functions"></a>模块函数

[List 模块](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)提供了访问列表中的元素的函数。 访问头元素的速度最快且最为容易。 使用属性[Head](https://msdn.microsoft.com/library/5f9414fd-6bdb-470a-8b72-40016db30740)或模块函数[List.head](https://msdn.microsoft.com/library/22514cc5-0511-498b-a2cc-837b688a6da2)。 可以使用访问列表尾[尾部](https://msdn.microsoft.com/library/2a6f8eb9-dc32-41aa-8b62-2baffaface91)属性或[List.tail](https://msdn.microsoft.com/library/da0a0638-4420-4571-84b6-d09ae601f601)函数。 若要按索引查找元素，使用[List.nth](https://msdn.microsoft.com/library/1f717d57-89be-4007-a971-9cf5a28d83b1)函数。 `List.nth` 将遍历列表。 因此，它是 O (*n*)。 如果你的代码经常使用 `List.nth`，那么可能需要考虑使用数组而不是列表。 数组中的元素访问的运算复杂度为 O(1)。

### <a name="boolean-operations-on-lists"></a>针对列表的布尔操作

[List.isEmpty](https://msdn.microsoft.com/library/a7941d44-9e92-427c-b806-c378f4558107)函数确定一个列表是否包含任何元素。

[List.exists](https://msdn.microsoft.com/library/15a3ebd5-98f0-44c0-8220-7dedec3e68a8)函数将应用一个布尔值的列表，并返回元素的测试`true`是否有任何元素满足该测试。 [List.exists2](https://msdn.microsoft.com/library/7532b39e-3f4f-4534-a60b-d7721dc6fa7e)类似，但对连续对两个列表中的元素进行操作。

以下代码演示了 `List.exists` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet1.fs)]

输出如下所示：

```
For list [0; 1; 2; 3], contains zero is true
```

以下示例演示了 `List.exists2` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet2.fs)]

输出如下所示：

```
Lists [1; 2; 3; 4; 5] and [5; 4; 3; 2; 1] have at least one equal element at the same position.
```

可以使用[List.forall](https://msdn.microsoft.com/library/e11a5233-d612-40ac-833b-d5cf496900b7)如果想要测试是否列表中的所有元素都满足条件。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet3.fs)]

输出如下所示：

```
true
false
```

同样， [List.forall2](https://msdn.microsoft.com/library/bb611f02-8277-48f5-9af3-6194ae27d07e)确定两个列表中的相应位置中的所有元素是否都满足涉及每对元素的布尔表达式。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet4.fs)]

输出如下所示：

```
true
false
```

### <a name="sort-operations-on-lists"></a>针对列表的排序操作

[List.sort](https://msdn.microsoft.com/library/17f1030e-aa7e-41dd-94ea-72cb6c04fd3d)， [List.sortBy](https://msdn.microsoft.com/library/955bfc5f-ad9c-4f2d-a7ab-91e43eb21359)，并[List.sortWith](https://msdn.microsoft.com/library/1d806a54-9166-4198-906d-15101f7916c7)函数对列表进行排序。 排序函数可确定要使用上面三个函数中的哪一个函数。 `List.sort` 使用默认的泛型比较。 泛型比较根据泛型比较函数使用全局运算符来比较值。 它能够有效地处理各种元素类型，例如简单数值类型、元组、记录、可区分联合、列表、数组以及任何实现 `System.IComparable` 的类型。 对于实现 `System.IComparable` 的类型，泛型比较将使用 `System.IComparable.CompareTo()` 函数。 泛型比较还可处理字符串，只不过使用的是不依赖于区域性的排序顺序。 不应对不支持的类型（例如函数类型）使用泛型比较。 此外，默认泛型比较的性能最适用于小型结构化类型；对于需要经常比较和排序的大型结构化类型，请考虑实现 `System.IComparable` 并提供 `System.IComparable.CompareTo()` 方法的有效实现。

`List.sortBy` 使用一个函数，此函数返回一个用作排序条件的值，而 `List.sortWith` 将比较函数用作参数。 当你使用不支持比较的类型或比较需要更复杂的比较语义（对于区域性识别字符串）时，后面这两个函数会很有用。

以下示例演示了 `List.sort` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet5.fs)]

输出如下所示：

```
[-2; 1; 4; 5; 8]
```

以下示例演示了 `List.sortBy` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet6.fs)]

输出如下所示：

```
[1; -2; 4; 5; 8]
```

下一个示例演示了 `List.sortWith` 的用法。 在此示例中，使用自定义比较函数 `compareWidgets` 首先比较自定义类型的一个字段，在第一个字段的值相等的情况下，再比较另一个字段。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet7.fs)]

输出如下所示：

```
[{ID = 92;
Rev = 1;}; {ID = 92;
Rev = 1;}; {ID = 100;
Rev = 2;}; {ID = 100;
Rev = 5;}; {ID = 110;
Rev = 1;}]
```

### <a name="search-operations-on-lists"></a>针对列表的搜索操作

可以对列表执行各种搜索操作。 最简单[List.find](https://msdn.microsoft.com/library/0594593e-9c75-44c1-8f5a-a37b2e561c06)，允许您查找符合给定的条件的第一个元素。

以下代码示例演示了如何使用 `List.find` 来查找列表中可被 5 整除的第一个元素。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet8.fs)]

结果为 5。

如果必须先转换元素，则调用[List.pick](https://msdn.microsoft.com/library/0430b515-7fe4-49a1-a616-d2286d8b08b2)，后者采用一个函数来返回一个选项，然后查找第一个选项值是`Some(x)`。 `List.pick` 返回结果 `x`，而不是返回元素。 如果未找到匹配的元素，则 `List.pick` 将引发 `System.Collections.Generic.KeyNotFoundException`。 以下代码显示了 `List.pick` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet9.fs)]

输出如下所示：

```
"b"
```

另一组搜索操作[List.tryFind](https://msdn.microsoft.com/library/37f4532e-9fd0-4802-8bbd-e1aa2380287d)和相关的函数返回选项值。 `List.tryFind` 函数返回列表中满足条件的第一个元素（如果该元素存在）；如果该元素不存在，则返回选项值 `None`。 变体[List.tryFindIndex](https://msdn.microsoft.com/library/5e31968c-c3d3-43d2-859a-0526825895ec)返回的元素的索引; 如果找到一个对象，而不是元素本身。 下面的代码中阐释了这些函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet10.fs)]

输出如下所示：

```
The first even value is 22.
The first even value is at position 8.
```

### <a name="arithmetic-operations-on-lists"></a>针对列表的算术运算

常见的算术运算，如 sum 和 average 内置[List 模块](https://msdn.microsoft.com/library/a2264ba3-2d45-40dd-9040-4f7aa2ad9788)。 若要使用[List.sum](https://msdn.microsoft.com/library/54d47fe3-5ecf-4883-beb5-e915342a17f9)，列表元素类型必须支持`+`运算符并具有零值。 所有内置算术类型都满足这些条件。 若要使用[List.average](https://msdn.microsoft.com/library/2b9a627b-106d-4548-8c4c-ab5058b8f8e1)，元素类型必须支持不带余数，这不包括整型类型，但允许使用浮点型的部门。 [List.sumBy](https://msdn.microsoft.com/library/b7623389-0fe1-4762-9c67-51079903ab7d)并[List.averageBy](https://msdn.microsoft.com/library/936cc9ec-62af-464d-8726-7999c2f48403)函数采用一个函数作为参数，并且此函数的结果用于计算的总和或平均值的值。

以下代码演示了 `List.sum`、`List.sumBy` 和 `List.average` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet11.fs)]

输出为 `1.000000`。

以下代码显示了 `List.averageBy` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet12.fs)]

输出为 `5.5`。

### <a name="lists-and-tuples"></a>列表和元组

包含元组的列表可由压缩和解压缩函数操作。 这些函数将两个包含单值的列表合并为一个元组列表，或将一个元组列表分成两个包含单值的列表。 最简单[List.zip](https://msdn.microsoft.com/library/3028d790-8f48-4c94-bf08-b058bec3689c)函数采用两个列表的单个元素，并生成单个元组对的列表。 另一个版本， [List.zip3](https://msdn.microsoft.com/library/003cc28e-0de3-4d99-89ed-cb19028e3c5b)、 采用单元素的三个列表，并生成具有三个元素的元组的单个列表。 以下代码示例演示了 `List.zip` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet13.fs)]

输出如下所示：

```
[(1, -1); (2, -2); (3; -3)]
```

以下代码示例演示了 `List.zip3` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet14.fs)]

输出如下所示：

```
[(1, -1, 0); (2, -2, 0); (3, -3, 0)]
```

相应的解压缩版本中， [List.unzip](https://msdn.microsoft.com/library/639db80c-41b5-45bb-a6b4-1eaa04d61d21)并[List.unzip3](https://msdn.microsoft.com/library/43078c77-32ec-4342-85b3-c31ccf984db4)、 需要的元组的列表和返回列表中的元组，其中第一个列表包含了每个元组中的第一行的所有元素，并第二个列表包含每个元组和等等的第二个元素。

下面的代码示例演示如何将[List.unzip](https://msdn.microsoft.com/library/639db80c-41b5-45bb-a6b4-1eaa04d61d21)。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet15.fs)]

输出如下所示：

```
([1; 3], [2; 4])
[1; 3] [2; 4]
```

下面的代码示例演示如何将[List.unzip3](https://msdn.microsoft.com/library/43078c77-32ec-4342-85b3-c31ccf984db4)。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet16.fs)]

输出如下所示：

```
([1; 4], [2; 5], [3; 6])
```

### <a name="operating-on-list-elements"></a>针对列表元素的操作

F# 支持针对列表元素执行各种操作。 简单的方法是[List.iter](https://msdn.microsoft.com/library/f778d075-81a9-4994-af60-cddcc53a201f)，这样您就可以在列表中的每个元素调用的函数。 变体包括[List.iter2](https://msdn.microsoft.com/library/ea3b7761-916c-4016-9bd8-651124c98b40)，这样您就可以对两个列表元素执行运算[List.iteri](https://msdn.microsoft.com/library/6dd21ae6-5c00-41cd-8306-821e513d8f60)，这就像`List.iter`只不过作为传递的每个元素的索引为每个元素调用函数的参数和[List.iteri2](https://msdn.microsoft.com/library/9658d740-9be5-4bf7-b663-c8ab2b3e196c)，它是组合的功能`List.iter2`和`List.iteri`。 以下代码示例阐释了这些函数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet17.fs)]

输出如下所示：

```
List.iter: element is 1
List.iter: element is 2
List.iter: element is 3
List.iteri: element 0 is 1
List.iteri: element 1 is 2
List.iteri: element 2 is 3
List.iter2: elements are 1 4
List.iter2: elements are 2 5
List.iter2: elements are 3 6
List.iteri2: element 0 of list1 is 1; element 0 of list2 is 4
List.iteri2: element 1 of list1 is 2; element 1 of list2 is 5
List.iteri2: element 2 of list1 is 3; element 2 of list2 is 6
```

另一个常用的函数的转换列表元素是[List.map](https://msdn.microsoft.com/library/c6b49c99-d4f3-4ba3-b1d0-85a312683dc6)，这样您就可以将函数应用于列表中的每个元素，并将所有结果都放入一个新列表。 [List.map2](https://msdn.microsoft.com/library/5f48cce7-6eaf-4e54-8996-2b04d3c31e57)并[List.map3](https://msdn.microsoft.com/library/dd9fb190-6980-4537-be96-5645a64908f8)是采用多个列表的变体。 此外可以使用[List.mapi](https://msdn.microsoft.com/library/284b9234-3d26-409b-b328-ac79638d9e14)并[List.mapi2](https://msdn.microsoft.com/library/680643af-233c-40a3-82f2-43d5af27ec49)，如果除了元素，该函数需要传递每个元素的索引。 `List.mapi2` 和 `List.mapi` 之间的唯一区别在于 `List.mapi2` 使用了两个列表。 下面的示例阐释[List.map](https://msdn.microsoft.com/library/c6b49c99-d4f3-4ba3-b1d0-85a312683dc6)。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet18.fs)]

输出如下所示：

```
[2; 3; 4]
```

以下示例显示了 `List.map2` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet19.fs)]

输出如下所示：

```
[5; 7; 9]
```

以下示例显示了 `List.map3` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet20.fs)]

输出如下所示：

```
[7; 10; 13]
```

以下示例显示了 `List.mapi` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet21.fs)]

输出如下所示：

```
[1; 3; 5]
```

以下示例显示了 `List.mapi2` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet22.fs)]

输出如下所示：

```
[0; 7; 18]
```

[List.collect](https://msdn.microsoft.com/library/cd08bbc7-a3b9-40ab-8c20-4e85ec84664f)类似于`List.map`，只不过每个元素生成一个列表，并且所有这些列表将串联成一个最终列表。 在以下代码中，列表的每个元素均生成三个数字。 所有这些数字将收集到一个列表中。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet23.fs)]

输出如下所示：

```
[1; 2; 3; 2; 4; 6; 3; 6; 9]
```

此外可以使用[List.filter](https://msdn.microsoft.com/library/11a8c926-547b-44dd-bbae-98d44f3dd248)，它采用布尔值条件，并生成一个仅包含满足给定的条件的元素的新列表。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet24.fs)]

生成的列表为 `[2; 4; 6]`。

映射和筛选器的组合[List.choose](https://msdn.microsoft.com/library/2e21d3fb-ce35-4824-8a57-c4404616093d)使您能够转换和同时选择元素。 `List.choose` 对列表的每个元素应用一个返回选项的函数，并在该函数返回选项值 `Some` 时为元素返回新的结果列表。

以下代码演示了如何使用 `List.choose` 从单词列表中选择大写单词。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet25.fs)]

输出如下所示：

```
["Rome's"; "Bob's"]
```

### <a name="operating-on-multiple-lists"></a>针对多个列表的操作

可以将多个列表联接在一起。 若要将两个列表联接成一个，请使用[List.append](https://msdn.microsoft.com/library/2954da80-3f4a-4a4b-9371-794645c03426)。 若要联接两个以上的列表，请使用[List.concat](https://msdn.microsoft.com/library/c5afd433-8764-4ea8-a6a8-937fb4d77c4c)。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet26.fs)]

### <a name="fold-and-scan-operations"></a>Fold 和 Scan 操作

一些列表操作涉及所有列表元素之间的相互依赖关系。 Fold 和 scan 操作就像`List.iter`并`List.map`之处，调用的函数对每个元素，但这些操作提供一个名为的附加参数*累加器*执行信息的计算。

使用 `List.fold` 可对列表执行计算。

下面的代码示例演示如何将[List.fold](https://msdn.microsoft.com/library/c272779e-bae7-4983-8d7f-16b345bb33a0)以执行各种操作。

将遍历列表；累加器 `acc` 是一个在计算过程中不断传递的值。 第一个参数采用累加器和列表元素，并返回针对列表元素的计算的中间结果。 第二个参数为累加器的初始值。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet27.fs)]

这些函数的各个版本（函数名中有一个数字）对多个列表执行操作。 例如， [List.fold2](https://msdn.microsoft.com/library/6cfcd043-a65d-4423-805a-2ab234cb5343)对两个列表执行计算。

以下示例演示了 `List.fold2` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet28.fs)]

`List.fold` 并[List.scan](https://msdn.microsoft.com/library/21f636db-885c-4a72-970e-e3841f33a1b8)差异在于`List.fold`返回额外参数的最终值但`List.scan`返回额外参数 （连同最终值） 的中间值的列表。

例如，包括反向变体，每个函数[List.foldBack](https://msdn.microsoft.com/library/b9a58e66-efe1-445f-a90c-ac9ffb9d40c7)中的顺序方面与它不同的将遍历列表和参数的顺序。 此外，`List.fold`和`List.foldBack`有变体， [List.fold2](https://msdn.microsoft.com/library/6cfcd043-a65d-4423-805a-2ab234cb5343)并[List.foldBack2](https://msdn.microsoft.com/library/56371d3e-5271-4183-9e8c-15a02eda9aa2)，采用两个列表的长度相等。 对每个元素执行的函数可以使用两个列表的对应元素来执行一些操作。 两个列表的元素类型可以不同（如以下示例所示），其中一个列表包含银行帐户的交易金额，而另一个列表包含交易的类型：存款或取款。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet29.fs)]

对于类似于求和这样的计算，`List.fold` 和 `List.foldBack` 具有相同的效果，因为结果不依赖于遍历顺序。 在以下示例中，`List.foldBack` 用于在列表中添加元素。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet30.fs)]

以下示例将返回到银行帐户示例。 这次，添加一个新的交易类型：利息计算。 期末余额现在取决于事务顺序。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet34.fs)]

该函数[List.reduce](https://msdn.microsoft.com/library/048e1f95-691b-49cb-bb99-fb85f68f3d8b)有点像`List.fold`和`List.scan`，只不过不是传递单独累加器，`List.reduce`会将采用两个参数的元素类型而不是一个函数只是一，这些参数的另一个将用作累加器，这意味着它将存储中间计算结果。 `List.reduce` 首先对前两个列表元素执行操作，然后将操作的结果和下一个元素一起使用。 由于不存在具有自己的类型的单独累加器，因此只可以在累加器和元素类型的类型相同时，使用 `List.reduce` 代替 `List.fold`。 以下代码演示了 `List.reduce` 的用法。 如果提供的列表中不包含任何元素，则 `List.reduce` 将引发异常。

在以下代码中，对 lambda 表达式的第一个调用提供了参数 2 和 4，并返回 6；下一个调用提供了参数 6 和 10，因此结果为 16。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lists/snippet33.fs)]

### <a name="converting-between-lists-and-other-collection-types"></a>在列表和其他集合类型之间进行转换

`List` 模块提供了用于来回转换序列和数组的函数。 若要将转换到或从序列，请使用[List.toSeq](https://msdn.microsoft.com/library/7024be4b-ee70-43cc-8d0a-e6564a4ff7c0)或[List.ofSeq](https://msdn.microsoft.com/library/74ab9289-4a59-4433-92eb-3f662d7f7db0)。 若要将转换到或从一个数组，请使用[List.toArray](https://msdn.microsoft.com/library/ac87dd82-a0cd-40b3-b1fa-dd3168134547)或[List.ofArray](https://msdn.microsoft.com/library/f4bddc26-8c8f-4307-a6d7-a49dceb97032)。

### <a name="additional-operations"></a>其他操作

有关针对列表的其他操作的信息，请参阅库参考主题[Collections.List 模块](https://msdn.microsoft.com/visualfsharpdocs/conceptual/collections.list-module-%5bfsharp%5d)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [F# 类型](fsharp-types.md)
- [序列](sequences.md)
- [数组](arrays.md)
- [选项](options.md)
