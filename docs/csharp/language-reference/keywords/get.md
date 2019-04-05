---
title: get - C# 参考
ms.custom: seodec18
ms.date: 03/10/2017
f1_keywords:
- get_CSharpKeyword
- get
helpviewer_keywords:
- get keyword [C#]
ms.assetid: a52de048-fbe0-41b0-82ec-8e4ac04d3a71
ms.openlocfilehash: 280b818534238207f901e1dcd125e03f5ce1d1fe
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54675175"
---
# <a name="get-c-reference"></a>get（C# 参考）

`get` 关键字在属性或索引器中定义访问器方法，它将返回属性值或索引器元素。 有关详细信息，请参阅[属性](../../../csharp/programming-guide/classes-and-structs/properties.md)、[自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)和[索引器](../../../csharp/programming-guide/indexers/index.md)。  
  
以下示例为名为 `Seconds` 的属性同时定义 `get` 和 `set` 访问器。 它使用名为 `_seconds` 的私有字段备份属性值。  
 
 [!code-csharp[get#1](../../../../samples/snippets/csharp/language-reference/keywords/get/get-1.cs)]  
  
通常，`get` 访问器包含返回一个值的单个语句，如前面的示例所示。 从 C# 7.0 开始，可以将 `get` 访问器作为 expression-bodied 成员实现。 以下示例将 `get` 和 `set` 访问器都作为 expression-bodied 成员实现。

 [!code-csharp[get#3](../../../../samples/snippets/csharp/language-reference/keywords/get/get-3.cs)]   
 
对于属性的 `get` 和 `set` 访问器不执行除设置或检索私有支持字段中的值以外的任何其他操作的简单情况，可以利用 C# 编译器对自动实现的属性的支持。 以下示例将 `Hours` 作为自动实现的属性来实现。 
  
 [!code-csharp[get#2](../../../../samples/snippets/csharp/language-reference/keywords/get/get-2.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](../../../csharp/language-reference/keywords/index.md)
- [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)
