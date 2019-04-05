---
title: 实体数据模型：基元数据类型
ms.date: 03/30/2017
ms.assetid: 7635168e-0566-4fdd-8391-7941b0d9f787
ms.openlocfilehash: 2c2e1056c43f974ec38407372a8f447e52b4a630
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54748007"
---
# <a name="entity-data-model-primitive-data-types"></a>实体数据模型：基元数据类型
实体数据模型 (EDM) 支持抽象的基元数据类型 （如字符串、 布尔值，Int32，等等），用于定义一组[属性](../../../../docs/framework/data/adonet/property.md)概念模型中。 这些基元数据类型是存储或承载环境（例如 SQL Server 数据库或公共语言运行库 (CLR)）中所支持的实际基元数据类型的代理。 EDM 没有定义基元数据类型的操作或转换语义；这些语义由存储或承载环境定义。 通常，EDM 中的基元数据类型将映射至存储或承载环境中的对应基元数据类型。 有关实体框架如何映射到 SQL Server 数据类型的 EDM 中的基元类型的信息，请参阅[SqlClient 实体 FrameworkTypes](../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-types.md)。  
  
> [!NOTE]
>  EDM 不支持基元数据类型的集合。  
  
 有关 EDM 中的结构化的数据类型的信息，请参阅[实体类型](../../../../docs/framework/data/adonet/entity-type.md)并[复杂类型](../../../../docs/framework/data/adonet/complex-type.md)。  
  
## <a name="primitive-data-types-supported-in-the-entity-data-model"></a>实体数据模型中支持的基元数据类型  
 下表列出了 EDM 支持的基元数据类型。 该表还列出[方面](../../../../docs/framework/data/adonet/facet.md)，可以应用于每个基元数据类型。  
  
|基元数据类型|描述|适用的方面|  
|-------------------------|-----------------|-----------------------|  
|二进制|包含二进制数据。|MaxLength、FixedLength、Nullable、Default|  
|Boolean|包含值 `true` 或 `false`。|Nullable、Default|  
|Byte|包含一个无符号的 8 位整数值。|Precision、Nullable、Default|  
|DateTime|表示日期和时间。|Precision、Nullable、Default|  
|DateTimeOffset|包含以相对于 GMT 的偏移量（以分钟为单位）表示的日期和时间。|Precision、Nullable、Default|  
|Decimal|包含一个具有固定精度和小数位数的数值。|Precision、Nullable、Default|  
|Double|包含一个具有 15 位精度的浮点数。|Precision、Nullable、Default|  
|Float|包含一个具有 7 位精度的浮点数。|Precision、Nullable、Default|  
|Guid|包含一个 16 字节的唯一标识符。|Precision、Nullable、Default|  
|Int16|包含一个带符号的 16 位整数值。|Precision、Nullable、Default|  
|Int32|包含一个带符号的 32 位整数值。|Precision、Nullable、Default|  
|Int64|包含一个带符号的 64 位整数值。|Precision、Nullable、Default|  
|SByte|包含一个带符号的 8 位整数值。|Precision、Nullable、Default|  
|String|包含字符数据。|Unicode、FixedLength、MaxLength、Collation、Precision、Nullable、Default|  
|时间|包含当天的时间。|Precision、Nullable、Default|  
  
## <a name="see-also"></a>请参阅
- [实体数据模型关键概念](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)
- [实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)
