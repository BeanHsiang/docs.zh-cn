---
title: SKIP (Entity SQL)
ms.date: 03/30/2017
ms.assetid: e2139412-8ea4-451b-8f10-91af18dfa3ec
ms.openlocfilehash: b17f73f97d32f151ed4f51b025c0c5a7a97393bb
ms.sourcegitcommit: c6f69b0cf149f6b54483a6d5c2ece222913f43ce
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55904181"
---
# <a name="skip-entity-sql"></a>SKIP (Entity SQL)
在 ORDER BY 子句中使用 SKIP 子子句可执行物理分页。 SKIP 不能脱离 ORDER BY 子句单独使用。  
  
## <a name="syntax"></a>语法  
  
```  
[ SKIP n ]  
```  
  
## <a name="arguments"></a>自变量  
 `n`  
 要跳过的项数。  
  
## <a name="remarks"></a>备注  
 如果 ORDER BY 子句中存在 SKIP 表达式子子句，则将根据排序规范对结果排序，结果集将包含从紧接着 SKIP 表达式之后的下一行开始的行。 例如，SKIP 5 将跳过前五行，并返回第六行以及后续行。  
  
> [!NOTE]
>  如果 TOP 修饰符和 SKIP 子子句同时出现在同一个查询表达式中， [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查询将无效。 应重写查询，将 TOP 表达式更改为 LIMIT 表达式。  
  
> [!NOTE]
>  在 [!INCLUDE[ssVersion2000](../../../../../../includes/ssversion2000-md.md)]中，对非键列同时使用 SKIP 和 ORDER BY 可能返回不正确的结果。 如果非键列中有重复数据，那么跳过的行数可能多于指定的行数。 这是由于 [!INCLUDE[ssVersion2000](../../../../../../includes/ssversion2000-md.md)]对 SKIP 的解释方式造成的。 例如，在下面的代码中，如果 `E.NonKeyColumn` 有重复值，则跳过的行可能超过 5 行：  
>   
>  `SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L`  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]查询中的[如何：通过查询结果进行分页](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))使用 ORDER BY 运算符与 SKIP 来指定用于 SELECT 语句中返回对象的排序顺序。  
  
## <a name="see-also"></a>请参阅
- [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)
- [如何：页查看查询结果](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))
- [分页](../../../../../../docs/framework/data/adonet/ef/language-reference/paging-entity-sql.md)
- [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)
