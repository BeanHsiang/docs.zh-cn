---
title: 泛型优势 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], benefits
ms.assetid: 80f037cd-9ea7-48be-bfc1-219bfb2d4277
ms.openlocfilehash: 7f882bcdf5c1d9b8c81531c0fe37a3ee27c2e3a0
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56965406"
---
# <a name="benefits-of-generics-c-programming-guide"></a>泛型的优点（C# 编程指南）
公共语言运行时和 C# 语言早期版本中存在一个局限，其中通过将类型与通用基类型 <xref:System.Object> 相互强制完成泛化，泛型提供了此局限的解决方案。 通过创建泛型类，可在编译时创建类型安全的集合。  
  
 通过编写一个使用 .NET 类库中 <xref:System.Collections.ArrayList> 集合类的小程序，可体现出使用非泛型集合类的局限。 <xref:System.Collections.ArrayList> 类的实例可以存储任何引用或值类型。  
  
 [!code-csharp[csProgGuideGenerics#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#4)]  
  
 但这种便利有一定代价。 添加到 <xref:System.Collections.ArrayList> 的任何引用或值类型均隐式向上转换为 <xref:System.Object>。 如果项为值类型，将它们添加到列表时必须将其装箱，检索它们时必须取消装箱。 转换与装箱/取消装箱这两种操作都会降低性能；在必须循环访问大型集合的方案中，装箱与取消装箱的影响非常大。  
  
 另一局限是缺少编译时类型检查；由于 <xref:System.Collections.ArrayList> 将所有内容都转换为 <xref:System.Object>，因此在编译时无法阻止客户端代码执行如下操作：  
  
 [!code-csharp[csProgGuideGenerics#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#5)]  
  
 虽然在创建异类集合时这完全可以接受，甚至有时是有意为之，但将字符串和 `ints` 合并到单个 <xref:System.Collections.ArrayList> 中更有可能属于编程错误，且此错误在运行时之前不会被检测出。  
  
 在 C# 语言 1.0 和 1.1 版中，仅可通过编写自己的类型特定集合来避免 .NET Framework 基类库集合类中出现泛化代码的风险。 当然，由于这样的类不能重复用于多个数据类型，因此你并不具有泛化的优势，且必须为要存储的每个类型重写类。  
  
 <xref:System.Collections.ArrayList> 以及其他相似的类真正需要的是一种方式，这种方式使客户端代码基于每个实例指定打算使用的特定数据类型。 这会省去向上转换为 <xref:System.Object> 的必要，并且使编译器可能执行类型检查。 换而言之，<xref:System.Collections.ArrayList> 需要一个类型参数。 那正是泛型所提供的内容。 在泛型 <xref:System.Collections.Generic.List%601> 集合中，在 <xref:System.Collections.Generic> 命名空间中，向集合添加项的操作类似于如下所示：  
  
 [!code-csharp[csProgGuideGenerics#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#6)]  
  
 对于客户端代码，与 <xref:System.Collections.ArrayList> 相比，<xref:System.Collections.Generic.List%601> 添加的唯一语法是声明和实例化中的类型参数。 虽然编码略为复杂，但与 <xref:System.Collections.ArrayList> 相比，你创建的列表不仅更加安全，而且创建速度大为提高，尤其是在列表项为值类型时。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Collections.Generic>
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)
- [装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)
- [何时使用泛型集合](../../../standard/collections/when-to-use-generic-collections.md)
- [集合准则](../../../standard/design-guidelines/guidelines-for-collections.md)
