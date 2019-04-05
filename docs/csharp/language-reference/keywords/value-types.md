---
title: 值类型 - C# 参考
ms.custom: seodec18
ms.date: 11/26/2018
f1_keywords:
- cs.valuetypes
helpviewer_keywords:
- value types [C#]
- types [C#], value types
- C# language, value types
ms.assetid: 471eb994-2958-49d5-a6be-19b4313f80a3
ms.openlocfilehash: 77aed78e7822e06b3b1e6c48b07790d93e09559c
ms.sourcegitcommit: fa38fe76abdc8972e37138fcb4dfdb3502ac5394
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53612720"
---
# <a name="value-types-c-reference"></a>值类型（C# 参考）

有两种值类型：

- [结构](struct.md)

- [枚举](enum.md)

## <a name="main-features-of-value-types"></a>值类型的主要功能

值类型的变量包含类型的值。 例如，`int` 类型的变量可以包含值 `42`。 它不同于引用类型的变量，后者（也称为对象）包含对类型实例的引用。 将新的值分配到值类型的变量时，会复制该值。 将新的值分配到引用类型的变量时，会复制引用，而不复制对象本身。

所有值类型都隐式派生自 <xref:System.ValueType?displayProperty=nameWithType>。

与引用类型不同，不能从值类型派生新类型。 但是，与引用类型一样，结构可以实现接口。

值类型变量不能默认为 `null`。 但相应的[可以为空的类型](../../../csharp/programming-guide/nullable-types/index.md)的变量可以为 `null`。

每个值类型都具有一个初始化该类型的默认值的隐式默认构造函数。 有关值类型的默认值的信息，请参阅[默认值表](default-values-table.md)。

## <a name="simple-types"></a>简单类型

简单类型是 C# 提供的一组预定义的结构类型，其中包括以下类型：

- [整型类型](integral-types-table.md)：整数类型和 [字符型](char.md)类型
- [浮点类型](floating-point-types-table.md)
- [bool](bool.md)

简单类型通过关键字标识，但这些关键字只是 <xref:System> 命名空间中的预定义结构类型的别名。 例如， [int](int.md) 是 <xref:System.Int32?displayProperty=nameWithType> 的别名。 有关别名的完整列表，请参阅[内置类型表](built-in-types-table.md)。

简单类型不同于其他结构类型，简单类型允许某些附加操作：

- 可以使用文本初始化简单类型。 例如，`'A'` 是类型 `char` 的文本，`2001` 是类型 `int` 的文本。

- 可以使用 [const](const.md) 关键字声明简单类型的常数。 无法包含其他结构类型的常数。

- 其操作数都是简单类型常数的常量表达式在编译时进行评估。

有关详细信息，请参阅 [C# 语言规范](../language-specification/index.md)中的[简单类型](~/_csharplang/spec/types.md#simple-types)部分。

## <a name="initializing-value-types"></a>初始化值类型

在使用 C# 中的本地变量之前，必须对其进行初始化。 例如，可以声明未初始化的本地变量，如以下示例所示：

```csharp
int myInt;
```

在未初始化之前，无法使用。 可以使用以下语句将其初始化：

```csharp
myInt = new int();  // Invoke default constructor for int type.
```

此语句等效于以下语句：

```csharp
myInt = 0;         // Assign an initial value, 0 in this example.
```

当然，可以在同一语句中进行声明和初始化，如以下示例所示：

```csharp
int myInt = new int();
```

- 或 -

```csharp
int myInt = 0;
```

使用 [new](new.md) 运算符将调用特定类型的默认构造函数，并向变量赋予默认值。 在前面的示例中，默认构造函数将值 `0` 赋予了 `myInt`。 有关通过调用默认构造函数所赋予的值的详细信息，请参阅[默认值表](default-values-table.md)。

对于用户定义类型，请使用 [new](new.md) 调用默认构造函数。 例如，以下语句调用 `Point` 结构的默认构造函数：

```csharp
Point p = new Point(); // Invoke default constructor for the struct.
```

进行此调用后，该结构被视为已明确赋值；即，它的所有成员都被初始化为其默认值。

有关 `new` 运算符的详细信息，请参阅 [new](new.md)。

有关设置数值类型的输出格式的信息，请参阅[设置数值结果表的格式](formatting-numeric-results-table.md)。

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [类型](types.md)
- [类型引用表](reference-tables-for-types.md)
- [引用类型](reference-types.md)
- [可以为 null 的类型](../../programming-guide/nullable-types/index.md)