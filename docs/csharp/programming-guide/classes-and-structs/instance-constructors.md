---
title: 实例构造函数 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- constructors [C#], instance constructors
- instance constructors [C#]
ms.assetid: 24663779-c1e5-4af4-a942-ca554e4c542d
ms.openlocfilehash: c698ffc8d1bc68b2ebcbdf4578ab5926d4743516
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57203465"
---
# <a name="instance-constructors-c-programming-guide"></a>实例构造函数（C# 编程指南）
使用 [new](../../../csharp/language-reference/keywords/new.md) 表达式创建[类](../../../csharp/language-reference/keywords/class.md)的对象时，实例构造函数可用于创建和初始化任意实例成员变量。 若要初始化[静态](../../../csharp/language-reference/keywords/static.md)类或非静态类中的静态变量，必须定义静态构造函数。 有关详细信息，请参阅[静态构造函数](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)。  
  
 下面的示例演示了实例构造函数：  
  
 [!code-csharp[csProgGuideObjects#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#5)]  
  
> [!NOTE]
>  为清楚起见，此类包含公共字段。 建议在编程时不要使用公共字段，因为这种做法会使程序中任何位置的任何方法都可以不受限制、不经验证地访问对象的内部组件。 数据成员通常应当为私有的，并且只应通过类方法和属性来访问。  
  
 只要创建基于 `Coords` 类的对象，就会调用此实例构造函数。 诸如此类不带参数的构造函数称为“默认构造函数”。 然而，提供其他构造函数通常十分有用。 例如，可以将构造函数添加到 `Coords` 类，以便可以为数据成员指定初始值：  
  
 [!code-csharp[csProgGuideObjects#76](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#76)]  
  
 这样便可以用默认或特定的初始值创建 `Coords` 对象，如下所示：  
  
 [!code-csharp[csProgGuideObjects#77](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#77)]  
  
 如果某个类没有构造函数，则会自动生成一个默认构造函数，并使用默认值来初始化对象字段。 例如，[int](../../../csharp/language-reference/keywords/int.md) 初始化为 0。 有关默认值的详细信息，请参阅[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。 由于 `Coords` 类的默认构造函数将所有数据成员都初始化为零，因此可以将它完全移除，而不会更改类的工作方式。 本主题稍后部分的示例 1 中提供了使用多个构造函数的完整示例，示例 2 中提供了自动生成的构造函数的示例。  
  
 也可以用实例构造函数来调用基类的实例构造函数。 类构造函数可通过初始值设定项来调用基类的构造函数，如下所示：  
  
 [!code-csharp[csProgGuideObjects#78](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#78)]  
  
 在此示例中，`Circle` 类将半径和高度的值传递给 `Shape`（`Circle` 从它派生而来）提供的构造函数。 使用 `Shape` 和 `Circle` 的完整示例完整示例请见本主题中的示例 3。  
  
## <a name="example-1"></a>示例 1  
 下面的示例说明包含两个类构造函数的类：一个类构造函数不带参数，另一个带有两个参数。  
  
 [!code-csharp[csProgGuideObjects#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#4)]  
  
## <a name="example-2"></a>示例 2  
 在此示例中，`Person` 没有任何构造函数；在这种情况下，将自动提供默认构造函数，同时将字段初始化为它们的默认值。  
  
 [!code-csharp[csProgGuideObjects#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#8)]  
  
 请注意，`age` 的默认值为 `0`，`name` 的默认值为`null`。 有关默认值的详细信息，请参阅[默认值表](../../../csharp/language-reference/keywords/default-values-table.md)。  
  
## <a name="example-3"></a>示例 3  
 下面的示例说明使用基类初始值设定项。 `Circle` 类派生自常规类 `Shape`，`Cylinder` 类派生自 `Circle` 类。 每个派生类的构造函数都使用其基类的初始值设定项。  
  
 [!code-csharp[csProgGuideObjects#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#9)]  
  
 有关调用基类构造函数的更多示例，请参阅 [virtual](../../../csharp/language-reference/keywords/virtual.md)、[override](../../../csharp/language-reference/keywords/override.md) 和 [base](../../../csharp/language-reference/keywords/base.md)。  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)
- [构造函数](../../../csharp/programming-guide/classes-and-structs/constructors.md)
- [终结器](../../../csharp/programming-guide/classes-and-structs/destructors.md)
- [static](../../../csharp/language-reference/keywords/static.md)
