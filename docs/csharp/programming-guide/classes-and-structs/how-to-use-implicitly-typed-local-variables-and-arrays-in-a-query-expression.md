---
title: 如何：在查询表达式中使用隐式类型本地变量和数组 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- implicitly-typed local variables [C#], how to use
ms.assetid: 6b7354d2-af79-427a-b6a8-f74eb8fd0b91
ms.openlocfilehash: 8e3534abf961ba7b8a41eed592455962e5b551e7
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56979029"
---
# <a name="how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression-c-programming-guide"></a>如何：在查询表达式中使用隐式类型本地变量和数组（C# 编程指南）
每当需要编译器确定本地变量类型时，均可使用隐式类型本地变量。 必须使用隐式类型本地变量来存储匿名类型，匿名类型通常用于查询表达式中。 以下示例说明了在查询中可以使用和必须使用隐式类型本地变量的情况。  
  
 隐式类型本地变量使用 [var](../../../csharp/language-reference/keywords/var.md) 上下文关键字进行声明。 有关详细信息，请参阅[隐式类型本地变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)和[隐式类型数组](../../../csharp/programming-guide/arrays/implicitly-typed-arrays.md)。  
  
## <a name="example"></a>示例  
 以下示例演示必须使用 `var` 关键字的常见情景：用于生成一系列匿名类型的查询表达式。 在此情景中，必须使用 `var` 隐式类型化 `foreach` 语句中的查询变量和迭代变量，因为你无权访问匿名类型的类型名称。 有关匿名类型的详细信息，请参阅[匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)。  
  
 [!code-csharp[csProgGuideLINQ#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#32)]  
  
## <a name="example"></a>示例  
 虽然以下示例在类似的情景中使用 `var` 关键字，但使用 `var` 是可选项。 因为 `student.LastName` 是字符串，所以执行查询将返回一系列字符串。 因此，`queryID` 的类型可声明为 `System.Collections.Generic.IEnumerable<string>`，而不是 `var`。 为方便起见，请使用关键字 `var`。 在示例中，虽然 `foreach` 语句中的迭代变量被显式类型化为字符串，但可改为使用 `var` 对其进行声明。 因为迭代变量的类型不是匿名类型，因此使用 `var` 是可选项，而不是必需项。 请记住，`var` 本身不是类型，而是发送给编译器用于推断和分配类型的指令。  
  
 [!code-csharp[csProgGuideLINQ#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#33)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [扩展方法](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)
- [LINQ（语言集成查询）](../../../csharp/linq/index.md)
- [var](../../../csharp/language-reference/keywords/var.md)
- [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)
