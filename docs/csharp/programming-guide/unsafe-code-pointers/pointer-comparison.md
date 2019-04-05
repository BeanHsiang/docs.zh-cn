---
title: 指针比较 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- pointers [C#], comparison
ms.assetid: fcafd514-7405-4deb-8490-cc58efda5495
ms.openlocfilehash: 5185bd5e1686858452efcc7c89e2c1977e094386
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56969201"
---
# <a name="pointer-comparison-c-programming-guide"></a>指针比较（C# 编程指南）
可以应用以下运算符比较任何类型的指针：  
  
 **==   !=   \<   >   \<=   >=**  
  
 比较运算符比较两个操作数的地址，如同它们是无符号整数。  
  
## <a name="example"></a>示例  
 [!code-csharp[csProgGuidePointers#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers2.cs#16)]  
  
 [!code-csharp[csProgGuidePointers#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers.cs#17)]  
  
## <a name="sample-output"></a>示例输出  
 `True`  
  
 `False`  
  
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
