---
title: XAML 中 xml:lang 的处理
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], xml:lang attribute
- xml:lang attribute [XAML Services]
- RFC 3066 standard [XAML Services]
- standards [XAML Services], RFC 3066
ms.assetid: 7aac0078-a1c5-41f8-b8b0-975510d9dca0
ms.openlocfilehash: 9ec844c37ee2ef7979c82b308cdf167a46a3c072
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58034425"
---
# <a name="xmllang-handling-in-xaml"></a>XAML 中 xml:lang 的处理
`xml:lang` 属性是 [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]定义的属性，用于在 XML 中声明元素的语言和区域性信息。 此属性的相同含义在 XAML 中持续存在；但有一些其他注意事项。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```xaml  
<object xml:lang="rfc3066lang" />  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|*rfc3066lang*|派生自 [RFC 3066](https://go.microsoft.com/fwlink/?LinkId=132454) 标准的字符串，并标识一种语言或语言-地区。 当为后者时，将由一个连字符分隔语言和区域。 请参阅 <xref:System.Windows.Markup.XmlLanguage> ，以了解有关值和格式的更多信息。|  
  
## <a name="remarks"></a>备注  
 `xml:lang` 中 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 属性的定义派生自 `xml:lang` ，又由 [!INCLUDE[TLA#tla_w3c](../../../includes/tlasharptla-w3c-md.md)] 定义为 [!INCLUDE[TLA2#tla_xml](../../../includes/tla2sharptla-xml-md.md)]的“特殊特性”。 语言和区域性信息可能由元素根据其实现以不同方式进行处理；但是， [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 属性没有默认的 `xml:lang` 处理方式。  
  
 `xml:lang` 属性的默认值是属性级空字符串。  
  
 当由作用于 `xml:lang` 值的系统进行解释时， `xml:lang` 属性效果和属性值通常永久保留到子元素中。  
  
 当由 .NET Framework XAML 服务的 XAML 编写器进行解释时， `xml:lang` 值可以以基础对象的表示形式创建 <xref:System.Windows.Markup.XmlLanguage> 或 <xref:System.Globalization.CultureInfo> 对象；但是，该行为取决于为 `xml:lang` 指定的值是否为这些类的有效构造。  
  
 通过将 `xml:lang` 应用到属性，框架可以在 XML 中创建框架定义属性和 <xref:System.Windows.Markup.XmlLangPropertyAttribute> 含义之间的关联。  
  
## <a name="wpf-usage-nodes"></a>WPF 使用情况节点  
 对于身为 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement>派生类的元素，可以使用等效 <xref:System.Windows.FrameworkElement.Language%2A> 依赖项属性取代 `xml:lang` 属性。 默认情况下，如果未通过属性或通过处理 <xref:System.Windows.FrameworkElement.Language%2A> 属性来另外设置 `xml:lang` 属性，则它使用“en-US”。  
  
## <a name="see-also"></a>请参阅
- [WPF 全球化](../wpf/advanced/globalization-for-wpf.md)
