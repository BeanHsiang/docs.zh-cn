---
title: as - C# 参考
ms.custom: seodec18
ms.date: 10/11/2018
f1_keywords:
- as_CSharpKeyword
- as
helpviewer_keywords:
- type conversion [C#], as keyword
- as keyword [C#]
ms.assetid: a9be126b-cbf4-4990-a70d-d0e1983cad0e
ms.openlocfilehash: 33f7971a95b8573168da11d2bd2abc80fa74370e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54736463"
---
# <a name="as-c-reference"></a>as（C# 参考）
可以使用 `as` 运算符在符合的引用类型或[可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)之间执行某些类型的转换。 以下代码显示一个示例。  
  
[!code-csharp[csrefKeywordsOperator#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#1)]

如示例所示，需要比较 `as` 表达式和 `null` 的结果以检查转换是否成功。 从 C# 7.0 开始，可以使用 [is](is.md) 表达式来测试转换是否成功，并在转换成功时有条件地分配变量。 在许多情况下，它比使用 `as` 运算符更简洁。 有关详细信息，请参阅 [`is` 运算符](is.md)一文中的[类型模式](is.md#type)部分。
  
## <a name="remarks"></a>备注  
 `as` 运算符类似于转换运算。 但是，如果无法进行转换，则 `as` 会返回 `null`，而不是引发异常。 请看下面的示例：  
  
```csharp  
expression as type  
```  
  
 该代码等效于以下表达式，但 `expression` 变量仅进行一次计算。  
  
```csharp  
expression is type ? (type)expression : (type)null  
```  
  
 请注意，`as` 运算符仅执行引用转换、可以为 null 的转换和装箱转换。 `as` 运算符无法执行其他转换，例如用户定义的转换，应使用转换表达式执行此转换。  
  
## <a name="example"></a>示例  

[!code-csharp[csrefKeywordsOperator#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#2)]
  
## <a name="c-language-specification"></a>C# 语言规范  

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的 [As 运算符](~/_csharplang/spec/expressions.md#the-as-operator)。 该语言规范是 C# 语法和用法的权威资料。
 
## <a name="see-also"></a>请参阅
- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](../../../csharp/language-reference/keywords/index.md)
- [is](../../../csharp/language-reference/keywords/is.md)
- [?:运算符](../../../csharp/language-reference/operators/conditional-operator.md)
- [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)
