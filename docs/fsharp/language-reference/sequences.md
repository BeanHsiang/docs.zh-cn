---
title: 序列
description: 了解如何使用F#序列，当你具有较大时排序的数据集合，但不一定希望使用的所有元素。
ms.date: 02/19/2019
ms.openlocfilehash: a7791be5e8bd07d81fe9e890fc5896b181f0cb39
ms.sourcegitcommit: 07c4368273b446555cb2c85397ea266b39d5fe50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2019
ms.locfileid: "56583922"
---
# <a name="sequences"></a>序列

> [!NOTE]
> 本文中的 API 参考链接将转至 MSDN。  Docs.microsoft.com API 参考尚未完成。

一个*序列*是以逻辑序列的元素类型相同的所有。 当具有较大，有序数据集合，但一定不希望使用的所有元素时，序列是特别有用。 各序列元素计算仅为所需，因此，序列可以提供更好的性能比中在不使用的所有元素的情况下的列表。 序列由`seq<'T>`类型，即别名为`System.Collections.Generic.IEnumerable`。 因此，任何.NET Framework 类型实现`System.IEnumerable`可作为一个序列。 [Seq 模块](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684)对涉及多个序列的操作提供支持。

## <a name="sequence-expressions"></a>序列表达式

一个*序列表达式*是表达式的计算结果为一个序列。 序列表达式可以采用多种形式。 最简单的形式指定的范围。 例如，`seq { 1 .. 5 }`创建一个序列，其中包含五个元素，其中包括 1 和 5 的终结点。 你可以还指定增量 （或减少） 之间两个双句点。 例如，以下代码创建的一系列为 10 的倍数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1502.fs)]

序列表达式组成的F#生成的序列值的表达式。 可以使用`yield`关键字来生成将成为序列的一部分的值。

以下是一个示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1503.fs)]

可以使用`->`而不是运算符`yield`，在这种情况下可以省略`do`关键字，如以下示例所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1504.fs)]

下面的代码生成到一个数组，表示网格以及索引的坐标对的列表。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1505.fs)]

`if`序列中使用的表达式是一个筛选器。 例如，若要生成的序列只包含质数，假设您有一个函数`isprime`类型的`int -> bool`，按如下所示构造序列。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1506.fs)]

当你使用`yield`或`->`迭代，在每次迭代应生成序列的单个元素。 如果每次迭代都会生成一系列元素，使用`yield!`。 在这种情况下，每个迭代上生成的元素连在一起可生成最终的序列。

你可以组合在一起在序列表达式中的多个表达式。 通过每个表达式生成的元素会连接在一起。 有关示例，请参阅本主题的"示例"部分。

## <a name="examples"></a>示例

第一个示例使用序列表达式包含迭代、 筛选器和 yield 来生成一个数组。 此代码将打印一系列 1 和 100 到控制台之间的素数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1507.fs)]

下面的代码使用`yield`若要创建的两个因素和产品组成的三个元素，元组组成的乘法表。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1508.fs)]

下面的示例演示如何将`yield!`合并各个序列合并为单一的最后一个序列。 在这种情况下，每个二进制树中的子树的序列被串联的递归函数以生成最终的序列中。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1509.fs)]

## <a name="using-sequences"></a>使用序列

序列支持许多相同的功能[列出了](lists.md)。 序列还支持分组，然后通过使用键生成函数计算等操作。 序列还支持更多的不同函数的提取子序列。

多种数据类型，例如列表、 数组、 集和地图隐式是序列，因为它们是可枚举集合。 将序列作为参数适用于任何常用的函数F#数据类型，除了实现的任何.NET Framework 数据类型`System.Collections.Generic.IEnumerable<'T>`。 使用列表作为参数，它只能使用列表的函数相反。 类型`seq<'T>`是类型缩写`IEnumerable<'T>`。 这意味着，任何实现泛型的类型`System.Collections.Generic.IEnumerable<'T>`，其中包括数组、 列表、 集和中的地图F#，和也大多数.NET Framework 集合类型，与兼容`seq`键入并可以在一个序列的任何地方.

## <a name="module-functions"></a>模块函数

[Seq 模块](https://msdn.microsoft.com/library/54e8f059-ca52-4632-9ae9-49685ee9b684)中[Microsoft.FSharp.Collections 命名空间](https://msdn.microsoft.com/library/24f64e5f-5030-47d0-9759-8d3e398ed13f)包含用于使用序列函数。 这些函数使用于列表、 数组、 映射和集，因为所有这些类型是可枚举的并且因此会被视为序列。

## <a name="creating-sequences"></a>创建序列

如前面所述，使用序列表达式，或使用某些功能，可以创建序列。

可以通过创建一个空序列[Seq.empty](https://msdn.microsoft.com/library/3c7f1c69-6117-4782-b2da-0e04d6854f59)，也可以通过使用创建的只是一个指定的元素序列[Seq.singleton](https://msdn.microsoft.com/library/9b8cc460-a282-4ec5-b29a-630ab17e9de7)。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet9.fs)]

可以使用[Seq.init](https://msdn.microsoft.com/library/059de69d-812c-4f8e-be86-88aa72101576)来创建其元素通过使用你提供的函数创建的序列。 此外提供序列的大小。 此函数则类似[List.init](https://msdn.microsoft.com/library/dd38c096-0ea8-4858-be6b-794b90418b83)，只不过直到循环访问序列，不会创建元素。 下面的代码演示如何使用`Seq.init`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet10.fs)]

输出为

```
0 10 20 30 40
```

通过使用[Seq.ofArray](https://msdn.microsoft.com/library/299cd4d9-be72-4511-aac8-089e1ddaac99)并[Seq.ofList&#60;不&#62;函数](https://msdn.microsoft.com/visualfsharpdocs/conceptual/seq.oflist%5b%27t%5d-function-%5bfsharp%5d)，可以从数组和列表创建序列。 但是，您也可以将数组和列表成序列通过使用转换运算符。 这两种技术如以下代码所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet11.fs)]

通过使用[Seq.cast](https://msdn.microsoft.com/library/1d087db3-a8b2-41dd-8ddc-227544529334)，可以从弱类型化的集合，如中所定义创建序列`System.Collections`。 此类弱类型化的集合具有元素类型`System.Object`并使用非泛型枚举`System.Collections.Generic.IEnumerable&#96;1`类型。 下面的代码演示如何使用`Seq.cast`转换`System.Collections.ArrayList`为一个序列。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet12.fs)]

您可以通过使用定义无限序列[Seq.initInfinite](https://msdn.microsoft.com/library/d1804e53-da92-48ec-8d6e-57eaf4c62bef)函数。 此类的序列时，你提供的元素的索引从生成的每个元素的函数。 无限序列都可能由于迟缓计算;可以根据需要通过调用指定函数创建元素。 下面的代码示例生成一系列交替出现的连续整数的平方的倒数浮点数，在此情况下无限的序列。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet13.fs)]

[Seq.unfold](https://msdn.microsoft.com/library/7d9232fc-742e-42bc-bdf7-6f130f0eff21)从使用一个状态和转换以生成序列中的每个后续元素的计算函数生成的序列。 状态为只是一个值，该值用于计算每个元素，并根据计算每个元素可以更改。 第二个参数`Seq.unfold`是用于启动序列的初始值。 `Seq.unfold` 使用状态时，这样就可以通过返回终止序列选项类型`None`值。 下面的代码演示的序列，两个示例`seq1`并`fib`，生成的`unfold`操作。 第一种`seq1`，是只具有最多 20 个数字的简单序列。 第二类是`fib`，使用`unfold`计算斐波那契序列。 斐波那契序列中的每个元素是前两个斐波那契数字的总和，因为状态值将为元组组成的序列中前两个数字。 初始值是`(1,1)`，序列中的前两个数字。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet14.fs)]

输出如下所示：

```
The sequence seq1 contains numbers from 0 to 20.

0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20

The sequence fib contains Fibonacci numbers.

2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```

下面的代码是使用此处所述来生成和计算无限序列的值的序列模块函数的许多示例。 代码可能需要几分钟才能运行。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet15.fs)]

## <a name="searching-and-finding-elements"></a>搜索和查找元素

序列支持适用于列表的功能：[Seq.exists](https://msdn.microsoft.com/library/428c97bf-599d-4c39-a5b9-f8717c198ad1)， [Seq.exists2](https://msdn.microsoft.com/library/efdf14a4-27f7-4dc1-9281-52639e66d565)， [Seq.find](https://msdn.microsoft.com/library/02c21ecd-97e5-4e99-a4c1-b4d0b730b7d8)， [Seq.findIndex](https://msdn.microsoft.com/library/96dfe86b-df15-4d92-8316-7cd6055e09f3)， [Seq.pick](https://msdn.microsoft.com/library/a87bc771-55f7-43f9-94f9-33d8f9bf325d)， [Seq.tryFind](https://msdn.microsoft.com/library/ac43c6f5-4dc7-4e9a-a222-00b5736aee47)，并[Seq.tryFindIndex](https://msdn.microsoft.com/library/c357b221-edf6-4f68-bf40-82a3156d945a)。 这些函数可用于序列的版本的计算结果最多要搜索的元素序列。 有关示例，请参阅[列出了](https://msdn.microsoft.com/library/83102799-f251-42e1-93ef-64232e8c5b1d)。

## <a name="obtaining-subsequences"></a>获取子序列

[Seq.filter](https://msdn.microsoft.com/library/7f2e9850-a660-460c-9831-3bbff5613770)并[Seq.choose](https://msdn.microsoft.com/library/63b83b06-4b24-4239-bf69-a2c12d891395)是否与相应的函数，只不过筛选和选择才会计算序列元素的列表，可类似。

[Seq.truncate](https://msdn.microsoft.com/library/1892dfeb-308e-45e2-857a-3c3405d02244)从另一个序列，创建一个序列，但限制为指定数量的元素序列。 [Seq.take](https://msdn.microsoft.com/library/6e75f701-640b-4c4a-9d63-4313fc090596)创建包含指定的数量的元素序列的开始一个新序列。 如果有更少元素序列中的指定若要充分，比`Seq.take`引发`System.InvalidOperationException`。 之间的差异`Seq.take`并`Seq.truncate`在于`Seq.truncate`数少于指定的元素数是否未生成错误。

下面的代码显示了的行为和之间的差异`Seq.truncate`和`Seq.take`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet16.fs)]

输出中，会发生错误之前，如下所示。

```
1 4 9 16 25 
1 4 9 16 25 36 49 64 81 100 
1 4 9 16 25 
1 4 9 16 25 36 49 64 81 100
```

通过使用[Seq.takeWhile](https://msdn.microsoft.com/library/19eea4ce-66e0-4353-b015-72eb03421d92)，可以指定的谓词函数 （布尔函数），并创建从另一个序列的谓词是为其原始序列中的这些元素组成的序列`true`，但停止谓词为其返回的第一个元素之前`false`。 [Seq.skip](https://msdn.microsoft.com/library/b4eb3f08-8594-4d17-8180-852c6c688bf1)返回跳过指定的数目的另一个序列中的第一个元素，并返回剩余元素的序列。 [Seq.skipWhile](https://msdn.microsoft.com/library/fb729021-2a3c-430f-83c3-0b37526f1a16)返回，只要该谓词返回跳过另一个序列中的第一个元素的序列`true`，然后返回剩余元素，谓词为其返回的第一个元素开始`false`.

下面的代码示例演示的行为和之间的差异`Seq.takeWhile`， `Seq.skip`，和`Seq.skipWhile`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet17.fs)]

输出如下所示。

```
1 4 9 
36 49 64 81 100 
16 25 36 49 64 81 100
```

## <a name="transforming-sequences"></a>转换序列

[Seq.pairwise](https://msdn.microsoft.com/library/210dcf26-4e24-4d83-af6d-a8288b2ae4b1)创建新的序列的输入序列中的连续的元素分组到元组。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet18.fs)]

[Seq.windowed](https://msdn.microsoft.com/library/8b565b8f-d645-4dba-be22-099075fe4744)类似于`Seq.pairwise`，只不过而不是生成的元组序列，它会生成一系列包含相邻元素的副本的数组 (*窗口*) 的序列中。 每个数组中指定所需的相邻元素的数目。

以下代码示例演示了 `Seq.windowed` 的用法。 在这种情况下的窗口中的元素数为 3。 该示例使用`printSeq`，前面的代码示例中定义。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet180.fs)]

输出如下所示。

初始序列：

```
1.0 1.5 2.0 1.5 1.0 1.5 

Windows of length 3: 
[|1.0; 1.5; 2.0|] [|1.5; 2.0; 1.5|] [|2.0; 1.5; 1.0|] [|1.5; 1.0; 1.5|] 

Moving average: 
1.5 1.666666667 1.5 1.333333333
```

## <a name="operations-with-multiple-sequences"></a>包含多个序列的操作

[Seq.zip](https://msdn.microsoft.com/library/0a5df8bf-0d48-44ce-bff4-e8ef1df5bca4)并[Seq.zip3](https://msdn.microsoft.com/library/ef13bebb-22ae-4eb9-873b-87dd29154d16)采用两个或三个序列并生成的元组序列。 这些函数如下所示的相应的函数可用于[列出了](https://msdn.microsoft.com/library/83102799-f251-42e1-93ef-64232e8c5b1d)。 没有相应功能用于将一个序列分为两个或多个序列。 如果您需要一个序列，此功能，将序列转换为列表，并使用[List.unzip](https://msdn.microsoft.com/library/639db80c-41b5-45bb-a6b4-1eaa04d61d21)。

## <a name="sorting-comparing-and-grouping"></a>排序、 比较和分组

可以对列表的排序函数也适用于序列。 这包括[Seq.sort](https://msdn.microsoft.com/library/327ea595-e77c-4529-b61e-8c6cbf5ec92e)并[Seq.sortBy](https://msdn.microsoft.com/library/4f8b4fb9-bf20-49d9-b4ee-dcc906c8208f)。 这些函数循环访问整个序列。

通过比较两个序列[Seq.compareWith](https://msdn.microsoft.com/library/5a740135-0b3a-4545-816f-8f91cc31290f)函数。 该函数将连续的元素进行比较，并停止时遇到的第一个不相等对。 比较并不影响任何其他元素。

以下代码显示了 `Seq.compareWith` 的用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet19.fs)]

在前面的代码，计算和检查，仅第一个元素，结果是-1。

[Seq.countBy](https://msdn.microsoft.com/library/721702a5-150e-4fe8-81cd-ffbf8476cc1f)将生成名为的值的函数*密钥*的每个元素。 通过对每个元素调用此函数的每个元素生成一个密钥。 `Seq.countBy` 然后返回一个序列，其中包含的项的值，并生成密钥的每个值的元素数的计数。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet201.fs)]

输出如下所示。

```
(1, 34) (2, 33) (0, 33)
```

前面的输出显示有 34 个元素生成的项 1，对原始序列的 33 个值生成密钥 2 和 33 个值生成的键 0。

可以通过调用组序列的元素[Seq.groupBy](https://msdn.microsoft.com/library/d46a04df-1a42-40cc-a368-058c9c5806fd)。 `Seq.groupBy` 采用序列和生成的密钥从元素的函数。 对序列的每个元素执行函数。 `Seq.groupBy` 返回元组，其中每个元组的第一个元素是键，第二个是一系列生成该键的元素的序列。

下面的代码示例演示如何使用`Seq.groupBy`进行分区成三组具有不同的密钥值 0、 1 和 2 的从 1 到 100 的数字序列。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet202.fs)]

输出如下所示。

```
(1, seq [1; 4; 7; 10; ...]) (2, seq [2; 5; 8; 11; ...]) (0, seq [3; 6; 9; 12; ...])
```

可以创建一个序列，其中通过调用来消除重复元素[Seq.distinct](https://msdn.microsoft.com/library/99d01014-7e0e-4e7b-9d0a-41a61d93f401)。 也可以使用[Seq.distinctBy](https://msdn.microsoft.com/library/9293293b-9420-49c8-848f-401a9cd49b75)，其将调用每个元素的键生成函数。 所产生的序列包含具有唯一键; 对原始序列的元素更高版本生成的早期元素有重复的键的元素将被丢弃。

下面的代码示例演示如何使用`Seq.distinct`。 `Seq.distinct` 通过生成序列表示二进制数字，然后显示仅非重复元素为 0 和 1 所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet22.fs)]

下面的代码演示`Seq.distinctBy`开始使用一个序列，其中包含负数和正数和使用绝对值函数作为键生成函数。 缺少对应的负号在序列中，因为负号前面顺序显示，因此选择而不是具有相同的绝对的正号的所有正号所产生的序列。值或项。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet23.fs)]

## <a name="readonly-and-cached-sequences"></a>在 Readonly 和缓存的序列

[Seq.readonly](https://msdn.microsoft.com/library/88059cb4-3bb0-4126-9448-fbcd48fe13a7)创建序列的只读副本。 `Seq.readonly` 有读写集合，如数组，并且你不想要修改原始集合时很有用。 此函数可用于保留数据封装。 在下面的代码示例中，创建包含数组的类型。 属性公开的数组，但而不是返回一个数组，它将返回一个序列，其中通过使用从该数组创建`Seq.readonly`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/fssequences/snippet24.fs)]

[Seq.cache](https://msdn.microsoft.com/library/d197f9cc-08bf-4986-9869-246e72ca73f0)创建序列的存储的版本。 使用`Seq.cache`以避免重新计算的序列，或如果你具有多个线程使用一个序列，但您必须确保每个元素执行操作时只进行一次。 如果您正由多个线程的序列，可以有一个线程的枚举，并计算原始序列的值，剩余线程可以使用缓存的序列。

## <a name="performing-computations-on-sequences"></a>对序列执行计算

简单的算术运算与其类似的列表，如[Seq.average](https://msdn.microsoft.com/library/609d793b-c70f-4e36-9ab4-d928056d65b8)， [Seq.sum](https://msdn.microsoft.com/library/01208515-4880-4358-91f5-af34f66dc77a)， [Seq.averageBy](https://msdn.microsoft.com/library/47c855c1-2dbd-415a-885e-b909d9d3e4f8)， [Seq.sumBy](https://msdn.microsoft.com/library/68cca78c-94ed-4a45-9b8d-34d2c5f2b1b1)，依次类推。

[Seq.fold](https://msdn.microsoft.com/library/30c4c95a-9563-4c96-bbe1-f7aacfd026e3)， [Seq.reduce](https://msdn.microsoft.com/library/a2ad4f64-ac69-47d2-92f0-7173d9dfeae9)，和[Seq.scan](https://msdn.microsoft.com/library/7e2d23e9-f153-4411-a884-b6d415ff627e)是否与所提供的列表的相应函数类似。 序列支持列出了支持这些函数的完整的变体的子集。 有关详细信息和示例，请参阅[列出了](lists.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [F# 类型](fsharp-types.md)
