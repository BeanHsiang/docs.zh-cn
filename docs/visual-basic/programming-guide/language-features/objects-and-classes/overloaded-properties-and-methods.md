---
title: 重载的属性和方法 (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- properties [Visual Basic], overloading
- methods [Visual Basic], overloading
- shadowing
- names [Visual Basic], multiple procedures with same
- procedures [Visual Basic], multiples with same name
- classes [Visual Basic], properties
- classes [Visual Basic], methods
- method overloading
- Overloads keyword [Visual Basic], overloaded members
ms.assetid: b686fb97-e7d7-4001-afaa-6650cba08f0d
ms.openlocfilehash: 8d7341370d9770d2e57f786ac7c68277e66a9bbd
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57677391"
---
# <a name="overloaded-properties-and-methods-visual-basic"></a>重载的属性和方法 (Visual Basic)

重载是创建多个过程、 实例构造函数或属性中具有相同名称但不同的参数类型的类。

## <a name="overloading-usage"></a>重载使用情况

当您的对象模型指示你使用有关对不同的数据类型进行操作的过程相同的名称，则重载是特别有用。 例如，可以显示多种不同的数据类型的类可以具有`Display`过程如下所示：

[!code-vb[VbVbalrOOP#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#64)]

无需使用重载，您将需要创建不同的名称，对于每个过程，即使它们执行相同的操作中，按如下所示：

[!code-vb[VbVbalrOOP#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#65)]

重载，使得更轻松地使用属性或方法，因为它提供了可用的数据类型的选择。 例如，重载`Display`之前可以使用以下代码行的任何调用所述的方法：

[!code-vb[VbVbalrOOP#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#66)]

在运行时，Visual Basic 调用正确的过程基于你指定的参数的数据类型。

## <a name="overloading-rules"></a>重载规则

 通过添加两个或多个属性或方法具有相同名称创建一个类的重载的成员。 除非是重载派生的成员，每个重载的成员必须具有不同的参数列表和重载属性或过程时，不能作为区别性功能使用以下各项：

- 修饰符，如`ByVal`或`ByRef`，适用于成员或该成员的参数。

- 参数的名称

- 返回类型的过程

`Overloads`关键字是可选的重载时，但如果任一重载成员均使用`Overloads`关键字，则所有其他重载的成员具有相同名称还必须指定此关键字。

派生的类可以重载具有相同的参数和参数类型，该过程称为的成员的继承的成员*按名称和签名隐藏*。 如果`Overloads`按名称和签名隐藏，成员的派生的类的实现将使用而不是在基类中实现且该成员的所有其他重载将可供使用的实例时，使用关键字在派生的类。

如果`Overloads`重载继承的成员具有相同的参数和参数类型的成员时省略了关键字，则该重载称为*按名称隐藏*。 按名称隐藏替换继承的成员，实现并使所有其他重载到派生的类和其对于实例不可用。

`Overloads`和`Shadows`修饰符不能同时使用具有相同属性或方法。

### <a name="example"></a>示例

下面的示例创建重载的方法均接受`String`或`Decimal`的美元金额限度并返回一个包含销售税的字符串表示形式。

#### <a name="to-use-this-example-to-create-an-overloaded-method"></a>若要使用此示例创建一个重载的方法

1. 打开新项目并添加一个名为类`TaxClass`。

2. 向 `TaxClass` 类添加下面的代码。

    [!code-vb[VbVbalrOOP#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#67)]

3. 将以下过程添加到你的窗体。

    [!code-vb[VbVbalrOOP#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#68)]

4. 将按钮添加到表单中，然后调用`ShowTax`过程从`Button1_Click`按钮的事件。

5. 运行该项目并单击要测试的重载的窗体上的按钮`ShowTax`过程。

在运行时，编译器将选择与正在使用的参数匹配的适当重载的函数。 重载的方法时单击按钮时，使用第一次调用`Price`参数，它是一个字符串，该消息，"价格是一个字符串。 税务是 $5.12"显示。 `TaxAmount` 使用调用`Decimal`值的第二个时间和消息，"价格是十进制数字。 税务是 $5.12"显示。

## <a name="see-also"></a>请参阅

- [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [在 Visual Basic 中隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)
- [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)
- [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
- [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
- [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)
- [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)
- [重载](../../../../visual-basic/language-reference/modifiers/overloads.md)
- [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)
