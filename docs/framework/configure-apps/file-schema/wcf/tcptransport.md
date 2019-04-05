---
title: <tcpTransport>
ms.date: 03/30/2017
ms.assetid: 8fcd18c1-9958-42e7-b442-7903f7bdb563
ms.openlocfilehash: 683c28d626f32971e7e1fa5f50343b3e7ea125be
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57845955"
---
# <a name="tcptransport"></a>\<tcpTransport>
定义通道用于传输自定义绑定消息的 TCP 传输。  
  
 \<system.serviceModel>  
\<bindings>  
\<customBinding>  
\<binding>  
\<tcpTransport>  
  
## <a name="syntax"></a>语法  
  
```xml  
<tcpTransport channelInitializationTimeout="TimeSpan"
              connectionBufferSize="Integer"
              hostNameComparisonMode="StrongWildcard/Exact/WeakWildcard"
              listenBacklog="Integer"
              manualAddressing="Boolean"
              maxBufferPoolSize="Integer"
              maxBufferSize="Integer"
              maxOutputDelay="TimeSpan"
              maxPendingAccepts="Integer"
              maxPendingConnections="Integer"
              maxReceivedMessageSize="Integer"
              portSharingEnabled="Boolean"
              teredoEnabled="Boolean"
              transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse" >
  <connectionPoolSettings groupName="String"
                          idleTimeout="TimeSpan"
                          leaseTimeout="TimeSpan"
                          maxOutboundConnectionsPerEndpopint="Integer" />
</tcpTransport>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|channelInitializationTimeout|获取或设置对要接受的通道进行初始化的时间限制。  通道在断开连接前可处于初始化状态的最长时间（秒）。 此配额包括 TCP 连接可能需要进行身份验证使用.NET Message Framing 协议本身的时间。 客户端需要发送一些初始数据，然后服务器才有足够的信息来执行身份验证。 默认值为 30 秒。|  
|connectionBufferSize|获取或设置用于从客户端或服务传输网络上的序列化消息块的缓冲区大小。|  
|hostNameComparisonMode|获取或设置一个值，该值指示在对 URI 进行匹配时，是否使用主机名来访问服务。|  
|listenBacklog|可为 Web 服务挂起的最大排队连接请求数。 `connectionLeaseTimeout` 属性限制客户端在引发连接异常之前将等待连接的持续时间。 这是一个套接字级别属性，控制可能为 Web 服务挂起的最大排队连接请求数。 ListenBacklog 太低时，WCF 将停止接受请求并因此删除新连接，直到服务器确认一些现有队列连接。 默认值为 16 * 处理器数。|  
|manualAddressing|获取或设置一个值，该值指示是否要求对消息进行手动寻址。|  
|maxBufferPoolSize|获取或设置传输使用的任何缓冲池的最大大小。|  
|maxBufferSize|获取或设置要使用的缓冲区的最大大小。 对于经过流处理的消息，该值最少应为以缓冲模式读取的消息头的最大可能大小。|  
|maxOutputDelay|获取或设置消息块或完整消息在发出之前可以在内存中保持缓冲的最大时间间隔。|  
|maxPendingAccepts|获取或设置可用于处理服务上的传入连接的最大挂起异步接受操作数。|  
|maxPendingConnections|获取或设置在服务上等待调度的最大连接数。|  
|maxReceivedMessageSize|获取和设置允许接收的最大消息大小。|  
|portSharingEnabled|一个布尔值，指定是否为此连接启用 TCP 端口共享。 如果此值为 `false`，则每个绑定都将使用自己的独占端口。 默认值为 `false`。<br /><br /> 此设置只与服务相关。 客户端并不会受影响。<br /><br /> 使用此设置要求通过将 Windows Communication Foundation (WCF) TCP 端口共享服务的“启动类型”设置为“手动”或“自动”来启用该服务。|  
|teredoEnabled|一个布尔值，指定是否启用 Teredo（一种用于对防火墙后的客户端进行寻址的技术）。 默认值为 `false`。<br /><br /> 此属性为基础 TCP 套接字启用 Teredo。 有关详细信息，请参阅[Teredo 概述](https://go.microsoft.com/fwlink/?LinkId=95339)。<br /><br /> 此属性仅适用于 [!INCLUDE[wxpsp2](../../../../../includes/wxpsp2-md.md)] 和 [!INCLUDE[ws2003](../../../../../includes/ws2003-md.md)]。 [!INCLUDE[wv](../../../../../includes/wv-md.md)] 具有用于 Teredo 的计算机范围的配置选项，因此运行 Vista 时将忽略此属性。 Teredo 要求客户端和服务计算机都安装 Microsoft IPv6 堆栈，并进行正确的配置以便使用 Teredo。 有关配置 Teredo 的详细信息，请参阅[Teredo 概述](https://go.microsoft.com/fwlink/?LinkId=95339)。 有关详细信息，请参阅[Windows Server 2003 技术中心](https://go.microsoft.com/fwlink/?LinkId=49888)。|  
|transferMode|获取或设置一个值，该值指示通过面向连接的传输对消息进行缓冲还是流处理。|  
|connectionPoolSettings|指定命名管道绑定的其他连接池设置。|  
  
### <a name="child-elements"></a>子元素  
 无  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<binding>](../../../../../docs/framework/misc/binding.md)|定义自定义绑定的所有绑定功能。|  
  
## <a name="remarks"></a>备注  
 此传输使用“net.tcp://hostname:port/path”形式的 URI。 其他 URI 组件是可选的。  
  
 `tcpTransport` 元素是创建实现 TCP 传输协议的自定义绑定的起始点。 针对 WCF 到 WCF 的通信对此传输进行了优化。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Configuration.TcpTransportElement>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>
- <xref:System.ServiceModel.Channels.TransportBindingElement>
- <xref:System.ServiceModel.Channels.CustomBinding>
- [传输](../../../../../docs/framework/wcf/feature-details/transports.md)
- [选择传输](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)
- [绑定](../../../../../docs/framework/wcf/bindings.md)
- [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)
- [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)
- [\<customBinding>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)
