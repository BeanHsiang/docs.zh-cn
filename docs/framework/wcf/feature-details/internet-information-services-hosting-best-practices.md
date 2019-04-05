---
title: Internet 信息服务承载最佳实践
ms.date: 03/30/2017
ms.assetid: 0834768e-9665-46bf-86eb-d4b09ab91af5
ms.openlocfilehash: a4312a9affc1103f613f3f8ffd9a14696f9d4bcc
ms.sourcegitcommit: 0069cb3de8eed4e92b2195d29e5769a76111acdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2019
ms.locfileid: "56333412"
---
# <a name="internet-information-services-hosting-best-practices"></a>Internet 信息服务承载最佳实践
本主题概述了用于承载 Windows Communication Foundation (WCF) 服务的一些最佳做法。  
  
## <a name="implementing-wcf-services-as-dlls"></a>将 WCF 服务实现为 DLL  
 实现 WCF 服务作为 DLL 部署到 Web 应用程序的 \bin 目录允许你重复使用服务模型外的 Web 应用程序，例如，可能没有 Internet 信息服务 (IIS) 部署的测试环境中。  
  
## <a name="service-hosts-in-iis-hosted-applications"></a>承载于 IIS 中的应用程序中的服务主机  
 不要使用强制性自承载 API 创建用于侦听 IIS 承载环境本身不支持的网络传输的新服务主机（例如，承载 TCP 服务的 [!INCLUDE[iis601](../../../../includes/iis601-md.md)]，因为 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 本身不支持 TCP 通信）。 建议不要使用此方法。 强制创建的服务主机在 IIS 承载环境内是未知的。 很重要的一点是，在 IIS 确定承载应用程序池是否空闲时，它未说明强制创建的服务所进行的处理。 结果是具有这样强制创建的服务主机的应用程序具有主动处置 IIS 托管进程的 IIS 承载环境。  
  
## <a name="uris-and-iis-hosted-endpoints"></a>URI 和承载于 IIS 中的终结点  
 承载于 IIS 中的服务的终结点应该使用相对统一资源标识符 (URI) 而不是绝对地址进行配置。 这保证终结点地址在属于承载应用程序的 URI 地址集范围内，并确保像预期的那样发生基于消息的激活。  
  
## <a name="state-management-and-process-recycling"></a>状态管理和进程回收  
 为不在内存中维护本地状态的服务优化了 IIS 承载环境。 IIS 回收托管进程以响应各种外部和内部事件，导致仅存储在内存中的任何可变状态丢失。 寄宿在 IIS 中的服务应该在进程外存储其状态（例如，在数据库中），或者在出现应用程序回收事件时可以轻松重新创建的内存中缓存中存储其状态。  
  
> [!NOTE]
>  使 WCF 用于消息层可靠性和安全性的协议使用的易失性内存中状态。 WCF 可靠会话和安全会话可能由于应用程序回收而意外终止。 这些协议的使用 IIS 承载的应用程序应该依赖于以外的关联应用程序层状态 （例如，应用程序层结构或自定义关联标头） 或禁用的 WCF 提供的会话密钥IIS 进程回收的托管应用程序。  
  
## <a name="optimizing-performance-in-middle-tier-scenarios"></a>在中间层方案中优化性能  
 中获得最佳性能*中间层方案*— 即会调用响应传入消息中的其他服务的服务 — 一次实例化远程服务的 WCF 服务客户端并将其重复跨多个传入请求数。 实例化 WCF 服务客户端是相对于进行服务调用对预先存在的客户端实例，代价高昂的操作和中间层方案通过跨请求缓存远程客户端来产生明显的性能提升。 WCF 服务客户端是线程安全的因此不需要跨多个线程同步对客户端访问。  
  
 中间层方案还通过使用由 `svcutil /a` 选项生成的异步 API 来产生性能提升。 `/a`选项使[ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)生成`BeginXXX/EndXXX`对于每个服务操作，它允许对远程服务可能需要长时间运行调用，使其上的方法后台线程。  
  
## <a name="wcf-in-multi-homed-or-multi-named-scenarios"></a>多宿主或多名称方案中的 WCF  
 可以部署 WCF 服务内部的 IIS Web 场，其中的一组计算机共享公共外部名称 (如`http://www.contoso.com`)，但由不同的主机名单独寻址 (例如，`http://www.contoso.com`可能会将流量定向到两个不同的计算机名为`http://machine1.internal.contoso.com`和`http://machine2.internal.contoso.com`)。 此部署方案中完全支持由 WCF，但需要承载 WCF 服务在服务的元数据 （Web 服务描述语言） 中显示正确的 （外部） 主机名的 IIS 网站的特殊配置。  
  
 若要确保正确的主机名显示在 WCF 服务元数据生成、 托管 WCF 服务以使用显式主机名的 IIS 网站的默认标识配置。 例如，位于内的计算机`www.contoso.com`场应使用的 IIS 站点绑定 *:80:www.contoso.com 为 HTTP 和\*: 443:www.contoso.com 为支持 HTTPS。  
  
 可以使用 IIS Microsoft 管理控制台 (MMC) 管理单元配置 IIS 网站绑定。  
  
## <a name="application-pools-running-in-different-user-contexts-overwrite-assemblies-from-other-accounts-in-the-temporary-folder"></a>在不同用户上下文中运行的应用程序池覆盖来自临时文件夹中其他帐户的程序集  
 若要确保在不同用户上下文中运行的应用程序池无法覆盖来自临时 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 文件夹中其他帐户的程序集，请对不同的应用程序使用不同的标识和临时文件夹。 例如，如果具有两个虚拟应用程序 /Application1 和 / Application2，则可以创建两个应用程序池 A 和 B，它们具有不同的标识。 应用程序池 A 可以使用一个用户标识 (user1) 运行，而应用程序池 B 可以使用其他用户标识 (user2) 运行，并将 /Application1 配置为使用 A，将 /Application2 配置为使用 B。  
  
 在 Web.config 文件中，你可以配置临时文件夹使用\< system.web/compilation/@tempFolder>。 有关/application1，它可以"c:\tempForUser1"并且对于应用程序 2 可以是"c:\tempForUser2"。 将相应的写入权限授予两个标识的这些文件夹。  
  
 之后，user2 无法更改 /application2 的代码生成文件夹（在 c:\tempForUser1 下）。  
  
## <a name="enabling-asynchronous-processing"></a>启用异步处理  
 默认情况下以同步方式处理发送到承载在 IIS 6.0 及更早版本的 WCF 服务的消息。 ASP.NET 在它自己的线程 （ASP.NET 工作线程） 上调用 WCF 和 WCF 使用另一个线程来处理该请求。 WCF 在完成其处理之前会保持 ASP.NET 工作线程。 这将导致同步处理请求。 以异步方式处理请求能够实现更高版本的可伸缩性，因为它减少了处理的请求 – WCF 不保持 ASP.NET 线程处理请求时所需的线程数。 运行 IIS 6.0，因为没有方法来限制到服务器的传入请求的计算机不建议使用异步行为*拒绝服务*(DOS) 攻击。 从 IIS 7.0 开始，引入了并发请求限制：`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\2.0.50727.0]"MaxConcurrentRequestsPerCpu`。 借助这一新的限制，可安全地使用异步处理。  默认情况下，在 IIS 7.0 中会注册异步处理程序和模块。 如果关闭了此功能，可在应用程序的 Web.config 文件中手动启用对请求的异步处理。 所使用的设置取决于 `aspNetCompatibilityEnabled` 设置。 如果已将 `aspNetCompatibilityEnabled` 设置为 `false`，请按照下面的配置代码段所示配置 `System.ServiceModel.Activation.ServiceHttpModule`。  
  
```xml  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="false" />      
  </system.serviceModel>  
  <system.webServer>  
    <modules>  
      <remove name="ServiceModel"/>  
      <add name="ServiceModel"   
           preCondition="integratedMode,runtimeVersionv2.0"   
           type="System.ServiceModel.Activation.ServiceHttpModule, System.ServiceModel,Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
    </modules>  
    </system.webServer>  
```  
  
 如果已将 `aspNetCompatibilityEnabled` 设置为 `true`，请按照下面的配置代码段所示配置 `System.ServiceModel.Activation.ServiceHttpHandlerFactory`。  
  
```xml  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />      
  </system.serviceModel>  
  <system.webServer>  
    <handlers>  
          <clear/>  
          <add name="TestAsyncHttpHandler"   
               path="*.svc"   
               verb="*"   
               type="System.ServiceModel.Activation.ServiceHttpHandlerFactory, System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"           
               />  
    </handlers>      
  </system.webServer>  
```  
  
## <a name="see-also"></a>请参阅

- [服务承载示例](../samples/hosting.md)
- [Windows Server App Fabric 承载功能](https://go.microsoft.com/fwlink/?LinkId=201276)
