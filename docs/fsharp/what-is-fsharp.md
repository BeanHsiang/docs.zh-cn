---
title: 什么F#
description: 了解F#编程语言是以及F#就像编程。 了解丰富的数据类型、 函数和它们如何组合在一起。
ms.date: 08/03/2018
ms.openlocfilehash: ea82147e4e6d3c980fb224eeafd805c7ed53f8f2
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56966952"
---
# <a name="what-is-f"></a>F 是什么\#

F# 是一种函数式编程语言，可用于轻松地编写正确和可维护的代码。

F#编程主要包括定义类型和函数的类型推断和自动通用化。 这样，你只需重点关注的问题域和操作其数据，而不是编程的详细信息。

```fsharp
open System // Gets access to functionality in System namespace.

// Defines a function that takes a name and produces a greeting.
let getGreeting name =
    sprintf "Hello, %s! Isn't F# great?" name

[<EntryPoint>]
let main args =
    // Defines a list of names
    let names = [ "Don"; "Julia"; "Xi" ]

    // Prints a greeting for each name!
    names
    |> List.map getGreeting
    |> List.iter (fun greeting -> printfn "%s" greeting)

    0
```

F# 具有许多特性，包括：

* 轻量语法
* 默认情况下不可变
* 类型推断和自动泛化
* 头等函数。
* 强大的数据类型
* 模式匹配
* 异步编程

[F# 语言参考](language-reference/index.md)中介绍了完整的特性。

## <a name="rich-data-types"></a>丰富的数据类型

[记录](language-reference/records.md)和[可区分联合](language-reference/discriminated-unions.md)等数据类型可以表示复杂的数据和域。

```fsharp
// Group data with Records
type SuccessfulWithdrawal = {
    Amount: decimal
    Balance: decimal
}

type FailedWithdrawal = {
    Amount: decimal
    Balance: decimal
    IsOverdraft: bool
}

// Use discriminated unions to represent data of 1 or more forms
type WithdrawalResult =
    | Success of SuccessfulWithdrawal
    | InsufficientFunds of FailedWithdrawal
    | CardExpired of System.DateTime
    | UndisclosedFailure
```

F#的“记录”和“可区分联合”默认情况下为非 null、不可变且可比较，因此它们非常易于使用。

## <a name="enforced-correctness-with-functions-and-pattern-matching"></a>利用函数和模式匹配强制实现正确性

F#函数是轻松地声明和在实践中功能强大。 再加上[模式匹配](language-reference/pattern-matching.md)，它们允许您定义由编译器强制执行其正确性的行为。

```fsharp
// Returns a WithdrawalResult
let withdrawMoney amount = // Implementation elided

let handleWithdrawal amount =
    let w = withdrawMoney amount

    // The F# compiler enforces accounting for each case!
    match w with
    | Success s -> printfn "Successfully withdrew %f" s.Amount
    | InsufficientFunds f -> printfn "Failed: balance is %f" f.Balance
    | CardExpired d -> printfn "Failed: card expired on %O" d
    | UndisclosedFailure -> printfn "Failed: unknown :("
```

F# 函数还是头等函数，也就是说，它们可以像参数一样传递以及从其他函数返回。

## <a name="functions-to-define-operations-on-objects"></a>用于定义对对象执行的操作的函数。

F# 具有对对象的完整支持，即在需要混合数据和功能时非常有用的数据类型。 F#函数用于操作对象。

```fsharp
type Set<[<EqualityConditionOn>] ‘T when ‘T: comparison>(elements: seq<'T>) =
    member s.IsEmpty = // Implementation elided
    member s.Contains (value) =// Implementation elided
    member s.Add (value) = // Implementation elided
    // ...
    // Further Implementation elided
    // ...
    interface IEnumerable<‘T>
    interface IReadOnlyCollection<‘T>

[<RequireQualifiedAccess>]
module Set =
    let isEmpty (set: Set<'T>) = set.IsEmpty

    let contains element (set: Set<'T>) = set.Contains(element)

    let add value (set: Set<'T>) = set.Add(value)
```

在 F# 中，你将经常编写一类代码，这些代码将对象视为函数要操作的其他数据类型，而不是编写面向对象的代码。 [泛型接口](language-reference/interfaces.md)、[对象表达式](language-reference/object-expressions.md)和明智地使用[成员](language-reference/members/index.md)在较大型的 F# 程序中很常见。

## <a name="next-steps"></a>后续步骤

若要详细了解大型数据集F#功能，请查看[F#教程](tour.md)。