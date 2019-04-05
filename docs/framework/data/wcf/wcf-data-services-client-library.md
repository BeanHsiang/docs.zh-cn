---
title: WCF 数据服务客户端库
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
- DataServiceQuery class, about DataServiceQuery class
- DataServiceContext class, about DataServiceContext class
ms.assetid: 21075e50-8917-413e-a8ea-35a0f6e65aa5
ms.openlocfilehash: 9af19f2ef552c5871d488c968368a9192bae9edb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54656214"
---
# <a name="wcf-data-services-client-library"></a>WCF 数据服务客户端库
如果任一应用程序可发送 HTTP 请求并处理数据服务返回的 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源，则该应用程序可与基于[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的数据服务进行交互。 通过这种互操作性，你可以从启用 Web 的诸多应用程序访问基于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的服务。 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 包括提供更丰富的编程体验，当您使用的客户端库[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]源从.NET Framework 或基于 Silverlight 的应用程序。  
  
 客户端库的两大主要类为 <xref:System.Data.Services.Client.DataServiceContext> 类和 <xref:System.Data.Services.Client.DataServiceQuery%601> 类。 <xref:System.Data.Services.Client.DataServiceContext> 类封装针对指定数据服务支持的操作。 尽管 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务是无状态的，但上下文不是。 因此，可以使用<xref:System.Data.Services.Client.DataServiceContext>诸如更改管理的类，以保持与数据服务以便支持各种交互之间客户端的状态功能。 该类还对更改的标识和跟踪进行管理。 <xref:System.Data.Services.Client.DataServiceQuery%601> 类表示一个针对特定实体集的查询。  
  
 本节介绍如何使用客户端库从 .NET Framework 客户端应用程序访问和更改数据。 有关如何使用详细信息[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端库与基于 Silverlight 的应用程序，请参阅[WCF 数据服务 (Silverlight)](https://go.microsoft.com/fwlink/?LinkId=186016)。 其他客户端库可让你使用[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]源中其他类型的应用程序。 有关详细信息，请参阅[OData SDK](https://go.microsoft.com/fwlink/?LinkID=185796)。  
  
## <a name="in-this-section"></a>本节内容  
 [生成数据服务客户端库](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)  
 介绍如何生成客户端库和客户端数据服务类基于[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]馈送。  
  
 [查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)  
 介绍如何使用客户端库从基于 .NET Framework 的应用程序查询数据服务。  
  
 [加载延迟的内容](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)  
 介绍如何加载未包含在初始查询响应中的附加内容。  
  
 [更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)  
 介绍如何使用客户端库来创建、修改和删除实体和关系。  
  
 [异步操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)  
 介绍客户端库提供的用于以异步方式使用数据服务的功能。  
  
 [批处理操作](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)  
 介绍如何使用客户端库在一个批处理中向数据服务发送多个请求。  
  
 [将数据绑定到控件](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md)  
 介绍如何将控件绑定到[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]数据服务返回的源。  
  
 [调用服务操作](../../../../docs/framework/data/wcf/calling-service-operations-wcf-data-services.md)  
 介绍如何使用客户端库调用服务操作。  
  
 [管理数据服务上下文](../../../../docs/framework/data/wcf/managing-the-data-service-context-wcf-data-services.md)  
 介绍用于管理客户端库的行为的选项。  
  
 [处理二进制数据](../../../../docs/framework/data/wcf/working-with-binary-data-wcf-data-services.md)  
 介绍如何访问和更改数据服务作为数据流返回的二进制数据。  
  
## <a name="see-also"></a>请参阅
- [定义 WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)
- [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)
