---
title: 重试...Catch...Finally 语句-Visual Basic
description: 了解如何使用异常处理用于 Visual Basic Try/Catch/Finally 语句。
ms.date: 12/07/2018
f1_keywords:
- vb.Try...Catch...Finally
- vb.when
- vb.Finally
- vb.Catch
- vb.Try
helpviewer_keywords:
- Try...Catch...Finally statements
- Try statement [Visual Basic]
- try-catch exception handling, Try...Catch...Finally statements
- error handling, while running code
- Try statement [Visual Basic], Try...Catch...Finally
- Finally keyword [Visual Basic], Try...Catch...Finally
- Catch statement [Visual Basic]
- When keyword [Visual Basic]
- Visual Basic code, handling errors while running
- structured exception handling, Try...Catch...Finally statements
ms.assetid: d6488026-ccb3-42b8-a810-0d97b9d6472b
ms.custom: seodec18
ms.openlocfilehash: 2e4fef836b08f536565105dbab76292b2fc4388e
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54221708"
---
# <a name="trycatchfinally-statement-visual-basic"></a>Try...Catch...Finally 语句 (Visual Basic)

提供了一种方法来处理可能会出现在给定的块的代码，同时仍在运行代码的部分或全部可能错误。

## <a name="syntax"></a>语法

```vb
Try
    [ tryStatements ]
    [ Exit Try ]
[ Catch [ exception [ As type ] ] [ When expression ]
    [ catchStatements ]
    [ Exit Try ] ]
[ Catch ... ]
[ Finally
    [ finallyStatements ] ]
End Try
```

## <a name="parts"></a>部件

|术语|定义|
|---|---|
|`tryStatements`|可选。 语句可能会出错。 可以是复合语句。|
|`Catch`|可选。 多个`Catch`允许的块。 如果处理时，会发生异常`Try`块，每个`Catch`语句检查按文本顺序，以确定是否将它与处理异常，`exception`表示已引发的异常。|
|`exception`|可选。 任何变量名称。 `exception` 的初始值是引发的错误的值。 用于`Catch`指定错误捕获。 如果省略，`Catch`语句将捕获所有异常。|
|`type`|可选。 指定类筛选器的类型。 如果的值`exception`是由指定类型的`type`或派生类型的标识符将成为绑定到的异常对象。|
|`When`|可选。 一个`Catch`语句`When`子句捕获了异常时，才`expression`的计算结果为`True`。 一个`When`只在检查异常的类型之后应用子句和`expression`可能指表示异常的标识符。|
|`expression`|可选。 必须可隐式转换为`Boolean`。 描述泛型的筛选器的任何表达式。 通常用于筛选的错误号。 用于`When`关键字来指定在其下捕获该错误的情况。|
|`catchStatements`|可选。 若要处理发生在关联的错误的语句`Try`块。 可以是复合语句。|
|`Exit Try`|可选。 关键字跳出`Try...Catch...Finally`结构。 紧跟代码处继续执行`End Try`语句。 `Finally`仍然要执行的语句。 中不允许使用`Finally`块。|
|`Finally`|可选。 一个`Finally`当执行离开的任何部分时始终执行块`Try...Catch`语句。|
|`finallyStatements`|可选。 所有其他错误处理发生后执行的语句。|
|`End Try`|终止`Try...Catch...Finally`结构。|

## <a name="remarks"></a>备注

如果希望在特定代码部分的过程中可能会发生特定异常，将代码放入`Try`阻止并使用`Catch`块保留控件和处理异常，如果发生这种情况。

一个`Try…Catch`语句组成`Try`块后跟一个或多个`Catch`子句指定不同异常的处理程序。 引发异常`Try`阻止，Visual Basic 查找`Catch`处理异常的语句。 如果匹配`Catch`找不到语句、 Visual Basic 会检查调用当前方法，并以此类推遍历调用堆栈的方法。 如果没有`Catch`找到块、 Visual Basic，向用户显示未处理的异常消息和停止程序执行。

可以使用多个`Catch`中的语句`Try…Catch`语句。 如果这样的顺序做`Catch`子句很重要，因为它们会按顺序检查。 在使用更笼统的子句之前获取特定性更强的异常。

以下`Catch`语句条件是最不具体，并将捕获所有派生的异常<xref:System.Exception>类。 应与上一通常使用这些变体之一`Catch`阻止入`Try...Catch...Finally`后捕获您期望的所有特定异常的结构。 控制流可以永远不会达到`Catch`遵循以下任一这些变体的块。

- `type`是`Exception`，例如： `Catch ex As Exception`

- 语句没有`exception`变量，例如： `Catch`

当`Try…Catch…Finally`语句嵌套在另一个`Try`块中，Visual Basic 首先检查每个`Catch`语句中使用最内层`Try`块。 如果没有匹配`Catch`找到语句，则继续搜索`Catch`语句的外部`Try…Catch…Finally`块。

从本地变量`Try`块中均不提供`Catch`阻止，因为它们是单独的块。 如果你想要在多个块中使用变量，声明外部变量`Try...Catch...Finally`结构。

> [!TIP]
> `Try…Catch…Finally`语句是可作为 IntelliSense 代码片段。 在代码片段管理器中，展开**代码模式-If、 为每个，Try Catch、 属性等**，然后**错误处理 （异常）**。 有关详细信息，请参阅[代码片段](/visualstudio/ide/code-snippets)。

## <a name="finally-block"></a>Finally 块

如果必须在退出之前必须运行的一个或多个语句`Try`结构，请使用`Finally`块。 控制权将传递给`Finally`阻止它传递出之前`Try…Catch`结构。 即使内任何位置发生异常，这是如此`Try`结构。

一个`Finally`块可用于运行任何代码必须执行，即使出现异常。 控制权将传递给`Finally`块而不考虑如何`Try...Catch`阻止退出。

中的代码`Finally`阻止运行，即使你的代码遇到`Return`中的语句`Try`或`Catch`块。 控件不会传递从`Try`或`Catch`阻止对相应`Finally`阻止在以下情况下：

- [End 语句](end-statement.md)中遇到`Try`或`Catch`块。

- 一个<xref:System.StackOverflowException>中引发`Try`或`Catch`块。

它不是有效显式传输到执行`Finally`块。 将执行共转`Finally`块不是有效的除非通过异常。

如果`Try`语句不包含至少一个`Catch`块中，它必须包含`Finally`块。

> [!TIP]
> 如果不需要捕获特定异常`Using`语句的行为类似于`Try…Finally`块，并保证可供使用的资源，而不考虑如何退出块。 这是即使使用未经处理的异常，则返回 true。 有关详细信息，请参阅 [Using 语句](using-statement.md)。

## <a name="exception-argument"></a>异常自变量

`Catch`块`exception`自变量是实例<xref:System.Exception>类或派生自类`Exception`类。 `Exception`类实例对应于中发生的错误`Try`块。

属性`Exception`对象帮助以确定原因和处理的异常的位置。 例如，<xref:System.Exception.StackTrace%2A>属性列出了导致异常，从而帮助你查找代码中发生错误的被调用的方法。 <xref:System.Exception.Message%2A> 返回描述异常的消息。 <xref:System.Exception.HelpLink%2A> 返回一个链接到关联的帮助文件。 <xref:System.Exception.InnerException%2A> 返回`Exception`导致当前异常，或其对象返回`Nothing`如果没有原始`Exception`。

## <a name="considerations-when-using-a-trycatch-statement"></a>使用一试时的注意事项...Catch 语句

使用`Try…Catch`语句只是为了发出的信号的异常或意外程序事件。 此问题的原因包括：

- 在运行时捕获的异常创建额外的开销，并可能速度要慢于预检查，以避免异常。

- 如果`Catch`无法正确处理块、 异常可能不会正确报告给用户。

- 异常处理会使程序更复杂。

不始终需要`Try…Catch`语句来检查可能发生的条件。 以下示例检查文件是否存在之前尝试将其打开。 这减少了用于捕获引发的异常需要<xref:System.IO.File.OpenText%2A>方法。

[!code-vb[VbVbalrStatements#94](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#94)]

确保在该代码`Catch`块可以正确地报告给用户，异常，通过线程安全日志记录或相应的消息。 否则，异常可能仍是未知的。

## <a name="async-methods"></a>异步方法

如果标记与方法[异步](../modifiers/async.md)修饰符，可以使用[Await](../operators/await-operator.md)方法中的运算符。 使用语句`Await`运算符挂起执行方法，直到等待的任务完成。 任务表示正在进行的工作。 当与之关联的任务`Await`运算符完成后，执行将继续在同一方法中。 有关详细信息，请参阅[异步程序中的控制流](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)。

异步方法返回的任务可能最终处于错误状态，指示它完成由于未经处理的异常。 任务最终还会在已取消状态，这会导致`OperationCanceledException`引发从 await 表达式。 若要捕获异常的任何一种，将置于`Await`与中的任务相关联的表达式`Try`阻止，并捕捉的异常中`Catch`块。 本主题后面提供示例。

任务可能处于错误状态，因为多个异常的负责其出错。 例如，任务可能是对 <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> 调用的结果。 当等待此类任务时，捕获的异常都只有一个异常，异常，并且不能预测将捕获的异常。 本主题后面提供示例。

`Await`表达式不能包含在内`Catch`块或`Finally`块。

## <a name="iterators"></a>Iterators

迭代器函数或`Get`访问器对集合执行自定义迭代。 迭代器使用[产生](yield-statement.md)语句返回一次的集合的每个元素。 使用调用迭代器函数[为每个...下一条语句](for-each-next-statement.md)。

一个`Yield`语句可以是内部`Try`块。 一个`Try`包含块`Yield`语句可以有`Catch`阻止，并且可以具有`Finally`块。 请参阅的"重试块中 Visual Basic"部分[迭代器](../../programming-guide/concepts/iterators.md)有关的示例。

一个`Yield`语句不能包含在内`Catch`块或`Finally`块。

如果`For Each`正文 （之外的迭代器函数） 会引发异常，`Catch`未执行迭代器函数中的块，但`Finally`执行迭代器函数中的块。 一个`Catch`迭代器函数内的块将捕获在迭代器函数内部发生的异常。

## <a name="partial-trust-situations"></a>部分信任情况下

在部分信任情况下，例如网络共享上托管的应用程序`Try...Catch...Finally`不会捕获包含在调用的方法调用之前发生的安全异常。 以下示例中，将其放在服务器共享上并从这里，运行时生成错误"System.Security.SecurityException:请求失败。" 有关安全异常的详细信息，请参阅<xref:System.Security.SecurityException>类。

[!code-vb[VbVbalrStatements#85](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#85)]

在这种部分信任情况下，您必须将放`Process.Start`在单独的语句`Sub`。 首次调用`Sub`将失败。 这使得`Try...Catch`捕获它之前`Sub`，其中包含`Process.Start`启动和产生安全异常。

## <a name="examples"></a>示例

### <a name="the-structure-of-trycatchfinally"></a>Try 结构...Catch...最后

下面的示例演示了结构`Try...Catch...Finally`语句。

[!code-vb[VbVbalrStatements#86](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#86)]  

### <a name="exception-in-a-method-called-from-a-try-block"></a>在 Try 块中调用的方法中的异常

在以下示例中，`CreateException`方法会抛出`NullReferenceException`。 生成异常的代码不在`Try`块。 因此，`CreateException`方法不会处理异常。 `RunSample`方法未处理该异常，因为在调用`CreateException`方法处于`Try`块。

该示例包含`Catch`几种类型的异常的语句按从最具体到最抽象。

[!code-vb[VbVbalrStatements#91](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#91)]

### <a name="the-catch-when-statement"></a>当 Catch 语句

下面的示例演示如何使用`Catch When`要作为筛选依据的条件表达式的语句。 如果条件表达式的计算结果为`True`中的代码`Catch`块将运行。

[!code-vb[VbVbalrStatements#92](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#92)]

### <a name="nested-try-statements"></a>嵌套的 Try 语句

下面的示例有`Try…Catch`中包含的语句`Try`块。 内部`Catch`块将引发异常有其`InnerException`属性设置为原始异常。 外部`Catch`块都会报告自己的异常和内部异常。

[!code-vb[VbVbalrStatements#93](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#93)]

### <a name="exception-handling-for-async-methods"></a>异步方法处理异常

下面的示例阐释异步方法的异常处理。 若要捕获应用于异步任务，异常`Await`表达式是在`Try`的调用方和异常块中捕获`Catch`块。

在示例中取消注释 `Throw New Exception` 行以演示异常处理。 在捕获的异常`Catch`阻止的任务`IsFaulted`属性设置为`True`，和任务的`Exception.InnerException`属性设置为异常。

取消注释 `Throw New OperationCancelledException` 行以演示在取消异步进程时发生的情况。 在捕获的异常`Catch`块中，并且该任务`IsCanceled`属性设置为`True`。 但是，在不会应用于此示例中，某些情况下`IsFaulted`设置为`True`并`IsCanceled`设置为`False`。

[!code-vb[csAsyncExceptions#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncexceptions/vb/class1.vb#1)]

### <a name="handling-multiple-exceptions-in-async-methods"></a>异步方法中的多个异常处理

下面的示例阐释了在多个任务可能导致多个异常的情况中的异常处理。 `Try`块都有`Await`任务的表达式的<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>返回。 任务已完成时向其三个任务<xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType>应用完成。

三个任务中的每一个都会导致异常。 `Catch`块循环访问异常，异常中找到`Exception.InnerExceptions`任务属性的`Task.WhenAll`返回。

[!code-vb[csAsyncExceptions#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncexceptions/vb/class1.vb#3)]

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:System.Exception>
- [Exit 语句](exit-statement.md)
- [On Error 语句](on-error-statement.md)
- [有关使用代码片段的最佳做法](/visualstudio/ide/best-practices-for-using-code-snippets)
- [异常处理](../../../standard/parallel-programming/exception-handling-task-parallel-library.md)
- [Throw 语句](throw-statement.md)