---
title: where（泛型类型约束）- C# 参考
ms.custom: seodec18
ms.date: 04/12/2018
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.openlocfilehash: 094358dea9054bf198ded77736dc45af1a436787
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54221123"
---
# <a name="where-generic-type-constraint-c-reference"></a>where（泛型类型约束）（C# 参考）

泛型定义中的 `where` 子句指定对用作泛型类型、方法、委托或本地函数中类型参数的参数类型的约束。 约束可指定接口、基类或要求泛型类型为引用、值或非托管类型。 它们声明类型参数必须具备的功能。

例如，可以声明一个泛型类 `MyGenericClass`，以使类型参数 `T` 实现 <xref:System.IComparable%601> 接口：

[!code-csharp[using an interface constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#1)]

> [!NOTE]
> 有关查询表达式中的 where 子句的详细信息，请参阅 [where 子句](where-clause.md)。

`where` 子句还可包括基类约束。 基类约束表明用作该泛型类型的类型参数的类型具有指定的类作为基类（或者是该基类），以用作该泛型类型的类型参数。 该基类约束一经使用，就必须出现在该类型参数的所有其他约束之前。 某些类型不允许作为基类约束：<xref:System.Object>、<xref:System.Array> 和 <xref:System.ValueType>。 在 C# 7.3 之前，<xref:System.Enum>、<xref:System.Delegate> 和 <xref:System.MulticastDelegate> 也不允许作为基类约束。 以下示例显示现可指定为基类的类型：

[!code-csharp[using an interface constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#2)]

`where` 子句可指定类型为 `class` 或 `struct`。 `struct` 约束不再需要指定 `System.ValueType` 的基类约束。 `System.ValueType` 类型可能不用作基类约束。 以下示例显示 `class` 和 `struct` 约束：

[!code-csharp[using the class and struct constraints](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#3)]

`where` 子句还可包括 `unmanaged` 约束。 `unmanaged` 约束将类型参数限制为名为“非托管类型”的类型。 “非托管类型”不是引用类型，且任何嵌套级别都不包含引用类型字段。 `unmanaged` 约束使得在 C# 中编写低级别的互操作代码变得更容易。 此约束支持跨所有非托管类型的可重用例程。 `unmanaged` 约束不能与 `class` 或 `struct` 约束结合使用。 `unmanaged` 约束强制该类型必须为 `struct`：

[!code-csharp[using the unmanaged constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#4)]

`where` 子句也可能包括构造函数约束 `new()`。 该约束使得能够使用 `new` 运算符创建类型参数的实例。 [new() 约束](new-constraint.md)可以让编译器知道：提供的任何类型参数都必须具有可访问的无参数（或默认）构造函数。 例如:

[!code-csharp[using the new constraint](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#5)]

`new()` 约束出现在 `where` 子句的最后。 `new()` 约束不能与 `struct` 或 `unmanaged` 约束结合使用。 所有满足这些约束的类型必须具有可访问的无参数构造函数，这使得 `new()` 约束冗余。

对于多个类型参数，每个类型参数都使用一个 `where` 子句，例如：

[!code-csharp[using multiple where constraints](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#6)]

还可将约束附加到泛型方法的类型参数，如以下示例所示：

[!code-csharp[where constraints with generic methods](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#7)]

请注意，对于委托和方法两者来说，描述类型参数约束的语法是一样的：

[!code-csharp[where constraints with generic methods](../../../../samples/snippets/csharp/keywords/GenericWhereConstraints.cs#8)]

有关泛型委托的信息，请参阅[泛型委托](../../../csharp/programming-guide/generics/generic-delegates.md)。

有关约束的语法和用法的详细信息，请参阅[类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)。

## <a name="c-language-specification"></a>C# 语言规范

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)
- [new 约束](../../../csharp/language-reference/keywords/new-constraint.md)
- [类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)