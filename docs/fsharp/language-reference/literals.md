---
title: 文本
description: 了解有关在中的文本类型F#编程语言。
ms.date: 02/08/2019
ms.openlocfilehash: 28ce34dee3c3c3d4d0cfd4107e8cbc375a23032c
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56092158"
---
# <a name="literals"></a>文本

> [!NOTE]
> 在本文中的 API 参考链接将转至 MSDN （适用于暂时）。

本主题提供了表显示了如何指定的类型中的文本F#。

## <a name="literal-types"></a>文本类型

下表显示了中的文本类型F#。 表示以十六进制表示法表示的数字的字符不区分大小写;标识类型的字符是区分大小写。

|类型|描述|后缀或前缀|示例|
|----|-----------|----------------|--------|
|sbyte|8 位有符号整数|y|`86y`<br /><br />`0b00000101y`|
|byte|无符号的 8 位自然数|uy|`86uy`<br /><br />`0b00000101uy`|
|int16|16 位有符号整数|秒|`86s`|
|uint16|无符号的 16 位自然数|us|`86us`|
|int<br /><br />int32|32 位有符号整数|l 或 none|`86`<br /><br />`86l`|
|uint<br /><br />uint32|无符号的 32 位自然数|u 或 ul|`86u`<br /><br />`86ul`|
|unativeint|无符号自然数形式的本机指针|取消|`0x00002D3Fun`|
|int64|64 位有符号整数|L|`86L`|
|uint64|无符号的 64 位自然数|UL|`86UL`|
|单一的 float32|32 位浮点数|F 或 f|`4.14F` 或 `4.14f`|
|||lf|`0x00000000lf`|
|float;双精度|64 位浮点数|无|`4.14` 或 `2.3E+32` 或 `2.3e+32`|
|||LF|`0x0000000000000000LF`|
|bigint|不限制为 64 位表示形式的整数|I|`9999999999999999999999999999I`|
|decimal|表示为固定的点或有理数的小数|M 或 m|`0.7833M` 或 `0.7833m`|
|Char|Unicode 字符|无|`'a'`|
|String|Unicode 字符串|无|`"text\n"`<br /><br />或<br /><br />`@"c:\filename"`<br /><br />或<br /><br />`"""<book title="Paradise Lost">"""`<br /><br />或<br /><br />`"string1" + "string2"`<br /><br />另请参阅[字符串](Strings.md)。|
|byte|ASCII 字符|B|`'a'B`|
|byte[]|ASCII 字符串|B|`"text"B`|
|字符串或 byte]|逐字字符串|@ prefix|`@"\\server\share"` (Unicode)<br /><br />`@"\\server\share"B` (ASCII)|

## <a name="remarks"></a>备注

Unicode 字符串可包含可以通过使用指定的显式编码`\u`跟 16 位十六进制代码或可以通过使用指定的 UTF-32 编码`\U`跟表示 Unicode 的 32 位十六进制代码代理项对。

在F#3.1 中，可以使用`+`符号合并字符串文本。 你还可以使用按位或 (`|||`) 运算符来组合枚举标志。 例如，下面的代码是合法中F#3.1:

```fsharp
[<Literal>]
let Literal1 = "a" + "b"

[<Literal>]
let FileLocation =   __SOURCE_DIRECTORY__ + "/" + __SOURCE_FILE__

[<Literal>]
let Literal2 = 1 ||| 64

[<Literal>]
let Literal3 = System.IO.FileAccess.Read ||| System.IO.FileAccess.Write
```

不允许使用其他按位运算符。

## <a name="named-literals"></a>指定的文字

可以使用标记值都应是常量[文字](https://msdn.microsoft.com/library/465f36ce-d146-41c0-b425-679c509cd285)属性。 此属性具有导致被编译为一个常量值的效果。

在模式匹配表达式中，小写字母开头的标识符始终被当作变量绑定，而不是文字，因此通常应使用首字母大写定义文字。

## <a name="integers-in-other-bases"></a>在其他基数的整数

有符号的 32 位整数，还可以指定在使用十六进制、 八进制或二进制`0x`，`0o`或`0b`分别前缀。

```fsharp
let numbers = (0x9F, 0o77, 0b1010)
// Result: numbers : int * int * int = (159, 63, 10)
```

## <a name="underscores-in-numeric-literals"></a>数值文字中的下划线

从F#4.1，您可以使用下划线字符分隔数字 (`_`)。

```fsharp
let value = 0xDEAD_BEEF

let valueAsBits = 0b1101_1110_1010_1101_1011_1110_1110_1111

let exampleSSN = 123_456_7890
```

## <a name="see-also"></a>请参阅

- [Core.LiteralAttribute 类](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.literalattribute-class-%5bfsharp%5d)
