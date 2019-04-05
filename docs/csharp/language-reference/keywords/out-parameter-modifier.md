---
title: out 参数修饰符 - C# 参考
ms.custom: seodec18
ms.date: 03/06/2018
helpviewer_keywords:
- parameters [C#], out
- out parameters [C#]
ms.openlocfilehash: 8aebe0492728f3ef87256f5d8c4859220d9106cf
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54660003"
---
# <a name="out-parameter-modifier-c-reference"></a>out 参数修饰符（C# 参考）
`out` 关键字通过引用传递参数。 它与 [ref](ref.md) 关键字相似，只不过 `ref` 要求在传递之前初始化变量。 它也类似于 [in](in-parameter-modifier.md) 关键字，只不过 `in` 不允许通过调用方法来修改参数值。 若要使用 `out` 参数，方法定义和调用方法均必须显式使用 `out` 关键字。 例如:  
  
[!code-csharp-interactive[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/OutParameterModifier.cs#1)]  

> [!NOTE] 
> `out` 关键字也可与泛型类型参数结合使用，以指定该类型参数是协变参数。 有关在此上下文中使用 `out` 关键字的详细信息，请参阅 [out（泛型修饰符）](out-generic-modifier.md)。
  
作为 `out` 参数传递的变量在方法调用中传递之前不必进行初始化。 但是，被调用的方法需要在返回之前赋一个值。  
  
尽管 `in`、`ref` 和 `out` 关键字会导致不同的运行时行为，它们并不被视为编译时方法签名的一部分。 因此，如果唯一的不同是一个方法采用 `ref` 或 `in` 参数，而另一个方法采用 `out` 参数，则无法重载这两个方法。 例如，以下代码将不会编译：  
  
```csharp
class CS0663_Example
{
    // Compiler error CS0663: "Cannot define overloaded 
    // methods that differ only on ref and out".
    public void SampleMethod(out int i) { }
    public void SampleMethod(ref int i) { }
}
```
  
但是，如果一个方法采用 `ref`、`in` 或 `out` 参数，而另一个方法采用其他参数，则可以完成重载，如：  
  
[!code-csharp[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/OutParameterModifier.cs#2)]  

编译器通过将调用站点上的参数修饰符与方法调用中使用的参数修饰符进行匹配，从而选择最佳重载。
 
属性不是变量，因此不能作为 `out` 参数传递。
  
不能将 `in`、`ref` 和 `out` 关键字用于以下几种方法：  
  
-   异步方法，通过使用 [async](../../../csharp/language-reference/keywords/async.md) 修饰符定义。  
  
-   迭代器方法，包括 [yield return](../../../csharp/language-reference/keywords/yield.md) 或 `yield break` 语句。  

## <a name="declaring-out-arguments"></a>声明 `out` 参数   

 如果希望方法返回多个值，可以声明具有多个 `out` 参数的方法。 下面的示例使用 `out` 返回具有单个方法调用的三个变量。 注意，第三个参数赋 null 值。 这使得方法可以有选择地返回值。  
  
[!code-csharp-interactive[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/OutParameterModifier.cs#3)]  

 [重试模式](/visualstudio/code-quality/ca1021-avoid-out-parameters#try-pattern-methods)会返回一个 `bool`，指示某个操作是成功还是失败，并在 `out` 参数中返回该操作生成的值。 许多分析方法（如 [DateTime.TryParse](xref:System.DateTime.TryParse(System.String,System.DateTime@)) 方法）都采用此模式。
   
## <a name="calling-a-method-with-an-out-argument"></a>调用具有 `out` 参数的方法

在 C# 6 及更早版本中，必须先在单独的语句中声明变量，然后才能将其作为 `out` 参数传递。 下面的示例先声明了变量 `number`，然后再将它传递给将字符串转换为数字的 [Int32.TryParse](xref:System.Int32.TryParse(System.String,System.Int32@)) 方法。

[!code-csharp-interactive[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/OutParameterModifier.cs#4)]  

从 C# 7.0 开始，可以在方法调用的参数列表而不是单独的变量声明中声明 `out` 变量。 这使得代码更简洁可读，还能防止在方法调用之前无意中向该变量赋值。 下面的示例与上一个示例基本相同，不同之处在于它在对 [Int32.TryParse](xref:System.Int32.TryParse(System.String,System.Int32@)) 方法的调用中定义了 `number` 变量。

[!code-csharp-interactive[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/OutParameterModifier.cs#5)]  
   
在上一个示例中，`number` 变量被强类型化为 `int`。 你也可以声明一个隐式类型本地变量，如以下示例所示。

[!code-csharp-interactive[cs-out-keyword](../../../../samples/snippets/csharp/language-reference/keywords/in-ref-out-modifier/OutParameterModifier.cs#6)]  
   
## <a name="c-language-specification"></a>C# 语言规范  
[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](../../../csharp/language-reference/keywords/index.md)
- [方法参数](../../../csharp/language-reference/keywords/method-parameters.md)
