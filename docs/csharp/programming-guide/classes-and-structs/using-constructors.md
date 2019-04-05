---
title: 使用构造函数 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- constructors [C#], about constructors
ms.assetid: 464253b2-fd5d-469a-836d-df0fdf2a43f7
ms.openlocfilehash: 7422267d6ce067ed30d0fbd4be8de2fd122b4a90
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57200632"
---
# <a name="using-constructors-c-programming-guide"></a>使用构造函数（C# 编程指南）
创建[类](../../../csharp/language-reference/keywords/class.md)或[结构](../../../csharp/language-reference/keywords/struct.md)时，将会调用其构造函数。 构造函数与该类或结构具有相同名称，并且通常初始化新对象的数据成员。  
  
 在下面的示例中，通过使用简单构造函数定义了一个名为 `Taxi` 的类。 然后使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符对该类进行实例化。 在为新对象分配内存之后，`new` 运算符立即调用 `Taxi` 构造函数。  
  
 [!code-csharp[csProgGuideObjects#53](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#53)]  
  
 不带任何参数的构造函数称为“默认构造函数”。 每当使用 `new` 运算符实例化对象且不为 `new` 提供任何参数时，会调用默认构造函数。 有关详细信息，请参阅[实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)。  
  
 除非类是[静态](../../../csharp/language-reference/keywords/static.md)的，否则 C# 编译器将为无构造函数的类提供一个公共的默认构造函数，以便该类可以实例化。 有关详细信息，请参阅[静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
 通过将构造函数设置为私有构造函数，可以阻止类被实例化，如下所示：  
  
 [!code-csharp[csProgGuideObjects#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#11)]  
  
 有关详细信息，请参阅[私有构造函数](../../../csharp/programming-guide/classes-and-structs/private-constructors.md)。  
  
 [结构](../../../csharp/language-reference/keywords/struct.md)类型的构造函数与类的构造函数类似，但是 `structs` 不能包含显式默认构造函数，因为编译器将自动提供一个显式默认构造函数。 此构造函数会将 `struct` 中的每个字段初始化为默认值。 有关详细信息，请参阅[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。 但是，只有使用 `new` 实例化 `struct` 时，才会调用此默认构造函数。 例如，下面的代码使用 <xref:System.Int32> 的默认构造函数，因此可确保整数已初始化：  
  
```csharp  
int i = new int();  
Console.WriteLine(i);  
```  
  
 但是，下面的代码会导致编译器错误，因为它不使用 `new`，而且尝试使用尚未初始化的对象：  
  
```  
int i;  
Console.WriteLine(i);  
```  
  
 或者，可将基于 `structs` 的对象（包括所有内置数值类型）初始化或赋值后使用，如下面的示例所示：  
  
```  
int a = 44;  // Initialize the value type...  
int b;  
b = 33;      // Or assign it before using it.  
Console.WriteLine("{0}, {1}", a, b);  
```  
  
 因此不需要调用值类型的默认构造函数。  
  
 两个类和 `structs` 都可以定义带参数的构造函数。 必须通过 `new` 语句或 [base](../../../csharp/language-reference/keywords/base.md) 语句调用带参数的构造函数。 类和 `structs` 还可以定义多个构造函数，并且二者均不需要定义默认构造函数。 例如:  
  
 [!code-csharp[csProgGuideObjects#54](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#54)]  
  
 可使用下面任一语句创建此类：  
  
 [!code-csharp[csProgGuideObjects#55](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#55)]  
  
 构造函数可以使用 `base` 关键字调用基类的构造函数。 例如:  
  
 [!code-csharp[csProgGuideObjects#56](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#56)]  
  
 在此示例中，在执行构造函数块之前调用基类的构造函数。 `base` 关键字可带参数使用，也可不带参数使用。 构造函数的任何参数都可用作 `base` 的参数，或用作表达式的一部分。 有关详细信息，请参阅 [base](../../../csharp/language-reference/keywords/base.md)。  
  
 在派生类中，如果不使用 `base` 关键字来显式调用基类构造函数，则将隐式调用默认构造函数（若有）。 这意味着下面的构造函数声明等效：  
  
 [!code-csharp[csProgGuideObjects#58](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#58)]  
  
 [!code-csharp[csProgGuideObjects#57](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#57)]  
  
 如果基类没有提供默认构造函数，派生类必须使用 `base` 显式调用基类构造函数。  
  
 构造函数可以使用 [this](../../../csharp/language-reference/keywords/this.md) 关键字调用同一对象中的另一构造函数。 和 `base` 一样，`this` 可带参数使用也可不带参数使用，构造函数中的任何参数都可用作 `this` 的参数，或者用作表达式的一部分。 例如，可以使用 `this` 重写前一示例中的第二个构造函数：  
  
 [!code-csharp[csProgGuideObjects#59](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#59)]  
  
 上一示例中使用 `this` 关键字会导致此构造函数被调用：  
  
 [!code-csharp[csProgGuideObjects#60](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#60)]  
  
 可以将构造函数标记为[public](../../../csharp/language-reference/keywords/public.md)、[private](../../../csharp/language-reference/keywords/private.md)、[protected](../../../csharp/language-reference/keywords/protected.md)、[internal](../../../csharp/language-reference/keywords/internal.md)、[protected internal](../../../csharp/language-reference/keywords/protected-internal.md) 或 [private protected](../../../csharp/language-reference/keywords/private-protected.md)。 这些访问修饰符定义类的用户构造该类的方式。 有关详细信息，请参阅[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 可使用 [static](../../../csharp/language-reference/keywords/static.md) 关键字将构造函数声明为静态构造函数。 在访问任何静态字段之前，都将自动调用静态构造函数，它们通常用于初始化静态类成员。 有关详细信息，请参阅[静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)。  
  
## <a name="c-language-specification"></a>C# 语言规范  

有关详细信息，请参阅 [C# 语言规范](../../language-reference/language-specification/index.md)中的[实例构造函数](~/_csharplang/spec/classes.md#instance-constructors)和[静态构造函数](~/_csharplang/spec/classes.md#static-constructors)。 该语言规范是 C# 语法和用法的权威资料。
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)
- [终结器](../../../csharp/programming-guide/classes-and-structs/destructors.md)
