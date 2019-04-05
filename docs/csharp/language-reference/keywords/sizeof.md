---
title: sizeof - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- sizeof_CSharpKeyword
- sizeof
helpviewer_keywords:
- sizeof keyword [C#]
ms.assetid: c548592c-677c-4f40-a4ce-e613f7529141
ms.openlocfilehash: 1c5526366651d7e6623724c939b08ac46aa7db56
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53242628"
---
# <a name="sizeof-c-reference"></a>sizeof（C# 参考）

用于获取非托管类型的大小（以字节为单位）。

非托管类型包括：

- 下表列出了简单类型：

   |表达式|常量值|
   |----------------|--------------------|
   |`sizeof(sbyte)`|1|
   |`sizeof(byte)`|1|
   |`sizeof(short)`|2|
   |`sizeof(ushort)`|2|
   |`sizeof(int)`|4|
   |`sizeof(uint)`|4|
   |`sizeof(long)`|8|
   |`sizeof(ulong)`|8|
   |`sizeof(char)`|2 (Unicode)|
   |`sizeof(float)`|4|
   |`sizeof(double)`|8|
   |`sizeof(decimal)`|16|
   |`sizeof(bool)`|1|

- 枚举类型。

- 指针类型。

- 用户定义的结构，不包含任何实例字段或作为引用类型或构造类型的自动实现的实例属性。

下面的示例演示如何检索 `int` 的大小：

```csharp
// Constant value 4:
int intSize = sizeof(int);
```

## <a name="remarks"></a>备注

从 C# 2.0 版开始，将 `sizeof` 应用于简单类型或枚举类型不再需要在[不安全](unsafe.md)上下文中编译代码。

不能重载 `sizeof` 运算符。 `sizeof` 运算符的返回值是 `int` 类型。 上表列出了一些常量值，这些值对应于以某些简单类型为操作数的 `sizeof` 表达式。

对于所有其他类型（包括结构），`sizeof` 运算符只能在不安全代码块中使用。 虽然可以使用 <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 方法，但此方法返回的值并不总是与 `sizeof` 返回的值相同。 <xref:System.Runtime.InteropServices.Marshal.SizeOf%2A?displayProperty=nameWithType> 在封送类型后返回大小，而 `sizeof` 返回公共语言运行时分配的大小（包括所有填充）。

## <a name="example"></a>示例

[!code-csharp[csrefKeywordsOperator#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#11)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [运算符关键字](operator-keywords.md)
- [enum](enum.md)
- [不安全代码和指针](../../programming-guide/unsafe-code-pointers/index.md)
- [结构](../../programming-guide/classes-and-structs/structs.md)
- [常量](../../programming-guide/classes-and-structs/constants.md)