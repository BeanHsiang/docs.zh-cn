---
title: delegate - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- delegate_CSharpKeyword
- delegate
- CS0123
helpviewer_keywords:
- delegate keyword [C#]
- function pointers [C#]
ms.assetid: 0bb8cb6d-2f87-47c7-9d1f-d65c1cd01e9f
ms.openlocfilehash: f9df40c3ca721ca97b575a05377bbac29a29aec9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54560602"
---
# <a name="delegate-c-reference"></a>委托（C# 参考）

委托类型的声明与方法签名相似。 它有一个返回值和任意数目任意类型的参数：

```csharp
public delegate void TestDelegate(string message);
public delegate int TestDelegate(MyType m, long num);
```

`delegate` 是一种可用于封装命名方法或匿名方法的引用类型。 委托类似于 C++ 中的函数指针；但是，委托是类型安全和可靠的。 有关委托的应用，请参阅[委托](../../../csharp/programming-guide/delegates/index.md)和[泛型委托](../../../csharp/programming-guide/generics/generic-delegates.md)。

## <a name="remarks"></a>备注

委托是[事件](../../../csharp/programming-guide/events/index.md)的基础。

通过将委托与命名方法或匿名方法关联，可以实例化委托。 有关详细信息，请参阅[命名方法](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)和[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)。

必须使用具有兼容返回类型和输入参数的方法或 lambda 表达式实例化委托。 有关方法签名中允许的差异程度的详细信息，请参阅[委托中的变体](../../programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)。 为了与匿名方法一起使用，委托和与之关联的代码必须一起声明。 本节讨论这两种实例化委托的方法。

## <a name="example"></a>示例

[!code-csharp[csrefKeywordsTypes#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#8)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](../../../csharp/language-reference/keywords/index.md)
- [引用类型](../../../csharp/language-reference/keywords/reference-types.md)
- [委托](../../../csharp/programming-guide/delegates/index.md)
- [事件](../../../csharp/programming-guide/events/index.md)
- [带有命名方法的委托与带有匿名方法的委托](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)
- [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)
- [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
