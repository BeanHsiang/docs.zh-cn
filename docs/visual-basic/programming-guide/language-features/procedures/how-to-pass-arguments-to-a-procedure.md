---
title: 如何：将参数传递给过程 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- arguments [Visual Basic], passing to procedures
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], calling
- argument passing [Visual Basic], procedures
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
ms.openlocfilehash: 0bc7c9d09922b7fbef534e6b58389ca343cc1e13
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56974388"
---
# <a name="how-to-pass-arguments-to-a-procedure-visual-basic"></a>如何：将参数传递给过程 (Visual Basic)
在调用过程时，过程名后面加上括号中的参数列表。 你提供该过程定义，对应于每个所需的参数的自变量，则可以选择提供参数`Optional`参数。 如果不提供`Optional`中调用的参数，必须包含一个逗号来标记其原位置自变量列表中的，如果你提供的任何后续自变量。  
  
 如果你想要的自变量传递的数据类型不同于其相应的参数，如`Byte`到`String`，可以设置类型检查开关 ([Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) 到`Off`。 如果`Option Strict`是`On`，则必须使用扩大转换或显式转换关键字。 有关详细信息，请参阅[Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)并[类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)。  
  
 有关详细信息，请参阅[过程形参和实参](./procedure-parameters-and-arguments.md)。  
  
### <a name="to-pass-one-or-more-arguments-to-a-procedure"></a>若要将一个或多个自变量传递给过程  
  
1.  在调用语句中，过程名后面加上括号。  
  
2.  在圆括号内放置的参数列表。 包括每个所需的参数的参数定义了该过程，以及用逗号分隔参数。  
  
3.  请确保每个自变量是有效的表达式的计算结果为一个数据类型可转换为该过程的类型定义的相应参数。  
  
4.  如果参数指[可选](../../../../visual-basic/language-reference/modifiers/optional.md)，可以将其包含在参数列表或省略此参数。 如果省略此参数，该过程将使用为该参数定义的默认值。  
  
5.  如果省略参数`Optional`参数和另一个参数之后没有它的参数列表中，可以将省略自变量的位置标记的参数列表中一个多余的逗号。  
  
     下面的示例调用 Visual Basic<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>函数。  
  
     [!code-vb[VbVbcnProcedures#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#34)]  
  
     前面的示例中提供了所需的第一个参数，它是要显示的消息字符串。 它会省略了可选的第二个参数，它指定要在消息框上显示的按钮的参数。 在调用不会提供一个值，因为`MsgBox`使用默认值`MsgBoxStyle.OKOnly`，后者将仅显示**确定**按钮。  
  
     参数列表中的第二个逗号将标记省略的第二个参数的位置和最后一个字符串传递给第三个可选参数`MsgBox`，这是要在标题栏中显示的文本。  
  
## <a name="see-also"></a>请参阅

- [Sub 过程](./sub-procedures.md)
- [Function 过程](./function-procedures.md)
- [属性过程](./property-procedures.md)
- [运算符过程](./operator-procedures.md)
- [如何：为过程定义参数](./how-to-define-a-parameter-for-a-procedure.md)
- [按值和按引用传递自变量](./passing-arguments-by-value-and-by-reference.md)
- [递归过程](./recursive-procedures.md)
- [过程重载](./procedure-overloading.md)
- [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [面向对象的编程 (Visual Basic)](../../concepts/object-oriented-programming.md)
