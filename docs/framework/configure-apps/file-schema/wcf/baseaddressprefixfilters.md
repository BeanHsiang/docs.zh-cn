---
title: <baseAddressPrefixFilters>
ms.date: 03/30/2017
ms.assetid: 8cab2a9a-c51f-4283-bb60-2ad0c274fd46
ms.openlocfilehash: 303e1d0ab9150c16cb36439940ade73cf012b2d1
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55261786"
---
# <a name="baseaddressprefixfilters"></a>\<baseAddressPrefixFilters>
表示的配置元素，用于指定传递筛选器提供了一种机制，托管在 IIS 中的 Windows Communication Foundation (WCF) 应用程序时可选取适当的 Internet 信息服务 (IIS) 绑定的集合。  
  
> [!WARNING]
>  \<Baseaddressprefixfilter > 不识别"localhost"，则改为使用完全限定的计算机名称。  
  
 \<system.ServiceModel>  
\<ServiceHostingEnvironment>  
  
## <a name="syntax"></a>语法  
  
```xml  
<serviceHostingEnvironment>
  <baseAddressPrefixFilters>
    <add prefix="String" />
   </baseAddressPrefixFilters>
</serviceHostingEnvironment>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
 无。  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<add>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-baseaddressprefixfilter.md)|添加一个配置元素，用于指定服务主机所使用的基址的前缀筛选器。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<serviceHostingEnvironment>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)|定义服务承载环境要为特定传输实例化的类型。|  
  
## <a name="remarks"></a>备注  
 前缀筛选器为共享的宿主提供程序提供一种指定服务要使用的 URI 的方法。 它使得共享主机可以在同一站点上通过同一方案的不同基址承载多个应用程序。  
  
 IIS 网站是包含虚拟目录的虚拟应用程序的容器。 可通过一个或多个 IIS 绑定访问站点上的应用程序。 IIS 绑定提供两条信息：绑定协议和绑定信息。 绑定协议（例如 HTTP）定义发生通信所基于的方案，而绑定信息（例如 IP 地址、端口、主机头）包含用于访问站点的数据。  
  
 IIS 支持为每个站点指定多个 IIS 绑定，这会导致每个方案有多个基址。 由于一个站点下承载的 WCF 服务允许每个方案只能有一个基址的绑定，可以使用前缀筛选器功能选取所需的托管服务的基址。 根据可选前缀列表筛选器筛选 IIS 提供的传入基址。  
  
 例如，您的站点可包含以下基址。  
  
```  
http://testl.fabrikam.com/Service.svc  
http://test2.fabrikam.com/Service.svc  
```  
  
 可以使用下面的配置文件在 appdomain 级指定前缀筛选器。  
  
```xml  
<system.serviceModel>
  <serviceHostingEnvironment>
    <baseAddressPrefixFilters>
      <add prefix="net.tcp://test1.fabrikam.com:8000" />
      <add prefix="http://test2.fabrikam.com:9000" />
    </baseAddressPrefixFilters>
  </serviceHostingEnvironment>
</system.serviceModel>
```  
  
 在此示例中，`net.tcp://test1.fabrikam.com:8000` 和 `http://test2.fabrikam.com:9000` 是允许传递的各自方案的唯一基址。  
  
 默认情况下，未指定前缀时，将传递所有地址。 而指定前缀后，将只允许传递该方案的匹配基址。  
  
> [!NOTE]
>  筛选器不支持任何通配符。 此外，IIS 提供的基址可能有绑定到在 `baseAddressPrefixFilters` 列表中未列出的其他方案的地址。 不会筛选出这些地址。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Configuration.BaseAddressPrefixFilterElementCollection>
- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection>
- <xref:System.ServiceModel.ServiceHostingEnvironment>
- [承载](../../../../../docs/framework/wcf/feature-details/hosting.md)
