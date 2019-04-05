---
title: 如何：定义抽象属性 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], abstract
- abstract properties [C#]
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
ms.openlocfilehash: 98a535f68efc50c2ff7409d8eadf52f9e7549566
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57201945"
---
# <a name="how-to-define-abstract-properties-c-programming-guide"></a>如何：定义抽象属性（C# 编程指南）
以下示例演示如何定义[抽象](../../../csharp/language-reference/keywords/abstract.md)属性。 抽象属性声明不提供属性访问器的实现，它声明该类支持属性，而将访问器实现留给派生类。 以下示例演示如何实现从基类继承抽象属性。  
  
 此示例由三个文件组成，其中每个文件都单独编译，产生的程序集由下一次编译引用：  
  
-   abstractshape.cs：包含抽象 `Area` 属性的 `Shape` 类。  
  
-   shapes.cs：`Shape` 类的子类。  
  
-   shapetest.cs：测试程序，用于显示一些 `Shape` 派生对象的区域。  
  
 若要编译该示例，请使用以下命令：  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 这将创建可执行文件 shapetest.exe。  
  
## <a name="example"></a>示例  
 此文件声明 `Shape` 类，该类包含 `double` 类型的 `Area` 属性。  
  
 [!code-csharp[csProgGuideInheritance#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#1)]  
  
-   属性的修饰符放置在属性声明中。 例如:  
  
    ```csharp  
    public abstract double Area  
    ```  
  
-   声明抽象属性时（如本示例中的 `Area`），只需指明哪些属性访问器可用即可，不要实现它们。 在此示例中，仅 [get](../../../csharp/language-reference/keywords/get.md) 访问器可用，因此该属性是只读属性。  
  
## <a name="example"></a>示例  
 下面的代码演示 `Shape` 的三个子类，并演示它们如何替代 `Area` 属性来提供自己的实现。  
  
 [!code-csharp[csProgGuideInheritance#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#2)]  
  
## <a name="example"></a>示例  
 下面的代码演示一个创建若干 `Shape` 派生对象并输出其区域的测试程序。  
  
 [!code-csharp[csProgGuideInheritance#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#3)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)
- [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)
- [如何：使用命令行创建和使用程序集](../concepts/assemblies-gac/how-to-create-and-use-assemblies-using-the-command-line.md)
