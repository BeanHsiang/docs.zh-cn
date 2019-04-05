---
title: '{} 转义序列-标记扩展'
ms.date: 03/30/2017
f1_keywords:
- '{}'
helpviewer_keywords:
- XAML [XAML Services], quotation mark (")
- '{} escape sequence [XAML Services]'
- XAML [XAML Services], {} escape sequence
- XAML [XAML Services], escape sequence
- quotation mark (") [XAML Services]
- escape sequence [XAML Services]
ms.assetid: 3ce3e2ad-a868-43f9-9c98-b29561cb146e
ms.openlocfilehash: eaee0a1f92d8b7cb3810651eda21f1cc800ebf57
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58018547"
---
# <a name="-escape-sequence--markup-extension"></a>{} 转义序列 / 标记扩展
为属性值提供 XAML 转义序列。 转义序列允许后续值中的属性将被解释为文本。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```xml  
<object property="{} literalValue" .../>  
```  
  
## <a name="xaml-property-element-usage"></a>XAML 属性元素用法  
  
```  
<object>  
  <object.property>  
    {} literalValue  
  </object.property>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|*literalValue*|后面的转义序列的文本字符串。 此字符串通常包含一个打开或关闭的大括号 （{或}）。|  
  
## <a name="remarks"></a>备注  
 转义序列 ({}) 使用，以便可以作为 XAML 中的文字字符使用左大括号 （{}）。  
  
 XAML 读取器通常使用左大括号 （{}） 来表示标记扩展的入口点; 但是，它们首先检查以确定它是否是右大括号 （}） 的下一个字符。 仅当两个大括号 ({}) 相邻情况是它们被视为一个转义序列。  
  
 如果遇到转义序列时，XAML 读取器应作为字符串处理字符串的其余部分。 但是，如果转义序列应用于成员具有的类型转换器，该字符串会被类型转换时解释由 XAML 编写器。  
  
 转义序列不是标记扩展，且不支持由类。 但是，它是 XAML 读取器 （包括自定义 XAML 读取器） 应遵循的约定。  
  
 引号 （"） 不能用作转义序列以这种方式。 如果您需要将英文引号连用设置为非内容属性的属性值，使用属性元素语法和属性元素内的字符串将引号或使用 XML 字符实体。 内容属性，英文引号连用可以是整个内容。  
  
 转义序列 ({}) 时，经常需要指定在 XAML 标记扩展可能出现的位置中必须包含命名空间限定符的 XML 类型。 这包括开始的 XAML 属性值和在标记扩展中，紧等号 （=）。 下面的示例显示了 XAML 特性值的开头处显示的 XML 命名空间的转义序列。  
  
 [!code-xaml[XLINQExample#StackPanelResources](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]  
  
## <a name="see-also"></a>请参阅
- [XAML 的类型转换器和标记扩展](type-converters-and-markup-extensions-for-xaml.md)
- [XML 字符实体和 XAML](xml-character-entities-and-xaml.md)
