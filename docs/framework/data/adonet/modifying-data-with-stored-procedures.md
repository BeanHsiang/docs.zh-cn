---
title: 使用存储过程修改数据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7d8e9a46-1af6-4a02-bf61-969d77ae07e0
ms.openlocfilehash: 2093554eb59746d6b52c2895ec3ded5d9088fa3e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54658268"
---
# <a name="modifying-data-with-stored-procedures"></a>使用存储过程修改数据
存储过程可以接受数据作为输入参数并可以返回数据作为输出参数、结果集或返回值。 下面的示例演示 ADO.NET 如何发送和接收输入参数、输出参数及返回值。 该示例将一条新记录插入到一个表中，该表中的主键列为 SQL Server 数据库中的标识列。  
  
> [!NOTE]
>  如果您要通过 SQL Server 存储过程使用 <xref:System.Data.SqlClient.SqlDataAdapter> 来编辑或删除数据，请确保不要在存储过程定义中使用 SET NOCOUNT ON。 这将使返回的受影响的行数为零，`DataAdapter` 会将其解释为并发冲突。 在这种情况下，将引发 <xref:System.Data.DBConcurrencyException>。  
  
## <a name="example"></a>示例  
 该示例使用以下存储的过程插入到新的类别**Northwind** **类别**表。 存储的过程将值**CategoryName**列作为输入的参数，并使用 scope_identity （） 函数来检索标识字段的新值**CategoryID**，并将其返回output 参数。 RETURN 语句使用 @@ROWCOUNT函数返回插入的行数。  
  
```sql
CREATE PROCEDURE dbo.InsertCategory  
  @CategoryName nvarchar(15),  
  @Identity int OUT  
AS  
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)  
SET @Identity = SCOPE_IDENTITY()  
RETURN @@ROWCOUNT  
```  
  
 下面的代码示例使用上面显示的 `InsertCategory` 存储过程作为 <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> 的 <xref:System.Data.SqlClient.SqlDataAdapter> 的来源。 如果在将记录插入到数据库后调用 `@Identity` 的 <xref:System.Data.DataSet> 方法，`Update` 中将会反映出 <xref:System.Data.SqlClient.SqlDataAdapter> 输出参数。 此代码还会检索返回值。  
  
> [!NOTE]
>  使用时<xref:System.Data.OleDb.OleDbDataAdapter>，你必须指定与参数<xref:System.Data.ParameterDirection>的**ReturnValue**之前其他参数。  
  
 [!code-csharp[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/VB/source.vb#1)]  
  
## <a name="see-also"></a>请参阅
- [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [DataAdapters 和 DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)
- [执行命令](../../../../docs/framework/data/adonet/executing-a-command.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
