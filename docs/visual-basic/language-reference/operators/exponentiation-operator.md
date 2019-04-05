---
title: ^ 运算符 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.^
helpviewer_keywords:
- raising numbers to powers
- ^ operator [Visual Basic], exponentiation
- square operator [Visual Basic]
- ^ operator [Visual Basic]
- exponentiation operator [Visual Basic]
- exponent
- numbers [Visual Basic], rasing
- powers
- arithmetic operators [Visual Basic], exponentiation
ms.assetid: d89a1ca8-83da-4784-a87b-a9d7dceb3f62
ms.openlocfilehash: 54de9c91d4e166b8ca1733952dfa9c98ebf11ffe
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57674089"
---
# <a name="-operator-visual-basic"></a>^ 运算符 (Visual Basic)

引发到另一个数字的幂的数字。

## <a name="syntax"></a>语法

```
number ^ exponent
```

## <a name="parts"></a>部件

`number`\
必需。 任何数值表达式。

`exponent`\
必需。 任何数值表达式。

## <a name="result"></a>结果

结果是`number`次的幂`exponent`，始终为`Double`值。

## <a name="supported-types"></a>支持的类型

`Double`。 任何其他类型的操作数将转换为`Double`。

## <a name="remarks"></a>备注

Visual Basic 始终执行中的求幂[双精度数据类型](../../../visual-basic/language-reference/data-types/double-data-type.md)。

值`exponent`可以是小数，负号，或两者。

当在单个表达式中执行多个求幂`^`运算符从左到右出现的顺序进行计算。

> [!NOTE]
> `^`运算符可以被*重载*，这意味着，某个类或结构可以重新定义其行为时，操作数的类或结构的类型。 如果你的代码对此类的类或结构使用此运算符，请确保了解其被重新定义的行为。 有关详细信息，请参阅 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。

## <a name="example"></a>示例

下面的示例使用`^`运算符为指数的幂数。 结果是第一个操作数的次幂的第二个。

[!code-vb[VbVbalrOperators#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#20)]

前面的示例生成以下结果：

`exp1` 设置为 4 (平方的 2)。

`exp2` 设置为 19683 (3 立方，然后立方值)。

`exp3` 设置为-125 (-5 的立方)。

`exp4` 设置为 625 (-5 的四次幂)。

`exp5` 设置为 2 （8 的立方根）。

`exp6` 设置为 0.5 (1.0 除以 8 的立方根)。

请注意前面示例中的表达式中的括号的重要性。 由于*运算符优先级*，通常情况下，Visual Basic 执行`^`运算符先于任何其他，甚至是一元`–`运算符。 如果`exp4`和`exp6`计算时不带括号，将会产生以下结果：

`exp4 = -5 ^ 4` 将计算为 – (5 四次幂)，这会导致-625。

`exp6 = 8 ^ -1.0 / 3.0` 将计算为 (8 – 1 电源或 0.125) 除以 3.0，这将导致 0.041666666666666666666666666666667。

## <a name="see-also"></a>请参阅

- [^= 运算符](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)
- [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [在 Visual Basic 中的算术运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
