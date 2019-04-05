---
title: 选择传输方式
ms.date: 03/30/2017
helpviewer_keywords:
- choosing transports [WCF]
ms.assetid: b169462b-f7b6-4cf4-9fca-d306909ee8bf
ms.openlocfilehash: 30585263b4c7c9e1f5e593dde15b19e37d5da6a0
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54494439"
---
# <a name="choosing-a-transport"></a>选择传输方式
本主题讨论 Windows Communication Foundation (WCF) 中包含的三个主要传输之间进行选择的条件：HTTP、 TCP 和命名的管道。 WCF 还包括消息队列 (也称为 MSMQ) 传输，但本文不讨论消息队列。  
  
 WCF 编程模型分离开来终结点操作 （如表示服务协定中） 连接两个终结点的传输机制。 这样，在您决定如何向网络公开服务时，就具有一定的灵活性。  
  
 在 WCF 中，指定如何通过使用终结点之间通过网络传输数据*绑定*，这由一系列组成*绑定元素*。 传输由传输绑定元素（绑定的一部分）表示。 绑定包括可选的协议绑定元素（如安全）、必需的消息编码器绑定元素和必需的传输绑定元素。 传输会将消息的序列化形式发送到另一个应用程序，或者从另一个应用程序接收消息的序列化形式。  
  
 如果必须连接到现有的客户端或服务器，则您可能不能选择使用特定传输。 但是，WCF 服务可进行访问通过多个终结点，每个都有一个不同的传输。 当单一传输方式不能涵盖您的服务目标受众时，请考虑通过多个终结点来公开服务。 这样，客户端应用程序就可以使用最适合的终结点。  
  
 在选择传输方式后，必须选择一个使用此传输方式的绑定。 可以选择一个系统提供的绑定 (请参阅[System-Provided Bindings](../../../../docs/framework/wcf/system-provided-bindings.md))，也可以生成自己的自定义绑定 (请参阅[自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md))。 还可以创建自己的绑定。 有关详细信息，请参阅[创建用户定义绑定](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)。  
  
## <a name="advantages-of-each-transport"></a>每种传输方式的优点  
 本节介绍在三种主要传输方式中选择其中之一的主要理由，包括一个用于进行选择的详细决策表。  
  
### <a name="when-to-use-http-transport"></a>适合使用 HTTP 传输的情况  
 HTTP 是客户端与服务器之间的一个请求/响应协议。 最常见的应用程序包括与 Web 服务器进行通信的 Web 浏览器客户端。 该客户端向服务器发送一个请求，服务器侦听客户端请求消息。 当服务器接收到一个请求时，会返回响应，其中包含请求的状态。 如果成功，将返回可选数据，如网页、错误消息或其他信息。 有关 HTTP 协议的详细信息，请参阅[HTTP-超文本传输协议](https://go.microsoft.com/fwlink/?LinkId=94858)。  
  
 HTTP 协议不是基于连接的 － 一旦发送了响应，就不会再维护任何状态。 要处理多页事务，应用程序必须持续保持任何必要的状态。  
  
 在 WCF 中，HTTP 传输绑定针对与旧式非 WCF 系统互操作性进行了优化。 如果所有通信方使用的 WCF，基于 TCP 或命名管道的绑定会更快。 有关详细信息，请参阅 <xref:System.ServiceModel.NetTcpBinding> 和 <xref:System.ServiceModel.NetNamedPipeBinding>。  
  
### <a name="when-to-use-the-tcp-transport"></a>适合使用 TCP 传输的情况  
 TCP 是一个基于连接、面向流的传递服务，具有端对端错误检测和更正功能。 *基于连接的*意味着，交换数据前建立主机之间的通信会话。 主机是 TCP/IP 网络上由逻辑 IP 地址标识的任意设备。  
  
 TCP 提供可靠的数据传递，并且易于使用。 具体地说，TCP 会通知发送方开始传递包，保证按发送时同样的顺序传递这些包，重新传送丢失的包，并确保数据包不重复。 请注意此可靠传递两个 TCP/IP 节点之间应用并不是与相同的功能*WS-ReliableMessaging*、 其应用终结点之间，无论多少个中间节点可能包括。  
  
 针对在有两个通信端使用 WCF 的方案进行优化的是 WCF TCP 传输。 此绑定是涉及不同计算机之间进行通信的方案中的最快 WCF 绑定。 消息交换使用 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> 来实现优化的消息传输。 TCP 提供双工通信，因此可以用于实现双工协定，即使客户端位于网络地址转换 (NAT) 的后端也没有关系。  
  
### <a name="when-to-use-the-named-pipe-transport"></a>适合使用命名管道传输的情况  
 命名管道是 Windows 操作系统内核中的一个对象，例如，进程可用于通信的一个共享内存区段。 命名管道具有一个名称，可用于单一计算机上的进程之间的单向或双工通信。  
  
 当通信需要一台计算机上的不同 WCF 应用程序之间，并且你想要防止任何来自另一台计算机的通信时，然后使用命名的管道传输。 另一个限制就是：从 Windows 远程桌面运行的进程可能只能用于同一 Windows 远程桌面会话，除非它们具有提升的特权。  
  
> [!WARNING]
>  当在 IIS 中承载的多个站点上一个弱通配符 URL 保留项中使用命名的管道传输，可能会发生以下错误：尝试侦听站点"2"时，激活服务 NetPipeActivator 协议 net.pipe 中出现错误，因此该协议为该站点临时禁用。 请参阅更多详细信息的异常消息。 URL:Weakwildcard: Net.pipe:\<计算机名称 > / 状态：ConflictingRegistration 异常：进程名称：SMSvcHost 进程 ID:1076\  
  
## <a name="decision-points-for-choosing-a-transport"></a>选择传输方式的决策点  
 下表列出了选择传输方式的常用决策点。 您应该考虑适合您的应用程序的其他所有属性和传输方式。 识别对您的应用程序非常重要的属性，识别对每个属性有益的传输方式，然后选择最适合您的属性集的传输方式。  
  
|特性|描述|适合的传输方式|  
|---------------|-----------------|------------------------|  
|诊断|使用诊断可自动检测传输的连接性问题。 所有传输方式均支持发回描述连接性的错误信息这一功能。 但是，WCF 不包括用于调查网络问题的诊断工具。|无|  
|宿主|所有 WCF 终结点必须都承载在应用程序。 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 和早期版本仅支持承载使用 HTTP 传输的应用程序。 在[!INCLUDE[wv](../../../../includes/wv-md.md)]，增加对承载所有 WCF 传输，包括 TCP 和命名管道支持。 有关详细信息，请参阅[在 Internet 信息服务中承载](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)并[在 Windows 进程激活服务中承载](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)。|HTTP|  
|检查|检查是在传送期间从消息中提取并处理信息的功能。 HTTP 协议会从数据中分离出路由和控制信息，使得可以更方便地生成用于检查和分析消息的工具。 易于检查的传输方式还可能要求网络设备中有较低的处理能力。 使用的安全级别会影响是否可以检查消息。|HTTP|  
|滞后时间|滞后时间是指完成消息交换所需的最少时间。 所有网络操作都具有或长或端的滞后时间，具体取决于选择的传输方式。 由于消息的强制相关性，利用固有消息交换模式为请求-答复的传输方式（如 HTTP）进行双工或单向通信会导致滞后时间增加。 这种情况下，请考虑使用固有消息交换模式为双工的传输方式，如 TCP。|TCP、命名<br /><br /> 管道|  
|连接距离|传输的连接距离反映了传输在与其他系统连接时的能力。 命名管道传输的连接距离很小；它只能连接到在同一计算上运行的服务。 TCP 和 HTTP 传输方式都有很好的连接距离，并可以渗透某些 NAT 和防火墙配置。 有关详细信息，请参阅[使用 Nat 和防火墙](../../../../docs/framework/wcf/feature-details/working-with-nats-and-firewalls.md)。|HTTP、TCP|  
|安全性|安全性是在传输期间通过提供保密性、完整性或身份验证来保护消息的能力。 保密性使消息免于检查，完整性防止消息被修改，身份验证保证消息发送方或接收方的身份。<br /><br /> WCF 支持在消息级别和传输级别的传输安全。 如果传输支持缓冲传输模式，则消息安全性与传输组合在一起。 对传输安全性的支持会根据您所选择的传输方式而有所不同。 HTTP、TCP 和命名管道传输利用合理的奇偶校验对传输安全提供支持。|全部|  
|吞吐量|吞吐量度量指定的时间内可以传送和处理的数据量。 与滞后时间类似，选择的传输方式会影响服务操作的吞吐量。 将传输的吞吐量最大化要求尽量减小传送内容的开销，并尽量缩短等待消息交换完成的时间。 TCP 和命名管道传输使消息正文增加的开销都不大，并支持减少消息答复等待时间的固有双工形状。|TCP、命名管道|  
|工具|工具表示对用于开发、诊断、承载和其他活动的协议的第三方应用程序支持。 开发工具和软件以便与 HTTP 协议协同工作意味着巨大的投资。|HTTP|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.BasicHttpBinding>
- <xref:System.ServiceModel.WSHttpBinding>
- <xref:System.ServiceModel.WSDualHttpBinding>
- <xref:System.ServiceModel.WSFederationHttpBinding>
- <xref:System.ServiceModel.Channels.HttpTransportBindingElement>
- <xref:System.ServiceModel.NetTcpBinding>
- <xref:System.ServiceModel.Channels.TcpTransportBindingElement>
- <xref:System.ServiceModel.NetNamedPipeBinding>
- <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>
- [绑定](../../../../docs/framework/wcf/feature-details/bindings.md)
- [系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)
- [创建用户定义的绑定](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md)
