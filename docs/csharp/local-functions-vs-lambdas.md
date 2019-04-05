---
title: 本地函数与 Lambda 表达式
description: 了解为什么选择本地函数比选择 Lambda 表达式更好。
ms.date: 06/27/2016
ms.assetid: 368d1752-3659-489a-97b4-f15d87e49ae3
ms.openlocfilehash: 17ad1e8782adbf9e0f892d72849e58ef9c5ddce1
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "58125767"
---
# <a name="local-functions-compared-to-lambda-expressions"></a>本地函数与 Lambda 表达式比较

乍看之下，[本地函数](programming-guide/classes-and-structs/local-functions.md)和 [lambda 表达式](./programming-guide/statements-expressions-operators/lambda-expressions.md)非常相似。 在许多情况下，选择使用 Lambda 表达式还是本地函数是风格和个人偏好的问题。 但是，应该注意，从两者中选用一种的时机和条件其实是存在差别的。

让我们检查一下阶乘算法的本地函数实现和 lambda 表达式实现之间的差异。 首先使用本地函数的版本：

[!code-csharp[LocalFunctionFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#37_LocalFunctionFactorial "Recursive factorial using local function")]

将该实现与使用 Lambda 表达式的版本对比：

[!code-csharp[26_LambdaFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#38_LambdaFactorial "Recursive factorial using lambda expressions")]

本地函数具有名称。 Lambda 表达式是赋给 `Func` 或 `Action` 类型变量的匿名方法。 在声明本地函数时，参数类型和返回类型是函数声明的一部分。 参数类型和返回类型不是 Lambda 表达式主体的一部分，而是 Lambda 表达式变量类型声明的一部分。 这两种差别可以产生跟清楚的代码。

本地函数的明确赋值规则与 Lambda 表达式的不同。 从范围内的任意代码位置都可以引用本地函数声明。 在可以访问（或通过引用 Lambda 表达式的委托调用）Lambda 表达式之前，必须先将 Lambda 表达式赋给委托变量。请注意，使用 lambda 表达式的版本必须先定义 lambda 表达式 `nthFactorial`，然后再对其进行声明并实例化。 否则，会导致分配前引用 `nthFactorial` 时出现编译时错误。
这些区别意味着使用本地函数创建递归算法会更轻松。 你可以声明和定义一个调用自身的本地函数。 必须声明 Lambda 表达式，赋给默认值，然后才能将其重新赋给引用相同 Lambda 表达式的主体。

明确分配规则也会影响本地函数或 Lambda 表达式捕获的任何变量。 本地函数和 Lambda 表达式规则都要求在将本地函数或 Lambda 表达式转换为委托时，明确分配任何捕获的变量。 区别在于 Lambda 表达式在声明时转换为委托。 只有在用作委托时，本地函数才转换为委托。 如果声明了本地函数，但只是通过像调用方法一样调用该函数来引用该函数，它将不会转换成委托。 使用该规则可在封闭范围内的任何方便的位置声明本地函数。 声明本地函数的位置常见于父方法的末尾和返回任何语句后方。

第三，编译器可以执行静态分析，因此本地函数能够在封闭范围内明确分配捕获的变量。 请看以下示例：

```csharp
int M()
{
    int y;
    LocalFunction();
    return y;

    void LocalFunction() => y = 0;
}
```

编译器可以确定 `LocalFunction` 在调用时明确分配 `y`。 因为在 `return` 语句之前调用了 `LocalFunction`，所以在 `return` 语句中明确分配了 `y`。

可实现示例分析的分析允许第四个差异。
根据它们的用途，本地函数可以避免 Lambda 表达式始终需要的堆分配。 如果本地函数永远不会转换为委托，并且本地函数捕获的变量都不会被其他转换为委托的 lambda 或本地函数捕获，则编译器可以避免堆分配。 

请看以下异步示例：

[!code-csharp[TaskLambdaExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#36_TaskLambdaExample "Task returning method with lambda expression")]

该 lambda 表达式的闭包包含 `address`、`index` 和 `name` 变量。 就本地函数而言，实现闭包的对象可能为 `struct` 类型。 该结构类型将通过引用传递给本地函数。 实现中的这个差异将保存在分配上。

Lambda 表达式所需的实例化意味着额外的内存分配，后者可能是时间关键代码路径中的性能因素。
本地函数不会产生这种开销。 在以上示例中，本地函数版本具有的分配比 lambda 表达式版本少 2 个。

> [!NOTE]
> 等效于此方法的本地函数还将类用于闭包。 实现详细信息包括本地函数的闭包是作为 `class` 还是 `struct` 实现。 本地函数可能使用 `struct`，而 lambda 将始终使用 `class`。

[!code-csharp[TaskLocalFunctionExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#29_TaskExample "Task returning method with local function")]

在本示例中尚未演示的最后一个优点是，可将本地函数作为迭代器实现，使用 `yield return` 语法生成一系列值。 Lambda 表达式中不允许使用 `yield return` 语句。

虽然本地函数对 lambda 表达式可能有点冗余，但实际上它们的目的和用法都不一样。
如果想要编写仅从上下文或其他方法中调用的函数，则使用本地函数更高效。
