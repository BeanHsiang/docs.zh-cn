---
title: XML 文档 (F#)
description: 了解有关支持在F#用于从注释生成文档。
ms.date: 05/16/2016
ms.openlocfilehash: c5305dea8832112644710b2863269ef00feddd10
ms.sourcegitcommit: e39d93d358974b9ed4541cedf4e25c0101015c3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2019
ms.locfileid: "55204673"
---
# <a name="xml-documentation"></a>XML 文档

您可以生成三斜杠 （/ /） 从文档中的注释的代码F#。 XML 注释之前可以放置在代码文件 (.fs) 或签名 (.fsi) 文件中的声明。

## <a name="generating-documentation-from-comments"></a>从注释生成文档

中的支持F#从注释生成文档是相同的其他.NET Framework 语言中。 如其他.NET Framework 语言中所示[-doc 编译器选项](https://msdn.microsoft.com/library/434394ae-0d4a-459c-a684-bffede519a04)使您能够生成一个 XML 文件，其中包含你可以通过使用一种工具，如将文档转换的信息[DocFX](https://dotnet.github.io/docfx/)或[Sandcastle](https://github.com/EWSoftware/SHFB)。 通过使用适用于与通常用其他.NET Framework 语言编写的程序集一起使用的设计的工具生成的文档生成一个视图的已编译形式基于 Api 的F#构造。 除非专门支持工具F#，这些工具生成的文档不匹配F#API 的视图。

有关如何从 XML 生成文档的详细信息，请参阅[XML 文档注释&#40;C&#35;编程指南&#41;](https://msdn.microsoft.com/library/b2s063f7)。

## <a name="recommended-tags"></a>建议的标记

有两种方法编写 XML 文档注释。 一个是直接在三斜杠注释中，只需编写文档，而无需使用 XML 标记。 如果执行此操作时，整个注释文本被视为紧跟在后面的代码构造的摘要文档。 如果想要编写仅为每个构造的简短摘要，请使用此方法。 另一种方法是使用 XML 标记来提供更结构化的文档。 第二种方法，可分别为简短摘要、 其他备注、 每个参数和类型参数和异常抛出，文档和返回值的说明指定注释。 下表描述了在中识别的 XML 标记F#XML 代码注释。

|标记语法|描述|
|----------|-----------|
|**\<c\>**_text_**\</c\>**|指定的*文本*是代码。 文档生成器可以使用此标记适用于代码的字体显示文本。|
|**\<summary\>**_text_**\</summary\>**|指定的*文本*是程序元素的简要说明。 说明通常是一个或两个句子。|
|**\<remarks\>**_text_**\</remarks\>**|指定的*文本*包含有关程序元素的补充信息。|
|**\<param name="**_name_**"\>**_description_**\</param\>**|指定的名称和描述函数或方法参数。|
|**\<typeparam name="**_name_**"\>**_description_**\</typeparam\>**|指定的名称和类型参数的说明。|
|**\<returns\>**_text_**\</returns\>**|指定的*文本*描述函数或方法的返回值。|
|**\<exception cref="**_type_**"\>**_description_**\</exception\>**|指定可以生成的异常以及在其下引发的环境类型。|
|**\<see cref="**_reference_**"\>**_text_**\</see\>**|指定的内联链接到另一个程序元素。 *引用*是出现在 XML 文档文件的名称。 *文本*是链接中所示的文本。|
|**\<seealso cref="**_reference_**"/\>**|指定指向另一种类型的文档的另请参阅链接。 *引用*是出现在 XML 文档文件的名称。 另请参阅链接通常出现在文档页的底部。|
|**\<para\>**_text_**\</para\>**|指定文本的段落。 这用于分隔中的文本**备注**标记。|

## <a name="example"></a>示例

### <a name="description"></a>描述

以下是典型的 XML 文档注释中的签名文件。

### <a name="code"></a>代码

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet7101.fs)]

## <a name="example"></a>示例

### <a name="description"></a>描述

下面的示例演示的替代方法，而无需 XML 标记。 在此示例中，在注释中的整个文本被视为摘要。 请注意，如果未显式指定摘要的标记，则应不指定其他标记，如**param**或**返回**标记。

### <a name="code"></a>代码

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-2/snippet7102.fs)]

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [编译器选项](compiler-options.md)
