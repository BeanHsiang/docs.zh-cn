---
title: Oracle BFILE
ms.date: 03/30/2017
ms.assetid: 341bbf84-4734-4d44-8723-ccedee954e21
ms.openlocfilehash: 825cb9eb4bdb54509c8ca3c20db4dade8b3ece73
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54677233"
---
# <a name="oracle-bfiles"></a>Oracle BFILE
Oracle .NET Framework 数据提供程序包括 <xref:System.Data.OracleClient.OracleBFile> 类，该类用于使用 Oracle <xref:System.Data.OracleClient.OracleType.BFile> 数据类型。  
  
 Oracle **BFILE**数据类型是一种 Oracle **LOB**数据类型，包含最大大小为 4 千兆字节的二进制数据的引用。 Oracle **BFILE**不同于其他 Oracle **LOB**数据类型，其数据存储在服务器上的物理文件中而不是操作系统中。 请注意， **BFILE**数据类型提供对数据的只读访问。  
  
 其他特征**BFILE**将其从区分开来的数据类型**LOB**数据类型是：  
  
-   包含非结构化数据。  
  
-   支持服务器端分块。  
  
-   使用引用复制语义。 例如，如果在执行复制操作**BFILE**，则只**BFILE**复制定位符 （这是对文件的引用）。 而不会复制文件中的数据。  
  
 **BFILE**为引用较大，Lob，应使用数据类型，因此，在数据库中存储不可行。 当使用涉及更多的客户端、 服务器和通信开销**BFILE**数据类型与比较**LOB**数据类型。 若要访问效率更高**BFILE**如果只需要获取少量的数据。 如果需要获取整个对象，访问数据库驻留的 LOB 会更加有效。  
  
 每个非 NULL **OracleBFile**对象是与定义的基础物理文件位置的两个实体相关联：  
  
1.  一个 Oracle DIRECTORY 对象，它是文件系统中一个目录的数据库别名，以及  
  
2.  基础物理文件的文件名，它位于与 DIRECTORY 对象关联的目录中。  
  
## <a name="example"></a>示例  
 下面的 C# 示例演示如何创建**BFILE**在 Oracle 表中，然后检索它的形式**OracleBFile**对象。 该示例演示了如何使用<xref:System.Data.OracleClient.OracleDataReader>对象和**OracleBFile** **Seek**并**读取**方法。 请注意，若要使用此示例，您必须首先创建一个名为"c:\\\bfiles"和 Oracle 服务器上名为"MyFile.jpg"的文件。  
  
```csharp  
using System;  
using System.IO;  
using System.Data;  
using System.Data.OracleClient;  
  
public class Sample  
{  
   public static void Main(string[] args)  
   {  
      OracleConnection connection = new OracleConnection(  
        "Data Source=Oracle8i;Integrated Security=yes");  
      connection.Open();  
  
      OracleCommand command = connection.CreateCommand();  
      command.CommandText =   
        "CREATE or REPLACE DIRECTORY MyDir as 'c:\\bfiles'";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "DROP TABLE MyBFileTable";  
      try {  
        command.ExecuteNonQuery();  
      }  
      catch {  
      }  
      command.CommandText =   
        "CREATE TABLE MyBFileTable(col1 number, col2 BFILE)";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "INSERT INTO MyBFileTable values ('2', BFILENAME('MyDir', " +  
        "'MyFile.jpg'))";  
      command.ExecuteNonQuery();  
      command.CommandText = "SELECT * FROM MyBFileTable";  
  
        byte[] buffer = new byte[100];  
  
      OracleDataReader reader = command.ExecuteReader();  
      using (reader) {  
          if (reader.Read()) {  
                OracleBFile bFile = reader.GetOracleBFile(1);  
                using (bFile) {  
                  bFile.Seek(0, SeekOrigin.Begin);  
                  bFile.Read(buffer, 0, 100);  
              }  
          }  
      }  
  
      connection.Close();  
   }  
  
}  
```  
  
## <a name="see-also"></a>请参阅
- [Oracle 和 ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
