---
title: SQL Server 架构集合
ms.date: 03/30/2017
ms.assetid: c6403cc3-d78b-4f85-bab1-ada7a3446ec5
ms.openlocfilehash: 2445ab2ffbe30b647e256e223f712300bcf19931
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54635034"
---
# <a name="sql-server-schema-collections"></a>SQL Server 架构集合
除了通用架构集合之外，适用于 SQL Server 的 Microsoft .NET Framework 数据提供程序还支持其他架构集合。 架构集合因使用的 SQL Server 的版本而稍有不同。 若要确定支持的架构集合的列表，请调用**GetSchema**不带任何参数，或使用架构集合名称"MetaDataCollections"的方法。 此时将返回 <xref:System.Data.DataTable>，包含支持的架构集合列表、每个架构集合支持的限制数以及所使用的标识符部分数。  
  
## <a name="databases"></a>数据库  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|database_name|String|数据库的名称。|  
|dbid|Int16|数据库 ID。|  
|create_date|DateTime|数据库的创建日期。|  
  
## <a name="foreign-keys"></a>Foreign Keys  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|CONSTRAINT_CATALOG|String|约束所属的编录。|  
|CONSTRAINT_SCHEMA|String|包含约束的架构。|  
|CONSTRAINT_NAME|String|名称。|  
|TABLE_CATALOG|String|约束所属的表名。|  
|TABLE_SCHEMA|String|包含表的架构。|  
|TABLE_NAME|String|表名称|  
|CONSTRAINT_TYPE|String|约束的类型。 只允许“FOREIGN KEY”。|  
|IS_DEFERRABLE|String|指定约束是否可以推迟。 返回 NO。|  
|INITIALLY_DEFERRED|String|指定约束最初是否可以推迟。 返回 NO。|  
  
## <a name="indexes"></a>索引  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|constraint_catalog|String|索引所属的编录。|  
|constraint_schema|String|包含索引的架构。|  
|constraint_name|String|索引的名称。|  
|table_catalog|String|索引关联的表名。|  
|table_schema|String|包含索引关联的表的架构。|  
|table_name|String|表名。|  
|index_name|String|索引名称。|  
  
### <a name="indexes-sql-server-2008"></a>Indexes (SQL Server 2008)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，以下列已经添加到 Indexes 架构集合以支持新的空间类型、文件流和稀疏列。 早期版本的 .NET Framework 和 SQL Server 不支持这些列。  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|type_desc|String|索引类型可以为以下值之一：<br /><br /> -   HEAP<br />群集<br />-非聚集<br />-   XML<br />-   SPATIAL|  
  
## <a name="indexcolumns"></a>IndexColumns  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|constraint_catalog|String|索引所属的编录。|  
|constraint_schema|String|包含索引的架构。|  
|constraint_name|String|索引的名称。|  
|table_catalog|String|索引关联的表名。|  
|table_schema|String|包含索引关联的表的架构。|  
|table_name|String|表名。|  
|column_name|String|索引关联的列名。|  
|ordinal_position|Int32|列的序号位置。|  
|KeyType|Byte|对象的类型。|  
|index_name|String|索引名称。|  
  
## <a name="procedures"></a>过程  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|SPECIFIC_CATALOG|String|编录的特定名称。|  
|SPECIFIC_SCHEMA|String|架构的特定名称。|  
|SPECIFIC_NAME|String|编录的特定名称。|  
|ROUTINE_CATALOG|String|存储过程所属的编录。|  
|ROUTINE_SCHEMA|String|包含存储过程的架构。|  
|ROUTINE_NAME|String|存储过程的名称。|  
|ROUTINE_TYPE|String|对于存储过程，返回 PROCEDURE，对于函数，返回 FUNCTION。|  
|CREATED|DateTime|过程的创建时间。|  
|LAST_ALTERED|DateTime|上次修改过程的时间。|  
  
## <a name="procedure-parameters"></a>Procedure Parameters  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|SPECIFIC_CATALOG|String|此参数所属的过程的编录名称。|  
|SPECIFIC_SCHEMA|String|包含此参数所属的过程的架构。|  
|SPECIFIC_NAME|String|此参数所属的过程的名称。|  
|ORDINAL_POSITION|Int32|参数的序号位置，从 1 开始。 对于过程的返回值，此位置为 0。|  
|PARAMETER_MODE|String|如果是输入参数，返回 IN，如果是输出参数，返回 OUT，如果是输入/输出参数，返回 INOUT。|  
|IS_RESULT|String|如果指示属于函数的过程的结果，返回 YES。 否则，返回 NO。|  
|AS_LOCATOR|String|如果声明为定位符，返回 YES。 否则，返回 NO。|  
|PARAMETER_NAME|String|参数的名称。 如果对应于函数的返回值，返回 NULL。|  
|DATA_TYPE|String|系统提供的数据类型。|  
|CHARACTER_MAXIMUM_LENGTH|Int32|二进制或字符数据类型的最大长度（字符数）。 否则，返回 NULL。|  
|CHARACTER_OCTET_LENGTH|Int32|二进制或字符数据类型的最大长度（字节数）。 否则，返回 NULL。|  
|COLLATION_CATALOG|String|参数排序规则的编录名称。 如果不属于某种字符类型，返回 NULL。|  
|COLLATION_SCHEMA|String|始终返回 NULL。|  
|COLLATION_NAME|String|参数分页的名称。 如果不属于某种字符类型，返回 NULL。|  
|CHARACTER_SET_CATALOG|String|参数字符集的编录名称。 如果不属于某种字符类型，返回 NULL。|  
|CHARACTER_SET_SCHEMA|String|始终返回 NULL。|  
|CHARACTER_SET_NAME|String|参数字符集的名称。 如果不属于某种字符类型，返回 NULL。|  
|NUMERIC_PRECISION|Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|NUMERIC_PRECISION_RADIX|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|NUMERIC_SCALE|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|DATETIME_PRECISION|Int16|如果参数类型为 datetime 或 smalldatetime，则为小数秒数的精度。 否则，返回 NULL。|  
|INTERVAL_TYPE|String|NULL。 保留供 SQL Server 以后使用。|  
|INTERVAL_PRECISION|Int16|NULL。 保留供 SQL Server 以后使用。|  
  
## <a name="tables"></a>表  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|表的编录。|  
|TABLE_SCHEMA|String|包含表的架构。|  
|TABLE_NAME|String|表名。|  
|TABLE_TYPE|String|表的类型。 可以是 VIEW 或 BASE TABLE。|  
  
## <a name="columns"></a>Columns  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|表的编录。|  
|TABLE_SCHEMA|String|包含表的架构。|  
|TABLE_NAME|String|表名。|  
|COLUMN_NAME|String|列名称。|  
|ORDINAL_POSITION|Int32|列标识号。|  
|COLUMN_DEFAULT|String|列的默认值。|  
|IS_NULLABLE|String|列的可空性。 如果此列允许 NULL，此列将返回 YES。 否则，返回 No。|  
|DATA_TYPE|String|系统提供的数据类型。|  
|CHARACTER_MAXIMUM_LENGTH|Int32 – Sql8、Int16 – Sql7|二进制数据、字符数据或文本和图像数据的最大长度（字符数）。 否则，返回 NULL。|  
|CHARACTER_OCTET_LENGTH|Int32 – SQL8、Int16 – Sql7|二进制数据、字符数据或文本和图像数据的最大长度（字节数）。 否则，返回 NULL。|  
|NUMERIC_PRECISION|Unsigned Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|NUMERIC_PRECISION_RADIX|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|NUMERIC_SCALE|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|DATETIME_PRECISION|Int16|datetime 和 SQL-92 interval 数据类型的子类型代码。 对于其他数据类型，返回 NULL。|  
|CHARACTER_SET_CATALOG|String|如果列为字符数据或文本数据类型，则返回 master，指示字符集所处的数据库。 否则，返回 NULL。|  
|CHARACTER_SET_SCHEMA|String|始终返回 NULL。|  
|CHARACTER_SET_NAME|String|如果此列为字符数据或文本数据类型，则返回字符集的唯一名称。 否则，返回 NULL。|  
|COLLATION_CATALOG|String|如果列为字符数据或文本数据类型，则返回 master，指示定义分页的数据库。 否则，此列为 NULL.|  
  
### <a name="columns-sql-server-2008"></a>Columns (SQL Server 2008)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，以下列已经添加到 Colums 架构集合以支持新的空间类型、文件流和稀疏列。 早期版本的 .NET Framework 和 SQL Server 不支持这些列。  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|IS_FILESTREAM|String|YES       FILESTREAM    <br /><br /> NO，如果列不具有 FILESTREAM 属性。|  
|IS_SPARSE|String|YES，如果列是稀疏列。<br /><br /> NO，如果列不是稀疏列。|  
|IS_COLUMN_SET|String|YES，如果列是一个列集列。<br /><br /> NO            |  
  
### <a name="allcolumns-sql-server-2008"></a>AllColumns (SQL Server 2008)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，添加了 AllColumns 架构集合以支持稀疏列。 早期版本的 .NET Framework 和 SQL Server 不支持 AllColumns。  
  
 AllColumns 与 Columns 架构集合具有相同的限制和生成的 DataTable 架构。 唯一的区别是 AllColumns 包含 Columns 架构集合中未包含的列集列。 下表介绍了这些列。  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|表的编录。|  
|TABLE_SCHEMA|String|包含表的架构。|  
|TABLE_NAME|String|表名。|  
|COLUMN_NAME|String|列名称。|  
|ORDINAL_POSITION|Int32|列标识号。|  
|COLUMN_DEFAULT|String|列的默认值。|  
|IS_NULLABLE|String|列的可空性。 如果此列允许 NULL，此列将返回 YES。 否则，返回 NO。|  
|DATA_TYPE|String|系统提供的数据类型。|  
|CHARACTER_MAXIMUM_LENGTH|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字符数）。 否则，返回 NULL。|  
|CHARACTER_OCTET_LENGTH|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字节数）。 否则，返回 NULL。|  
|NUMERIC_PRECISION|Unsigned Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|NUMERIC_PRECISION_RADIX|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|NUMERIC_SCALE|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|DATETIME_PRECISION|Int16|datetime 和 SQL-92 interval 数据类型的子类型代码。 对于其他数据类型，返回 NULL。|  
|CHARACTER_SET_CATALOG|String|如果列为字符数据或文本数据类型，则返回 master，指示字符集所处的数据库。 否则，返回 NULL。|  
|CHARACTER_SET_SCHEMA|String|始终返回 NULL。|  
|CHARACTER_SET_NAME|String|如果此列为字符数据或文本数据类型，则返回字符集的唯一名称。 否则，返回 NULL。|  
|COLLATION_CATALOG|String|如果列为字符数据或文本数据类型，则返回 master，指示定义分页的数据库。 否则，此列为 NULL.|  
|IS_FILESTREAM|String|YES       FILESTREAM    <br /><br /> NO，如果列不具有 FILESTREAM 属性。|  
|IS_SPARSE|String|YES，如果列是稀疏列。<br /><br /> NO，如果列不是稀疏列。|  
|IS_COLUMN_SET|String|YES，如果列是一个列集列。<br /><br /> NO            |  
  
### <a name="columnsetcolumns-sql-server-2008"></a>ColumnSetColumns (SQL Server 2008)  
 从 .NET Framework 版本 3.5 SP1 和 SQL Server 2008 开始，添加了 ColumnSetColumns 架构集合以支持稀疏列。 早期版本的 .NET Framework 和 SQL Server 不支持 ColumnSetColumns。 ColumnSetColumns 架构集合返回列集中所有列的架构。 下表介绍了这些列。  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|表的编录。|  
|TABLE_SCHEMA|String|包含表的架构。|  
|TABLE_NAME|String|表名。|  
|COLUMN_NAME|String|列名称。|  
|ORDINAL_POSITION|Int32|列标识号。|  
|COLUMN_DEFAULT|String|列的默认值。|  
|IS_NULLABLE|String|列的可空性。 如果此列允许 NULL，此列将返回 YES。 否则，返回 NO。|  
|DATA_TYPE|String|系统提供的数据类型。|  
|CHARACTER_MAXIMUM_LENGTH|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字符数）。 否则，返回 NULL。|  
|CHARACTER_OCTET_LENGTH|Int32|二进制数据、字符数据或文本和图像数据的最大长度（字节数）。 否则，返回 NULL。|  
|NUMERIC_PRECISION|Unsigned Byte|近似数值数据、精确数值数据、整数数据或货币数据的精度。 否则，返回 NULL。|  
|NUMERIC_PRECISION_RADIX|Int16|近似数值数据、精确数值数据、整数数据或货币数据的精度基数。 否则，返回 NULL。|  
|NUMERIC_SCALE|Int32|近似数值数据、精确数值数据、整数数据或货币数据的小数位数。 否则，返回 NULL。|  
|DATETIME_PRECISION|Int16|datetime 和 SQL-92 interval 数据类型的子类型代码。 对于其他数据类型，返回 NULL。|  
|CHARACTER_SET_CATALOG|String|如果列为字符数据或文本数据类型，则返回 master，指示字符集所处的数据库。 否则，返回 NULL。|  
|CHARACTER_SET_SCHEMA|String|始终返回 NULL。|  
|CHARACTER_SET_NAME|String|如果此列为字符数据或文本数据类型，则返回字符集的唯一名称。 否则，返回 NULL。|  
|COLLATION_CATALOG|String|如果列为字符数据或文本数据类型，则返回 master，指示定义分页的数据库。 否则，此列为 NULL.|  
|IS_FILESTREAM|String|YES       FILESTREAM    <br /><br /> NO，如果列不具有 FILESTREAM 属性。|  
|IS_SPARSE|String|YES，如果列是稀疏列。<br /><br /> NO，如果列不是稀疏列。|  
|IS_COLUMN_SET|String|YES，如果列是一个列集列。<br /><br /> NO            |  
  
## <a name="users"></a>Users  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|uid|Int16|在此数据库中唯一的用户 ID。 1 为数据库所有者。|  
|user_name|String|在此数据库中唯一的用户名和组名。|  
|createdate|DateTime|添加帐户的日期。|  
|updatedate|DateTime|上次更改帐户的日期。|  
  
## <a name="views"></a>视图  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|TABLE_CATALOG|String|视图的编录。|  
|TABLE_SCHEMA|String|包含视图的架构。|  
|TABLE_NAME|String|视图名称。|  
|CHECK_OPTION|String|WITH CHECK OPTION 的类型。 如果原始视图使用 WITH CHECK OPTION 创建，则为 CASCADE。 否则，返回 NONE。|  
|IS_UPDATABLE|String|指定视图是否可以更新。 始终返回 NO。|  
  
## <a name="viewcolumns"></a>ViewColumns  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|VIEW_CATALOG|String|视图的编录。|  
|VIEW_SCHEMA|String|包含视图的架构。|  
|VIEW_NAME|String|视图名称。|  
|TABLE_CATALOG|String|与此视图关联的表的编录。|  
|TABLE_SCHEMA|String|包含与此视图关联的表的架构。|  
|TABLE_NAME|String|与此视图关联的表的名称。 基表。|  
|COLUMN_NAME|String|列名称。|  
  
## <a name="userdefinedtypes"></a>UserDefinedTypes  
  
|列名|数据类型|描述|  
|----------------|--------------|-----------------|  
|assembly_name|String|程序集文件的名称。|  
|udt_name|String|程序集的类名。|  
|version_major|对象|主版本号。|  
|version_minor|对象|次版本号。|  
|version_build|对象|Build 号。|  
|version_revision|对象|修订号。|  
|culture_info|对象|与此 UDT 关联的区域性信息。|  
|public_key|对象|此程序集使用的公钥。|  
|is_fixed_length|Boolean|指定类型的长度是否始终与 max_length 相同。|  
|max_length|Int16|类型的最大长度（字节数）。|  
|Create_Date|DateTime|创建/注册程序集的日期。|  
|Permission_set_desc|String|程序集的权限集/安全级别的友好名称。|  
  
## <a name="see-also"></a>请参阅
- [检索数据库架构信息](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
