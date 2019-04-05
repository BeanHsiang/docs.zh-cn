---
title: 扩展方法 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- methods [C#], adding to existing types
- extension methods [C#]
- methods [C#], extension
ms.assetid: 175ce3ff-9bbf-4e64-8421-faeb81a0bb51
ms.openlocfilehash: 35ab91279c9ed8703f29d8cbb8df3d7d4bf2a6b8
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57202218"
---
# <a name="extension-methods-c-programming-guide"></a>扩展方法（C# 编程指南）
扩展方法使你能够向现有类型“添加”方法，而无需创建新的派生类型、重新编译或以其他方式修改原始类型。 扩展方法是一种特殊的静态方法，但可以像扩展类型上的实例方法一样进行调用。 对于用 C#、F# 和 Visual Basic 编写的客户端代码，调用扩展方法与调用在类型中实际定义的方法没有明显区别。  
  
 最常见的扩展方法是 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 标准查询运算符，它将查询功能添加到现有的 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 和 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 类型。 若要使用标准查询运算符，请先使用 `using System.Linq` 指令将它们置于范围中。 然后，任何实现了 <xref:System.Collections.Generic.IEnumerable%601> 的类型看起来都具有 <xref:System.Linq.Enumerable.GroupBy%2A>、<xref:System.Linq.Enumerable.OrderBy%2A>、<xref:System.Linq.Enumerable.Average%2A> 等实例方法。 在 <xref:System.Collections.Generic.IEnumerable%601> 类型的实例（如 <xref:System.Collections.Generic.List%601> 或 <xref:System.Array>）后键入“dot”时，可以在 IntelliSense 语句完成中看到这些附加方法。  
  
 下面的示例演示如何对一个整数数组调用标准查询运算符 `OrderBy` 方法。 括号里面的表达式是一个 lambda 表达式。 很多标准查询运算符采用 Lambda 表达式作为参数，但这不是扩展方法的必要条件。 有关详细信息，请参阅 [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
 [!code-csharp[csProgGuideExtensionMethods#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#3)]  
  
 扩展方法被定义为静态方法，但它们是通过实例方法语法进行调用的。 它们的第一个参数指定该方法作用于哪个类型，并且该参数以 [this](../../../csharp/language-reference/keywords/this.md) 修饰符为前缀。 仅当你使用 `using` 指令将命名空间显式导入到源代码中之后，扩展方法才位于范围中。  
  
 下面的示例演示为 <xref:System.String?displayProperty=nameWithType> 类定义的一个扩展方法。 请注意，它是在非嵌套的、非泛型静态类内部定义的：  
  
 [!code-csharp[csProgGuideExtensionMethods#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#4)]  
  
 可使用此 `WordCount` 指令将 `using` 扩展方法置于范围中：  
  
```csharp  
using ExtensionMethods;  
```  
  
 而且，可以使用以下语法从应用程序中调用该扩展方法：  
  
```csharp  
string s = "Hello Extension Methods";  
int i = s.WordCount();  
```  
  
 在代码中，可以使用实例方法语法调用该扩展方法。 但是，编译器生成的中间语言 (IL) 会将代码转换为对静态方法的调用。 因此，并未真正违反封装原则。 实际上，扩展方法无法访问它们所扩展的类型中的私有变量。  
  
 有关详细信息，请参阅[如何：实现和调用自定义扩展方法](../../../csharp/programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method.md)。  
  
 通常，你更多时候是调用扩展方法而不是实现你自己的扩展方法。 由于扩展方法是使用实例方法语法调用的，因此不需要任何特殊知识即可从客户端代码中使用它们。 若要为特定类型启用扩展方法，只需为在其中定义这些方法的命名空间添加 `using` 指令。 例如，若要使用标准查询运算符，请将此 `using` 指令添加到代码中：  
  
```csharp  
using System.Linq;  
```  
  
 （你可能还必须添加对 System.Core.dll 的引用。）你将注意到，标准查询运算符现在作为可供大多数 <xref:System.Collections.Generic.IEnumerable%601> 类型使用的附加方法显示在 IntelliSense 中。  
  
## <a name="binding-extension-methods-at-compile-time"></a>在编译时绑定扩展方法  
 可以使用扩展方法来扩展类或接口，但不能重写扩展方法。 与接口或类方法具有相同名称和签名的扩展方法永远不会被调用。 编译时，扩展方法的优先级总是比类型本身中定义的实例方法低。 换句话说，如果某个类型具有一个名为 `Process(int i)` 的方法，而你有一个具有相同签名的扩展方法，则编译器总是绑定到该实例方法。 当编译器遇到方法调用时，它首先在该类型的实例方法中寻找匹配的方法。 如果未找到任何匹配方法，编译器将搜索为该类型定义的任何扩展方法，并且绑定到它找到的第一个扩展方法。 下面的示例演示编译器如何确定要绑定到哪个扩展方法或实例方法。  
  
## <a name="example"></a>示例  
 下面的示例演示 C# 编译器在确定是将方法调用绑定到类型上的实例方法还是绑定到扩展方法时所遵循的规则。 静态类 `Extensions` 包含为任何实现了 `IMyInterface` 的类型定义的扩展方法。 类 `A`、`B` 和 `C` 都实现了该接口。  
  
 `MethodB` 扩展方法永远不会被调用，因为它的名称和签名与这些类已经实现的方法完全匹配。  
  
 如果编译器找不到具有匹配签名的实例方法，它会绑定到匹配的扩展方法（如果存在这样的方法）。  
  
 [!code-csharp[csProgGuideExtensionMethods#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExtensionMethods/cs/extensionmethods.cs#5)]  
  
## <a name="general-guidelines"></a>通用准则  
 通常，建议你只在不得已的情况下才实现扩展方法，并谨慎地实现。 只要有可能，必须扩展现有类型的客户端代码都应该通过创建从现有类型派生的新类型来达到这一目的。 有关详细信息，请参阅[继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  
  
 在使用扩展方法来扩展你无法更改其源代码的类型时，你需要承受该类型实现中的更改会导致扩展方法失效的风险。  
  
 如果确实为给定类型实现了扩展方法，请记住以下几点：  
  
-   如果扩展方法与该类型中定义的方法具有相同的签名，则扩展方法永远不会被调用。  
  
-   在命名空间级别将扩展方法置于范围中。 例如，如果你在一个名为 `Extensions` 的命名空间中具有多个包含扩展方法的静态类，则这些扩展方法将全部由 `using Extensions;` 指令置于范围中。  
  
 针对已实现的类库，不应为了避免程序集的版本号递增而使用扩展方法。 如果要向你拥有源代码的库中添加重要功能，应遵循适用于程序集版本控制的标准 .NET Framework 准则。 有关详细信息，请参阅[程序集版本控制](../../../../docs/framework/app-domains/assembly-versioning.md)。  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [并行编程示例（这些示例包括许多示例扩展方法）](https://code.msdn.microsoft.com/Samples-for-Parallel-b4b76364)
- [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
- [标准查询运算符概述](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Conversion rules for Instance parameters and their impact](https://blogs.msdn.microsoft.com/sreekarc/2007/10/11/conversion-rules-for-instance-parameters-and-their-impact)（实例参数及其影响的转换规则）
- [Extension methods Interoperability between languages](https://blogs.msdn.microsoft.com/sreekarc/2007/10/11/extension-methods-interoperability-between-languages)（语言间扩展方法的互操作性）
- [Extension methods and Curried Delegates](https://blogs.msdn.microsoft.com/sreekarc/2007/05/01/extension-methods-and-curried-delegates)（扩展方法和扩充委托）
- [Extension method Binding and Error reporting](https://blogs.msdn.microsoft.com/sreekarc/2007/04/26/extension-method-binding-and-error-reporting)（扩展方法绑定和错误报告）
