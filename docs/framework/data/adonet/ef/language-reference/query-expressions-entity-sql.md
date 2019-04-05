---
title: 查询表达式 (Entity SQL)
ms.date: 03/30/2017
ms.assetid: c36f327b-e230-48d4-bbd5-78dc6478c447
ms.openlocfilehash: 5a200c8fc5adcb6334d0a0ddf290d275de4eb768
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54696875"
---
# <a name="query-expressions-entity-sql"></a>查询表达式 (Entity SQL)
查询表达式将许多不同的查询运算符组合成单个语法。 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供了不同类型的表达式，包括以下：[文字](../../../../../../docs/framework/data/adonet/ef/language-reference/literals-entity-sql.md)，[参数](../../../../../../docs/framework/data/adonet/ef/language-reference/parameters-entity-sql.md)，[变量](../../../../../../docs/framework/data/adonet/ef/language-reference/variables-entity-sql.md)，运算符，[函数](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md)、 集运算符，依次类推。 有关详细信息，请参阅[实体 SQL 引用](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)。  
  
## <a name="clauses"></a>子句  
 查询表达式由一系列子句组成，这些子句将连续的操作应用于一个对象集合。 查询表达式基于标准 SQL SELECT 语句中存在的相同子句：[选择](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)， [FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md)，[其中](../../../../../../docs/framework/data/adonet/ef/language-reference/where-entity-sql.md)，[分组依据](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md)， [HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md)，并[ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)。  
  
## <a name="scope"></a>范围  
 在 FROM 子句中定义的名称以从左到右的出现顺序引入到 FROM 作用域。 在 JOIN 列表中，表达式可以引用以前在列表中定义的名称。 在 FROM 子句中标识的元素的公共属性不会添加到 FROM 作用域：必须总是通过别名限定名称来引用这些属性。 通常，SELECT 表达式的所有部分都视作在 FROM 作用域内。  
  
## <a name="see-also"></a>请参阅
- [实体 SQL 引用](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
