---
title: 'C# 关键字'
ms.date: 03/07/2017
f1_keywords:
  - cs.keywords
helpviewer_keywords:
  - 'keywords [C#]'
  - 'C# language, keywords'
  - 'Visual C#, keywords'
  - '@ keyword'
ms.assetid: e929b0f2-4b92-4d37-8060-23d323b098ad
---
# <a name="c-keywords"></a>C# 关键字
关键字是预定义的保留标识符，对编译器有特殊意义。 除非前面有 `@` 前缀，否则不能在程序中用作标识符。 例如，`@if` 是有效标识符，而 `if` 则不是，因为 `if` 是关键字。  
  
 此主题中的第一个表列出了是 C# 程序任意部分中的保留标识符的关键字。 此主题中的第二个表列出了 C# 中的上下文关键字。 上下文关键字仅在一部分程序上下文中有特殊含义，可以在相应上下文范围之外用作标识符。 一般来说，C# 语言中新增的关键字会作为上下文关键字添加，以免破坏用旧版语言编写的程序。  
  
|||||  
|---|---|---|---|  
|[abstract](../../../csharp/language-reference/keywords/abstract.md)|[as](../../../csharp/language-reference/keywords/as.md)|[base](../../../csharp/language-reference/keywords/base.md)|[bool](../../../csharp/language-reference/keywords/bool.md)|  
|[break](../../../csharp/language-reference/keywords/break.md)|[byte](../../../csharp/language-reference/keywords/byte.md)|[case](../../../csharp/language-reference/keywords/switch.md)|[catch](../../../csharp/language-reference/keywords/try-catch.md)|  
|[char](../../../csharp/language-reference/keywords/char.md)|[checked](../../../csharp/language-reference/keywords/checked.md)|[class](../../../csharp/language-reference/keywords/class.md)|[const](../../../csharp/language-reference/keywords/const.md)|  
|[continue](../../../csharp/language-reference/keywords/continue.md)|[decimal](../../../csharp/language-reference/keywords/decimal.md)|[default](../../../csharp/language-reference/keywords/default.md)|[delegate](../../../csharp/language-reference/keywords/delegate.md)|  
|[do](../../../csharp/language-reference/keywords/do.md)|[double](../../../csharp/language-reference/keywords/double.md)|[else](../../../csharp/language-reference/keywords/if-else.md)|[enum](../../../csharp/language-reference/keywords/enum.md)|  
|[event](../../../csharp/language-reference/keywords/event.md)|[explicit](../../../csharp/language-reference/keywords/explicit.md)|[extern](../../../csharp/language-reference/keywords/extern.md)|[false](../../../csharp/language-reference/keywords/false.md)|  
|[finally](../../../csharp/language-reference/keywords/try-finally.md)|[fixed](../../../csharp/language-reference/keywords/fixed-statement.md)|[float](../../../csharp/language-reference/keywords/float.md)|[for](../../../csharp/language-reference/keywords/for.md)|  
|[foreach](../../../csharp/language-reference/keywords/foreach-in.md)|[goto](../../../csharp/language-reference/keywords/goto.md)|[if](../../../csharp/language-reference/keywords/if-else.md)|[implicit](../../../csharp/language-reference/keywords/implicit.md)|  
|[in](../../../csharp/language-reference/keywords/in.md)|[int](../../../csharp/language-reference/keywords/int.md)|[interface](../../../csharp/language-reference/keywords/interface.md)|[internal](../../../csharp/language-reference/keywords/internal.md)|
|[is](../../../csharp/language-reference/keywords/is.md)|[lock](../../../csharp/language-reference/keywords/lock-statement.md)|[long](../../../csharp/language-reference/keywords/long.md)|[namespace](../../../csharp/language-reference/keywords/namespace.md)|
|[new](../../../csharp/language-reference/keywords/new.md)|[null](../../../csharp/language-reference/keywords/null.md)|[object](../../../csharp/language-reference/keywords/object.md)|[operator](../../../csharp/language-reference/keywords/operator.md)|
|[out](../../../csharp/language-reference/keywords/out.md)|[override](../../../csharp/language-reference/keywords/override.md)|[params](../../../csharp/language-reference/keywords/params.md)|[private](../../../csharp/language-reference/keywords/private.md)|
|[protected](../../../csharp/language-reference/keywords/protected.md)|[public](../../../csharp/language-reference/keywords/public.md)|[readonly](../../../csharp/language-reference/keywords/readonly.md)|[ref](../../../csharp/language-reference/keywords/ref.md)|
|[return](../../../csharp/language-reference/keywords/return.md)|[sbyte](../../../csharp/language-reference/keywords/sbyte.md)|[sealed](../../../csharp/language-reference/keywords/sealed.md)|[short](../../../csharp/language-reference/keywords/short.md)||
[sizeof](../../../csharp/language-reference/keywords/sizeof.md)|[stackalloc](../../../csharp/language-reference/keywords/stackalloc.md)|[static](../../../csharp/language-reference/keywords/static.md)|[string](../../../csharp/language-reference/keywords/string.md)|
|[struct](../../../csharp/language-reference/keywords/struct.md)|[switch](../../../csharp/language-reference/keywords/switch.md)|[this](../../../csharp/language-reference/keywords/this.md)|[throw](../../../csharp/language-reference/keywords/throw.md)|
|[true](../../../csharp/language-reference/keywords/true.md)|[try](../../../csharp/language-reference/keywords/try-catch.md)|[typeof](../../../csharp/language-reference/keywords/typeof.md)|[uint](../../../csharp/language-reference/keywords/uint.md)|
|[ulong](../../../csharp/language-reference/keywords/ulong.md)|[unchecked](../../../csharp/language-reference/keywords/unchecked.md)|[unsafe](../../../csharp/language-reference/keywords/unsafe.md)|[ushort](../../../csharp/language-reference/keywords/ushort.md)|
|[using](../../../csharp/language-reference/keywords/using.md)|[using static](using-static.md)|[virtual](../../../csharp/language-reference/keywords/virtual.md)|[void](../../../csharp/language-reference/keywords/void.md)|
|[volatile](../../../csharp/language-reference/keywords/volatile.md)|[while](../../../csharp/language-reference/keywords/while.md)|

## <a name="contextual-keywords"></a>上下文关键字  
 上下文关键字用于在代码中提供特定含义，但不是 C# 中的保留字。 一些上下文关键字（如 `partial` 和 `where`）在两个或多个上下文中有特殊含义。  
  
||||  
|---|---|---|  
|[add](add.md)|[alias](extern-alias.md)|[ascending](ascending.md)|
|[async](async.md)|[await](await.md)|[by](by.md)|
|[descending](descending.md)|[dynamic](dynamic.md)|[equals](equals.md)|
|[from](from-clause.md)|[get](get.md)|[global](global.md)|
|[group](group-clause.md)|[into](into.md)|[join](join-clause.md)|
|[let](let-clause.md)|[nameof](nameof.md)|[on](on.md)|
|[orderby](orderby-clause.md)|[partial（类型）](partial-type.md)|[partial（方法）](partial-method.md)|
|[remove](remove.md)|[select](select-clause.md)|[set](set.md)|
|[值](value.md)|[var](var.md)|[when（筛选条件）](when.md)|
|[where（泛型类型约束）](where-generic-type-constraint.md)|[where（查询子句）](where-clause.md)|[yield](yield.md)|
  
## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
