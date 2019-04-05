---
title: 引用单元格
description: 了解如何F#引用单元格是使您能够创建具有引用语义的可变值的存储位置。
ms.date: 05/16/2016
ms.openlocfilehash: e4fcd3cf1abcf5f5e3b4d5439c9215b79ff8dbcd
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612759"
---
# <a name="reference-cells"></a>引用单元格

*引用单元格*是使您能够创建具有引用语义的可变值的存储位置。

## <a name="syntax"></a>语法

```fsharp
ref expression
```

## <a name="remarks"></a>备注

可以在值前面使用 `ref` 运算符来创建用于封装该值的新引用单元格。 然后，您可以更改基础值，因为该值是可变的。

引用单元格容纳实际值；它不仅仅是一个地址。 使用 `ref` 运算符创建引用单元格时，将以封装的可变值的形式创建基础值的副本。

可以使用 `!`（感叹号）运算符取消对引用单元格的引用。

下面的代码示例阐释了引用单元格的声明和用法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2201.fs)]

输出为 `50`。

引用单元格是 `Ref` 泛型记录类型的实例，声明方式如下所示。

```fsharp
type Ref<'a> =
{ mutable contents: 'a }
```

类型 `'a ref` 是 `Ref<'a>` 的同义词。 IDE 中的编译器和 IntelliSense 显示此类型的前者，而基础定义是后者。

`ref` 运算符创建新引用单元格。 下面的代码声明 `ref` 运算符。

```fsharp
let ref x = { contents = x }
```

下表显示了可用于引用单元格的功能。

|运算符、成员或字段|描述|类型|定义|
|--------------------------|-----------|----|----------|
|`!`（取消引用运算符）|返回基础值。|`'a ref -> 'a`|`let (!) r = r.contents`|
|`:=`（赋值运算符）|更改基础值。|`'a ref -> 'a -> unit`|`let (:=) r x = r.contents <- x`|
|`ref`（运算符）|将值封装到新的引用单元格中。|`'a -> 'a ref`|`let ref x = { contents = x }`|
|`Value`（属性）|获取或设置基础值。|`unit -> 'a`|`member x.Value = x.contents`|
|`contents`（记录字段）|获取或设置基础值。|`'a`|`let ref x = { contents = x }`|

可通过多种方式来访问基础值。 取消引用运算符 (`!`) 返回的值不是可赋值的值。 因此，如果要修改基础值，您必须改用赋值运算符 (`:=`)。

`Value` 属性和 `contents` 字段都是可赋值的值。 因此，你可以使用它们来访问或更改基础值，如下面的代码所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2203.fs)]

输出如下所示。

```
10
10
11
12
```

提供字段 `contents` 的目的是为了与其他版本的 ML 兼容，并且该字段将在编译过程中产生警告。 若要禁用警告，请使用 `--mlcompatibility` 编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。

C#程序员应知道`ref`在C#不是与相同`ref`中F#。 中的构造等效于F#都[byref](byrefs.md)，这是从引用单元格不同的概念。

值标记为`mutable`可能会自动提升为`'a ref`如果捕获的闭包中; 请参阅[值](values/index.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [参数和自变量](parameters-and-arguments.md)
- [符号和运算符参考](symbol-and-operator-reference/index.md)
- [值](values/index.md)
