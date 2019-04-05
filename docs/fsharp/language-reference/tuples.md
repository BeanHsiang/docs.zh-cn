---
title: 元组
description: 了解如何F#元组，可能是不同类型的未命名但有序值的分组。
ms.date: 05/16/2016
ms.openlocfilehash: a1fc31d4dc97c0921545e53b91dcde0547002006
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53611043"
---
# <a name="tuples"></a>元组

一个*元组*是不同类型的可能是未命名但有序值的分组。  元组可以是引用类型或结构。

## <a name="syntax"></a>语法

```fsharp
(element, ... , element)
struct(element, ... ,element )
```

## <a name="remarks"></a>备注

每个*元素*在上述语法中可以是任何有效F#表达式。

## <a name="examples"></a>示例

元组的示例包括对、 三元组和等等的相同或不同类型。 在下面的代码阐释了一些示例。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L6-L21)]

## <a name="obtaining-individual-values"></a>获取单个值

可用于模式匹配访问和分配名称的元组元素，如下面的代码中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L27-L29)]

此外可以通过模式匹配外部的元组析构`match`通过表达式`let`绑定：

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L34-L37)]

或可以模式作为函数的输入匹配的元组：

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L43-L47)]

如果您需要的元组只有一个元素，可以使用通配符字符 （下划线） 以避免创建不需要值的新名称。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L53-L54)]

将引用元组中的元素复制到结构元组也很简单：

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L62-L66)]

函数`fst`和`snd`（引用仅元组） 返回第一个和第二个元素元组，分别。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L72-L73)]

返回构成三元组的第三个元素没有内置函数，但可轻松编写一个，如下所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L78-L78)]

通常情况下，最好使用模式匹配来访问各个元组元素。

## <a name="using-tuples"></a>使用元组

元组提供从函数返回多个值的简便方法，如下面的示例中所示。 此示例执行整除并返回该操作，因为元组对的第一个成员，作为第二个成员对其余的舍入的结果。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L83-L86)]

时您想要避免隐含的常用函数语法的函数参数的隐式扩充，也可以作为函数参数使用元组。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L88-L88)]

用于定义函数的常见语法`let sum a b = a + b`使您能够定义函数，则部分应用函数的第一个参数，如下面的代码中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/basic-examples.fsx#L90-L94)]

作为参数使用一个元组将禁用扩充。 详细信息，请参阅"的参数的部分应用程序"中[函数](functions/index.md)。

## <a name="names-of-tuple-types"></a>元组类型的名称

在写出为一个元组类型的名称时，您使用`*`符号来分隔元素。 元组组成`int`、 一个`float`，和一个`string`，如`(10, 10.0, "ten")`，将按以下方式编写的类型。

```fsharp
int * float * string
```

## <a name="interoperation-with-c-tuples"></a>与 C# 元组互操作

C# 7.0 引入了语言的元组。  中的元组C#是结构，并等效于结构中的元组F#。  如果你需要与 C# 进行互操作，则必须使用结构元组。

这很容易地执行操作。  例如，假设您需要将元组传递给 C# 类，然后使用其结果，这也是一个元组：

```csharp
namespace CSharpTupleInterop
{
    public static class Example
    {
        public static (int, int) AddOneToXAndY((int x, int y) a) =>
            (a.x + 1, a.y + 1);
    }
}
```

在你F#代码，然后可以将作为参数传递的结构元组，并使用的结构元组形式的结果。

```fsharp
open TupleInterop

let struct (newX, newY) = Example.AddOneToXAndY(struct (1, 2))
// newX is now 2, and newY is now 3
```

### <a name="converting-between-reference-tuples-and-struct-tuples"></a>引用的元组和结构元组之间进行转换

引用的元组和结构元组具有完全不同的基础表示形式，因为它们不是隐式转换。  也就是说，将不会编译代码如下所示：

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/interop.fsx#L5-L12)]

必须模式匹配上一个元组，并构建另一种具有的构成部分。  例如：

[!code-fsharp[Main](../../../samples/snippets/fsharp/tuples/interop.fsx#L18-L22)]

## <a name="compiled-form-of-reference-tuples"></a>已编译的形式引用元组

本部分介绍元组的形式，它们在编译时。  此处的信息不需读取除非面向.NET Framework 3.5 或更低。

元组被编译到的一种多个泛型类型，所有命名对象`System.Tuple`，该重载上的实参数量或类型参数的数目。 在此窗体中显示的元组类型，查看这些状态时从另一种语言，如C#或 Visual Basic 中，或者当使用的一种工具，并不知道F#构造。 `Tuple`类型在.NET Framework 4 中引入。 如果面向.NET Framework 的早期版本，则编译器将使用的版本[System.Tuple](https://msdn.microsoft.com/library/5ac7953d-acdc-4a58-bfb7-c1f6406c0fa3)从 2.0 版本的F#核心库。 此库中的类型仅用于面向 2.0、 3.0 和 3.5 版本的.NET Framework 的应用程序。 使用类型转发，以确保.NET Framework 2.0 和.NET Framework 4 之间的二进制文件兼容性F#组件。

### <a name="compiled-form-of-struct-tuples"></a>已编译的形式的结构元组

结构元组 (例如， `struct (x, y)`)，从根本上不同于引用的元组。  编译为<xref:System.ValueTuple>重载的实参数量，或类型参数的数目的类型。  它们等效于[C# 7.0 元组](../../csharp/tuples.md)并[Visual Basic 2017 元组](../../visual-basic/programming-guide/language-features/data-types/tuples.md)，并进行双向互操作。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [F# 类型](fsharp-types.md)