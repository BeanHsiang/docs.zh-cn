---
title: 访问修饰符 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# Language, access modifiers
- access modifiers [C#], about
ms.assetid: 6e81ee82-224f-4a12-9baf-a0dca2656c5b
ms.openlocfilehash: d328f8e73824a4773c6e10f506f3021d3c88d085
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378047"
---
# <a name="access-modifiers-c-programming-guide"></a>访问修饰符（C# 编程指南）
所有类型和类型成员都具有可访问性级别，该级别可以控制是否可以从你的程序集或其他程序集中的其他代码中使用它们。 可以使用以下访问修饰符在进行声明时指定类型或成员的可访问性：  
  
 [public](../../../csharp/language-reference/keywords/public.md)  
 同一程序集中的任何其他代码或引用该程序集的其他程序集都可以访问该类型或成员。 
  
 [private](../../../csharp/language-reference/keywords/private.md)  
 只有同一类或结构中的代码可以访问该类型或成员。  
  
 [受保护](../../../csharp/language-reference/keywords/protected.md)  
 只有同一类或者从该类派生的类中的代码可以访问该类型或成员。  
 [internal](../../../csharp/language-reference/keywords/internal.md)  
 同一程序集中的任何代码都可以访问该类型或成员，但其他程序集中的代码不可以。  
  
 [受保护的内部](../../../csharp/language-reference/keywords/protected-internal.md) 该类型或成员可由对其进行声明的程序集或另一程序集中的派生类中的任何代码访问。 

 [专用受保护](../../../csharp/language-reference/keywords/private-protected.md)只有在其声明程序集内，通过相同类中的代码或派生自该类的类型，才能访问类型或成员。
  
 下面的示例演示如何在类型和成员上指定访问修饰符：  
  
 [!code-csharp[csProgGuideObjects#72](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#72)]  
  
 并非所有的访问修饰符都可以由所有上下文中的所有类型或成员使用，并且在某些情况下，类型成员的可访问性受其包含类型的可访问性限制。 以下各节提供了有关可访问性的更多详细信息。  
  
## <a name="class-and-struct-accessibility"></a>类和结构可访问性  
 在命名空间内直接声明（换句话说，不嵌套在其他类或结构中）的类和结构可以为公共或内部。 如果未指定任何访问修饰符，则默认设置为内部。  
  
 结构成员（包括嵌套的类和结构）可以声明为公共、内部或私有。 类成员（包括嵌套的类和结构）可以为公共、受保护的内部、受保护、内部、专用受保护或专用。 默认情况下，类成员和结构成员（包括嵌套的类和结构）的访问级别为私有。 不能从包含类型的外部访问私有嵌套类型。  
  
 派生类不能具有高于其基类型的可访问性。 换而言之，不能具有派生自内部类 `A` 的公共类 `B`。 如果允许这样，则它将具有使 `A` 公开的效果，因为可从派生类访问 `A` 的所有受保护的或内部成员。  
  
 可以通过使用 InternalsVisibleToAttribute 启用特定的其他程序集访问内部类型。 有关详细信息，请参阅[友元程序集](../../../standard/assembly/friend-assemblies.md)。  
  
## <a name="class-and-struct-member-accessibility"></a>类和结构成员可访问性  
 可以使用六种访问类型中的任意一种声明类成员（包括嵌套的类和结构）。 结构成员无法声明为受保护，因为结构不支持继承。  
  
 通常情况下，成员的可访问性不大于包含该成员的类型的可访问性。 但是，如果内部类的公共成员实现了接口方法或替代了在公共基类中定义的虚拟方法，则可从该程序集的外部访问该成员。  
  
 为字段、属性或事件的任何成员的类型必须至少与该成员本身具有相同的可访问性。 同样，为方法、索引器或委托的任何成员的返回类型和参数类型必须至少与该成员本身具有相同的可访问性。 例如，不能具有返回类 `C` 的公共方法 `M`，除非 `C` 也是公共的。 同样，如果 `A` 声明为私有，则不能具有类型 `A` 的受保护的属性。  
  
 用户定义的运算符始终必须声明为公共。 有关详细信息，请参阅[运算符（C# 参考）](../../../csharp/language-reference/keywords/operator.md)。  
  
 终结器不能具有可访问性修饰符。  
  
 若要设置类或结构成员的访问级别，向成员声明添加适当的关键字，如以下示例中所示。  
  
 [!code-csharp[csProgGuideObjects#73](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#73)]  
  
> [!NOTE]
>  受保护的内部可访问性级别意味着受保护或内部，而非受保护和内部。 换而言之，可以从同一程序集中的任何类（包括派生类）访问受保护的内部成员。 若要将同一程序集中的可访问性限制为仅派生类，请声明类本身为内部，并声明其成员为受保护。 此外，从 C# 7.2 开始，可以使用专用受保护的访问修饰符实现相同的效果，而无需使包含的类属于内部。  
  
## <a name="other-types"></a>其他类型  
 在命名空间内直接声明的接口可以声明为公共或内部，就像类和结构一样，接口默认设置为内部访问。 接口成员始终为公共的，因为接口的用途是启用其他类型以访问类或结构。 没有访问修饰符可以应用于接口成员。  
  
 枚举成员始终为公共的，并且不应用任何访问修饰符。  
  
 委托类似于类和结构。 默认情况下，当在命名空间内直接声明它们时，它们具有内部访问，当将它们嵌套在命名空间内时，它们具有私有访问。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [接口](../../../csharp/programming-guide/interfaces/index.md)
- [private](../../../csharp/language-reference/keywords/private.md)
- [public](../../../csharp/language-reference/keywords/public.md)
- [internal](../../../csharp/language-reference/keywords/internal.md)
- [受保护](../../../csharp/language-reference/keywords/protected.md)
- [受保护的内部](../../../csharp/language-reference/keywords/protected-internal.md)
- [专用受保护](../../../csharp/language-reference/keywords/private-protected.md)
- [class](../../../csharp/language-reference/keywords/class.md)
- [struct](../../../csharp/language-reference/keywords/struct.md)
- [interface](../../../csharp/language-reference/keywords/interface.md)
