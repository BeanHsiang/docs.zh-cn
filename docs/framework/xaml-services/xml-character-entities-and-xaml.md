---
title: XML 字符实体和 XAML
ms.date: 03/30/2017
f1_keywords:
- '&'
- '&amp'
- '&gt'
- '&lt'
helpviewer_keywords:
- XAML [XAML Services], special characters
- ampersand (&) [XAML Services]
- special characters [XAML Services]
- apostrophe (') [XAML Services]
- greater-than (>) character [XAML Services]
- XAML [XAML Services], quotation mark (")
- XAML [XAML Services], apostrophe (')
- '& (ampersand) [XAML Services]'
- XAML [XAML Services], & (ampersand)
- XAML [XAML Services], escape sequence
- quotation mark (") [XAML Services]
- less-than (<) character [XAML Services]
ms.assetid: 6896d0ce-74f7-420a-9ab4-de9bbf390e8d
ms.openlocfilehash: 3fefbe9696ba7618dc811c6ac8f600bb6322dad5
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58048057"
---
# <a name="xml-character-entities-and-xaml"></a>XML 字符实体和 XAML
XAML 使用在 XML 中为特殊字符定义的字符实体。 本主题介绍一些特定的字符实体和 XAML 中其他 XML 概念的一般注意事项。  
  
<a name="character_entities_and_escaping_issues_that_are_unique_to_xaml"></a>   
## <a name="character-entities-and-escaping-issues-that-are-unique-to-xaml"></a>XAML 独有的字符实体和转义问题  
 XAML 标记通常使用相同的字符实体和在 XML 中定义的转义序列。  
  
 主要的例外是大括号（{ 和 }）在 XAML 中具有意义，因为这些字符通知 XAML 处理器必须将括在大括号中的字符序列解释为标记扩展。 有关标记扩展的详细信息，请参阅 [Markup Extensions for XAML Overview](markup-extensions-for-xaml-overview.md)。  
  
 但是，你仍可通过使用特定于 XAML（而非 XML）的转义序列将大括号显示为原义字符。 有关详细信息，请参阅[{}转义序列-标记扩展](escape-sequence-markup-extension.md)。  
  
 请注意，反斜杠 (\\) 作为字符串处理时不需要转义序列。  
  
<a name="xml_character_entities"></a>   
## <a name="xml-character-entities"></a>XML 字符实体  
 如前所述，通常用于编写 XAML 标记的大多数字符实体和转义序列都由 XML 定义。 本主题不提供这些实体的完整列表；实体的详细参考可在外部文档（如 XML 规范）中找到。 但是，为方便起见，本主题列出了一些常在 XAML 标记中使用的特定 XML 字符实体。  
  
|字符|实体|说明|  
|---------------|------------|-----------|  
|&（"and"符）|\&amp;|必须用于属性值和元素内容两者。|  
|> (大于-号字符)|\&gt;|必须用于属性值，但 > 是可作为内容的元素，只要 < 不之前。|  
|< (小于-号字符)|\&lt;|必须用于属性值，但\<是可作为内容的元素，只要 > 不跟随其后。|  
|"（直双引号）|\&quot;|必须用于属性值，但直双引号 (") 可作为元素内容。 请注意，属性值可能括在直单引号 (') 或直双引号 (") 内；首先出现的字符定义属性值的引号，另一个引号则可用作值内部的文字。|  
|'（直单引号）|\&apos;|必须用于属性值，但直单引号 (') 可作为元素内容。 请注意，属性值可能括在直单引号 (') 或直双引号 (") 内；首先出现的字符定义属性值的引号，另一个引号则可用作值内部的文字。|  
|（数字字符映射）|&#*[整数]*; 或 &#x *[十六进制]*;|XAML 支持向处于活动状态的编码的数字字符映射。|  
|（不间断空格）|&\#160;（假定 utf-8 编码）|对于流文档元素或采用文本（如 WPF <xref:System.Windows.Controls.TextBox>）的元素，不间断空格没有超出标记范围进行规范化，甚至是对于 `xml:space="default"` 也是如此。 (有关详细信息，请参阅[空格处理在 XAML 中](whitespace-processing-in-xaml.md)。)|  
  
<a name="xml_comment_format"></a>   
## <a name="xml-comment-format"></a>XML 注释格式  
 XAML 使用 XML 注释格式：注释的开头为 `<!--`，注释的结尾为 `-->,` 且序列 `--` 不能出现在注释中。  
  
<a name="xml_processing_instructions"></a>   
## <a name="xml-processing-instructions"></a>XML 处理指令  
 XAML 根据 XML 规范处理 XML 处理指令，该规范说明必须传递指令。 在.NET Framework XAML 服务中处理的 XAML 不使用任何处理指令。 使用 XAML 的其他现有框架也不会使用 XAML 中的处理指令。  
  
## <a name="see-also"></a>请参阅
- [XAML 概述 (WPF)](../wpf/advanced/xaml-overview-wpf.md)
- [标记扩展和 WPF XAML](../wpf/advanced/markup-extensions-and-wpf-xaml.md)
- [XamlName 语法](xamlname-grammar.md)
- [在 XAML 中处理空白](whitespace-processing-in-xaml.md)
