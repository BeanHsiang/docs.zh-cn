---
title: 构造函数 - C# 编程指南
ms.custom: seodec18
ms.date: 05/05/2017
helpviewer_keywords:
- constructors [C#]
- classes [C#], constructors
- C# language, constructors
ms.assetid: df2e2e9d-7998-418b-8e7d-890c17ff6c95
ms.openlocfilehash: e88cc9b36f64a559105620359f4c163978cf9d8c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54692254"
---
# <a name="constructors-c-programming-guide"></a>构造函数（C# 编程指南）
每当创建[类](../../../csharp/language-reference/keywords/class.md)或[结构](../../../csharp/language-reference/keywords/struct.md)时，将会调用其构造函数。 类或结构可能具有采用不同参数的多个构造函数。 使用构造函数，程序员能够设置默认值、限制实例化，并编写灵活易读的代码。 有关详细信息和示例，请参阅[使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)和[实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)。  

## <a name="default-constructors"></a>默认构造函数
  
如果没有为类提供构造函数，默认情况下，C# 将创建一个会实例化对象并将成员变量设置为默认值的构造函数，如[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)中所列。 如果没有为结构提供构造函数，C# 将依赖于隐式默认构造函数，自动将值类型的每个字段初始化为其默认值，如[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)中所列。 有关详细信息和示例，请参阅[实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)。  

## <a name="constructor-syntax"></a>构造函数语法

构造函数是一种方法，其名称与其类型的名称相同。 其方法签名仅包含方法名称和其参数列表；它不包含返回类型。 以下示例演示一个名为 `Person` 的类的构造函数。

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#1)]  

如果某个构造函数可以作为单个语句实现，则可以使用[表达式主体定义](../statements-expressions-operators/expression-bodied-members.md)。 以下示例定义 `Location` 类，其构造函数具有一个名为“name”的字符串参数。 表达式主体定义给 `locationName` 字段分配参数。

[!code-csharp[expression-bodied-constructor](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/expr-bodied-ctor.cs#1)]  

## <a name="static-constructors"></a>静态构造函数

前面的示例具有所有已展示的实例构造函数，这些构造函数创建一个新对象。 类或结构也可以具有静态构造函数，该静态构造函数初始化类型的静态成员。  静态构造函数是无参数构造函数。 如果未提供静态构造函数来初始化静态字段，C# 编译器将提供默认静态构造函数，该静态构造函数会将静态字段初始化为其默认值，如[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)中所列。 

以下示例使用静态构造函数来初始化静态字段。

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#2)]  

也可以通过表达式主体定义来定义静态构造函数，如以下示例所示。 

[!code-csharp[constructors](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/constructors1.cs#3)]  

有关详细信息和示例，请参阅[静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)  
  
 [实例构造函数](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)  
  
 [私有构造函数](../../../csharp/programming-guide/classes-and-structs/private-constructors.md)  
  
 [静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)  
  
 [如何：编写复制构造函数](../../../csharp/programming-guide/classes-and-structs/how-to-write-a-copy-constructor.md)  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [终结器](../../../csharp/programming-guide/classes-and-structs/destructors.md)
- [static](../../../csharp/language-reference/keywords/static.md)
- [Why Do Initializers Run In The Opposite Order As Constructors?Part One](https://blogs.msdn.microsoft.com/ericlippert/2008/02/15/why-do-initializers-run-in-the-opposite-order-as-constructors-part-one)（为何初始值设定项作为构造函数以相反顺序运行？第一部分）
