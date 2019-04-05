---
title: 可靠会话概述
ms.date: 03/30/2017
ms.assetid: a7fc4146-ee2c-444c-82d4-ef6faffccc2d
ms.openlocfilehash: 6dd90ef800daf236d77c419d48c0857ac2d78aa2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54548019"
---
# <a name="reliable-sessions-overview"></a>可靠会话概述

Windows Communication Foundation (WCF) SOAP 可靠消息传递提供 SOAP 终结点之间的端到端消息传输可靠性。 此消息传递通过克服传输失败和 SOAP 消息级别失败，可在不可靠的网络上实现传输可靠性。 具体而言，它为跨 SOAP 或传输中介发送的消息提供了一种基于会话的、单一的和（可选）有序的传送。 为具有可选排序的消息的会话中对消息进行分组提供基于会话的交付。

本主题描述可靠会话、 如何和何时使用它们，以及如何保护它们。

## <a name="wcf-reliable-sessions"></a>WCF 可靠会话

WCF 可靠会话是 SOAP 可靠消息传递定义的 WS-ReliableMessaging 协议的实现。

WCF SOAP 可靠消息传递提供两个终结点，而不考虑的数量或类型的单独的消息传递终结点的中介之间的端到端可靠会话。 这包括不使用 SOAP （例如，HTTP 代理） 的任何传输中介或使用 SOAP （例如，基于 SOAP 的路由器或网桥） 所需的消息传递终结点之间的中介。 支持可靠会话通道*交互式*通信，以便同时运行这类通道所连接的服务和交换和处理消息的低延迟，也就是说，条件下在相对较短按时间间隔。 这种耦合意味着这些组件将同时或同时失败，因此它们之间没有提供隔离。

可靠会话可以屏蔽两种失败情况：

- SOAP 消息级失败，其中包括消息丢失或重复的情况以及消息到达的顺序与消息发送的顺序不同的情况。

- 传输失败。

可靠会话实现 WS-ReliableMessaging 协议和内存中传输窗口以屏蔽 SOAP 消息级失败，并在传输失败的情况下重新建立连接。

可靠会话为 SOAP 消息提供 TCP 为 IP 数据包提供的内容。 TCP 套接字连接在节点之间提供单个的 IP 数据包有序传输。 可靠通道提供相同类型的可靠传输，但在以下方面与 TCP 套接字可靠性不同：

- 可靠性位于 SOAP 消息级别，而不是针对一个任意大小的字节数据包。

- 可靠性是传输模式无关，而不仅仅用于通过 TCP 的传输。

- 可靠性不绑定到特定的传输会话 （例如，TCP 连接提供了会话），可以使用多个传输会话同时或按顺序在可靠会话的生存期内。

- 可靠会话是发送方和接收方的 SOAP 终结点之间的会话，与二者之间的连接所需的传输连接的数目无关。 简单地说，TCP 可靠性结束传输连接结束的位置，而可靠会话提供端到端可靠性。

## <a name="reliable-sessions-and-bindings"></a>可靠会话和绑定

前面曾提到，可靠会话是非传输特定。 此外，您可以通过许多消息交换模式，如请求-答复或双工模式建立可靠会话。 WCF 可靠会话作为一组绑定的属性。

使用可靠会话上使用的终结点：

- 基于 HTTP 的传输协议标准绑定：

  - `WsHttpBinding` 并公开请求-答复或单向协定。

  - 在通过请求-答复或简单的单向服务协定使用可靠会话。

  - `WsDualHttpBinding` 并公开双工、请求-答复或单向协定。

  - `WsFederationHttpBinding` 并公开请求-答复或单向协定。

- 基于 TCP 的传输协议标准绑定：

  - `NetTcpBinding` 并公开双工、请求答复或单向协定。

通过创建自定义绑定，如 HTTPS 上的任何其他绑定使用可靠会话 (有关问题的详细信息，请参阅<a href="#reliable-sessions-and-security">可靠会话和安全</a>) 或命名的管道绑定。

您可以堆栈上不同的基础通道类型的可靠会话，并生成可靠会话通道形状将会不同。 在客户端和服务器，支持可靠会话通道的类型取决于使用的基础通道的类型。 下表列出了在客户端上作为基础通道的一项功能支持的会话通道的类型。

| 支持可靠会话通道类型&#8224; | `IRequestChannel` | `IRequestSessionChannel` | `IDuplexChannel` | `IDuplexSessionChannel` |
| ----------------------------------------------- | :---------------: | :----------------------: | :--------------: | :---------------------: |
| `IOutputSessionChannel`                         | 是               | 是                      | 是              | 是                     |
| `IRequestSessionChannel`                        | 是               | 是                      | No               | 否                      |
| `IDuplexSessionChannel`                         | 否                | 否                       | 是              | 是                     |

&#8224;支持的通道类型是可用于泛型值`TChannel`参数值传递到<xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelFactory%60%601%28System.ServiceModel.Channels.BindingContext%29>方法。

下表列出了在服务器上作为基础通道的一项功能支持的会话通道的类型。

| 支持可靠会话通道类型&#8225; | `IReplyChannel` | `IReplySessionChannel` | `IDuplexChannel` | `IDuplexSessionChannel` |
| ----------------------------------------------- | :-------------: | :--------------------: | :--------------: | :---------------------: |
| `IInputSessionChannel`                          | 是             | 是                    | 是              | 是                     |
| `IReplySessionChannel`                          | 是             | 是                    | No               | 否                      |
| `IDuplexSessionChannel`                         | 否              | 否                     | 是              | 是                     |

&#8225;支持的通道类型是可用于泛型值`TChannel`参数值传递到<xref:System.ServiceModel.Channels.ReliableSessionBindingElement.BuildChannelListener%60%601%28System.ServiceModel.Channels.BindingContext%29>方法。

## <a name="reliable-sessions-and-security"></a>可靠会话和安全

保护可靠会话是一定要确保通信方 （服务和客户端） 进行身份验证和会话中交换的消息不篡改。 此外，务必确保每个单独的可靠会话的完整性。 绑定到具有表示并由安全会话通道的安全上下文被保护可靠会话。 安全通道提供安全会话。 然后，使用在会话建立的过程中交换的安全令牌保护可靠会话中的消息。

通过 TCP-S 进行可靠会话时，TCP 会话将关联到可靠会话。 因此，传输安全确保安全也绑定到可靠会话。 在此情况下，将关闭重新建立连接的操作。

唯一的例外是在使用 HTTPS 时。 安全套接字层 (SSL) 会话未绑定到可靠会话。 这会威胁，因为共享安全上下文 （SSL 会话） 的会话将从每个其他; 不受保护这可能会也可能不是真正的威胁，具体取决于应用程序。

## <a name="using-reliable-sessions"></a>使用可靠会话

若要使用 WCF 可靠会话，创建支持可靠会话的绑定的终结点。 使用 WCF 提供了可靠会话的系统提供绑定之一启用或创建您自己的自定义绑定的就是如此。

默认情况下支持并启用可靠会话的系统定义的绑定包括：

- <xref:System.ServiceModel.WSDualHttpBinding>

系统提供绑定支持可靠会话作为一个选项，但不要启用默认情况下包括：

- <xref:System.ServiceModel.WSHttpBinding>

- <xref:System.ServiceModel.WSFederationHttpBinding>

- <xref:System.ServiceModel.NetTcpBinding>

有关如何创建自定义绑定的示例，请参阅[如何：使用 HTTPS 创建自定义可靠会话绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md)。

有关支持可靠会话的 WCF 绑定的讨论，请参阅[System-Provided Bindings](../../../../docs/framework/wcf/system-provided-bindings.md)。

## <a name="when-to-use-reliable-sessions"></a>何时使用可靠会话

请务必了解何时在应用程序中使用可靠会话。 WCF 支持同时处于活动状态且处于活动状态的终结点之间的可靠会话。 如果应用程序需要一个终结点将不可用的持续时间的时间，然后使用队列来实现可靠性。

如果方案需要通过 TCP 连接的两个终结点，TCP 可能足以提供可靠的消息交换。 尽管没有必要使用可靠会话，因为 TCP 可确保数据包到达顺序和仅一次。

如果你的方案具有任何以下特征，然后您必须认真考虑使用可靠会话。

- SOAP 中介，例如 SOAP 路由器

- 代理中介或传输桥

- 间歇性连接

- 通过 HTTP 会话

## <a name="see-also"></a>请参阅

- [使用绑定配置服务和客户端](../../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [WS 可靠会话](../../../../docs/framework/wcf/samples/ws-reliable-session.md)
