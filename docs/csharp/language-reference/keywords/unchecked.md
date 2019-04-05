---
title: unchecked 关键字 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- unchecked_CSharpKeyword
- unchecked
helpviewer_keywords:
- unchecked keyword [C#]
ms.assetid: 0c021f7c-923f-4b3d-a58f-55336f5ac27e
ms.openlocfilehash: 44301333f7a36e6b0baa6ea9e089d930bb485a45
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53238450"
---
# <a name="unchecked-c-reference"></a>unchecked（C# 参考）

`unchecked` 关键字用于取消整型类型的算术运算和转换的溢出检查。

在未经检查的上下文中，如果表达式生成的值超出目标类型的范围，则不会标记溢出。 例如，由于以下示例中的计算在 `unchecked` 块或表达式中执行，因此将忽略计算结果对于整数而言过大的事实，并且向 `int1` 赋予值 -2,147,483,639。

[!code-csharp[csrefKeywordsChecked#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#5)]

如果删除 `unchecked` 环境，会发生编译错误。 由于表达式的所有项都是常量，因此可在编译时检测到溢出。

在编译时和运行时，默认不检查包含非常数项的表达式。 请参阅[启用检查](checked.md)，获取有关使用启用了检查的环境的信息。

由于检查溢出需要时间，因此在没有溢出风险的情况下使用取消检查的代码可能会提高性能。 但是，如果存在溢出的可能，则应使用启用了检查的环境。

## <a name="example"></a>示例

此示例演示如何使用 `unchecked`关键字。

[!code-csharp[csrefKeywordsChecked#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#2)]

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../../csharp/language-reference/index.md)
- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [C# 关键字](index.md)
- [Checked and Unchecked](checked-and-unchecked.md)
- [checked](checked.md)