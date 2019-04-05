---
title: 查询关键字 - C# 参考
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- query keywords [C#]
- LINQ [C#], query keywords
ms.assetid: 6c9bec16-dbd7-4a7c-a060-fe4600b2021f
ms.openlocfilehash: e5010c7e9f3550c79c86c6cab4579a0fb15eef10
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53239480"
---
# <a name="query-keywords-c-reference"></a>查询关键字（C# 参考）

本部分包含在查询表达式中使用的上下文关键字。

## <a name="in-this-section"></a>本节内容

|子句|说明|
|------------|-----------------|
|[from](from-clause.md)|指定数据源和范围变量（类似于迭代变量）。|
|[where](where-clause.md)|基于由逻辑 AND 和 OR 运算符（`&&` 或 <code>&#124;&#124;</code>）分隔的一个或多个布尔表达式筛选源元素。|
|[select](select-clause.md)|指定执行查询时，所返回序列中元素的类型和形状。|
|[group](group-clause.md)|根据指定的密钥值对查询结果分组。|
|[into](into.md)|提供可作为对 join、group 或 select 子句结果引用的标识符。|
|[orderby](orderby-clause.md)|根据元素类型的默认比较器对查询结果进行升序或降序排序。|
|[join](join-clause.md)|基于两个指定匹配条件间的相等比较而联接两个数据源。|
|[let](let-clause.md)|引入范围变量，在查询表达式中存储子表达式结果。|
|[in](in.md)|[join](join-clause.md) 子句中的上下文关键字。|
|[on](on.md)|[join](join-clause.md) 子句中的上下文关键字。|
|[equals](equals.md)|[join](join-clause.md) 子句中的上下文关键字。|
|[by](by.md)|[group](group-clause.md) 子句中的上下文关键字。|
|[ascending](ascending.md)|[orderby](orderby-clause.md) 子句中的上下文关键字。|
|[descending](descending.md)|[orderby](orderby-clause.md) 子句中的上下文关键字。|

## <a name="see-also"></a>请参阅

- [C# 关键字](index.md)
- [LINQ（语言集成查询）](../../programming-guide/concepts/linq/index.md)
- [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)
- [C# 中的 LINQ 入门](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)