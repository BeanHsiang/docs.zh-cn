---
title: let 子句 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- let_CSharpKeyword
- let
helpviewer_keywords:
- let keyword [C#]
- let clause [C#]
ms.assetid: 13c9c1a4-ce57-48ef-8e1b-4c2a59b99fb4
ms.openlocfilehash: 941ad41d75e14420699022a07bd6a3b10d83c896
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53243395"
---
# <a name="let-clause-c-reference"></a>let 子句（C# 参考）

在查询表达式中，存储子表达式的结果有时很有帮助，可在后续子句中使用。 可以通过 `let` 关键字执行此操作，该关键字创建一个新的范围变量并通过提供的表达式结果初始化该变量。 使用值进行初始化后，范围变量不能用于存储另一个值。 但是，如果范围变量持有可查询类型，则可以查询该变量。

## <a name="example"></a>示例

以两种方式使用以下示例 `let`：

1. 创建一个可以查询其自身的可枚举类型。

2. 使查询仅调用一次范围变量 `word` 上的 `ToLower`。 如果不使用 `let`，则不得不调用 `where` 子句中的每个谓词的 `ToLower`。

[!code-csharp[cscsrefQueryKeywords#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Let.cs#28)]

## <a name="see-also"></a>请参阅

- [C# 参考](../../language-reference/index.md)
- [查询关键字 (LINQ)](query-keywords.md)
- [语言集成查询 (LINQ)](../../linq/index.md)
- [C# 中的 LINQ 入门](../../programming-guide/concepts/linq/getting-started-with-linq.md)
- [在查询表达式中处理异常](../../linq/handle-exceptions-in-query-expressions.md)