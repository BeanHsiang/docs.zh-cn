---
title: 字符串
description: 了解如何F#'string' 类型不可变的文本表示为一系列 Unicode 字符。
ms.date: 05/16/2016
ms.openlocfilehash: 5b55b0c87b6636346677b973e093e7bcba324e98
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53610653"
---
# <a name="strings"></a>字符串

> [!NOTE]
> 本文中的 API 参考链接将转至 MSDN。  Docs.microsoft.com API 参考尚未完成。

`string`类型将不可变的文本表示为一系列 Unicode 字符。 `string` 是 .NET Framework 中 `System.String` 的别名。

## <a name="remarks"></a>备注

字符串文本用引号 （"） 字符分隔。 反斜杠字符 ( \\ ) 使用某些特殊字符进行编码。 反斜杠和组合在一起的下一个字符被称为*转义序列*。 转义序列中支持F#字符串文本下表中所示。

|字符|转义序列|
|---------|---------------|
|Backspace|`\b`|
|换行符|`\n`|
|回车|`\r`|
|Tab|`\t`|
|反斜杠|`\\`|
|引号|`\"`|
|撇号|`\'`|
|Unicode 字符|`\uXXXX` 或`\UXXXX`(其中`X`表示一个十六进制数字)|

如果前面有 @ 符号，则该文本是原义字符串。 这意味着，将忽略任何转义序列，但两个引号字符解释为一个引号字符。

此外，字符串可能包含三个引号引起来。 在这种情况下，将忽略所有转义序列，包括双引号字符。 若要指定包含嵌入的带引号的字符串的字符串，您可以使用原义字符串或三引号字符串。 如果使用原义字符串，则必须指定两个引号字符来表示单引号字符。 如果使用三引号字符串时，您可以使用单引号字符没有它们解析为字符串的末尾。 当您使用 XML 或其他结构包含嵌入的引号时，此技术很有用。

```fsharp
// Using a verbatim string
let xmlFragment1 = @"<book author=""Milton, John"" title=""Paradise Lost"">"

// Using a triple-quoted string
let xmlFragment2 = """<book author="Milton, John" title="Paradise Lost">"""
```

在代码中，接受有换行符的字符串的和换行是按字面解释为换行符，除非反斜杠字符为换行符之前的最后一个字符。 使用反斜杠字符时，将忽略在下一行中前导空白字符。 下面的代码生成一个字符串`str1`具有值`"abc\ndef"`和一个字符串`str2`具有值`"abcdef"`。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1001.fs)]

可以按以下方式使用的类似数组的语法来访问字符串中的单个字符。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1002.fs)]

输出为 `b`。

或者，可以通过使用数组切片语法提取子字符串，如下面的代码中所示。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1003.fs)]

输出如下所示。

```
abc
def
```

您可以通过无符号字节，类型的数组表示 ASCII 字符串`byte[]`。 添加后缀`B`到字符串文本以指示它是一个 ASCII 字符串。 ASCII 字符串文本使用的字节数组支持相同的转义序列作为 Unicode 字符串，除了 Unicode 转义序列。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1004.fs)]

## <a name="string-operators"></a>字符串运算符

有两种方法来连接字符串： 通过使用`+`运算符或通过使用`^`运算符。 `+`运算符维护与.NET Framework 字符串处理功能的兼容性。

下面的示例说明了字符串串联。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1006.fs)]

## <a name="string-class"></a>字符串类

因为字符串类型在F#是实际.NET Framework`System.String`键入所有`System.String`成员均可。 这包括`+`运算符，用来连接字符串`Length`属性，并`Chars`Unicode 字符数组的形式返回字符串的属性。 有关字符串的详细信息，请参阅`System.String`。

通过使用`Chars`属性的`System.String`，可以通过指定一个索引，如下面的代码中所示访问字符串中的单个字符。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet1005.fs)]

## <a name="string-module"></a>字符串模块

字符串处理的附加功能包含在`String`中的模块`FSharp.Core`命名空间。 有关详细信息，请参阅[Core.String 模块](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.string-module-%5bfsharp%5d)。

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)