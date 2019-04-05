---
title: “<proceduresignature1>”不符合 CLS，因为它重载仅在数组参数类型的数组或数组参数类型的秩方面与它不同的“<proceduresignature2>”
ms.date: 07/20/2015
f1_keywords:
- vbc40035
- bc40035
helpviewer_keywords:
- BC40035
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
ms.openlocfilehash: 0bda4ad6a4d5368d93e2ca603b78bf9db6aca858
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55269557"
---
# <a name="proceduresignature1-is-not-cls-compliant-because-it-overloads-proceduresignature2-which-differs-from-it-only-by-array-of-array-parameter-types-or-by-the-rank-of-the-array-parameter-types"></a>\<proceduresignature1 > 是因为它重载不符合 CLS 規格\<proceduresignature2 > 与它不同的仅通过数组参数类型的数组或数组参数类型的秩
过程或属性被标记为`<CLSCompliant(True)>`时它将替代另一个过程或属性，而且它们的参数列表之间的唯一区别是交错数组的嵌套级别或数组的秩。  
  
 在以下声明中，第二个和第三个声明生成此错误。  
  
 `Overloads Sub processArray(ByVal arrayParam() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam()() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam(,) As Integer)`  
  
 第二个声明更改原始的一维参数`arrayParam`到数组的数组。 第三个声明更改`arrayParam`到二维数组 （级别 2）。 尽管 Visual Basic 允许重载，可只是某项更改不同，此类重载不符合[语言独立性和与语言无关的组件](../../../standard/language-independence-and-language-independent-components.md)(CLS)。  
  
 当将 <xref:System.CLSCompliantAttribute> 应用到编程元素中时，需要将该特性的 `isCompliant` 参数设置为 `True` 或 `False` 来指示符合或不符合性。 此参数没有默认值，必须为其提供一个值。  
  
 如果不将 <xref:System.CLSCompliantAttribute> 应用到元素，则它将被视为不符合规范。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC40035  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   如果你需要 CLS 遵从性，定义在重载，可通过比仅引用此帮助页上的更改的更多方式彼此不同。  
  
-   如果你需要重载的区别仅由所做的更改引用上此帮助页上，删除<xref:System.CLSCompliantAttribute>与其定义或将其作为标记`<CLSCompliant(False)>`。  
  
## <a name="see-also"></a>请参阅

- [过程重载](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)
- [重载](../../../visual-basic/language-reference/modifiers/overloads.md)
