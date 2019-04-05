---
title: <applicationPool> 元素（Web 设置）
ms.date: 03/30/2017
helpviewer_keywords:
- applicationPool element
- <applicationPool> element
ms.assetid: 46d1baaa-e343-4639-b70d-2a43a9f62b2a
ms.openlocfilehash: a9c81d98a5e531eaa547614c4d236b6c84526398
ms.sourcegitcommit: 01ea420eaa4bf76d5fc47673294c8881379b3369
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2019
ms.locfileid: "55758269"
---
# <a name="applicationpool-element-web-settings"></a>\<applicationPool > 元素 （Web 设置）
指定 ASP.NET 用于 ASP.NET 应用程序在中集成模式下运行时管理的进程范围行为的配置设置[!INCLUDE[iisver](../../../../../includes/iisver-md.md)]或更高版本。  
  
> [!IMPORTANT]
>  此元素和功能它支持唯一工作，如果 ASP.NET 应用程序承载于[!INCLUDE[iisver](../../../../../includes/iisver-md.md)]或更高版本。  
  
 \<configuration>  
\<system.web > 元素 （Web 设置）  
\<applicationPool > 元素 （Web 设置）  
  
## <a name="syntax"></a>语法  
  
```xml  
<applicationPool   
    maxConcurrentRequestsPerCPU="5000"   
    maxConcurrentThreadsPerCPU="0"   
    requestQueueLimit="5000" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`maxConcurrentRequestsPerCPU`|指定 ASP.NET 允许每个 CPU 的并发请求数。|  
|`maxConcurrentThreadsPerCPU`|指定为每个 CPU 可以为应用程序池运行并发线程数。 这提供了用于控制 ASP.NET 并发的替代方法，因为您可以限制可每 CPU 用于为请求提供服务的托管线程数。 默认情况下此设置为 0，这意味着 ASP.NET 不尽管 CLR 线程池还限制可创建的线程数限制每个 CPU，可以创建的线程数。|  
|`requestQueueLimit`|指定的最大可以为 ASP.NET 在单个进程中排队的请求数。 当两个或多个 ASP.NET 应用程序运行在单个应用程序池时，向应用程序池的任何应用程序发出的请求的累积一受到此设置。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<system.web>](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)|包含有关 ASP.NET 如何与主机应用程序进行交互的信息。|  
  
## <a name="remarks"></a>备注  
 当你运行[!INCLUDE[iisver](../../../../../includes/iisver-md.md)]或更高版本在集成模式下，此元素组合可让你配置 ASP.NET 如何管理线程和队列请求，当应用程序承载于 IIS 应用程序池。 如果运行 IIS 6 也运行[!INCLUDE[iisver](../../../../../includes/iisver-md.md)]在经典模式下或在 ISAPI 模式下，将忽略这些设置。  
  
 `applicationPool`设置适用于特定版本的.NET Framework 运行的所有应用程序池。 设置包含在 aspnet.config 文件中。 没有此文件的版本 2.0 和.NET Framework 4.0 版本。 （版本 3.0 和.NET Framework 3.5 的 aspnet.config 文件与共享版本 2.0。）  
  
> [!IMPORTANT]
>  如果在运行[!INCLUDE[iisver](../../../../../includes/iisver-md.md)]上[!INCLUDE[win7](../../../../../includes/win7-md.md)]，可以配置每个应用程序池的单独的 aspnet.config 文件。 这样，你可以定制每个应用程序池的线程的性能。  
  
 有关`maxConcurrentRequestsPerCPU`中的设置，默认值为"5000"[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]有效地将关闭请求限制，它受 ASP.NET 中，除非您真正使用每个 CPU 的 5000 或多个请求。 默认设置改为依赖于 CLR 线程池来自动管理每个 CPU 的并发。 请广泛使用的异步请求处理，或具有网络 I/O 上阻塞的很多长时间运行请求的应用程序将受益于中的增大的默认限制[!INCLUDE[net_v40_short](../../../../../includes/net-v40-short-md.md)]。 设置`maxConcurrentRequestsPerCPU`到用于处理 ASP.NET 请求零将关闭托管线程的使用。 应用程序中运行时的 IIS 应用程序池，请求将停留在 IIS I/O 线程和线程的 IIS 设置因此阻止并发。  
  
 `requestQueueLimit`设置的工作方式相同`requestQueueLimit`的属性[processModel](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7w2sway1(v=vs.100))元素，它在 ASP.NET 应用程序的 Web.config 文件中设置。 但是， `requestQueueLimit` aspnet.config 文件中的设置将重写`requestQueueLimit`Web.config 文件中的设置。 换而言之，如果将这两个属性都设置 （默认情况下为 true）， `requestQueueLimit` aspnet.config 文件中的设置优先。  
  
## <a name="example"></a>示例  
 下面的示例演示如何在以下情况下的 aspnet.config 文件中配置 ASP.NET 进程范围行为：  
  
-   应用程序托管在[!INCLUDE[iisver](../../../../../includes/iisver-md.md)]应用程序池。  
  
-   [!INCLUDE[iisver](../../../../../includes/iisver-md.md)] 在集成模式下运行。  
  
-   应用程序使用[!INCLUDE[net_v35SP1_short](../../../../../includes/net-v35sp1-short-md.md)]或更高版本。  
  
 在示例中的值是默认值。  
  
```xml  
<configuration>  
  <system.web>  
    <applicationPool   
        maxConcurrentRequestsPerCPU="5000"  
        maxConcurrentThreadsPerCPU="0"   
        requestQueueLimit="5000" />  
  </system.web>  
</configuration>  
```  
  
## <a name="element-information"></a>元素信息  
  
|||  
|-|-|  
|命名空间||  
|架构名称||  
|验证文件||  
|可以为空||  
  
## <a name="see-also"></a>请参阅
- [\<system.web> 元素（Web 设置）](../../../../../docs/framework/configure-apps/file-schema/web/system-web-element-web-settings.md)
