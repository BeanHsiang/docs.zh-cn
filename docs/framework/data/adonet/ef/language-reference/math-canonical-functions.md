---
title: 数学规范函数
ms.date: 03/30/2017
ms.assetid: 6f6cddc6-b561-4ebe-84b6-841ef5b4113b
ms.openlocfilehash: 3e8122806e31fc72b3d390e5e8671fada7f3a47d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54492698"
---
# <a name="math-canonical-functions"></a>数学规范函数

实体 SQL 包括以下数学规范函数：
  
## <a name="absvalue"></a>Abs(value)

返回 `value` 的绝对值。

**参数**

`Int16`， `Int32`， `Int64`， `Byte`， `Single`， `Double`，和`Decimal`。

**返回值**

`value` 的类型。

**示例**

`Abs(-2)`

## <a name="ceilingvalue"></a>Ceiling(value)

返回不小于 `value` 的最小整数。

**参数**

一个`Single`， `Double`，和`Decimal`。

**返回值**

`value` 的类型。

**示例**

[!code-csharp[DP EntityServices Concepts#EDM_CEILING](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_ceiling)]
[!code-sql[DP EntityServices Concepts#EDM_CEILING](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_ceiling)]

## <a name="floorvalue"></a>Floor(value)

返回不大于 `value` 的最大整数。

**参数**

一个`Single`， `Double`，和`Decimal`。

**返回值**

`value` 的类型。

**示例**

[!code-csharp[DP EntityServices Concepts#EDM_FLOOR](~/samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#edm_floor)]
[!code-sql[DP EntityServices Concepts#EDM_FLOOR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#edm_floor)]

## <a name="powervalue-exponent"></a>Power(值, 指数)

返回对指定的 `value` 求指定的 `exponent` 幂次所得的结果。

**参数**

|  |  |
|--|--|
|`value` | `Int32, Int64, Double`，或`Decimal`。 |
|`exponent` | `Int64`， `Double`，或`Decimal`。 |

**返回值**

`value` 的类型。

**示例**

`Power(748.58,2)`

## <a name="roundvalue"></a>Round(value)

返回 `value` 的整数部分，舍入到最近的整数。

**参数**

一个`Single`， `Double`，和`Decimal`。

**返回值**

`value` 的类型。

**示例**

`Round(748.58)`

## <a name="roundvalue-digits"></a>Round(值, 位数)

返回 `value`，舍入到最近的指定 `digits`。

**参数**

|  |  |
|--|--|
|`value`|`Double` 或 `Decimal`。|
|`digits`|`Int16` 或 `Int32`。|

**返回值**

`value` 的类型。

**示例**

`Round(748.58,1)`

## <a name="truncatevalue-digits"></a>Truncate(值, 位数)

返回 `value`，截断至最近的指定 `digits`。

**参数**

|  |  |
|--|--|
|`value`|`Double` 或 `Decimal`。|
|`digits`|`Int16` 或 `Int32`。|

**返回值**

`value` 的类型。

**示例**

`Truncate(748.58,1)`  
  
 如果提供 `null` 输入，则这些函数返回 `null`。  
  
 Microsoft SQL 客户端托管提供程序中提供了等效功能。 有关详细信息，请参阅[用于实体框架函数的 SqlClient](../../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)。  
  
## <a name="see-also"></a>请参阅
- [规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)
