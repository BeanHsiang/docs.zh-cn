---
title: Oracle REF CURSOR
ms.date: 03/30/2017
ms.assetid: c6b25b8b-0bdd-41b2-9c7c-661f070c2247
ms.openlocfilehash: 4dd0a78fafe63197987938021195723e3eed0885
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54740991"
---
# <a name="oracle-ref-cursors"></a>Oracle REF CURSOR
Oracle.NET Framework 数据提供程序支持 Oracle **REF CURSOR**数据类型。 在通过数据提供程序使用 Oracle REF CURSOR 时，应考虑下列行为。  
  
> [!NOTE]
>  有些行为与 Microsoft Oracle OLE DB 提供程序 (MSDAORA) 的行为不同。  
  
-   出于性能原因，Oracle 数据提供程序不会自动绑定**REF CURSOR**数据类型，因为 MSDAORA 会这样做，除非显式指定。  
  
-   数据提供程序不支持任何 ODBC 转义序列，包括用于指定 REF CURSOR 参数的 {resultset} 转义。  
  
-   若要执行返回 REF Cursor 的存储的过程，必须定义中的参数<xref:System.Data.OracleClient.OracleParameterCollection>与<xref:System.Data.OracleClient.OracleType>的**光标**和一个<xref:System.Data.OracleClient.OracleParameter.Direction%2A>的**输出**。 数据提供程序只支持作为输出参数绑定 REF CURSOR。 提供程序不支持 REF CURSOR 作为输入参数。  
  
-   不支持从参数值获取 <xref:System.Data.OracleClient.OracleDataReader>。 在执行命令后，值属于 <xref:System.DBNull> 类型。  
  
-   唯一**CommandBehavior**适用于 REF Cursor 的枚举值 (例如，当调用<xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A>) 是**CloseConnection**; 忽略所有其他。  
  
-   中的 REF Cursor 的顺序**OracleDataReader**取决于中的参数顺序**OracleParameterCollection**。 <xref:System.Data.OracleClient.OracleParameter.ParameterName%2A> 属性被忽略。  
  
-   PL/SQL**表**不支持数据类型。 但是，REF CURSOR 的效率更高。 如果必须使用**表**数据类型，使用 MSDAORA OLE DB.NET 数据提供程序。  
  
## <a name="in-this-section"></a>本节内容  
 [REF CURSOR 示例](../../../../docs/framework/data/adonet/ref-cursor-examples.md)  
 包含三个示例，演示如何使用 REF CURSOR。  
  
 [OracleDataReader 中的 REF CURSOR 参数](../../../../docs/framework/data/adonet/ref-cursor-parameters-in-an-oracledatareader.md)  
 演示如何执行一个 PL/SQL 存储过程，返回 REF CURSOR 参数，并读取的值作为**OracleDataReader**。  
  
 [使用 OracleDataReader 从多个 REF CURSOR 中检索数据](../../../../docs/framework/data/adonet/retrieving-data-from-multiple-ref-cursors.md)  
 演示如何执行一个 PL/SQL 存储过程，返回两个 REF CURSOR 参数，并读取使用的值**OracleDataReader**。  
  
 [使用一个或多个 REF CURSOR 填充数据集](../../../../docs/framework/data/adonet/filling-a-dataset-using-one-or-more-ref-cursors.md)  
 演示如何执行一个 PL/SQL 存储过程，返回两个 REF CURSOR 参数，并使用返回的行填充 <xref:System.Data.DataSet>。  
  
## <a name="see-also"></a>请参阅
- [Oracle 和 ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
