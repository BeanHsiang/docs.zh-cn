---
title: 用于实体框架的 SqlClient 类型
ms.date: 03/30/2017
ms.assetid: f2a95ead-c845-4e97-9fb3-04b444f7ed81
ms.openlocfilehash: b121020c8779cfb3959425b1019eaf085b97d6cf
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54505181"
---
# <a name="sqlclient-for-entity-frameworktypes"></a>用于实体框架的 SqlClient 类型
SQL Server .NET Framework        (SqlClient)                                                                                       
  
 下表介绍了 SQL Server 2008 [!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)]，和[!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)]数据库类型以及这些类型如何映射到概念模型类型。 在 SQL Server 的较新版本中引入的某些新类型在 SQL Server 早期版本中不受支持。 下表中注明了这些类型。  
  
|提供程序类型<br /><br /> name|提供程序类型<br /><br /> 特性|`EDMSimpleType`<br /><br /> name|方面|  
|----------------------------|----------------------------------|------------------------------|------------|  
|`bit`|无|`Edm.Boolean`|不可用|  
|`tinyint`|不可用|`Edm.Byte`|不可用|  
|`smallint`|不可用|`Edm.Int16`|不可用|  
|`int`|不可用|`Edm.Int32`|不可用|  
|`bigint`|不可用|`Edm.Int64`|不可用|  
|`float`|不可用|`Edm.Double`|不可用|  
|`real`|不可用|`Edm.Double`|不可用|  
|`decimal`|n/a|`Edm.Decimal`|精度：<br /><br /> -最小值：1<br /><br /> -最大值：38<br /><br /> -默认值：18<br /><br /> -常数：False<br /><br /> 缩放：<br /><br /> -最小值：0<br /><br /> -最大值：38<br /><br /> -默认值：0<br /><br /> -常数：False|  
|`numeric`|n/a|`Edm.Decimal`|精度：<br /><br /> -最小值：1<br /><br /> -最大值：38<br /><br /> -默认值：18<br /><br /> -常数：False<br /><br /> 缩放：<br /><br /> -最小值：0<br /><br /> -最大值：38<br /><br /> -默认值：0<br /><br /> -常数：False|  
|`smallmoney`|n/a|`Edm.Decimal`|精度：<br /><br /> -默认值：10<br /><br /> -常数：True<br /><br /> 缩放：<br /><br /> -默认值：4<br /><br /> -常数：True|  
|`money`|n/a|`Edm.Decimal`|精度：<br /><br /> -默认值：19<br /><br /> -常数：True<br /><br /> 缩放：<br /><br /> -默认值：4<br /><br /> -常数：True|  
|`binary`|n/a|`Edm.Binary`|MaxLength:<br /><br /> -最小值：1<br /><br /> -最大值：8000<br /><br /> -默认值：8000<br /><br /> -常数：False<br /><br /> FixedLength:<br /><br /> -默认值：True<br /><br /> -常数：True|  
|`varbinary`|n/a|`Edm.Binary`|MaxLength:<br /><br /> -最小值：1<br /><br /> -最大值：8000<br /><br /> -默认值：8000<br /><br /> -常数：False<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`varbinary(max)`<br /><br /> 注意:中不支持此类型[!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)]。|n/a|`Edm.Binary`|MaxLength:<br /><br /> -默认值：214748364780<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`image`|n/a|`Edm.Binary`|MaxLength:<br /><br /> -默认值：2147483647<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`timestamp`|n/a|`Edm.Binary`|MaxLength:<br /><br /> -默认值：8<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：True<br /><br /> -常数：True|  
|`rowversion`|n/a|`Edm.Binary`|MaxLength:<br /><br /> -默认值：8<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：True<br /><br /> -常数：True|  
|`smalldatetime`|n/a|`Edm.DateTime`|精度：<br /><br /> -默认值：0<br /><br /> -常数：True|  
|`datetime`|n/a|`Edm.DateTime`|精度：<br /><br /> -默认值：3<br /><br /> -常数：True|  
|`date`<br /><br /> 注意:SQL Server 2005 和 SQL Server 2000 中不支持此类型。|n/a|`Edm.DateTime`|精度：<br /><br /> -默认值：0<br /><br /> -常数：False|  
|`time`<br /><br /> 注意:SQL Server 2005 和 SQL Server 2000 中不支持此类型。|n/a|`Edm.Time`|精度：<br /><br /> -默认值：7<br /><br /> -常数：False|  
|`datetime2`<br /><br /> 注意:SQL Server 2005 和 SQL Server 2000 中不支持此类型。|n/a|`Edm.DateTime`|精度：<br /><br /> -默认值：7<br /><br /> -常数：False|  
|`datetimeoffset`<br /><br /> 注意:SQL Server 2005 和 SQL Server 2000 中不支持此类型。|n/a|`Edm.DateTimeOffset`|精度：<br /><br /> -默认值：7<br /><br /> -常数：False|  
|`nvarchar`<br /><br /> 注意:中不支持此类型[!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)]。|n/a|`Edm.String`|MaxLength:<br /><br /> -最小值：1<br /><br /> -最大值：4000<br /><br /> -默认值：4000<br /><br /> -常数：False<br /><br /> Unicode:<br /><br /> -默认值：True<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`varchar`<br /><br /> 注意:中不支持此类型[!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)]。|n/a|`Edm.String`|MaxLength:<br /><br /> -最小值：1<br /><br /> -最大值：8000<br /><br /> -默认值：8000<br /><br /> -常数：False<br /><br /> Unicode:<br /><br /> -默认值：False<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`char`|n/a|`Edm.String`|MaxLength:<br /><br /> -最小值：1<br /><br /> -最大值：8000<br /><br /> -默认值：8000<br /><br /> -常数：False<br /><br /> Unicode:<br /><br /> -默认值：False<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：True<br /><br /> -常数：True|  
|`nchar`|n/a|`Edm.String`|MaxLength:<br /><br /> -最小值：1<br /><br /> -最大值：4000<br /><br /> -默认值：4000<br /><br /> -常数：False<br /><br /> Unicode:<br /><br /> -默认值：True<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：True<br /><br /> -常数：True|  
|`varchar`(`max`)|n/a|`Edm.String`|MaxLength:<br /><br /> -默认值：2147483647<br /><br /> -常数：True<br /><br /> Unicode:<br /><br /> -默认值：False<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`nvarchar`(`max`)|n/a|`Edm.String`|MaxLength:<br /><br /> -默认值：1073741823<br /><br /> -常数：True<br /><br /> Unicode:<br /><br /> -默认值：True<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`ntext`|可比较相等：False<br /><br /> 可比较顺序：False|`Edm.String`|MaxLength:<br /><br /> -默认值：1073741823<br /><br /> -常数：True<br /><br /> Unicode:<br /><br /> -默认值：False<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`text`|可比较相等：False<br /><br /> 可比较顺序：False|`Edm.String`|MaxLength:<br /><br /> -默认值：2147483647<br /><br /> -常数：True<br /><br /> Unicode:<br /><br /> -默认值：False<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
|`Unique`<br /><br /> `identifier`|可比较相等：True<br /><br /> 可比较顺序：True|`Edm.Guid`|n/a|  
|`xml`|可比较相等：False<br /><br /> 可比较顺序：False|`Edm.String`|MaxLength:<br /><br /> -默认值：1073741823<br /><br /> -常数：True<br /><br /> Unicode:<br /><br /> -默认值：True<br /><br /> -常数：True<br /><br /> FixedLength:<br /><br /> -默认值：False<br /><br /> -常数：True|  
  
## <a name="see-also"></a>请参阅
- [CSDL、SSDL 和 MSL 规范](../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md)
