---
title: 如何：测试引用相等性（标识）- C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- object identity [C#]
- reference equality [C#]
ms.assetid: 91307fda-267b-4fd2-a338-2aada39ee791
ms.openlocfilehash: 057532cae42d7a0b6d11750ae0e33e43108cfda9
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57203582"
---
# <a name="how-to-test-for-reference-equality-identity-c-programming-guide"></a>如何：测试引用相等性（标识）（C# 编程指南）
无需实现任何自定义逻辑，即可支持类型中的引用相等性比较。 此功能由静态 <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> 方法向所有类型提供。  
  
 以下示例演示如何确定两个变量是否具有引用相等性，即它们引用内存中的同一对象。  
  
 该示例还演示 <xref:System.Object.ReferenceEquals%2A?displayProperty=nameWithType> 为何始终为值类型返回 `false`，以及您为何不应使用 <xref:System.Object.ReferenceEquals%2A> 来确定字符串相等性。  
  
## <a name="example"></a>示例  
 [!code-csharp[csProgGuideObjects#90](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#90)]  
  
 在 <xref:System.Object?displayProperty=nameWithType> 通用基类中实现 `Equals` 也会执行引用相等性检查，但最好不要使用这种检查，因为如果恰好某个类替代了此方法，结果可能会出乎意料。 以上情况同样适用于 `==` 和 `!=` 运算符。 当它们作用于引用类型时，`==` 和 `!=` 的默认行为是执行引用相等性检查。 但是，派生类可重载运算符，执行值相等性检查。 为了尽量降低错误的可能性，当需要确定两个对象是否具有引用相等性时，最好始终使用 <xref:System.Object.ReferenceEquals%2A>。  
  
 运行时始终暂存同一程序集内的常量字符串。 也就是说，仅维护每个唯一文本字符串的一个实例。 但是，运行时不能保证会暂存在运行时创建的字符串，也不保证会暂存不同程序集中两个相等的常量字符串。  
  
## <a name="see-also"></a>请参阅

- [相等比较](../../../csharp/programming-guide/statements-expressions-operators/equality-comparisons.md)
