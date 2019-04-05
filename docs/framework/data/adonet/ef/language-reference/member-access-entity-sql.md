---
title: . （成员访问）(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 4733e3b2-3efa-4b96-b591-ac31350e96ad
ms.openlocfilehash: e2874e5bff8d8c34f700a81bf52c6729df49aca5
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54626658"
---
# <a name="-member-access-entity-sql"></a>. （成员访问）(Entity SQL)
点运算符 （.） 是[!INCLUDE[esql](../../../../../../includes/esql-md.md)]成员访问运算符。 使用成员访问运算符可生成结构化概念模型类型实例的属性或字段的值。  
  
## <a name="syntax"></a>语法  
  
```  
expression.identifier  
```  
  
## <a name="arguments"></a>自变量  
 `expression`  
 结构化概念模型类型的实例。  
  
 `identifier`  
 属于对象实例的属性或字段。  
  
## <a name="remarks"></a>备注  
 点 (.) 运算符可以用于从记录中提取字段，类似于提取复杂类型或实体类型的属性。 例如，如果类型 Name 的 n 是类型 Person 的成员，而 p 是类型 Person 的实例，则 p.n 是合法的成员访问表达式，该表达式生成类型为 Name 的值。  
  
 `select p.Name.FirstName from LOB.Person as p`  
  
## <a name="see-also"></a>请参阅
- [实体 SQL 引用](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
