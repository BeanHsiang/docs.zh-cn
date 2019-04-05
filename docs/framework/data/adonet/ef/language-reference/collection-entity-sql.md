---
title: COLLECTION (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 03228bfa-be3a-4ccc-82f8-eee429f85cf1
ms.openlocfilehash: d4e52bb62412e61e1a71e0fe9a8555068ca18dbd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54506454"
---
# <a name="collection-entity-sql"></a>COLLECTION (Entity SQL)
COLLECTION 关键字仅在内联函数的定义中使用。 集合函数是对值的集合进行操作并生成标量输出的函数。  
  
## <a name="syntax"></a>语法  
  
```  
COLLECTION(type_definition)   
```  
  
## <a name="arguments"></a>自变量  
 `type_definition`  
 一个表达式，返回受支持类型、行或引用的集合。  
  
## <a name="remarks"></a>备注  
 有关 COLLECTION 关键字的详细信息，请参阅 [Type Definitions](../../../../../../docs/framework/data/adonet/ef/language-reference/type-definitions-entity-sql.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 COLLECTION 关键字将十进制值集合声明为内联查询函数的参数。  
  
 [!code-csharp[DP EntityServices Concepts 2#Collection_GroupPartition](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#collection_grouppartition)]  
  
## <a name="see-also"></a>请参阅
- [实体 SQL 引用](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
