---
title: bool 关键字 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- bool_CSharpKeyword
- bool
helpviewer_keywords:
- bool keyword [C#]
ms.assetid: 551cfe35-2632-4343-af49-33ad12da08e2
ms.openlocfilehash: 958b58b31193dbf4c03709e4ab7ba38f7f30e0ac
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54590470"
---
# <a name="bool-c-reference"></a>bool（C# 参考）

`bool` 关键字是 <xref:System.Boolean?displayProperty=nameWithType> 的别名。 它用于声明变量来存储布尔值：[true](true-literal.md) 和 [false](false-literal.md)。

> [!NOTE]
> 如果需要一个也可以有 `null` 值的布尔型变量，请使用 `bool?`。 有关详细信息，请参阅[使用可以为空的类型](../../programming-guide/nullable-types/using-nullable-types.md)一文的 [bool? 类型](../../programming-guide/nullable-types/using-nullable-types.md#the-bool-type)部分。

## <a name="literals"></a>文本

可将布尔值赋给 `bool` 变量。 也可以将计算结果为 `bool` 类型的表达式赋给 `bool` 变量。

[!code-csharp[csrefKeywordsTypes#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#1)]

`bool` 变量的默认值为 `false`。 `bool?` 变量的默认值为 `null`。

## <a name="conversions"></a>转换

在 C++ 中，`bool` 类型的值可转换为 `int` 类型的值；也就是说，`false` 等效于零值，而 `true` 等效于非零值。 在 C# 中，不存在 `bool` 类型与其他类型之间的相互转换。 例如，下面的 `if` 语句在 C# 中无效：

[!code-csharp[csrefKeywordsTypes#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#2)]

若要测试 `int` 类型的变量，必须将该变量与一个值（例如零）进行显式比较，如下所示：

[!code-csharp[csrefKeywordsTypes#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#3)]

## <a name="example"></a>示例

在此例中，你通过键盘输入一个字符，然后程序检查输入的字符是否是一个字母。 如果字符是一个字母，则程序检查它是大写还是小写。 执行这些检查使用的是 <xref:System.Char.IsLetter%2A> 和 <xref:System.Char.IsLower%2A>，二者均返回 `bool` 类型：

[!code-csharp[csrefKeywordsTypes#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#4)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](../../../csharp/language-reference/keywords/index.md)
- [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)
- [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)
- [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)
- [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
