---
title: 重载过程注意事项 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- signatures [Visual Basic], ParamArray arguments
- ParamArray keyword [Visual Basic], parameter arrays
- ParamArray keyword [Visual Basic], arguments and signatures
- function overloading [Visual Basic], implicit overloads for ParamArray
- ParamArray keyword [Visual Basic], signatures
- Visual Basic code, procedures
- arguments [Visual Basic], parameter arrays
- procedures [Visual Basic], overloading
- parameters [Visual Basic], lists
- function overloading [Visual Basic], typeless programming
- typeless programming
- function overloading [Visual Basic], restrictions
- arguments [Visual Basic], optional
- optional arguments [Visual Basic], overloading
- signatures [Visual Basic], procedure
- parameter lists [Visual Basic]
- parameter arrays [Visual Basic], overloading arguments
- Visual Basic code, parameter lists
- procedure overloading [Visual Basic], considerations
- Option Explicit statement [Visual Basic]
- restrictions [Visual Basic], overloading procedures
- procedures [Visual Basic], parameter lists
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
ms.openlocfilehash: f14cc28960af28530bda9a78c1309dea10c18b8f
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58815583"
---
# <a name="considerations-in-overloading-procedures-visual-basic"></a>重载过程注意事项 (Visual Basic)
重载的过程，您必须使用不同*签名*为每个重载版本。 这通常意味着每个版本必须指定不同的参数列表。 详细信息，请参阅"不同的签名"中[过程重载](./procedure-overloading.md)。  
  
 可重载`Function`过程使用`Sub`过程中，反之亦然，只要它们具有不同的签名和。 仅在于其中一个的返回值，另一个不，不能区分两个重载。  
  
 可重载属性相同的方式重载的过程，并采用相同的限制。 但是，不能重载的过程与属性，反之亦然。  
  
## <a name="alternatives-to-overloaded-versions"></a>重载版本的替代方法  
 尤其是在的参数是可选的参数或其数量可变时，有时必须重载版本的替代方法。  
  
 请记住，可选参数不是支持的所有语言和参数数组限制为 Visual Basic。 如果你正在编写很可能在任何几种不同语言编写的代码中调用的过程，重载版本的产品/服务最大的灵活性。  
  
### <a name="overloads-and-optional-arguments"></a>重载和可选自变量  
 当调用代码可以根据需要提供或省略一个或多个自变量时，可以定义多个重载的版本，或使用可选参数。  
  
#### <a name="when-to-use-overloaded-versions"></a>何时使用重载的版本  
 您可以考虑在以下情况下定义一系列的重载版本：  
  
-   在过程代码中的逻辑是具体取决于是否调用代码提供的可选参数，或不明显不同。  
  
-   过程代码不能可靠地测试是否调用代码已提供的可选参数。 这种情况，例如，如果没有备选的默认值对于调用的代码可能不需要提供。  
  
#### <a name="when-to-use-optional-parameters"></a>何时使用可选参数  
 你可能希望在以下情况下的一个或多个可选参数：  
  
-   唯一所需的操作时调用的代码不会提供一个可选参数是将参数设置为默认值。 在这种情况下，过程代码可以降低复杂程度如果定义一个或多个与单个版本`Optional`参数。  
  
 有关详细信息，请参阅[可选参数](./optional-parameters.md)。  
  
### <a name="overloads-and-paramarrays"></a>参数和重载  
 如果调用代码可以通过数目可变的参数，可以定义多个重载的版本，或使用参数数组。  
  
#### <a name="when-to-use-overloaded-versions"></a>何时使用重载的版本  
 您可以考虑在以下情况下定义一系列的重载版本：  
  
-   您知道，调用代码永远不会将传递数超过了小的值给参数数组。  
  
-   在过程代码中的逻辑是明显不同，具体取决于调用代码传递的多少个值。  
  
-   调用代码可以通过不同的数据类型的值。  
  
#### <a name="when-to-use-a-parameter-array"></a>何时使用参数数组  
 你会更好`ParamArray`在以下情况下的参数：  
  
-   您不能预测多少个值调用代码可以将传递给参数数组，它可能是大量。  
  
-   过程逻辑本身适于循环访问所有通过调用代码，执行的每个值实质上是相同的操作的值。  
  
 有关详细信息，请参阅[参数数组](./parameter-arrays.md)。  
  
## <a name="implicit-overloads-for-optional-parameters"></a>可选参数的隐式重载  
 使用过程[可选](../../../../visual-basic/language-reference/modifiers/optional.md)参数相当于两个重载过程，一个具有可选参数，而无需它的一个。 不能重载带有对应于任何一种方法的参数列表的此类的过程。 下面的声明说明这一点。  
  
 [!code-vb[VbVbcnProcedures#58](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#58)]  
  
 [!code-vb[VbVbcnProcedures#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#60)]  
  
 [!code-vb[VbVbcnProcedures#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#61)]  
  
 对于具有多个可选参数的过程，没有隐式重载，到达由逻辑类似于前面的示例中的一组。  
  
## <a name="implicit-overloads-for-a-paramarray-parameter"></a>ParamArray 参数的隐式重载  
 编译器会考虑使用为过程[ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)参数具有无限数目的重载，不同于彼此中调用代码传递的内容到参数的数组，如下所示：  
  
-   调用代码未提供的参数的一个重载 `ParamArray`  
  
-   调用代码时提供的一维数组的一个重载`ParamArray`元素类型  
  
-   对于每个正整数，其中一个重载的调用代码提供该数量的参数，每个时`ParamArray`元素类型  
  
 下面的声明演示了这些隐式重载。  
  
 [!code-vb[VbVbcnProcedures#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#68)]  
  
 [!code-vb[VbVbcnProcedures#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#70)]  
  
 不能重载采用一维数组的参数数组的参数列表的此类的过程。 但是，可以使用其他隐式重载的签名。 下面的声明说明这一点。  
  
 [!code-vb[VbVbcnProcedures#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#71)]  
  
## <a name="typeless-programming-as-an-alternative-to-overloading"></a>作为一种替代方法重载无类型编程  
 如果你想要允许调用代码将传递给参数的不同数据类型，另一种方法是无类型编程。 可以设置类型检查开关`Off`带有[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)或[/optionstrict](../../../../visual-basic/reference/command-line-compiler/optionstrict.md)编译器选项。 然后无需声明参数的数据类型。 但是，这种方法具有以下缺点相比重载：  
  
-   无类型编程生成效率较低的执行代码。  
  
-   该过程必须测试预期将传递的每个数据类型。  
  
-   如果调用代码传递过程不支持的数据类型，编译器不能发出错误信号。  
  
## <a name="see-also"></a>请参阅

- [过程](./index.md)
- [过程参数和自变量](./procedure-parameters-and-arguments.md)
- [过程疑难解答](./troubleshooting-procedures.md)
- [如何：定义一个过程的多个版本](./how-to-define-multiple-versions-of-a-procedure.md)
- [如何：调用重载的过程](./how-to-call-an-overloaded-procedure.md)
- [如何：重载带有可选参数的过程](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [如何：重载的参数数量不确定的过程](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [重载决策](./overload-resolution.md)
- [重载](../../../../visual-basic/language-reference/modifiers/overloads.md)
