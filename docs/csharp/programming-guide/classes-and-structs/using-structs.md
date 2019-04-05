---
title: 使用 struct - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- structs [C#], using
ms.assetid: cea4a459-9eb9-442b-8d08-490e0797ba38
ms.openlocfilehash: fe7cf3cf1982060d22f648c5e17d002b1a695ac0
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56978522"
---
# <a name="using-structs-c-programming-guide"></a>使用结构（C# 编程指南）
`struct` 类型适用于表示轻量级对象，如 `Point`、 `Rectangle`和 `Color`。 尽管用它来表示一个点就如同具有 [Auto-Implemented Properties（自动实现的属性）](../../../csharp/language-reference/keywords/class.md) 的 [类](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)那样方便，但在某些情况下，使用 [结构](../../../csharp/language-reference/keywords/struct.md) 可能更高效。 例如，如果你声明具有 1000 个 `Point` 对象的数组，那么你将分配额外的内存用于引用每个对象；在这种情况下，使用结构将更为便宜。 因为 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 包含一个称为 <xref:System.Drawing.Point> 的对象，因此在此示例中的结构改名为“Coords”。  
  
 [!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]  
  
 定义结构的默认（无参数）构造函数是错误的。 在结构体中初始化实例字段也是错误的。 只能通过使用参数化构造函数、隐式默认构造函数、[对象初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)，或在声明结构之后通过单独访问各个成员，才能初始化可从外部访问的结构成员。 任何私有或其他不可访问的成员需要以独占方式使用构造函数。
  
 使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符创建结构对象时，会创建结构对象且会遵循[构造函数签名](../../../csharp/programming-guide/classes-and-structs/constructors.md#constructor-syntax)来调用相应的构造函数。 与类不同，可以对结构进行实例化，而无需使用 `new` 运算符。 在这种情况下，没有调用任何构造函数，从而提高了分配效率。 但是，字段将保持为未分配状态且必须在在初始化所有字段之后才可使用对象。 这包括无法通过自动实现的属性获取或设置值。
 
 如果使用默认的无参数构造函数实例化结构对象，则根据成员的[默认值](../../../csharp/programming-guide/statements-expressions-operators/default-value-expressions.md)分配所有成员。
  
 当为某个结构编写带有参数的构造函数时，必须显式初始化所有成员，否则一个或更多的成员将不被分配，并且不能使用结构，这会生成编译器错误 CS0171。  
  
 由于全都是用于类的继承，因此没有用于结构的继承。 一个结构无法继承自另一个结构或类，并且它不能为类的基类。 但是，它可以从基类 <xref:System.Object>继承。 结构也可以实现接口，且实现方法与类相同。  
  
 不能使用关键字 `struct`声明一个类。 在 C# 中，类和结构在语义上是不同的。 结构是值类型，而类是引用类型。 有关更多信息，请参阅 [值类型](../../../csharp/language-reference/keywords/value-types.md)。  
  
 除非需要引用类型语义，将较小的类声明为结构，可以提高系统的处理效率。  
  
## <a name="example-1"></a>示例 1  
  
### <a name="description"></a>说明  
 此示例同时使用了默认构造函数和参数化构造函数来演示 `struct` 初始化。  
  
### <a name="code"></a>代码  
 [!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]  
  
 [!code-csharp[csProgGuideObjects#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#2)]  
  
## <a name="example-2"></a>示例 2  
  
### <a name="description"></a>说明  
 此示例演示了一个特定于结构的功能。 此功能可以创建 Coords 对象，而无需使用 `new` 运算符。 如果将 `struct` 替换为 `class`，程序将不会进行编译。  
  
### <a name="code"></a>代码  
 [!code-csharp[csProgGuideObjects#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#1)]  
  
 [!code-csharp[csProgGuideObjects#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#3)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [结构](../../../csharp/programming-guide/classes-and-structs/structs.md)
