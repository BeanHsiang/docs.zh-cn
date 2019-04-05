---
title: System.DateTimeOffset 方法
ms.date: 03/30/2017
ms.assetid: 25b3e5c0-7603-4a70-b3e5-2149e3da69a2
ms.openlocfilehash: 46b1622cdc8a38544f1c8a8104abb935c9ff1269
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54637198"
---
# <a name="systemdatetimeoffset-methods"></a>System.DateTimeOffset 方法
在对象模型或外部映射文件中进行映射后，LINQ to SQL 允许您从 LINQ to SQL 查询内调用大部分的 <xref:System.DateTimeOffset?displayProperty=nameWithType> 方法、运算符和属性。  
  
 不支持的方法仅包括那些继承自 <xref:System.Object?displayProperty=nameWithType> 的方法，这些方法在 LINQ to SQL 查询的上下文中没有意义，例如：`Finalize`、`GetHashCode`、`GetType` 和 `MemberwiseClone`。 这些方法不受支持的原因是 LINQ to SQL 无法转换它们以在 SQL Server 上执行。  
  
> [!NOTE]
>  若要能够使用公共语言运行库 (CLR) <xref:System.DateTimeOffset?displayProperty=nameWithType> 结构并通过 LINQ to SQL 将其映射到 SQL `DATETIMEOFFSET` 列，必须安装 .NET Framework 3.5 SP1 或更高版本。 SQL `DATETIMEOFFSET` 列仅在 Microsoft SQL Server 2008 和更高版本中提供。  
  
## <a name="sqlmethods-date-and-time-methods"></a>SQLMethods 日期和时间方法  
 除了 <xref:System.DateTimeOffset> 结构提供的方法，LINQ to SQL 还提供下表列出的来自 <xref:System.Data.Linq.SqlClient.SqlMethods?displayProperty=nameWithType> 类的方法，以便与日期和时间一起使用。  
  
||||  
|-|-|-|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffDay%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMillisecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffNanosecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffHour%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMinute%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffSecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMicrosecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMonth%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffYear%2A>|  
  
## <a name="see-also"></a>请参阅
- [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)
- [创建对象模型](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)
- [SQL-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)
