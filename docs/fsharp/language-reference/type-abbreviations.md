---
title: 类型缩写
description: 了解如何F#类型缩写，用来以使代码更易于读取为类型更有意义的名称。
ms.date: 05/16/2016
ms.openlocfilehash: 0deaef789367aad413e5a537bf7164034e1275c0
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613344"
---
# <a name="type-abbreviations"></a>类型缩写

一个*类型缩写*是别名或备用名称的类型。

## <a name="syntax"></a>语法

```fsharp
type [accessibility-modifier] type-abbreviation = type-name
```

## <a name="remarks"></a>备注

类型缩写可用于为指定类型的更有意义的名称，以使代码易于阅读。 此外可以使用它们创建易于使用为原本不方便，写出的类型名称。此外，可以使用类型缩写来轻松地更改基础类型，而无需更改使用类型的所有代码。 下面是简单类型缩写。

类型缩写的可访问性默认为`public`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2301.fs)]

类型缩写可以包含泛型参数，如以下代码所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2302.fs)]

在前面的代码，`Transform`是表示任何类型的一个自变量的函数的类型缩写，将返回相同类型的单个值。

类型缩写不会保留在.NET Framework MSIL 代码。 因此，当你使用F#程序集从另一种.NET Framework 语言，必须使用类型缩写的基础类型名称。

此外可以上度量单位的使用类型缩写。 有关详细信息，请参阅[度量单位](units-of-measure.md)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)