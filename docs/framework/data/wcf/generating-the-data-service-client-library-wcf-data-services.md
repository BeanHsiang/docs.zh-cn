---
title: 生成数据服务客户端库（WCF 数据服务）
ms.date: 03/30/2017
helpviewer_keywords:
- client applications, WCF Data Services
- WCF Data Services, client library
- Add Service Reference dialog box
ms.assetid: 314077c1-ac10-47e1-bed4-940b5462359d
ms.openlocfilehash: 41f4e7cd633cf6175b6b167937cf53ceb4d9ec59
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56092093"
---
# <a name="generating-the-data-service-client-library-wcf-data-services"></a>生成数据服务客户端库（WCF 数据服务）
实现的数据服务[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]可返回描述数据模型公开的服务元数据文档[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]源。 有关详细信息，请参阅[OData:服务元数据文档](https://go.microsoft.com/fwlink/?LinkId=186070)。 可以使用**添加服务引用**在 Visual Studio 将引用添加到对话框[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]-基于服务。 当使用此工具添加到返回的元数据的引用[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]源客户端项目中，执行以下操作：  
  
-   从数据服务请求服务元数据文档并截获返回的元数据。  
  
    > [!NOTE]
    >  返回的元数据作为 .edmx 文件存储在客户端项目中。 此 .edmx 文件无法通过实体数据模型设计器打开，因为此文件的格式与实体框架所使用的 .edmx 文件的格式不相同。 可以通过使用 XML 编辑器或任何文本编辑器查看此元数据文件。 有关详细信息，请参阅[ \[MC EDMX\]:用于数据服务打包格式的实体数据模型](https://go.microsoft.com/fwlink/?LinkID=178833)规范  
  
-   作为从 <xref:System.Data.Services.Client.DataServiceContext> 继承的实体容器类生成数据服务的表示形式。 此生成的实体容器类与实体数据模型工具生成的实体容器类似。 有关详细信息，请参阅[对象服务概述 (Entity Framework)](https://docs.microsoft.com/previous-versions/bb386871(v=vs.100))。  
  
-   为在服务元数据中发现的数据模型类型生成数据类。  
  
-   在项目中添加对 `System.Data.Services.Client` 程序集的引用。  
  
 有关详细信息，请参阅[如何：添加数据服务引用](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)。  
  
 此外可以通过使用生成的客户端数据服务类[DataSvcUtil.exe](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md)工具在命令提示符处。 有关详细信息，请参阅[如何：手动生成客户端数据服务类](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md)。  
  
## <a name="client-data-type-mapping"></a>客户端数据类型映射  
 当你使用**添加服务引用**Visual Studio 中的对话框或`DataSvcUtil.exe`工具生成基于客户端数据类[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]馈送，.NET Framework 数据类型映射到中的基元类型数据模型，如下所示：  
  
|数据模型类型|.NET Framework 数据类型|  
|---------------------|------------------------------|  
|`Edm.Binary`|<xref:System.Byte> `[]`|  
|`Edm.Boolean`|<xref:System.Boolean>|  
|`Edm.Byte`|<xref:System.Byte>|  
|`Edm.DateTime`|<xref:System.DateTime>|  
|`Edm.Decimal`|<xref:System.Decimal>|  
|`Edm.Double`|<xref:System.Double>|  
|`Edm.Guid`|<xref:System.Guid>|  
|`Edm.Int16`|<xref:System.Int16>|  
|`Edm.Int32`|<xref:System.Int32>|  
|`Edm.Int64`|<xref:System.Int64>|  
|`Edm.SByte`|<xref:System.SByte>|  
|`Edm.Single`|<xref:System.Single>|  
|`Edm.String`|<xref:System.String>|  
  
 有关详细信息，请参阅[OData:基元数据类型](https://go.microsoft.com/fwlink/?LinkId=186072)。  
  
## <a name="see-also"></a>请参阅
- [WCF Data Services 客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)
- [快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)
