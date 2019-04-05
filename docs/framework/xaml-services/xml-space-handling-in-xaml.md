---
title: XAML 中的 xml:space 处理
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], xml:space attribute
- XAML [XAML Services], white-space processing
- xml:space attribute [XAML Services]
- white-space processing [XAML Services]
ms.assetid: 5e1814f0-5b30-43d5-8c88-dede335a89d7
ms.openlocfilehash: 20a25b36857a7116f3599e3fbbbe4b438540f782
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58037051"
---
# <a name="xmlspace-handling-in-xaml"></a>XAML 中的 xml:space 处理
`xml:space`属性是声明了大量空白处理行为对象元素中的 XML 定义的属性。 此行为是相关的所有内容 （内部文本） 元素中包含其中`xml:space`声明和范围也限于子元素。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```xaml  
<object xml:space="preserve" />  
```  
  
 \- 或 -  
  
```xaml  
<object xml:space="default" />  
```  
  
## <a name="remarks"></a>备注  
 用于定义`xml:space`中包括其两个可能值的 XAML 属性派生自`xml:space`由 W3C XML 规范定义的"特殊特性"。  
  
 默认值`xml:space`属性是文本值`"default"`。 值`"default"`，或者如果`xml:space`根本未指定，分析大量空白区域的行为是默认的处理，如本主题中所定义[空格处理在 XAML 中](whitespace-processing-in-xaml.md)。  
  
 若要保留在对象元素内容中的空白区域，指定`xml:space="preserve"`在该对象元素。  
  
 在大多数解释下`xml:space`属性效果和属性的值的作用域为子元素。  
  
 在 XAML 中处理空白的完整讨论，请参阅[空格处理在 XAML 中](whitespace-processing-in-xaml.md)。  
  
## <a name="see-also"></a>请参阅
- [在 XAML 中处理空白](whitespace-processing-in-xaml.md)
- [XAML 概述 (WPF)](../wpf/advanced/xaml-overview-wpf.md)
