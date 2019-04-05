---
title: '[] 运算符 - C# 参考'
ms.custom: seodec18
ms.date: 01/10/2019
f1_keywords:
- '[]_CSharpKeyword'
helpviewer_keywords:
- subscript operator [C#]
- square brackets [ ] operator [C#]
- '[] operator [C#]'
- indexing operator [C#]
ms.assetid: 5c16bb45-88f7-45ff-b42c-1af1972b042c
ms.openlocfilehash: 9088393f61d300ee76e56e320bec17b4a79bfebb
ms.sourcegitcommit: bd28ff1e312eaba9718c4f7ea272c2d4781a7cac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2019
ms.locfileid: "56835585"
---
# <a name="-operator-c-reference"></a>[] 运算符（C# 参考）

方括号 `[]` 通常用于数组、索引器或指针元素访问。

有关指针元素访问的详细信息，请参阅[如何：通过指针访问数组元素](../../programming-guide/unsafe-code-pointers/how-to-access-an-array-element-with-a-pointer.md)。

方括号还用于指定[属性](../../programming-guide/concepts/attributes/index.md)：

```csharp
[System.Diagnostics.Conditional("DEBUG")]
void TraceMethod() {}
```

## <a name="array-access"></a>数组访问

下面的示例演示如何访问数组元素：

[!code-csharp-interactive[array access](~/samples/snippets/csharp/language-reference/operators/IndexOperatorExamples.cs#Arrays)]

如果数组索引超出数组相应维度的边界，将引发 <xref:System.IndexOutOfRangeException>。

如前面的示例所示，还可以在声明数组类型和实例化数组实例时使用方括号。

有关数组的详细信息，请参阅[数组](../../programming-guide/arrays/index.md)。

## <a name="indexer-access"></a>索引器访问

下面的示例使用 .NET <xref:System.Collections.Generic.Dictionary%602>类型来演示索引器访问：

[!code-csharp-interactive[indexer access](~/samples/snippets/csharp/language-reference/operators/IndexOperatorExamples.cs#Indexers)]

使用索引器，可通过类似于编制数组索引的方式对用户定义类型的实例编制索引。 与必须是整数的数组索引不同，可以将索引器参数声明为任何类型。

有关索引器的详细信息，请参阅[索引器](../../programming-guide/indexers/index.md)。

## <a name="operator-overloadability"></a>运算符可重载性

元素访问 `[]` 不被视为可重载运算符。 使用[索引器](../../programming-guide/indexers/index.md)以支持对用户定义的类型编制索引。

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[元素访问](~/_csharplang/spec/expressions.md#element-access)和[指针元素访问](~/_csharplang/spec/unsafe-code.md#pointer-element-access)部分。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 运算符](index.md)
- [数组](../../programming-guide/arrays/index.md)
- [索引器](../../programming-guide/indexers/index.md)
- [指针类型](../../programming-guide/unsafe-code-pointers/pointer-types.md)
- [特性](../../programming-guide/concepts/attributes/index.md)
- [?. 和 ?[] 运算符](null-conditional-operators.md)