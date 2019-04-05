---
title: XamlName 语法
ms.date: 03/30/2017
helpviewer_keywords:
- DottedXamlName grammar [XAML Services]
- grammar [XAML Services], DottedXamlName
- grammar [XAML Services], XamlName
- names in XAML [XAML Services]
- XamlName grammar [XAML Services]
ms.assetid: 11e4cada-41d2-494d-9531-0d3df4dfcbe3
ms.openlocfilehash: 642ca16142bdfe78a40ddf4e6a3a79ce6a8a4985
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58031600"
---
# <a name="xamlname-grammar"></a>XamlName 语法
XamlName 语法是为了方便起见，此处重现的 XAML 语言规范 [MS-XAML] 中定义的特定语法。  
  
## <a name="from-the-xaml-specification"></a>从 XAML 规范  
 [MS-XAML] 规范定义语法 XamlName 来标识用于类型和属性的合法符号标识符的集。  
  
 字符串值的类型 XamlName 必须符合以下语法：  
  
```  
XamlName ::= NameStartChar ( NameChar )*   
NameStartChar ::= LetterCharacter | '_'   
NameChar ::= NameStartChar | DecimalDigit | CombiningCharacter   
LetterCharacter ::= UnicodeLu | UnicodeLl | UnicodeLo | UnicodeLt | UnicodeNl   
DecimalDigit ::= UnicodeNd   
CombiningCharacter ::= UnicodeMn | UnicodeMc  
```  
  
 这假定以下常规类别值为 Unicode 字符数据库中定义  
  
```  
Lu  
Letter, Uppercase  
Ll  
Letter, Lowercase  
Lt  
Letter, Titlecase  
Lm  
Letter, Modifier  
Lo  
Letter, Other  
Mn  
Mark, Non-Spacing  
Mc  
Mark, Spacing Combining  
Nd  
Number, Decimal  
Nl  
Number, Letter  
```  
  
 XAML 定义的第二个语法，DottedXamlName，是用于属性和事件限定的引用，并还为附加成员。 有关详细信息，请参阅<xref:System.Windows.DependencyProperty>并[XAML 概述 (WPF)](../wpf/advanced/xaml-overview-wpf.md)。  
  
 字符串值的类型 DottedXamlName 必须符合以下语法：  
  
```  
DottedXamlName ::= XamlName '.' XamlName  
```  
  
## <a name="remarks"></a>备注  
 有关完整规范，请参见[ \[MS XAML\]](https://go.microsoft.com/fwlink/?LinkId=114525)。
