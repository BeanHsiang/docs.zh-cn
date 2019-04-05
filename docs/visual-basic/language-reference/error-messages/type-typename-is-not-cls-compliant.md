---
title: 类型 <typename> 不符合 CLS
ms.date: 07/20/2015
f1_keywords:
- bc40041
- vbc40041
helpviewer_keywords:
- BC40041
ms.assetid: 634132c2-5646-44aa-98c6-f773e2e63882
ms.openlocfilehash: 243f51b3e6c798c82fdbe7b28557c4f96c728bf2
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55281718"
---
# <a name="type-typename-is-not-cls-compliant"></a>类型\<类型名称 > 不符合 cls 的
不符合 CLS 規格的数据类型声明变量、 属性或函数返回。  
  
 应用程序符合[语言独立性和与语言无关的组件](../../../standard/language-independence-and-language-independent-components.md)(CLS)，它必须只使用符合 cls 的类型。  
  
 以下 Visual Basic 数据类型不符合 CLS 規格：  
  
-   [SByte 数据类型](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [ULong 数据类型](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [UShort 数据类型](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 **错误 ID:** BC40041  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   如果你的应用程序需要符合 CLS 規格，将此元素的数据类型更改为最接近的符合 cls 的类型。 例如，如果不需要 2147483647 以上的数值范围，可以使用 `UInteger` 取代 `Integer` 。 如果确实需要更大范围，可以用 `UInteger` 代替 `Long`。  
  
-   如果你的应用程序不需要为符合 CLS 規格，您不需要更改任何内容。 您应注意它是不符合，但是。