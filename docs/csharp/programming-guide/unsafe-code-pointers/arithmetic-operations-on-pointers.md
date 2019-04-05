---
title: 指针算术运算 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- pointers [C#], arithmetic operations
ms.assetid: d4f0b623-827e-45ce-8649-cfcebc8692aa
ms.openlocfilehash: bfa81bc926b4fe81455cecb88bc55f4dcd69268e
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56977833"
---
# <a name="arithmetic-operations-on-pointers-c-programming-guide"></a>指针的算术运算（C# 编程指南）
本主题讨论如何使用算术运算符 `+` 和 `-` 操作指针。  
  
> [!NOTE]
>  不能对 void 指针执行任何算术运算。  
  
## <a name="adding-and-subtracting-numeric-values-to-or-from-pointers"></a>对指针执行加减数值操作  
 可以将类型为 [int](../../../csharp/language-reference/keywords/int.md)、[uint](../../../csharp/language-reference/keywords/uint.md)、[long](../../../csharp/language-reference/keywords/long.md) 或 [ulong](../../../csharp/language-reference/keywords/ulong.md) 的值 `n` 与指针相加。 如果 `p` 是 `pointer-type*` 类型的指针，`p+n` 结果是将 `n * sizeof(pointer-type)` 添加到 `p` 的地址所产生的指针。 同样，`p-n` 是从 `p` 的地址中减去 `n * sizeof(pointer-type)` 得到的指针。  
  
## <a name="subtracting-pointers"></a>指针相减  
 也可以对相同类型的指针进行减法运算。 计算结果的类型始终为 `long`。 例如，如果 `p1` 和 `p2` 都是类型为 `pointer-type*` 的指针，则表达式 `p1-p2` 的计算结果为：  
  
 `((long)p1 - (long)p2)/sizeof(pointer-type)`  
  
 当算术运算溢出指针范围时，不会产生异常，并且结果取决于实现。  
  
## <a name="example"></a>示例  
 [!code-csharp[csProgGuidePointers#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers2.cs#14)]  
  
 [!code-csharp[csProgGuidePointers#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers.cs#15)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [不安全代码和指针](../../../csharp/programming-guide/unsafe-code-pointers/index.md)
- [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)
- [C# 运算符](../../../csharp/language-reference/operators/index.md)
- [操作指针](../../../csharp/programming-guide/unsafe-code-pointers/manipulating-pointers.md)
- [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)
- [类型](../../../csharp/language-reference/keywords/types.md)
- [unsafe](../../../csharp/language-reference/keywords/unsafe.md)
- [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)
- [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)
