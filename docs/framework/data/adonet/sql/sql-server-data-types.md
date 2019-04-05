---
title: SQL Server 数据类型和 ADO.NET
ms.date: 03/30/2017
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
ms.openlocfilehash: 14a3c8b2f520efce96667b2028405ca36ed17a28
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54741504"
---
# <a name="sql-server-data-types-and-adonet"></a>SQL Server 数据类型和 ADO.NET
SQL Server 和 .NET Framework 基于不同的类型系统，这可导致潜在的数据丢失。 为了保持数据的完整性，适用于 SQL Server 的 .NET Framework 数据提供程序 (<xref:System.Data.SqlClient>) 提供了用于处理 SQL Server 数据的类型化访问器方法。 可以使用 <xref:System.Data.SqlDbType> 类中的枚举来指定 <xref:System.Data.SqlClient.SqlParameter> 数据类型。  
  
 有关详细信息和说明 SQL Server 和.NET Framework 数据类型之间的数据类型映射的表，请参阅[SQL Server 数据类型映射](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)。  
  
 SQL Server 2008 引入了旨在满足业务需求的新数据类型，以用于处理日期和时间、结构化、半结构化和非结构化的数据。 这些文档位于 SQL Server 2008 联机丛书中。  
  
 可在应用程序中使用的 SQL Server 数据类型取决于您正在使用的 SQL Server 版本。 有关更多信息，请参见下表中的相关版本的 SQL Server 联机丛书。  
  
 **SQL Server 联机丛书**  
  
1.  [数据类型 （数据库引擎）](https://go.microsoft.com/fwlink/?LinkID=107468)  
  
## <a name="in-this-section"></a>本节内容  
 [SqlTypes 和数据集](../../../../../docs/framework/data/adonet/sql/sqltypes-and-the-dataset.md)  
 说明对 `SqlTypes` 中 `DataSet` 的类型支持。  
  
 [处理 NULL 值](../../../../../docs/framework/data/adonet/sql/handling-null-values.md)  
 演示如何使用空值和三值逻辑。  
  
 [比较 GUID 和 uniqueidentifier 值](../../../../../docs/framework/data/adonet/sql/comparing-guid-and-uniqueidentifier-values.md)  
 演示如何在 SQL Server 和 .NET Framework 中使用 GUID 和 uniqueidentifier 值。  
  
 [日期和时间数据](../../../../../docs/framework/data/adonet/sql/date-and-time-data.md)  
 说明如何使用在 SQL Server 2008 中引入的新的日期和时间数据类型。  
  
 [大型 UDT](../../../../../docs/framework/data/adonet/sql/large-udts.md)  
 演示如何从在 SQL Server 2008 中引入的大值 UDT 检索数据。  
  
 [SQL Server 中的 XML 数据](../../../../../docs/framework/data/adonet/sql/xml-data-in-sql-server.md)  
 说明如何使用从 SQL Server 中检索的 XML 数据。  
  
## <a name="reference"></a>参考  
 <xref:System.Data.DataSet>  
 描述 `DataSet` 类及其所有成员。  
  
 <xref:System.Data.SqlTypes>  
 说明 `SqlTypes` 命名空间及其所有成员。  
  
 <xref:System.Data.SqlDbType>  
 说明 `SqlDbType` 枚举及其所有成员。  
  
 <xref:System.Data.DbType>  
 说明 `DbType` 枚举及其所有成员。  
  
## <a name="see-also"></a>请参阅
- [SQL Server 数据类型映射](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)
- [配置参数和参数数据类型](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)
- [表值参数](../../../../../docs/framework/data/adonet/sql/table-valued-parameters.md)
- [SQL Server 二进制和大值数据](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
