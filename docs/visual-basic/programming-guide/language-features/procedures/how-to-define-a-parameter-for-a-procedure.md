---
title: 如何：定义参数的过程 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- procedure parameters [Visual Basic], defining data types for
- procedures [Visual Basic], parameters
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedure parameters [Visual Basic], defining
ms.assetid: 7962808d-407e-4e84-984e-43e9857c53c9
ms.openlocfilehash: 01b150d70c07897f8217ed6958e3654aa28fdf51
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56971788"
---
# <a name="how-to-define-a-parameter-for-a-procedure-visual-basic"></a>如何：定义参数的过程 (Visual Basic)
一个*参数*允许调用代码将调用它时，将值传递给过程。 声明过程每个参数相同的方式声明变量，指定其名称和数据类型。 您还指定的传递机制，以及该参数是否可选。  
  
 有关详细信息，请参阅[过程形参和实参](./procedure-parameters-and-arguments.md)。  
  
### <a name="to-define-a-procedure-parameter"></a>若要定义过程参数  
  
1.  在过程声明中，将添加到过程的参数列表中，使用逗号将其与其他参数的参数名称。  
  
2.  决定参数的数据类型。  
  
3.  在参数名称后的加`As`子句指定的数据类型。  
  
4.  确定所需的参数的传递机制。 通常情况下，按值传递参数，除非你想要能够调用代码中更改其值的过程。  
  
5.  参数名称前面加上[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)指定的传递机制。 有关详细信息，请参阅[差异之间传递参数值和按引用来](./differences-between-passing-an-argument-by-value-and-by-reference.md)。  
  
6.  如果参数是可选的前, 加上使用的传递机制[可选](../../../../visual-basic/language-reference/modifiers/optional.md)并按照参数的数据类型以等号 (`=`) 和默认值。  
  
     下面的示例定义的大纲`Sub`具有三个参数的过程。 所需的前两个和第三个是可选的。 参数声明由逗号分隔参数列表中。  
  
     [!code-vb[VbVbcnProcedures#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#33)]  
  
     第一个参数接受`customer`对象，并`updateCustomer`可以直接更新变量传递给`c`因为将实参传递[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)。 该过程不能更改的最后两个参数的值，因为它们的传递[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)。  
  
     如果调用代码不会提供的值`level`参数，Visual Basic 将其设置为默认值为 0。  
  
     如果类型检查开关 ([Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) 是`Off`，则`As`子句是可选的时定义的参数。 但是，如果任何一个参数使用`As`子句中，所有这些必须使用它。 如果类型检查开关`On`，则`As`子句是必需的每个参数定义。  
  
     指定所有编程元素的数据类型被称为*强类型化*。 当您将设置`Option Strict On`，Visual Basic 强制实施强类型化。 这是强烈建议，原因如下：  
  
    -   这样，对变量和参数的 IntelliSense 支持。 这样可以查看其属性和其他成员，当您键入代码。  
  
    -   它允许编译器执行类型检查。 这有助于 catch 语句可以在运行时因等溢出错误而失败。 不支持它们的对象，它还捕获对方法的调用。  
  
    -   这会导致代码更快地执行。 原因之一就是，如果不指定编程元素的数据类型，Visual Basic 编译器为其分配`Object`类型。 已编译的代码可能需要将之间来回转换`Object`和其他数据类型，这会降低性能。  
  
## <a name="see-also"></a>请参阅

- [过程](./index.md)
- [Sub 过程](./sub-procedures.md)
- [Function 过程](./function-procedures.md)
- [如何：将参数传递给过程](./how-to-pass-arguments-to-a-procedure.md)
- [按值和按引用传递自变量](./passing-arguments-by-value-and-by-reference.md)
- [递归过程](./recursive-procedures.md)
- [过程重载](./procedure-overloading.md)
- [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [面向对象的编程 (Visual Basic)](../../concepts/object-oriented-programming.md)
