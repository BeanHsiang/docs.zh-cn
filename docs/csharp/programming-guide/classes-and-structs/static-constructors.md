---
title: 静态构造函数 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- static constructors [C#]
- constructors [C#], static
ms.assetid: 151ec95e-3c4d-4ed7-885d-95b7a3be2e7d
ms.openlocfilehash: 6a990dbf26ac1a6bdc642442b9f4b75c05ee9635
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57200112"
---
# <a name="static-constructors-c-programming-guide"></a>静态构造函数（C# 编程指南）
静态构造函数用于初始化任何[静态](../../../csharp/language-reference/keywords/static.md)数据，或执行仅需执行一次的特定操作。 将在创建第一个实例或引用任何静态成员之前自动调用静态构造函数。  
  
 [!code-csharp[csProgGuideObjects#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#14)]  
  
 静态构造函数具有以下属性：  
  
-   静态构造函数不使用访问修饰符或不具有参数。  
  
-   在创建第一个实例或引用任何静态成员之前，将自动调用静态构造函数以初始化[类](../../../csharp/language-reference/keywords/class.md)。  
  
-   不能直接调用静态构造函数。  
  
-   用户无法控制在程序中执行静态构造函数的时间。  
  
-   静态构造函数的一种典型用法是在类使用日志文件且将构造函数用于将条目写入到此文件中时使用。  
  
-   静态构造函数对于创建非托管代码的包装类也非常有用，这种情况下构造函数可调用 `LoadLibrary` 方法。  
  
-   如果静态构造函数引发异常，运行时将不会再次调用该函数，并且类型在程序运行所在的应用程序域的生存期内将保持未初始化。  
  
## <a name="example"></a>示例  
 在此示例中，类 `Bus` 具有静态构造函数。 创建 `Bus` 的第一个实例 (`bus1`) 时，将调用该静态构造函数，以便初始化类。 示例输出验证即使创建了两个 `Bus` 的实例，静态构造函数也仅运行一次，并且在实例构造函数运行前运行。  
  
 [!code-csharp[csProgGuideObjects#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#15)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)
- [静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
- [终结器](../../../csharp/programming-guide/classes-and-structs/destructors.md)
