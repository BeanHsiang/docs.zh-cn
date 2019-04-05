---
title: enum 关键字 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- enum
- enum_CSharpKeyword
helpviewer_keywords:
- enum keyword [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
ms.openlocfilehash: 768d8da320022a686f2ecfe5222880eccacee7dd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54727633"
---
# <a name="enum-c-reference"></a>enum（C# 参考）

`enum` 关键字用于声明枚举，一种包含一组被称为枚举数列表的已命名常数的不同类型。  

通常最好是直接在命名空间内定义枚举，以便命名空间中的所有类都可以同样方便地访问它。 但是，也可能会在类或结构中嵌套枚举。

默认情况下，第一个枚举数具有值 0，并且每个连续枚举数的值将增加 1。 例如，在以下枚举中， `Sat` 的值为 `0`， `Sun` 的值为 `1`， `Mon` 的值为 `2`，依次类推。

```csharp
enum Day {Sat, Sun, Mon, Tue, Wed, Thu, Fri};
```

枚举数可以使用初始值设定项来替代默认值，如下面的示例中所示。

```csharp
enum Day {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
```

在此枚举中，强制元素的序列从 `1` 开始，而不是 `0`。 但建议包括一个值为 0 的常量。 有关详细信息，请参阅[枚举类型](../../programming-guide/enumeration-types.md)。

每个枚举类型都有一个基础类型，该基础类型可以是除 [char](char.md) 外的任何整型类型。 枚举元素的默认基础类型是 [int](int.md)。若要声明另一整型的枚举（如 [byte](byte.md)），则请在后跟该类型的标识符后使用冒号，如以下示例所示。

```csharp
enum Day : byte {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
```

已批准的枚举类型有 [byte](byte.md)、[sbyte](sbyte.md)、[short](short.md)、[ushort](ushort.md)、[int](int.md)、[uint](uint.md), [long](long.md) 或 [ulong](ulong.md)。

枚举类型的变量可在基本类型范围内分配到任何值；这些值不限于已命名常数。

`enum E` 的默认值是由表达式 `(E)0`生成的值。

> [!NOTE]
> 枚举数名称中不能含有空格。

基础类型指定为每个枚举数分配多少存储空间。 但要将 `enum` 类型转换为整型，则必须使用显示转换。 例如，以下语句通过使用转换将 `Sun` 转换为 [，从而将枚举数](int.md) 赋值为 `enum` int `int`类型的变量。

```csharp
int x = (int)Day.Sun;
```

当你将 <xref:System.FlagsAttribute?displayProperty=nameWithType> 应用到包含可与按位 `OR` 运算组合的元素的枚举中时，该特性与某些工具一起使用时会影响 `enum` 的行为。 当你使用工具（如 <xref:System.Console> 类方法和表达式计算器）时，你可以注意到这些更改。 （请参阅第三个示例。）

## <a name="robust-programming"></a>可靠编程

正如任何常量一样，对枚举的各项值的所有引用在编译时都会转换为数字参数。 这可能会造成如[常量](../../programming-guide/classes-and-structs/constants.md)中所述的潜在版本问题。

将其他值分配到枚举的新版本，或者在新版本中更改枚举成员的值，会导致出现相关源代码问题。 通常在 [switch](switch.md) 语句中使用枚举值。 如果已将其他元素添加到 `enum` 类型，则 switch 语句的默认部分可被意外地选中。

如果其他开发人员使用你的代码，则在将新元素添加到任何 `enum` 类型时应提供有关他们的代码应该如何响应的准则。

## <a name="example"></a>示例

在下面的示例中，已声明枚举 `Day`。 已将两个枚举数显式转换为整数，并赋值为整数变量。

[!code-csharp[csrefKeywordsTypes#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#10)]

## <a name="example"></a>示例

以下示例中，使用基类型选项来声明其成员是 `enum` 类型的 `long`。 请注意，即使该枚举的基础类型是 `long`，仍然需通过使用转换将枚举成员显式转换为类型 `long` 。

[!code-csharp[csrefKeywordsTypes#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#11)]

## <a name="example"></a>示例

下面的代码示例说明了 <xref:System.FlagsAttribute?displayProperty=nameWithType> 声明中 `enum` 特性的使用和作用。

[!code-csharp[csrefKeywordsTypes#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#12)]

## <a name="comments"></a>注释

如果删除 `Flags`，则示例将显示以下值：

`5`

`5`

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [枚举类型](../../programming-guide/enumeration-types.md)
- [C# 关键字](index.md)
- [整型表](integral-types-table.md)
- [内置类型表](built-in-types-table.md)
- [隐式数值转换表](implicit-numeric-conversions-table.md)
- [显式数值转换表](explicit-numeric-conversions-table.md)
- [枚举命名约定](../../../standard/design-guidelines/names-of-classes-structs-and-interfaces.md#naming-enumerations)
