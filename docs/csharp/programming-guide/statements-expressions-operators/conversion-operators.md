---
title: 转换运算符 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, conversion operators
- conversion operators [C#]
- operators [C#], conversion
- user-defined conversions [C#]
ms.assetid: c5ad73a3-d57b-4d2b-b4c9-24e3c2856efc
ms.openlocfilehash: 539a554da2ea2f785a54bd7e5ff81d09b908c9e4
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56965210"
---
# <a name="conversion-operators-c-programming-guide"></a>转换运算符（C# 编程指南）

C# 允许程序员在类或结构上声明转换，以便类或结构能够与其他类或结构或者基本类型进行相互转换。 以类似于运算符的方式定义转换，并根据它们所转换为的类型命名。 要转换的参数类型或转换结果的类型必须是包含类型（但不能两者同时都是）。  
  
 [!code-csharp[csProgGuideStatements#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#10)]  
  
## <a name="conversion-operators-overview"></a>转换运算符概述

 转换运算符具有以下属性：  
  
-   声明为 `implicit` 的转换在需要时自动执行。  
  
-   声明为 `explicit` 的转换需要调用强制转换。  
  
-   所有转换都必须都声明为 `static`。  
  
## <a name="related-sections"></a>相关章节

 更多相关信息：  
  
-   [使用转换运算符](../../../csharp/programming-guide/statements-expressions-operators/using-conversion-operators.md)  
  
-   [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)  
  
-   [如何：在结构之间实现用户定义的转换](../../../csharp/programming-guide/statements-expressions-operators/how-to-implement-user-defined-conversions-between-structs.md)  
  
-   [explicit](../../../csharp/language-reference/keywords/explicit.md)  
  
-   [implicit](../../../csharp/language-reference/keywords/implicit.md)  
  
-   [static](../../../csharp/language-reference/keywords/static.md)  
  
## <a name="see-also"></a>请参阅

- <xref:System.Convert>
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [Chained user-defined explicit conversions in C#](https://blogs.msdn.microsoft.com/ericlippert/2007/04/16/chained-user-defined-explicit-conversions-in-c/)（C# 中链接在一起的用户定义的显式转换）
