---
title: 关键字参考
description: 找到的所有信息的链接F#语言关键字。
ms.date: 05/16/2016
ms.openlocfilehash: d55846fe7c8d31454b6bc8684de75546800df7d6
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57845289"
---
# <a name="keyword-reference"></a>关键字参考

本主题包含有关所有信息的链接F#语言关键字。

## <a name="f-keyword-table"></a>F#关键字表

下表显示了所有F#中按字母顺序排列顺序，以及简要说明以及指向包含详细信息的相关主题的关键字。

|关键字|链接|描述|
|-------|----|-----------|
|`abstract`|[成员](members/index.md)<br /><br />[抽象类](abstract-classes.md)|指示在其中声明或类型，其中是虚拟的但默认实现中具有任何实现的方法。|
|`and`|[`let` Bindings](functions/let-bindings.md)<br /><br />[记录](records.md)<br /><br />[成员](members/index.md)<br /><br />[约束](generics/constraints.md)|使用中相互递归绑定和记录，在属性声明中，并使用多个泛型参数约束。|
|`as`|[类](classes.md)<br /><br />[模式匹配](Pattern-Matching.md)|用于为当前类对象的对象名称。 此外用于为中的模式匹配的整个模式提供名称。|
|`assert`|[断言](assertions.md)|用于在调试过程中验证代码。|
|`base`|[类](classes.md)<br /><br />[继承](inheritance.md)|用作基类对象的名称。|
|`begin`|[详细语法](verbose-syntax.md)|详细语法，指示代码块的开头。|
|`class`|[类](classes.md)|详细语法，指示类定义的开头。|
|`default`|[成员](members/index.md)|指示实现的抽象方法;与抽象方法声明一起使用，以创建一个虚拟方法。|
|`delegate`|[委托](delegates.md)|用于声明委托。|
|`do`|[do 绑定](functions/do-bindings.md)<br /><br />[循环：`for...to` 表达式](loops-for-to-expression.md)<br /><br />[循环：`for...in` 表达式](loops-for-in-expression.md)<br /><br />[循环：`while...do` 表达式](loops-while-do-expression.md)|用于在循环构造或执行命令性代码。|
|`done`|[详细语法](verbose-syntax.md)|详细语法，指示循环表达式中的代码块的末尾。|
|`downcast`|[强制转换和转换](casting-and-conversions.md)|用于将转换为较低的继承链中的类型。|
|`downto`|[循环：`for...to` 表达式](loops-for-to-expression.md)|在`for`按相反的顺序计算时所用的表达式。|
|`elif`|[条件表达式：`if...then...else`](conditional-expressions-if-then-else.md)|在条件分支中使用。 缩写形式`else if`。|
|`else`|[条件表达式：`if...then...else`](conditional-expressions-if-then-else.md)|在条件分支中使用。|
|`end`|[结构](structures.md)<br /><br />[可区分联合](discriminated-unions.md)<br /><br />[记录](records.md)<br /><br />[类型扩展](type-extensions.md)<br /><br />[详细语法](verbose-syntax.md)|在类型定义和类型扩展中，指示成员定义的节的结尾。<br /><br />详细语法，用于指定开头的代码块末尾`begin`关键字。|
|`exception`|[异常处理](exception-handling/index.md)<br /><br />[异常类型](exception-handling/exception-types.md)|用于声明异常类型。|
|`extern`|[外部函数](functions/external-functions.md)|指示在另一个二进制文件或程序集中定义的声明的程序元素。|
|`false`|[基元类型](primitive-types.md)|用作布尔值文字。|
|`finally`|[异常：`try...finally`表达式](exception-handling/the-try-finally-expression.md)|综合使用`try`引入的执行时不考虑是否发生了异常的代码块。|
|`fixed`|[已修复](fixed.md)|使用"固定"一个指针，以防止它被垃圾回收的堆栈上。|
|`for`|[循环：`for...to` 表达式](loops-for-to-expression.md)<br /><br />[循环：for...in 表达式](loops-for-in-expression.md)|在循环构造中使用。|
|`fun`|[Lambda 表达式：`fun` 关键字](functions/lambda-expressions-the-fun-keyword.md)|在 lambda 表达式，也称为匿名函数中使用。|
|`function`|[match 表达式](match-expressions.md)<br /><br />[Lambda 表达式：Fun 关键字](functions/lambda-expressions-the-fun-keyword.md)|用作到更短的替代`fun`关键字和一个`match`有模式匹配上一个自变量的 lambda 表达式中的表达式。|
|`global`|[命名空间](namespaces.md)|用于引用顶级.NET 命名空间。|
|`if`|[条件表达式：`if...then...else`](conditional-expressions-if-then-else.md)|在条件分支构造中使用。|
|`in`|[循环：for...in 表达式](loops-for-in-expression.md)<br /><br />[详细语法](verbose-syntax.md)|使用序列表达式，并在详细语法中，将从绑定表达式。|
|`inherit`|[继承](inheritance.md)|用于指定基类或基接口。|
|`inline`|[函数](functions/index.md)<br /><br />[内联函数](functions/inline-functions.md)|用于指示应直接集成到调用方的代码的函数。|
|`interface`|[接口](interfaces.md)|用于声明和实现接口。|
|`internal`|[访问控制](access-control.md)|用于指定成员是可见程序集内而非其外部。|
|`lazy`|[延迟表达式](lazy-expressions.md)|用于指定仅在需要结果时要执行的表达式。|
|`let`|[`let` Bindings](functions/let-bindings.md)|用于将相关联，或将绑定到值或函数的名称。|
|`let!`|[异步工作流](asynchronous-workflows.md)<br /><br />[计算表达式](computation-expressions.md)|用于在异步工作流可将名称绑定到一个异步计算的结果中，或在其他计算表达式中，用于将绑定到一个结果，其计算类型的名称。|
|`match`|[match 表达式](match-expressions.md)|用于通过一种模式值进行对比的分支。|
|`match!`|[计算表达式](computation-expressions.md#match)|适用于内联到调用计算表达式和模式匹配其结果。|
|`member`|[成员](members/index.md)|用于声明属性或方法中的对象类型。|
|`module`|[模块](modules.md)|用于将一个名称与相关的类型、 值和函数，以逻辑方式将其与其他代码的一组相关联。|
|`mutable`|[let 绑定](functions/let-bindings.md)|用于声明变量，即，可以更改的值。|
|`namespace`|[命名空间](namespaces.md)|用于将一个名称与相关的类型和模块，以逻辑方式将其与其他代码的一组相关联。|
|`new`|[构造函数](members/constructors.md)<br /><br />[约束](generics/constraints.md)|用于声明、 定义，或调用构造函数的创建，或可以创建一个对象。<br /><br />此外用于在泛型参数约束中指示类型必须具有某些构造函数。|
|`not`|[符号和运算符参考](symbol-and-operator-reference/index.md)<br /><br />[约束](generics/constraints.md)|不会真的关键字。 但是，`not struct`作为泛型参数约束使用结合使用。|
|`null`|[Null 值](values/null-values.md)<br /><br />[约束](generics/constraints.md)|表示一个对象不存在。<br /><br />此外用于泛型参数约束。|
|`of`|[可区分联合](discriminated-unions.md)<br /><br />[委托](delegates.md)<br /><br />[异常类型](exception-handling/exception-types.md)|在可区分联合来指示类型的类别的值，并在委托和异常声明中使用。|
|`open`|[导入声明：`open` 关键字](import-declarations-the-open-keyword.md)|用于使命名空间或模块的内容无需限定即可。|
|`or`|[符号和运算符参考](symbol-and-operator-reference/index.md)<br /><br />[约束](generics/constraints.md)|一个布尔值，使用布尔条件用作`or`运算符。 等效于 `||`。<br /><br />此外用于成员约束。|
|`override`|[成员](members/index.md)|用于实现的版本与基版本不同的抽象或虚拟方法。|
|`private`|[访问控制](access-control.md)|将访问限制为成员添加到相同类型或模块中的代码。|
|`public`|[访问控制](access-control.md)|允许访问外部类型中的成员。|
|`rec`|[函数](functions/index.md)|用于指示函数是递归。|
|`return`|[异步工作流](Asynchronous-Workflows.md)<br /><br />[计算表达式](computation-expressions.md)|用于指示要计算表达式的结果为提供的值。|
|`return!`|[计算表达式](computation-expressions.md)<br /><br />[异步工作流](asynchronous-workflows.md)|用于指示计算表达式，计算时，提供了包含的计算表达式的结果。|
|`select`|[查询表达式](query-expressions.md)|在查询表达式中用于指定哪些字段或要提取的列。 请注意，这是上下文关键字，这意味着，它并不实际的保留的字，仅充当相应的上下文中的关键字。|
|`static`|[成员](members/index.md)|用于指示方法或属性，可以调用而无需类型的实例或类型的所有实例之间共享的值成员。|
|`struct`|[结构](structures.md)<br /><br /> [元组](tuples.md)<br/><br/>[约束](generics/constraints.md)|用于声明结构类型。<br /><br/>用于指定结构元组。<br/><br />此外用于泛型参数约束。<br /><br />用于实现 OCaml 模块定义中的兼容性。|
|`then`|[条件表达式：`if...then...else`](conditional-expressions-if-then-else.md)<br /><br />[构造函数](members/constructors.md)|在条件表达式中使用。<br /><br />此外用于在对象构造后执行的负面影响。|
|`to`|[循环：`for...to` 表达式](loops-for-to-expression.md)|在中使用`for`循环，以表示一个范围。|
|`true`|[基元类型](primitive-types.md)|用作布尔值文字。|
|`try`|[异常：Try...with 表达式](exception-handling/the-try-with-expression.md)<br /><br />[异常：在尝试...最后表达式](exception-handling/the-try-finally-expression.md)|用于介绍可能会生成异常的代码块。 使用连同`with`或`finally`。|
|`type`|[F# 类型](fsharp-types.md)<br /><br />[类](classes.md)<br /><br />[记录](records.md)<br /><br />[结构](structures.md)<br /><br />[枚举](enumerations.md)<br /><br />[可区分联合](discriminated-unions.md)<br /><br />[类型缩写](type-abbreviations.md)<br /><br />[度量单位](units-of-measure.md)|用于声明类、 记录、 结构、 可区分的联合、 枚举类型、 单元的度量值，或类型缩写。|
|`upcast`|[强制转换和转换](casting-and-conversions.md)|用于将转换为更高版本的继承链中的类型。|
|`use`|[资源管理：`use` 关键字](resource-management-the-use-keyword.md)|而不是使用`let`的值需要`Dispose`调用来释放资源。|
|`use!`|[计算表达式](computation-expressions.md)<br /><br />[异步工作流](asynchronous-workflows.md)|而不是使用`let!`在异步工作流和其他计算表达式的值需要`Dispose`调用来释放资源。|
|`val`|[显式字段：`val` 关键字](members/explicit-fields-the-val-keyword.md)<br /><br />[签名](signatures.md)<br /><br />[成员](members/index.md)|在签名中用于指示一个值，或在类型声明一个成员，在有限的环境中使用。|
|`void`|[基元类型](primitive-types.md)|指示.NET`void`类型。 与其他.NET 语言进行互操作时使用。|
|`when`|[约束](generics/constraints.md)|用于布尔条件 (*时可保护*) 模式匹配并引入泛型类型参数的约束子句。|
|`while`|[循环：`while...do` 表达式](loops-while-do-expression.md)|引入了循环构造。|
|`with`|[match 表达式](match-expressions.md)<br /><br />[对象表达式](object-expressions.md)<br /><br />[复制和更新记录表达式](copy-and-update-record-expressions.md)<br /><br />[类型扩展](type-extensions.md)<br /><br />[异常：`try...with`表达式](exception-handling/the-try-with-expression.md)|综合使用`match`在模式匹配表达式的关键字。 此外使用对象表达式中，记录复制表达式，并键入扩展引入的成员定义，并引入异常处理程序。|
|`yield`|[序列](sequences.md)|在序列表达式中用于生成的序列值。|
|`yield!`|[计算表达式](computation-expressions.md)<br /><br />[异步工作流](asynchronous-workflows.md)|计算表达式中用于将给定的计算表达式的结果追加到包含的计算表达式的结果的集合。|

以下标记保留在F#因为它们是 OCaml 语言中的关键字：

* `asr`
* `land`
* `lor`
* `lsl`
* `lsr`
* `lxor`
* `mod`
* `sig`

如果使用`--mlcompatibility`编译器选项，上面的关键字是可供使用作为标识符。

以下标记将作为关键字的将来扩展保留F#语言：

* `atomic`
* `break`
* `checked`
* `component`
* `const`
* `constraint`
* `constructor`
* `continue`
* `eager`
* `event`
* `external`
* `functor`
* `include`
* `method`
* `mixin`
* `object`
* `parallel`
* `process`
* `protected`
* `pure`
* `sealed`
* `tailcall`
* `trait`
* `virtual`
* `volatile`

## <a name="see-also"></a>请参阅

- [F# 语言参考](index.md)
- [符号和运算符参考](symbol-and-operator-reference/index.md)
- [编译器选项](compiler-options.md)
