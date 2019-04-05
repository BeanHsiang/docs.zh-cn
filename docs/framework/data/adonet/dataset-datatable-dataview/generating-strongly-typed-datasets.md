---
title: 生成强类型化数据集
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 54333cbf-bb43-4314-a7d4-6dc1dd1c44b3
ms.openlocfilehash: d0a22a4ec4ed508a06e385d954a8ed5b9e9ff6a9
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55825584"
---
# <a name="generating-strongly-typed-datasets"></a>生成强类型化数据集
如果给定符合 XML 架构定义语言 (XSD) 标准的 XML 架构，您就可以使用随 <xref:System.Data.DataSet> 提供的 XSD.exe 工具生成强类型 [!INCLUDE[winsdklong](../../../../../includes/winsdklong-md.md)]。  
  
 (若要从数据库表创建 xsd，请参阅<xref:System.Data.DataSet.WriteXmlSchema%2A>或[使用 Visual Studio 中的数据集](/visualstudio/data-tools/dataset-tools-in-visual-studio))。  
  
 下面的代码显示了生成的语法**数据集**使用此工具。  
  
```  
xsd.exe /d /l:CS XSDSchemaFileName.xsd /eld /n:XSDSchema.Namespace  
```  
  
 在此语法中，`/d`指令指示该工具以生成**数据集**，和`/l:`指示该工具 （例如，C# 或 Visual Basic.NET） 使用的语言。 可选`/eld`指令指定了可用于[!INCLUDE[linq_dataset](../../../../../includes/linq-dataset-md.md)]对生成的查询**数据集。** 当同时指定 `/d` 选项时可使用此选项。 有关详细信息，请参阅[查询类型化数据集](../../../../../docs/framework/data/adonet/querying-typed-datasets.md)。 可选`/n:`指令指示该工具还生成的命名空间**数据集**调用**XSDSchema.Namespace**。 命令的输出为 XSDSchemaFileName.cs，该输出可以在 ADO.NET 应用程序中编译和使用。 所生成的代码可以编译成库或模块。  
  
 以下代码显示使用 C# 编译器 (csc.exe) 将生成的代码编译成库的语法。  
  
```  
csc.exe /t:library XSDSchemaFileName.cs /r:System.dll /r:System.Data.dll  
```  
  
 `/t:` 指令指示该工具编译成库，`/r:` 指令指定进行编译所需的依赖库。 该命令的输出为 XSDSchemaFileName.dll，它可以在使用 `/r:` 指令编译 ADO.NET 应用程序时传递给编译器。  
  
 以下代码显示访问向 ADO.NET 应用程序中的 XSD.exe 传递的命名空间的语法。  
  
```vb  
Imports XSDSchema.Namespace  
```  
  
```csharp  
using XSDSchema.Namespace;  
```  
  
 下面的代码示例使用类型化**数据集**名为**CustomerDataSet**加载客户列表**Northwind**数据库。 使用加载数据后**填充**方法，该示例循环访问每个客户**客户**表可使用类型化**CustomersRow** (**DataRow**) 对象。 这提供了直接访问权限**CustomerID**列中，而不是通过**DataColumnCollection**。  
  
```vb  
Dim customers As CustomerDataSet= New CustomerDataSet()  
Dim adapter As SqlDataAdapter New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers;", _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=Northwind")  
  
adapter.Fill(customers, "Customers")  
  
Dim customerRow As CustomerDataSet.CustomersRow  
For Each customerRow In customers.Customers  
  Console.WriteLine(customerRow.CustomerID)  
Next  
```  
  
```csharp  
CustomerDataSet customers = new CustomerDataSet();  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers;",  
  "Data Source=(local);Integrated " +  
  "Security=SSPI;Initial Catalog=Northwind");  
  
adapter.Fill(customers, "Customers");  
  
foreach(CustomerDataSet.CustomersRow customerRow in customers.Customers)  
  Console.WriteLine(customerRow.CustomerID);  
```  
  
 下面是用于该示例的 XML 架构。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet" xmlns="" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Data.DataColumnCollection>
- <xref:System.Data.DataSet>
- [类型化数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)
- [数据集、数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)
- [ADO.NET 托管提供程序和数据集开发人员中心](https://go.microsoft.com/fwlink/?LinkId=217917)
