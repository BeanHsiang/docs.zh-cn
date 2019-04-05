---
title: .NET 中的泛型集合
ms.date: 02/15/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- generics [.NET], collections
- generic collections [.NET]
- generic types [.NET]
ms.assetid: 5b646751-6ab7-465c-916c-b1a76aefa9f5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ec3f8fb16245318cab8706a2ed136e51f3dc31db
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54705792"
---
# <a name="generic-collections-in-net"></a>.NET 中的泛型集合

 .NET 类库提供了许多 <xref:System.Collections.Generic> 和 <xref:System.Collections.ObjectModel> 命名空间中的泛型集合类。 若要详细了解这些类，请参阅[常用集合类型](../../../docs/standard/collections/commonly-used-collection-types.md)。  
  
### <a name="systemcollectionsgeneric"></a>System.Collections.Generic  
 许多泛型集合类型均为非泛型类型的直接模拟。 <xref:System.Collections.Generic.Dictionary%602> 是 <xref:System.Collections.Hashtable> 的泛型版本；它使用枚举的泛型结构 <xref:System.Collections.Generic.KeyValuePair%602> 而不是 <xref:System.Collections.DictionaryEntry>。  
  
 <xref:System.Collections.Generic.List%601> 是 <xref:System.Collections.ArrayList> 的泛型版本。 存在响应非泛型版本的泛型 <xref:System.Collections.Generic.Queue%601> 和 <xref:System.Collections.Generic.Stack%601> 类。  
  
 存在 <xref:System.Collections.Generic.SortedList%602> 的泛型和非泛型版本。 这两个版本均为字典和列表的混合。 <xref:System.Collections.Generic.SortedDictionary%602> 泛型类是一个纯字典，并且没有任何非泛型对应项。  
  
 <xref:System.Collections.Generic.LinkedList%601> 泛型类是真正的链接列表。 它没有任何非泛型对应项。  
  
### <a name="systemcollectionsobjectmodel"></a>System.Collections.ObjectModel  
 <xref:System.Collections.ObjectModel.Collection%601> 泛型类提供用于派生自己的泛型集合类型的基类。 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 类提供了任何从实现 <xref:System.Collections.Generic.IList%601> 泛型接口的类型生成只读集合的简便方法。 <xref:System.Collections.ObjectModel.KeyedCollection%602> 泛型类提供了存储包含其自己的键的对象的方法。  
  
## <a name="other-generic-types"></a>其他泛型类型  
 <xref:System.Nullable%601> 泛型结构允许使用值类型，如同它们可分配 `null`。 这在处理数据库查询时很有用，其中字段包含可能丢失的值类型。 泛型类型参数可为任意值类型。  
  
> [!NOTE]
>  在 C# 和 Visual Basic 中，无需显式使用 <xref:System.Nullable%601>，因为语言具有可以为 null 类型的语法。 请参阅[可为 null 的类型（C# 编程指南）](../../csharp/programming-guide/nullable-types/index.md)或 [可为 null 的值类型 (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)。 
  
 <xref:System.ArraySegment%601> 泛型结构提供了分隔任何类型的从零开始的一维数组内的一系列元素的方法。 泛型类型参数是数组中元素的类型。  
  
 如果你的事件采用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 所使用的事件处理模式，则 <xref:System.EventHandler%601> 泛型委托不需要声明委托类型来处理事件。 例如，假设已创建从 <xref:System.EventArgs> 派生的 `MyEventArgs` 类，以包含事件的数据。 则可以声明此事件，如下所示：  
  
 [!code-cpp[Conceptual.Generics.Overview#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Generics.Overview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source2.cs#7)]
 [!code-vb[Conceptual.Generics.Overview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source2.vb#7)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [泛型](../../../docs/standard/generics/index.md)
- [用于控制数组和列表的泛型委托](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)
- [泛型接口](../../../docs/standard/generics/interfaces.md)
