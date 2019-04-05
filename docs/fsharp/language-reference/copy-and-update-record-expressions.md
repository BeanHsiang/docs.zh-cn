---
title: 复制和更新记录表达式
description: 了解如何编写的复制和更新记录表达式复制现有的记录，更新指定的字段，并返回已更新的记录。
author: ChrSteinert
ms.date: 06/04/2016
ms.openlocfilehash: 5f9b13ebf6c456aff73872b7522d7670c068dd88
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53613305"
---
# <a name="copy-and-update-record-expressions"></a>复制和更新记录表达式

一个*复制和更新记录表达式*一个表达式，将复制的现有记录、 更新指定的字段，并返回已更新的记录。

## <a name="syntax"></a>语法

```fsharp
{ record-name with
    updated-member-definitions }
```

## <a name="remarks"></a>备注

记录是默认情况下，固定不变的因此可能是不会更新到现有记录。 若要创建已更新的记录的记录的所有字段将需要再次指定。 若要简化此任务*复制和更新记录表达式*可用。 此表达式采用现有记录，通过使用指定的表达式的字段和由表达式指定的缺失字段创建一个新的相同的类型。
您需要复制现有记录，并可能更改的某些字段值时，这很有用。

需要对实例的新创建的记录。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

如果您打算更新仅在您可以使用该记录的字段*复制和更新记录表达式*如下所示：

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

## <a name="see-also"></a>请参阅

- [记录](records.md)
- [F# 语言参考](index.md)