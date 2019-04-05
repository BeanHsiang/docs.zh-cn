---
title: 抽象类、密封类和类成员 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- abstract classes [C#]
- sealed classes [C#]
- C# language, abstract classes
- C# language, sealed
ms.assetid: 99aa52f7-b435-43f9-936e-2470af734c4e
ms.openlocfilehash: fc3e29ad606cf8a60318a320e8ebc65b0d7f6e48
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56965249"
---
# <a name="abstract-and-sealed-classes-and-class-members-c-programming-guide"></a>抽象类、密封类及类成员（C# 编程指南）
使用 [abstract](../../../csharp/language-reference/keywords/abstract.md) 关键字可以创建不完整且必须在派生类中实现的类和 [class](../../../csharp/language-reference/keywords/class.md) 成员。  
  
 使用 [sealed](../../../csharp/language-reference/keywords/sealed.md) 关键字可以防止继承以前标记为 [virtual](../../../csharp/language-reference/keywords/virtual.md) 的类或某些类成员。  
  
## <a name="abstract-classes-and-class-members"></a>抽象类和类成员  
 通过在类定义前面放置关键字 `abstract`，可以将类声明为抽象类。 例如:  
  
 [!code-csharp[csProgGuideInheritance#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#13)]  
  
 抽象类不能实例化。 抽象类的用途是提供一个可供多个派生类共享的通用基类定义。 例如，类库可以定义一个抽象类，将其用作多个类库函数的参数，并要求使用该库的程序员通过创建派生类来提供自己的类实现。  
  
 抽象类也可以定义抽象方法。 方法是将关键字 `abstract` 添加到方法的返回类型的前面。 例如:  
  
 [!code-csharp[csProgGuideInheritance#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#14)]  
  
 抽象方法没有实现，所以方法定义后面是分号，而不是常规的方法块。 抽象类的派生类必须实现所有抽象方法。 当抽象类从基类继承虚方法时，抽象类可以使用抽象方法重写该虚方法。 例如:  
  
 [!code-csharp[csProgGuideInheritance#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#15)]  
  
 如果将 `virtual` 方法声明为 `abstract`，则该方法对于从抽象类继承的所有类而言仍然是虚方法。 继承抽象方法的类无法访问方法的原始实现，因此在上一示例中，类 F 上的 `DoWork` 无法调用类 D 上的 `DoWork`。通过这种方式，抽象类可强制派生类向虚拟方法提供新的方法实现。  
  
## <a name="sealed-classes-and-class-members"></a>密封类和类成员  
 通过在类定义前面放置关键字 `sealed`，可以将类声明为[密封类](../../../csharp/language-reference/keywords/sealed.md)。 例如:  
  
 [!code-csharp[csProgGuideInheritance#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#16)]  
  
 密封类不能用作基类。 因此，它也不能是抽象类。 密封类禁止派生。 由于密封类从不用作基类，所以有些运行时优化可以略微提高密封类成员的调用速度。  
  
 在对基类的虚成员进行重写的派生类上，方法、索引器、属性或事件可以将该成员声明为密封成员。 在用于以后的派生类时，这将取消成员的虚效果。 方法是在类成员声明中将 `sealed` 关键字置于 [override](../../../csharp/language-reference/keywords/override.md) 关键字前面。 例如:  
  
 [!code-csharp[csProgGuideInheritance#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#17)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)
- [方法](../../../csharp/programming-guide/classes-and-structs/methods.md)
- [字段](../../../csharp/programming-guide/classes-and-structs/fields.md)
- [如何：定义抽象属性](../../../csharp/programming-guide/classes-and-structs/how-to-define-abstract-properties.md)
