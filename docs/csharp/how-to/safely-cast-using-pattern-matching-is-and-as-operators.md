---
title: 如何：使用模式匹配以及 is 和 as 运算符安全地进行强制转换
description: 了解如何使用模式匹配方法将变量安全地转换为其他类型。 可以使用模式匹配以及 is 和 as 运算符来安全地转换类型。
ms.date: 09/05/2018
helpviewer_keywords:
- cast operators [C#], as and is operators
- as operator [C#]
- is operator [C#]
ms.openlocfilehash: 4e0eb53a44a6348d0f5154a0a08222da90985864
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53149310"
---
# <a name="how-to-safely-cast-by-using-pattern-matching-is-and-as-operators"></a>如何：使用模式匹配 is 和 as 运算符安全地进行强制转换

由于是多态对象，基类类型的变量可以保存派生[类型](../programming-guide/types/index.md)。 要访问派生类型的实例成员，必须将值[强制转换](../programming-guide/types/casting-and-type-conversions.md)回派生类型。 但是，强制转换会引发 <xref:System.InvalidCastException> 风险。 C# 提供[模式匹配](../pattern-matching.md)语句，该语句只有在成功时才会有条件地执行强制转换。 C# 还提供 [is](../language-reference/keywords/is.md) 和 [as](../language-reference/keywords/as.md) 运算符来测试值是否属于特定类型。

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

下面的代码演示模式匹配 `is` 语句。 它包含测试方法参数的方法，以确定它是否是一组可能的派生类型：

[!code-csharp-interactive[Pattern matching is statement](../../../samples/snippets/csharp/how-to/safelycast/patternmatching/Program.cs#PatternMatchingIs)]

前面的示例演示了模式匹配语法的一些功能。 `if (a is Mammal m)` 和 `if (o is Mammal m)` 语句将测试与初始化赋值相结合。 只有在测试成功时才会进行赋值。 变量 `m` 仅在已赋值的嵌入式 `if` 语句的范围内。 以后无法在同一方法中访问 `m`。 在交互式窗口中尝试操作。

也可以使用同一语法来测试[可以为 null 的类型](../programming-guide/nullable-types/index.md)是否具有值，如以下示例代码所示：

[!code-csharp-interactive[Pattern matching with nullable types](../../../samples/snippets/csharp/how-to/safelycast/nullablepatternmatching/Program.cs#PatternMatchingNullable)]

前面的示例演示了模式匹配用于转换的其他功能。 可以通过专门检查 `null` 值来测试 NULL 模式的变量。 当变量的运行时值为 `null` 时，用于检查类型的 `is` 语句始终返回 `false`。 模式匹配 `is` 语句不允许可以为 null 值的类型，如 `int?` 或 `Nullable<int>`，但你可以测试任何其他值类型。

前面的示例还演示如何在变量为其他类型的 `switch` 语句中使用模式匹配 `is` 表达式。

如果想要测试变量是否为给定类型，但不将其分配给新变量，则可以对引用类型和可以为 null 的类型使用 `is` 和 `as` 运算符。 以下代码演示如何在引入模式匹配以测试变量是否为给定类型前，使用 C# 语言中的 `is` 和 `as` 语句：

[!code-csharp-interactive[testing variable types with the is and as statements](../../../samples/snippets/csharp/how-to/safelycast/asandis/Program.cs#IsAndAs)]

正如你所看到的，将此代码与模式匹配代码进行比较，模式匹配语法通过在单个语句中结合测试和赋值来提供更强大的功能。 尽量使用模式匹配语法。

可通过查看 [GitHub 存储库](https://github.com/dotnet/samples/tree/master/snippets/csharp/how-to/safelycast)中的代码来尝试这些示例。 也可以下载这些示例的 [zip 文件](https://github.com/dotnet/samples/raw/master/snippets/csharp/how-to/safelycast.zip)。
