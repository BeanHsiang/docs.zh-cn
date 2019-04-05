---
title: 如何使用指针访问数组元素 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- pointers [C#], array access
ms.assetid: 6c46f2af-a730-4855-8638-f136d9abaa12
ms.openlocfilehash: 7b2991776ca032aa53111187a061835725cfe223
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56965600"
---
# <a name="how-to-access-an-array-element-with-a-pointer-c-programming-guide"></a>如何使用指针访问数组元素（C# 编程指南）

在不安全的上下文中，可通过指针元素访问来访问内存中的元素，如下方示例所示：

```csharp
char* charPointer = stackalloc char[123];
for (int i = 65; i < 123; i++)
{
    charPointer[i] = (char)i; //access array elements
}
```

方括号中的表达式必须可隐式转换为 `int`、`uint`、`long` 或 `ulong`。 `p[e]` 操作等效于 `*(p+e)`。 与 C 和 C++ 一样，指针元素访问不检查越界错误。

## <a name="example"></a>示例

此示例中，向字符数组 `charPointer` 分配了 123 个内存位置。 此数组用于显示两个 [for](../../../csharp/language-reference/keywords/for.md) 循环中的小写字母和大写字母。

请注意，表达式 `charPointer[i]` 等效于表达式 `*(charPointer + i)`，使用这两个表达式中任何一个获得的结果相同。

 [!code-csharp[csProgGuidePointers#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers2.cs#11)]

 [!code-csharp[csProgGuidePointers#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuidePointers/CS/Pointers.cs#12)]

大写字母：  
ABCDEFGHIJKLMNOPQRSTUVWXYZ  
小写字母：  
abcdefghijklmnopqrstuvwxyz  

## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [指针表达式](../../../csharp/programming-guide/unsafe-code-pointers/pointer-expressions.md)
- [指针类型](../../../csharp/programming-guide/unsafe-code-pointers/pointer-types.md)
- [类型](../../../csharp/language-reference/keywords/types.md)
- [unsafe](../../../csharp/language-reference/keywords/unsafe.md)
- [fixed 语句](../../../csharp/language-reference/keywords/fixed-statement.md)
- [stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)
