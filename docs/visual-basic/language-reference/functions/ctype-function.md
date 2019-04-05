---
title: CType 函数 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.CType
helpviewer_keywords:
- expression conversion results
- explicit data type conversions [Visual Basic]
- CType function
- conversions [Visual Basic], expression
ms.assetid: dd4b29e7-6fa1-428c-877e-69955420bb72
ms.openlocfilehash: dbf01263723a9e2890dab57d5ffc3d467ed250fc
ms.sourcegitcommit: 79066169e93d9d65203028b21983574ad9dcf6b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57212048"
---
# <a name="ctype-function-visual-basic"></a>CType 函数 (Visual Basic)

返回表达式显式转换为指定的数据类型、 对象、 结构、 类或接口的结果。

## <a name="syntax"></a>语法

```
CType(expression, typename)
```

## <a name="parts"></a>部件

`expression` 任何有效表达式。 如果的值`expression`超出了允许的范围`typename`，Visual Basic 将引发异常。

`typename` 任何表达式内合法`As`子句中的`Dim`语句中，任何数据类型、 对象、 结构、 类或接口的名称。

## <a name="remarks"></a>备注

> [!TIP]
> 此外可以使用以下函数来执行类型转换：
>
> - 类型转换函数，如`CByte`， `CDbl`，和`CInt`，可以执行到特定的数据类型的转换。 有关详细信息，请参阅[类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)。
> - [DirectCast 运算符](../../../visual-basic/language-reference/operators/directcast-operator.md)或[TryCast 运算符](../../../visual-basic/language-reference/operators/trycast-operator.md)。 这些运算符要求一个类型继承自或实现另一个类型。 他们可以提供一定程度上更好的性能比`CType`来回进行转换时`Object`数据类型。

`CType` 采用内联方式编译，这意味着转换代码是计算表达式的值的代码的一部分。 在某些情况下，代码运行速度更快由于未调用过程来执行此转换。

如果未定义转换从`expression`到`typename`(例如，从`Integer`到`Date`)，Visual Basic 将显示一条编译时错误消息。

如果在运行时转换失败，引发相应异常。 如果收缩转换失败，<xref:System.OverflowException>是最常见的结果。 如果未定义转换，<xref:System.InvalidCastException>中引发。 例如，可能的原因`expression`属于类型`Object`并且其运行时类型具有不转换为`typename`。

如果的数据类型`expression`或`typename`是类或结构定义了，您可以定义`CType`类或结构为转换运算符上。 这使得`CType`充当*重载运算符*。 如果执行此操作，则可以控制之间的转换在类或结构，包括可能引发的异常的行为。

## <a name="overloading"></a>重载

`CType`还可以在类或结构在代码之外定义重载运算符。 如果你的代码需要在这样的类或结构之间进行转换，请确保您了解的行为及其`CType`运算符。 有关详细信息，请参阅 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。

## <a name="converting-dynamic-objects"></a>转换动态对象

通过用户定义的动态转换的使用进行的动态对象的类型转换<xref:System.Dynamic.DynamicObject.TryConvert%2A>或<xref:System.Dynamic.DynamicMetaObject.BindConvert%2A>方法。 如果你正在使用动态对象，请使用<xref:Microsoft.VisualBasic.Conversion.CTypeDynamic%2A>方法转换动态对象。

## <a name="example"></a>示例

下面的示例使用`CType`函数将转换为表达式`Single`数据类型。

[!code-vb[VbVbalrFunctions#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#24)]

有关其他示例，请参阅[隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)。

## <a name="see-also"></a>请参阅

- <xref:System.OverflowException>
- <xref:System.InvalidCastException>
- [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [转换函数](../../../visual-basic/language-reference/functions/conversion-functions.md)
- [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)
- [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [.NET Framework 中的类型转换](../../../standard/base-types/type-conversion.md)
