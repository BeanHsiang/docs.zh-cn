---
title: 数组 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [C#]
- C# language, arrays
ms.assetid: bb79bdde-e570-4c30-adb0-1dd5759ae041
ms.openlocfilehash: 1b1a3d2e61507a497349deeb857e4333356f66a5
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857796"
---
# <a name="arrays-c-programming-guide"></a>数组（C# 编程指南）

可以将同一类型的多个变量存储在一个数组数据结构中。 通过指定数组的元素类型来声明数组。  
  
 `type[] arrayName;`  
  
 下面的示例创建一维数组、多维数组和交错数组：  
  
 [!code-csharp[csProgGuideArrays#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideArrays/CS/Arrays.cs#1)]  
  
## <a name="array-overview"></a>数组概述

 数组具有以下属性：  
  
-   数组可以是[一维](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)、[多维](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)或[交错](../../../csharp/programming-guide/arrays/jagged-arrays.md)的。  
  
-   创建数组实例时，将建立纬度数量和每个纬度的长度。 这些值在实例的生存期内无法更改。  
  
-   数值数组元素的默认值设置为零，而引用元素设置为 null。  
  
-   交错数组是数组的数组，因此其元素为引用类型且被初始化为 `null`。  
  
-   数组从零开始编制索引：包含 `n` 元素的数组从 `0` 索引到 `n-1`。  
  
-   数组元素可以是任何类型，其中包括数组类型。  
  
-   数组类型是从抽象的基类型 <xref:System.Array> 派生的[引用类型](../../../csharp/language-reference/keywords/reference-types.md)。 由于此类型实现 <xref:System.Collections.IEnumerable> 和 <xref:System.Collections.Generic.IEnumerable%601>，因此可以在 C# 中的所有数组上使用 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 迭代。  
  
## <a name="related-sections"></a>相关章节  
  
-   [作为对象的数组](../../../csharp/programming-guide/arrays/arrays-as-objects.md)  
  
-   [对数组使用 foreach](../../../csharp/programming-guide/arrays/using-foreach-with-arrays.md)  
  
-   [将数组作为参数传递](../../../csharp/programming-guide/arrays/passing-arrays-as-arguments.md)  
  
## <a name="c-language-specification"></a>C# 语言规范

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [集合](../../../csharp/programming-guide/concepts/collections.md)
