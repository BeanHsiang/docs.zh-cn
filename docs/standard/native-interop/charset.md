---
title: 字符集和封送 - .NET
description: 了解字符集的不同值如何更改 .NET 将数据封送到本机代码的方式。
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: 2ff6c485906db481cb5236f83e885ba9fd46450b
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2019
ms.locfileid: "56411359"
---
# <a name="charsets-and-marshalling"></a>字符集和封送

`char` 值、`string` 对象和 `System.Text.StringBuilder` 对象的封送方式取决于 P/Invoke 或结构上的 `CharSet` 字段的值。 可以通过在声明 P/Invoke 时设置 <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> 字段来设置 P/Invoke 的 `CharSet`。 若要设置结构的 `CharSet`，请在声明结构时设置 <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> 字段。 未设置这些属性字段时，将由语言编译器确定使用哪些 `CharSet`。 默认情况下，C# 使用 <xref:System.Runtime.InteropServices.CharSet.Ansi> 字符集。

下表显示了每个字符集之间的映射以及字符或字符串在使用该字符集封送时的表示形式：

| CharSet | Windows | Unix | 在 Unix 上为 Mono |
|---------|---------|-------|-------|
| Ansi    | `char` (ANSI)  | `char`（在 macOS 上为 ANSI，在 Linux 上为 UTF-8） | `char` (UTF-8) |
| Unicode | `wchar_t` (UTF-16) | `char16_t` (UTF-16) | `char16_t` (UTF-16) |
| 自动 | `wchar_t` (UTF-16) | `char16_t` (UTF-16) | `char` (UTF-8) |

确保了解选择字符集时所需的本机表示形式。
