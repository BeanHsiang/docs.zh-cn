---
title: 如何：递增和递减指针 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- pointers [C#], increment and decrement
- pointer expressions [C#], increment and decrement
ms.assetid: 1b8b9281-44ee-485a-9045-3db38a4b4b89
ms.openlocfilehash: 358decb73666d5a5ef7c0fa828168d90d2c22c1e
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56973699"
---
# <a name="how-to-increment-and-decrement-pointers-c-programming-guide"></a>如何：递增和递减指针（C# 编程指南）

使用增量运算符 (`++`) 和减量运算符 (`--`)，通过 `pointer-type*` 类型指针的 `sizeof(pointer-type)` 更改指针位置。 增量和减量表达式的形式如下：  
  
```csharp
++p;  
p++;  
--p;  
p--;  
```  
  
 增量和减量运算符可应用于除 `void*` 类型以外的任何类型的指针。  
  
 对 `pointer-type*` 类型的指针应用增量运算符的效果是向指针变量中包含的地址增加 `sizeof(pointer-type)`。  
  
 对 `pointer-type*` 类型的指针应用减量运算符的效果是从指针变量中包含的地址减去 `sizeof(pointer-type)`。  
  
 运算溢出指针范围时，不会产生异常，并且结果取决于实现。  
  
## <a name="example"></a>示例  
 在此示例中，通过按 `int` 大小递增指针单步调试数组。 每一步都将显示数组元素的地址和内容。  
  
 [!code-csharp[csProgGuidePointers#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers2.cs#3)]  
  
 [!code-csharp[csProgGuidePointers#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers.cs#13)]  
  
**Value:0 @ Address:12860272**
**Value:1 @ Address:12860276**
**Value:2 @ Address:12860280**
**Value:3 @ Address:12860284**
**Value:4 @ Address:12860288**

## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)
- [C# 运算符](../../../csharp/language-reference/operators/index.md)
- [操作指针](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)
- [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)
- [类型](../../../csharp/language-reference/keywords/types.md)
- [unsafe](../../../csharp/language-reference/keywords/unsafe.md)
- [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)
- [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)
- [sizeof](../../../csharp/language-reference/keywords/sizeof.md)
