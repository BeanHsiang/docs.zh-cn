---
title: 自定义数据服务提供程序（WCF 数据服务）
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: e702ecdb-3419-4743-92a9-c3c0e7d44082
ms.openlocfilehash: 0f2e7626cb0526ac897853374b483ad09c20d368
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54712608"
---
# <a name="custom-data-service-providers-wcf-data-services"></a>自定义数据服务提供程序（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 包括一组提供程序，用于基于后期绑定数据类型定义数据模型。  
  
|提供程序|描述|  
|--------------|-----------------|  
|元数据提供程序|这是核心的自定义数据服务提供程序，用于通过实现 <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> 接口在运行时定义自定义数据模型。|  
|查询提供程序|该提供程序用于对使用 <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> 接口定义的自定义数据模型执行查询。 查询提供程序通过实现 <xref:System.Data.Services.Providers.IDataServiceQueryProvider> 接口而创建。|  
|更新提供程序|该提供程序用于更新在自定义数据服务提供程序中公开的类型和管理并发性。 更新提供程序通过实现 <xref:System.Data.Services.Providers.IDataServiceUpdateProvider> 接口而创建。|  
|分页提供程序|该提供程序用于与自定义数据服务提供程序一起启用服务器驱动的分页支持。 自定义数据服务的分页提供程序通过实现 <xref:System.Data.Services.Providers.IDataServicePagingProvider> 接口而创建。|  
|流提供程序|此提供程序用于以流形式公开二进制大型对象数据类型。 流提供程序通过实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 接口而创建。 流提供程序还可与实体框架提供程序和反射数据源提供程序一起使用。 有关详细信息，请参阅[流式处理提供程序](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md)。|  
  
 有关详细信息，请参阅文章[自定义数据服务提供商](https://go.microsoft.com/fwlink/?LinkID=186850)并[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]中的提供程序工具包[OData SDK](https://go.microsoft.com/fwlink/?LinkId=186069)。  
  
## <a name="see-also"></a>请参阅
- [数据服务提供程序](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)
- [实体框架提供程序](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md)
- [反射提供程序](../../../../docs/framework/data/wcf/reflection-provider-wcf-data-services.md)
