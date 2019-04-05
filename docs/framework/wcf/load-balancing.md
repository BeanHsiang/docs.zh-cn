---
title: 负载平衡
ms.date: 03/30/2017
helpviewer_keywords:
- load balancing [WCF]
ms.assetid: 148e0168-c08d-4886-8769-776d0953b80f
ms.openlocfilehash: 2a0644ea17db2923f5729feda40f3b2bff364231
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54660744"
---
# <a name="load-balancing"></a>负载平衡
若要增加 Windows Communication Foundation (WCF) 应用程序的容量的一种方法是通过将它们部署到负载平衡服务器场中扩展它们。 WCF 应用程序可以使用标准负载均衡技术，包括如 Windows 网络负载平衡的软件负载均衡器，以及基于硬件的负载平衡设备达到负载平衡。  
  
 以下各节讨论负载平衡使用各种系统提供的绑定生成的 WCF 应用程序的注意事项。  
  
## <a name="load-balancing-with-the-basic-http-binding"></a>基本 HTTP 绑定的负载平衡  
 从负载平衡，使用进行通信的 WCF 应用程序的角度来看<xref:System.ServiceModel.BasicHttpBinding>与其他普通类型的 HTTP 网络流量 （静态 HTML 内容、 ASP.NET 页或 ASMX Web 服务） 没有什么不同。 使用此绑定的 WCF 通道本质上是无状态的并在通道关闭时终止它们的连接。 因此，<xref:System.ServiceModel.BasicHttpBinding> 可以很好地与现有的 HTTP 负载平衡技术一起使用。  
  
 默认情况下，<xref:System.ServiceModel.BasicHttpBinding> 会在消息中发送一个具有 `Keep-Alive` 值的连接 HTTP 标头，该标头可让客户端建立到支持这些客户端的服务的持续连接。 这种配置具有高的吞吐量，因为可以重新使用以前建立的连接向同一个服务器发送后续消息。 然而，重新使用连接可能导致客户端与负载平衡场中的特定服务器密切关联，从而降低循环负载平衡的效率。 如果不需要此行为，则可以使用 `Keep-Alive` 或用户定义的 <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A> 在使用 <xref:System.ServiceModel.Channels.CustomBinding> 属性的服务器上禁用 HTTP <xref:System.ServiceModel.Channels.Binding>。 下面的示例演示如何使用配置来执行该操作。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  
 <system.serviceModel>  
  <services>  
   <service   
     name="Microsoft.ServiceModel.Samples.CalculatorService"  
     behaviorConfiguration="CalculatorServiceBehavior">  
     <host>  
      <baseAddresses>  
       <add baseAddress="http://localhost:8000/servicemodelsamples/service"/>  
      </baseAddresses>  
     </host>  
    <!-- configure http endpoint, use base address provided by host  
         And the customBinding -->  
     <endpoint address=""  
           binding="customBinding"  
           bindingConfiguration="HttpBinding"   
           contract="Microsoft.ServiceModel.Samples.ICalculator" />  
   </service>  
  </services>  
  
  <bindings>  
    <customBinding>  
  
    <!-- Configure a CustomBinding that disables keepAliveEnabled-->  
      <binding name="HttpBinding" keepAliveEnabled="False"/>  
  
    </customBinding>  
  </bindings>  
 </system.serviceModel>  
</configuration>  
```  
  
 通过 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中引入的简化配置，可以使用下面的简化配置实现相同行为。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
 <system.serviceModel>  
    <protocolMapping>  
      <add scheme="http" binding="customBinding" />  
    </protocolMapping>  
    <bindings>  
      <customBinding>  
  
      <!-- Configure a CustomBinding that disables keepAliveEnabled-->  
        <binding keepAliveEnabled="False"/>  
  
      </customBinding>  
    </bindings>  
 </system.serviceModel>  
</configuration>  
```  
  
 有关默认终结点、绑定和行为的详细信息，请参阅[简化配置](../../../docs/framework/wcf/simplified-configuration.md)和 [WCF 服务的简化配置](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
## <a name="load-balancing-with-the-wshttp-binding-and-the-wsdualhttp-binding"></a>WSHttp 绑定和 WSDualHttp 绑定的负载平衡  
 如果对默认的绑定配置进行一些修改，则 <xref:System.ServiceModel.WSHttpBinding> 和 <xref:System.ServiceModel.WSDualHttpBinding> 都可以使用 HTTP 负载平衡技术来实现负载平衡。  
  
-   关闭安全上下文的建立：这可以通过将 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 上的 <xref:System.ServiceModel.WSHttpBinding> 属性设置为 `false` 来完成。 或者，如果安全会话是必需的则可以使用有状态安全会话中所述[安全会话](../../../docs/framework/wcf/feature-details/secure-sessions.md)主题。 有状态安全会话使服务保持无状态，因为安全会话的所有状态都随每个请求作为保护安全令牌的一部分进行传输。 请注意，若要启用有状态安全会话，必须使用 <xref:System.ServiceModel.Channels.CustomBinding> 或用户定义的 <xref:System.ServiceModel.Channels.Binding>，因为系统提供的 <xref:System.ServiceModel.WSHttpBinding> 和 <xref:System.ServiceModel.WSDualHttpBinding> 上并不会公开必需的配置设置。  
  
-   不要使用可靠会话。 默认情况下此功能处于关闭状态。  
  
## <a name="load-balancing-the-nettcp-binding"></a>使 Net.TCP 绑定实现负载平衡  
 可以使用 IP 层负载平衡技术实现 <xref:System.ServiceModel.NetTcpBinding> 的负载平衡。 不过，默认情况下，<xref:System.ServiceModel.NetTcpBinding> 会汇集 TCP 连接以减少连接延迟。 这是一种干扰负载平衡基本机制的优化。 用于优化 <xref:System.ServiceModel.NetTcpBinding> 的主配置值是租约超时，它是连接池设置的一部分。 连接池导致客户端连接与场内特定的服务器关联。 随着这些连接的生存期的增加（一个受租约超时设置控制的因素），场内不同服务器上的负载分布会变得不平衡。 结果使平均调用时间增加。 因此，在负载平衡方案中使用 <xref:System.ServiceModel.NetTcpBinding> 时，应考虑减少由绑定使用的默认租约超时。 虽然租约超时的最佳值取决于应用程序，但 30 秒的租约超时对于负载平衡方案不失为一个合理的始点。 有关通道租约超时和其他传输配额的详细信息，请参阅[传输配额](../../../docs/framework/wcf/feature-details/transport-quotas.md)。  
  
 若要在负载平衡方案中获得最佳性能，请考虑使用 <xref:System.ServiceModel.NetTcpSecurity>（<xref:System.ServiceModel.SecurityMode.Transport> 或 <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>）。  
  
## <a name="see-also"></a>请参阅
- [Internet Information Services 承载最佳做法](../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)
