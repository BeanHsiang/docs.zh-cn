---
title: 如何：修改字符串内容 - C# 指南
ms.date: 02/26/2018
helpviewer_keywords:
- strings [C#], modifying
ms.openlocfilehash: 48be71f35634222dd9898199f004ea1190b62f35
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54664004"
---
# <a name="how-to-modify-string-contents-in-c"></a>如何：修改以 C\# 编写的字符串内容

本文演示通过修改现有 `string` 来生成 `string` 的几种方法。 演示的所有方法均将修改的结果返回为新的 `string` 对象。 为了清楚地演示这一点，所有示例均将结果存储在新的变量中。 之后，你可以检查原始 `string` 和运行每个示例时从修改中得到的 `string`。

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

本文中演示了几种方法。 你可以替换现有文本。 可以搜索模式并将匹配的文本替换为其他文本。 可以将字符串视为字符序列。 还可以使用删除空格的简便方法。 应选择与你的方案最匹配的方法。

## <a name="replace-text"></a>替换文本

下面的代码通过将现有文本替换为替代文本来创建新的字符串。

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#1)]

上述代码演示了字符串的不可变属性。 在上述示例中可以看到，原始字符串 `source` 并未被修改。 <xref:System.String.Replace%2A?displayProperty=nameWithType> 方法创建的是包含修改的新 `string`。

<xref:System.String.Replace%2A> 可替换字符串或单个字符。 在这两种情况下，搜索文本的每个匹配项均被替换。  下面的示例将所有的“ ”替换为“\_”：

[!code-csharp-interactive[replace characters](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#2)]

源字符串并未发生更改，而是通过替换操作返回了一个新的字符串。

## <a name="trim-white-space"></a>去除空格

可使用 <xref:System.String.Trim%2A?displayProperty=nameWithType>、<xref:System.String.TrimStart%2A?displayProperty=nameWithType> 和 <xref:System.String.TrimEnd%2A?displayProperty=nameWithType> 方法删除任何前导空格或尾随空格。  下面的代码就是删除两种空格的示例。 源字符串不会发生变化；这些方法返回带修改内容的新字符串。

[!code-csharp-interactive[trim white space](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#3)]

## <a name="remove-text"></a>删除文本

可使用 <xref:System.String.Remove%2A?displayProperty=nameWithType> 方法删除字符串中的文本。 此方法移删除特定索引处开始的某些字符。 下面的示例演示如何使用 <xref:System.String.IndexOf%2A?displayProperty=nameWithType>（后接 <xref:System.String.Remove%2A>）方法，删除字符串中的文本：

[!code-csharp-interactive[remove text](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#4)]

## <a name="replace-matching-patterns"></a>替换匹配模式

可使用[正则表达式](../../standard/base-types/regular-expressions.md)将匹配模式的文本替换为新文本，新文本可能由模式定义。 下面的示例使用 <xref:System.Text.RegularExpressions.Regex?displayProperty=nameWithType> 类从源字符串中查找模式并将其替换为正确的大写。 <xref:System.Text.RegularExpressions.Regex.Replace(System.String,System.String,System.Text.RegularExpressions.MatchEvaluator,System.Text.RegularExpressions.RegexOptions)?displayProperty=nameWithType> 方法使用将替换逻辑提供为其参数之一的函数。 在本示例中，该函数 `LocalReplaceMatchCase` 是在示例方法中声明的本地函数。 `LocalReplaceMatchCase` 使用 <xref:System.Text.StringBuilder?displayProperty=nameWithType>类，以生成具有正确大写的替换字符串。

正则表达式最适合用于搜索和替换遵循模式的文本，而不是已知的文本。 请参阅[如何：搜索字符串](search-strings.md)了解详细信息。 搜索模式“the\s”搜索“the”后接空格字符的单词。 该部分的模式可确保它不与源字符串中的“there”相匹配。 有关正则表达式语言元素的更多信息，请参阅[正则表达式语言 - 快速参考](../../standard/base-types/regular-expression-language-quick-reference.md)。

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#5)]

<xref:System.Text.StringBuilder.ToString%2A?displayProperty=nameWithType> 方法返回一个不可变的字符串，其中包含 <xref:System.Text.StringBuilder> 对象中的内容。

## <a name="modifying-individual-characters"></a>修改单个字符

可从字符串生成字符数组，修改数组的内容，然后从数组的已修改内容创建新的字符串。

下面的示例演示如何替换字符串中的一组字符。 首先，它使用 <xref:System.String.ToCharArray?displayProperty=nameWithName> 方法来创建字符数组。 它使用 <xref:System.String.IndexOf%2A> 方法来查找单词“fox”的起始索引。 接下来的三个字符将替换为其他单词。 最终，从更新的字符串数组中构造了新的字符串。

[!code-csharp-interactive[replace creates a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#6)]

## <a name="unsafe-modifications-to-string"></a>对字符串进行不安全修改

使用不安全代码，可在创建字符串后“就地”进行修改。 不安全代码会绕过许多 .NET 旨在用于尽量减少代码中某些类型 bug 的功能。 需使用不安全代码来就地修改字符串，因为字符串类型已设计为不可变类型。 创建之后，它的值就不会更改。 不安全代码通过访问和修改 `string` 使用的内存来避开此属性，而不使用常规的 `string` 方法。
下面提供了这些少数情况下的示例，因为某些时候，你可能希望使用不安全代码就地修改字符串。 示例演示如何使用 `fixed` 关键字。 `fixed` 关键字可防止垃圾回收器 (GC) 在代码使用不安全指针访问内存时移动内存中的字符串对象。 此外还演示对字符串进行不安全操作可能产生的一个副作用，此副作用是由于 C# 编译器在内部存储（暂存）字符串的方式而导致的。 通常，除非绝对必要，否则不应使用这种方法。 可在关于 [unsafe](../language-reference/keywords/unsafe.md) 和 [fixed](../language-reference/keywords/fixed-statement.md) 的文章中了解详细信息。 <xref:System.String.Intern%2A> 的 API 参考包括字符串集中的信息。

[!code-csharp-interactive[unsafe ways to create a new string](../../../samples/snippets/csharp/how-to/strings/ModifyStrings.cs#7)]

可通过查看 [GitHub 存储库](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/strings)中的代码来尝试这些示例。 也可以下载这些示例的 [zip 文件](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/strings.zip)。

## <a name="see-also"></a>请参阅

- [.NET Framework 正则表达式](../../standard/base-types/regular-expressions.md)
- [正则表达式语言 - 快速参考](../../standard/base-types/regular-expression-language-quick-reference.md)
