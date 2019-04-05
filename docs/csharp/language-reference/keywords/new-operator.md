---
title: new 运算符 - C# 参考
ms.custom: seodec18
ms.date: 03/15/2018
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: e528771d7afeec705f35fa3093a3e4f534b3a1e4
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53239847"
---
# <a name="new-operator-c-reference"></a>new 运算符（C# 参考）

用于创建对象和调用构造函数。 例如:

```csharp
Class1 obj  = new Class1();
```

它还用于创建匿名类型的实例：

```csharp
var query = from cust in customers
            select new { Name = cust.Name, Address = cust.PrimaryAddress };
```

`new` 运算符还用于调用值类型的默认构造函数。 例如:

```csharp
int i = new int();
```

在前面的语句中，`i` 的初始值为 `0`，这是类型 `int` 的默认值。 此语句与下面的语句的效果相同：

```csharp
int i = 0;
```

有关默认值的完整列表，请参阅[默认值表](default-values-table.md)。

请记住，为 [struct](struct.md) 声明默认构造函数是错误的，因为每个值类型均隐式含有公共默认构造函数。 可以对结构类型声明参数化构造函数，以设置其初始值，但仅在需要除默认值以外的值时才需要这样做。

值类型对象（如结构）和引用类型对象（如类）都会自动销毁，但值类型对象是在其包含的上下文被销毁时才会销毁，而引用类型对象是在对它们的最后一个引用被删除后的未指定时间由垃圾回收器销毁。 对于包含文件句柄或网络连接等资源的类型，最好使用确定性清理来确保尽快释放其包含的资源。 有关详细信息，请参阅 [Using 语句](using-statement.md)。

不能重载 `new` 运算符。

如果 `new` 运算符无法分配内存，则引发异常 <xref:System.OutOfMemoryException>。

## <a name="example"></a>示例

在下面的示例中，使用 `new` 运算符创建并初始化 `struct` 对象和类对象，并向它们分配值。 显示默认值和分配的值。

[!code-csharp[csrefKeywordsOperator#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#7)]

请注意，本示例中字符串的默认值为 `null`。 因此，未显示此字符串。

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../language-reference/index.md)
- [C# 编程指南](../../programming-guide/index.md)
- [C# 关键字](index.md)
- [运算符关键字](operator-keywords.md)
- [new](new.md)
- [匿名类型](../../programming-guide/classes-and-structs/anonymous-types.md)