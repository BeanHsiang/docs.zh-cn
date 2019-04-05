---
title: typeof - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- typeof
- typeof_CSharpKeyword
helpviewer_keywords:
- typeof keyword [C#]
ms.assetid: 0c08d880-515e-46bb-8cd2-48b8dd62c08d
ms.openlocfilehash: f218414bf60a86b95461d747fb6c557f03bcfcb3
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "57846111"
---
# <a name="typeof-c-reference"></a>typeof（C# 参考）

用于为类型获取 <xref:System.Type?displayProperty=nameWithType> 对象。 `typeof` 表达式采用以下格式：

```csharp
System.Type type = typeof(int);
```

## <a name="remarks"></a>备注

若要获取表达式的运行时类型，可以使用 .NET Framework 方法 <xref:System.Object.GetType%2A>，如以下示例所示：

```csharp
int i = 0;
System.Type type = i.GetType();
```

不能重载 `typeof` 运算符。

`typeof` 运算符也可用于开放式泛型类型。 具有多个类型参数的类型必须在规范中具有适当数量的逗号。 例如，<xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWIthType> 有两个类型参数，因此，请使用一个逗号：

```csharp
Type t = typeof(System.Collection.Generic.Dictionary<,>);
```

以下示例显示如何确定方法的返回类型是否为泛型 <xref:System.Collections.Generic.IEnumerable%601>。 如果返回类型不是 <xref:System.Collections.Generic.IEnumerable%601> 泛型类型，则 <xref:System.Type.GetInterface%2A?displayProperty=nameWithType> 将返回 `null`。

[!code-csharp[typeof_3.cs](~/samples/snippets/csharp/keywords/typeof/typeof_3.cs)]

## <a name="example"></a>示例

[!code-csharp[csrefKeywordsOperator#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#12)] 

## <a name="example"></a>示例

此示例使用 <xref:System.Object.GetType%2A> 方法来确定用于包含数值计算结果的类型。 这取决于所得数字的存储要求。

[!code-csharp[csrefKeywordsOperator#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#13)]

## <a name="c-language-specification"></a>C# 语言规范

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的 [typeof 运算符](~/_csharplang/spec/expressions.md#the-typeof-operator)。 该语言规范是 C# 语法和用法的权威资料。

## <a name="see-also"></a>请参阅

- <xref:System.Type?displayProperty=nameWithType>
- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](../../../csharp/language-reference/keywords/index.md)
- [is](../../../csharp/language-reference/keywords/is.md)
- [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)
