---
title: '可以为 null 的类型 - C# 编程指南'
ms.custom: seodec18
description: '了解 C# 中可以为 null 的类型及其使用方法'
ms.date: 07/30/2018
helpviewer_keywords:
  - 'nullable types [C#]'
  - 'C# language, nullable types'
  - 'types [C#], nullable'
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
---
# <a name="nullable-types-c-programming-guide"></a>可以为 null 的类型（C# 编程指南）

可以为 null 的类型是 <xref:System.Nullable%601?displayProperty=nameWithType> 结构的实例。 可以为 null 的类型可表示一个基础类型的所有值 `T`，还可以再表示一个 [null](../../language-reference/keywords/null.md) 值。 基础类型 `T` 可以是任何不可为 null 的[值类型](../../language-reference/keywords/value-types.md)。 `T` 不能是引用类型。

例如，可以将 `null` 或任何整数值（从 <xref:System.Int32.MinValue?displayProperty=nameWithType> 到 <xref:System.Int32.MaxValue?displayProperty=nameWithType>）赋给 `Nullable<int>`，并可将 [true](../../language-reference/keywords/true-literal.md)[false](../../language-reference/keywords/false-literal.md) 或 `null` 赋给`Nullable<bool>`。

需要表示基础类型的未定义的值时，请使用可以为 null 的类型。 布尔变量只能有两个值：true 和 false。 没有“未定义”的值。 在许多编程应用程序中，尤其是数据库交互中，变量值可能未定义或缺失。 例如，数据库中的字段可能包含值 true 或 false，但它也可能根本不包含任何值。 这种情况下要使用 `Nullable<bool>` 类型。

可以为 null 的类型具有以下特征：
  
- 可以为 null 的类型表示可以向其赋与 `null` 值的值类型变量。 不能根据引用类型创建可以为 null 的类型 （引用类型已支持 `null` 值）。  
  
- 语法 `T?` 是 `Nullable<T>` 的简写。 这两种形式是可互换的。  
  
- 向可以为 null 的类型赋值的方法与向基础值类型赋值的方法相同：`int? x = 10;` 或 `double? d = 4.108;`。 还可赋予 `null` 值：`int? x = null;`。  
  
- 使用 <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> 和 <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> 只读属性可测试是否存在 null 值并检索值，如以下示例所示：`if (x.HasValue) y = x.Value;`  
  
  - 如果变量包含值，则 <xref:System.Nullable%601.HasValue%2A> 属性返回 `true`；如果值为 `null`，则返回 `false`。
  
  - 如果 <xref:System.Nullable%601.HasValue%2A> 返回 `true`，则 <xref:System.Nullable%601.Value%2A> 属性返回值。 否则会引发 <xref:System.InvalidOperationException>。  
  
- 还可将 `==` 和 `!=` 运算符用于可以为 null 的类型，如以下示例所示：`if (x != null) y = x.Value;` 如果 `a` 和 `b` 均为 null，则 `a == b` 的计算结果为 `true`。  

- 从 C# 7.0 开始，可以使用[模式匹配](../../pattern-matching.md#the-is-type-pattern-expression)来检查和获取可以为 null 的类型的值：`if (x is int valueOfX) y = valueOfX;`。
  
- `T?` 的默认值是一个实例，其 <xref:System.Nullable%601.HasValue%2A> 属性返回 `false`。  

- 使用 <xref:System.Nullable%601.GetValueOrDefault> 方法可返回赋予的值，如果可以为 null 的类型的值为 `null`，它还可返回基础值类型的[默认](../../language-reference/keywords/default-values-table.md)值。  

- 使用 <xref:System.Nullable%601.GetValueOrDefault(%600)> 方法可返回赋予的值，如果可以为 null 的类型的值为 `null`，它还可返回提供的默认值。
  
- 使用 [null 合并运算符](../../language-reference/operators/null-coalescing-operator.md) `??`，基于可以为 null 的类型的值向基础类型赋值：`int? x = null; int y = x ?? -1;`。 在示例中，由于 `x` 为 null，所以 `y` 的结果值为 `-1`。

- 如果定义了（用户定义的）两种数据类型之间的转换，还可将同一转换用于这些数据类型的可为 null 的版本。
  
- 不得嵌套可以为 null 的类型。 不会编译下面的一行代码：`Nullable<Nullable<int>> n;`  

有关详细信息，请参阅[使用可以为 null 的类型](using-nullable-types.md)，以及[如何：标识可以为 null 的类型](how-to-identify-a-nullable-type.md)主题。
  
## <a name="see-also"></a>请参阅

- <xref:System.Nullable%601?displayProperty=nameWithType>
- <xref:System.Nullable?displayProperty=nameWithType>
- [??运算符](../../language-reference/operators/null-coalescing-operator.md)
- [C# 编程指南](../index.md)
- [C# 指南](../../index.md)
- [C# 参考](../../language-reference/index.md)
- [可以为 Null 的值类型 (Visual Basic)](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
