---
title: 如何：在 COM 互操作编程中使用索引属性 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- indexed properties [C#]
- Office programming [C#], indexed properties
- properties [C#], indexed
ms.assetid: 756bfc1e-7c28-4d4d-b114-ac9288c73882
ms.openlocfilehash: 4b064f7042e5e5f0f6d5545c59de2f37897927b4
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56978028"
---
# <a name="how-to-use-indexed-properties-in-com-interop-programming-c-programming-guide"></a>如何：在 COM 互操作编程中使用索引属性（C# 编程指南）
索引属性改进了在 C# 编程中使用具有参数的 COM 属性的方式。 结合使用索引属性与 Visual C# 中的其他功能（如[命名实参和可选实参](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)、一种新类型（[动态](../../../csharp/language-reference/keywords/dynamic.md)）以及[嵌入类型信息](../../../csharp/programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md)）可以增强 Microsoft Office 编程。  
  
 在早期版本的 C# 中，仅当 `get` 方法没有参数且 `set` 方法有且只有一个值参数时，方法才能作为属性访问。 但是，并非所有 COM 属性都符合上述限制。 例如，Excel <xref:Microsoft.Office.Interop.Excel.Range.Range%2A> 属性具有一个 `get` 访问器，它需要该范围名称的一个参数。 过去，由于无法直接访问 `Range` 属性，因此必须使用 `get_Range` 方法，如以下示例所示。  
  
 [!code-csharp[csProgGuideIndexedProperties#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#1)]  
  
 利用索引属性，你可以改为编写以下代码：  
  
 [!code-csharp[csProgGuideIndexedProperties#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#2)]  
  
> [!NOTE]
>  上一示例还使用了[可选实参](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)功能，以便忽略 `Type.Missing`。  
  
 与在 Visual C# 2008 及更早版本中设置 <xref:Microsoft.Office.Interop.Excel.Range> 对象的 `Value` 属性的值类似，需要两个参数。 一个为指定范围值类型的可选参数提供实参。 另一个提供 `Value` 属性的值。 下面的示例说明了这些方法。 两者都将 A1 单元格的值设置为 `Name`。
  
 [!code-csharp[csProgGuideIndexedProperties#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#3)]  
  
 利用索引属性，你可以改为编写以下代码。  
  
 [!code-csharp[csProgGuideIndexedProperties#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#4)]  
  
 你不能创建自己的索引属性。 该功能仅支持使用现有索引属性。  
  
## <a name="example"></a>示例  
 以下代码显示完整示例。 若要详细了解如何设置访问 Office API 的项目，请参阅[操作说明：使用 Visual C# 功能访问 Office 互操作对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)。  
  
 [!code-csharp[csProgGuideIndexedProperties#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csprogguideindexedproperties/cs/program.cs#5)]  
  
## <a name="see-also"></a>请参阅

- [命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)
- [dynamic](../../../csharp/language-reference/keywords/dynamic.md)
- [使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)
- [如何：在 Office 编程中使用命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)
- [如何：通过使用 Visual C# 功能访问 Office 互操作对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)
- [演练：Office 编程](../../../csharp/programming-guide/interop/walkthrough-office-programming.md)
