---
title: 可靠消息传送协议版本 1.1
ms.date: 03/30/2017
ms.assetid: 0da47b82-f8eb-42da-8bfe-e56ce7ba6f59
ms.openlocfilehash: 6b8732e0b48797c219b53bb8bf70e1ba57e25c42
ms.sourcegitcommit: d9a0071d0fd490ae006c816f78a563b9946e269a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2019
ms.locfileid: "55073221"
---
# <a name="reliable-messaging-protocol-version-11"></a>可靠消息传送协议版本 1.1
本主题介绍 Windows Communication Foundation (WCF) 实现的详细信息用于 WS-ReliableMessaging 2007 年 2 月 （版本 1.1） 协议需要使用 HTTP 传输进行互操作。 WCF 遵循 WS-ReliableMessaging 规范的约束和澄清，本主题中所述。 请注意，从开始实现 WS-ReliableMessaging 版本 1.1 协议[!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)]。  
  
 WS-ReliableMessaging 2007 年 2 月在情况下，WCF 中实现协议<xref:System.ServiceModel.Channels.ReliableSessionBindingElement>。  
  
 为方便起见，本主题使用以下角色：  
  
-   发起方：启动 Ws-reliable Message 序列创建的客户端。  
  
-   响应方：接收发起方的请求的服务。  
  
 本文档使用下表中的前缀和命名空间。  
  
|前缀|命名空间|  
|-|-|  
|wsrm|http://docs.oasis-open.org/ws-rx/wsrm/200702|  
|netrm|http://schemas.microsoft.com/ws/2006/05/rm|  
|秒|http://www.w3.org/2003/05/soap-envelope|  
|wsa|http://schemas.xmlsoap.org/ws/2005/08/addressing|  
|wsse|http://docs.oasis-open.org/wss/2004/01/oasis-200401-wssecurity-secext-1.0.xsd|  
|wsrmp|http://docs.oasis-open.org/ws-rx/wsrmp/200702|  
|netrmp|http://schemas.microsoft.com/ws-rx/wsrmp/200702|  
|wsp|（WS-Policy 1.2 或 WS-Policy 1.5）|  
  
## <a name="messaging"></a>消息  
  
### <a name="sequence-creation"></a>序列创建  
 WCF 实现`CreateSequence`和`CreateSequenceResponse`消息以建立可靠消息序列。 适用以下约束：  
  
-   B1101:WCF 发起方将使用相同的终结点引用作为`CreateSequence`消息的`ReplyTo`，`AcksTo`和`Offer/Endpoint`。  
  
-   R1102:`AcksTo`，`ReplyTo`并`Offer/Endpoint`终结点引用中`CreateSequence`消息必须具有相同的字符串表示形式的地址值，以便它们与八进制形式匹配。  
  
    -   WCF 响应方验证的 URI 部分`AcksTo`，`ReplyTo`和`Endpoint`创建序列之前终结点引用是相同。  
  
-   R1103:`AcksTo`，`ReplyTo`并`Offer/Endpoint`终结点引用中`CreateSequence`消息应具有一组相同的引用参数。  
  
    -   WCF 并不强制但假定该引用的参数`AcksTo`，`ReplyTo`并`Offer/Endpoint`终结点引用上`CreateSequence`相同，并且使用从引用参数`ReplyTo`终结点引用确认和相反序列消息。  
  
-   B1104:WCF 发起方不会生成可选`Expires`或`Offer/Expires`中的元素`CreateSequence`消息。  
  
-   B1105:访问时`CreateSequence`消息时，WCF 响应方使用`Expires`中的值`CreateSequence`元素作为`Expires`中的值`CreateSequenceResponse`元素。 否则为 WCF 响应方读取并忽略`Expires`和`Offer/Expires`值。  
  
-   B1106:访问时`CreateSequenceResponse`消息时，WCF 发起方读取可选`Expires`值，但不使用它。  
  
-   B1107:WCF 发起方和响应方始终生成可选`IncompleteSequenceBehavior`中的元素`CreateSequence/Offer`和`CreateSequenceResponse`元素。  
  
-   B1108:仅使用 WCF`DiscardFollowingFirstGap`并`NoDiscard`中的值以`IncompleteSequenceBehavior`元素。  
  
    -   WS-ReliableMessaging 利用 `Offer` 机制建立构成会话的两个相反的相关序列。  
  
-   B1109:如果`CreateSequence`包含`Offer`元素中，一种方法 WCF 响应方拒绝所提供的序列通过`CreateSequenceResponse`而无需`Accept`元素。  
  
-   B1110:如果可靠消息响应方拒绝所提供的序列，WCF 发起方错误新建立的序列。  
  
-   B1111:如果`CreateSequence`不包含`Offer`元素，双向 WCF 响应方拒绝所提供的序列通过`CreateSequenceRefused`容错。  
  
-   R1112:使用建立的两个相反序列时`Offer`机制`[address]`的属性`CreateSequenceResponse/Accept/AcksTo`终结点引用必须与目标 URI 相匹配的`CreateSequence`字节的消息字节。  
  
-   R1113:使用建立的两个相反序列时`Offer`机制，从发起方流向响应方这两个序列上的所有消息必须都发送到相同的终结点引用。  
  
 WCF 使用 WS-ReliableMessaging 在发起方和响应方之间建立可靠会话。 WCF WS-ReliableMessaging 实现提供了可靠会话为单向、 请求-答复和完全双工消息传递模式。 `Offer` 和 `CreateSequence` 上的 WS-ReliableMessaging `CreateSequenceResponse` 机制允许您建立两个相关的相反序列，并提供适合于所有消息终结点的会话协议。 因为 WCF 提供了会话包括会话完整性的端到端保护的安全保障，是用于确保适用于同一参与方的消息到达同一目标。 这还允许应用程序消息上序列确认的“非法携带”。 因此，R1102、 R1112，以及 R1113 约束应用到 WCF。  
  
 `CreateSequence` 消息的一个示例。  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:MessageID>  
    <wsa:ReplyTo>  
        <wsa:Address>http://Business456.com/clientA</wsa:Address>   
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequence>  
      <wsrm:AcksTo>  
        <wsa:Address>http://Business456.com/clientA</wsa:Address>  
      </wsrm:AcksTo>  
      <wsrm:Offer>  
        <wsrm:Identifier>urn:uuid:066b4730-fc82-458a-a5c1-210be4fb4e4e</wsrm:Identifier>  
        <wsrm:Endpoint>  
          <wsa:Address>http://Business456.com/clientA</wsa:Address>  
        </wsrm:Endpoint>  
        <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>  
      </wsrm:Offer>  
    </wsrm:CreateSequence>  
  </s:Body>  
</s:Envelope>  
```  
  
 `CreateSequenceResponse` 消息的一个示例。  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CreateSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:949cca61-8813-42ff-ab33-18d9e3fa82fa</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CreateSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:IncompleteSequenceBehavior>DiscardFollowingFirstGap</wsrm:IncompleteSequenceBehavior>  
      <wsrm:Accept>  
        <wsrm:AcksTo>  
          <wsa:Address>http://BusinessABC.com/serviceA</wsa:Address>  
        </wsrm:AcksTo>  
      </wsrm:Accept>  
    </wsrm:CreateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="closing-a-sequence"></a>关闭序列  
 使用 WCF`CloseSequence`和`CloseSequenceResponse`的可靠消息源启动的关闭消息。 WCF 可靠消息目标不会启动关闭，WCF 可靠消息源不支持可靠消息目标启动的关闭。 适用以下约束：  
  
-   B1201:WCF 可靠消息源始终发送`CloseSequence`消息以关闭序列。  
  
-   B1202:可靠消息源等待确认的序列消息的全部发送之前`CloseSequence`消息。  
  
-   B1203:可靠消息源始终包括可选`LastMsgNumber`元素除非序列不包含消息。  
  
-   R1204:可靠消息目标不能通过发送启动关闭`CloseSequence`消息。  
  
-   B1205:在接收时`CloseSequence`消息时，WCF 可靠消息源认为序列不完整并发送错误。  
  
 `CloseSequence` 消息的一个示例。  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:MessageID>  
    <wsa:ReplyTo>  
      <wsa:Address>http://Business456.com/clientA</wsa:Address>  
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CloseSequence>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>  
    </wsrm:CloseSequence>  
  </s:Body>  
</s:Envelope>  
Example CloseSequenceResponse message:  
<s:Envelope>  
  <s:Header>  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>  
      <wsrm:Final></wsrm:Final>  
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/CloseSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:6ce1d4c3-e1c1-474f-a8c9-4210e37f7877</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">http://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:CloseSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
    </wsrm:CloseSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="sequence-termination"></a>序列终止  
 主要使用 WCF`TerminateSequence/TerminateSequenceResponse`握手后完成`CloseSequence/CloseSequenceResponse`握手。 WCF 可靠消息目标不启动终止和可靠消息源不支持可靠消息目标启动的终止。 适用以下约束：  
  
-   B1301:WCF 发起方仅发送`TerminateSequence`成功完成后的消息`CloseSequence/CloseSequenceResponse`握手。  
  
-   R1302:WCF 验证`LastMsgNumber`在所有元素都都一致`CloseSequence`和`TerminateSequence`对于给定的序列消息。 这意味着 `LastMsgNumber` 并不存在于所有 `CloseSequence` 和 `TerminateSequence` 消息上，或者它存在于所有 `CloseSequence` 和 `TerminateSequence` 消息上且完全相同。  
  
-   B1303:在接收时`TerminateSequence`消息后`CloseSequence/CloseSequenceResponse`握手，可靠消息目标的响应与`TerminateSequenceResponse`消息。 由于可靠消息源在发送 `TerminateSequence` 消息之前具有最终确认，因此可靠消息目标可毫无疑问地知道序列将结束，并立即回收资源。  
  
-   B1304:在接收时`TerminateSequence`消息之前`CloseSequence/CloseSequenceResponse`握手，WCF 可靠消息目标的响应与`TerminateSequenceResponse`消息。 如果可靠消息目标确定序列中没有不一致之处，则可靠消息目标将在回收资源之前等待应用程序目标指定的时间，以便客户端有机会接收最终确认。 否则，可靠消息目标立即回收资源，并通过引发 `Faulted` 事件向应用程序目标指出序列结束但存有疑问。  
  
 `TerminateSequence` 消息的一个示例。  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequence</wsa:Action>  
    <wsa:MessageID>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:MessageID>  
    <wsa:ReplyTo>  
      <wsa:Address>http://Business456.com/clientA</wsa:Address>  
    </wsa:ReplyTo>  
    <wsa:To s:mustUnderstand="1">http://BusinessABC.com/serviceA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:TerminateSequence>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:LastMsgNumber>30</wsrm:LastMsgNumber>  
      </wsrm:TerminateSequence>  
  </s:Body>  
</s:Envelope>  
Example TerminateSequenceResponse message:  
<s:Envelope>  
  <s:Header>  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Lower="1" Upper="30"></wsrm:AcknowledgementRange>  
      <wsrm:Final></wsrm:Final>  
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    <wsa:Action s:mustUnderstand="1">http://docs.oasis-open.org/ws-rx/wsrm/200702/TerminateSequenceResponse</wsa:Action>  
    <wsa:RelatesTo>urn:uuid:3597a398-4f3c-40f4-9335-8f1515572fdf</wsa:RelatesTo>  
    <wsa:To s:mustUnderstand="1">://Business456.com/clientA</wsa:To>  
  </s:Header>  
  <s:Body>  
    <wsrm:TerminateSequenceResponse>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
    </wsrm:TerminateSequenceResponse>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="sequences"></a>序列  
 以下是适用于序列的约束的列表：  
  
-   B1401:WCF 生成，并访问序列号不高于`xs:long`的最大包含值 9223372036854775807。  
  
 `Sequence` 标头的一个示例。  
  
```xml  
<wsrm:Sequence s:mustUnderstand="1">  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
  <wsrm:MessageNumber>1</wsrm:MessageNumber>  
</wsrm:Sequence>  
```  
  
### <a name="request-acknowledgement"></a>请求确认  
 WCF 使用`AckRequested`标头，因为保持活动状态的机制。  
  
 `AckRequested` 标头的一个示例。  
  
```xml  
<wsrm:AckRequested>  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
</wsrm:AckRequested>  
```  
  
### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement  
 WCF 将"非法携带"机制用于在 Ws-reliable Messaging 中提供的序列确认。 适用以下约束：  
  
-   R1601:使用建立的两个相反序列时`Offer`机制，`SequenceAcknowledgement`可能传输到目标接收方的任何应用程序消息中包括标头。 远程终结点必须能够访问非法携带的 `SequenceAcknowledgement` 标头。  
  
-   B1602:WCF 不会生成`SequenceAcknowledgement`标头包含`Nack`元素。 WCF 将验证每个`Nack`元素包含一个序列号，但否则忽略`Nack`元素和值。  
  
 `SequenceAcknowledgement` 标头的一个示例。  
  
```xml  
<wsrm:SequenceAcknowledgement>  
  <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
  <wsrm:AcknowledgementRange Lower="1" Upper="1"></wsrm:AcknowledgementRange>  
</wsrm:SequenceAcknowledgement>  
```  
  
### <a name="ws-reliablemessaging-faults"></a>WS-ReliableMessaging 错误  
 下面是适用于 WCF 实现的 WS-ReliableMessaging 错误的约束的列表。 适用以下约束：  
  
-   B1701:WCF 不会生成`MessageNumberRollover`故障。  
  
-   B1702:通过 SOAP 1.2，当服务终结点达到其连接限制并无法处理新连接时，WCF 生成嵌套`CreateSequenceRefused`错误子代码`netrm:ConnectionLimitReached`，如以下示例所示。  
  
```xml  
<s:Envelope>  
  <s:Header>  
    <wsa:Action>http://docs.oasis-open.org/ws-rx/wsrm/200702/fault</wsa:Action>  
  </s:Header>  
  <s:Body>  
    <s:Fault>  
      <s:Code>  
        <s:Value>s:Receiver</s:Value>  
        <s:Subcode>  
          <s:Value>wsrm:CreateSequenceRefused</s:Value>  
          <s:Subcode>  
            <s:Value>netrm:ConnectionLimitReached</s:Value>  
          </s:Subcode>  
        </s:Subcode>  
      </s:Code>  
      <s:Reason>  
        <s:Text xml:lang="en">Server 'http://BusinessABC.com/serviceA' is too busy to process this request. Try again later.</s:Text>  
      </s:Reason>  
    </s:Fault>  
  </s:Body>  
</s:Envelope>  
```  
  
### <a name="ws-addressing-faults"></a>WS-Addressing 错误  
 由于 WS-ReliableMessaging 使用 Ws-addressing，WCF WS-ReliableMessaging 实现可能会生成并传输 Ws-addressing 错误。 本部分介绍了 WCF 显式生成并传输在 WS-ReliableMessaging 层上的 Ws-addressing 错误：  
  
-   B1801:WCF 生成并传输`Message Addressing Header Required`发生故障时以下项之一为 true:  
  
    -   `CreateSequence``CloseSequence` 或 `TerminateSequence` 消息缺少 `MessageId` 头。  
  
    -   `CreateSequence``CloseSequence` 或 `TerminateSequence` 消息缺少 `ReplyTo` 头。  
  
    -   `CreateSequenceResponse`、`CloseSequenceResponse` 或 `TerminateSequenceResponse` 消息缺少 `RelatesTo` 头。  
  
-   B1802:WCF 生成并传输`Endpoint Unavailable`错误，以指示没有任何终结点侦听的可以处理基于对中的寻址标头的检查序列`CreateSequence`消息。  
  
## <a name="protocol-composition"></a>协议组合  
  
### <a name="composition-with-ws-addressing"></a>与 WS-Addressing 组合  
 WCF 支持两个版本的 Ws-addressing:的 Ws-addressing 2004/08 [WS-ADDR] 以及 W3C Ws-addressing 1.0 建议 [WS ADDR 核] 和 [WS ADDR SOAP]。  
  
 尽管 WS-ReliableMessaging 规范仅提及 WS-Addressing 2004/08，但是它不限制要使用的 WS-Addressing 版本。 下面是适用于 WCF 的约束的列表：  
  
-   R2101:可以与 Ws-reliable Messaging 使用 Ws-addressing 2004/08 和 Ws-addressing 1.0。  
  
-   R2102:必须在整个的给定的 WS-ReliableMessaging 序列或通过使用相关的反向序列对使用单一版本的 Ws-addressing`Offer`机制。  
  
### <a name="composition-with-soap"></a>与 SOAP 组合  
 WCF 支持 SOAP 1.1 和 SOAP 1.2 与 Ws-reliable Messaging 的使用。  
  
### <a name="composition-with-ws-security-and-ws-secureconversation"></a>与 WS-Security 和 WS-SecureConversation 组合  
 WCF 通过使用 Ws-secure Conversation 使用安全传输协议 (HTTPS)、 与 Ws-security 的组合和组合提供了对 WS-ReliableMessaging 序列的保护。 WS-ReliableMessaging 1.1 协议、WS-Security 1.1 和 WS-Secure Conversation 1.3 协议应该一起使用。 下面是适用于 WCF 的约束的列表：  
  
-   R2301:若要保护的各个消息的完整性 WS-ReliableMessaging 序列的完整性和保密性，WCF 需要必须使用 Ws-secure Conversation。  
  
-   R2302:AWS-必须在建立 WS-ReliableMessaging 序列之前建立安全对话会话中。  
  
-   R2303:如果 WS-ReliableMessaging 序列生存期超过了 Ws-secure Conversation 会话的生存期，`SecurityContextToken`建立通过使用 Ws-secure Conversation 必须续订通过使用相应的 Ws-secure Conversation 续订绑定。  
  
-   B2304:WS-ReliableMessaging 序列或一对相关的相反序列始终绑定到单个 Ws-secureconversation 会话。  
  
-   R2305:当使用 Ws-secure Conversation 撰写，WCF 响应方要求`CreateSequence`消息包含`wsse:SecurityTokenReference`元素和`wsrm:UsesSequenceSTR`标头。  
  
 `UsesSequenceSTR` 标头的一个示例。  
  
```xml  
<wsrm:UsesSequenceSTR></wsrm:UsesSequenceSTR>  
```  
  
### <a name="composition-with-ssltls-sessions"></a>与 SSL/TLS 会话组合  
 WCF 不支持与 SSL/TLS 会话组合：  
  
-   B2401:WCF 不会生成`wsrm:UsesSequenceSSL`标头。  
  
-   R2402:可靠消息发起方不能发送`CreateSequence`消息`wsrm:UsesSequenceSSL`向 WCF 响应程序的标头。  
  
### <a name="composition-with-ws-policy"></a>与 WS-Policy 组合  
 WCF 支持 Ws-policy 的两个版本：Ws-policy 1.2 和 Ws-policy 1.5。  
  
## <a name="ws-reliablemessaging-ws-policy-assertion"></a>WS-ReliableMessaging WS-Policy 断言  
 WCF 使用 WS-ReliableMessaging Ws-policy 断言`wsrm:RMAssertion`来描述终结点功能。 下面是适用于 WCF 的约束的列表：  
  
-   B3001:WCF 将附加`wsrmn:RMAssertion`Ws-policy 断言到`wsdl:binding`元素。 WCF 支持这两个附件`wsdl:binding`和`wsdl:port`元素。  
  
-   B3002:WCF 永远不会生成`wsp:Optional`标记。  
  
-   B3003:访问时`wsrmp:RMAssertion`Ws-policy 断言，WCF 将忽略`wsp:Optional`标记并将 WS-RM 策略视为强制。  
  
-   R3004:WCF 未构成与 SSL/TLS 会话，因为 WCF 不接受指定的策略`wsrmp:SequenceTransportSecurity`。  
  
-   B3005:WCF 始终生成`wsrmp:DeliveryAssurance`元素。  
  
-   B3006:WCF 始终指定`wsrmp:ExactlyOnce`传递保证。  
  
-   B3007:WCF 生成并读取 WS-ReliableMessaging 断言的以下属性和对它们的控制了 WCF`ReliableSessionBindingElement`:  
  
    -   `netrmp:InactivityTimeout`  
  
    -   `netrmp:AcknowledgementInterval`  
  
     `RMAssertion` 的一个示例。  
  
    ```xml  
    <wsrmp:RMAssertion>  
      <wsp:Policy>  
        <wsrmp:SequenceSTR/>  
        <wsrmp:DeliveryAssurance>  
          <wsp:Policy>  
            <wsrmp:ExactlyOnce/>  
            <wsrmp:InOrder/>  
          </wsp:Policy>  
        </wsrmp:DeliveryAssurance>  
      </wsp:Policy>  
      <netrmp:InactivityTimeout Milliseconds="600000"/>  
      <netrmp:AcknowledgementInterval Milliseconds="200"/>  
    </wsrmp:RMAssertion>  
    ```  
  
## <a name="flow-control-ws-reliablemessaging-extension"></a>流控制 WS-ReliableMessaging 扩展  
 WCF 使用 WS-ReliableMessaging 扩展性提供对序列消息流的可选更紧密控制。  
  
 设置启用流控制<xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled?displayProperty=nameWithType>属性设置为`true`。 下面是适用于 WCF 的约束的列表：  
  
-   B4001:当启用可靠消息流控制时，WCF 生成`netrm:BufferRemaining`元素的元素扩展性中`SequenceAcknowledgement`标头，如下面的示例中所示。  
  
    ```xml  
    <wsrm:SequenceAcknowledgement>  
      <wsrm:Identifier>urn:uuid:656652b8-9af2-4e94-9d07-2dc21c05ed27</wsrm:Identifier>  
      <wsrm:AcknowledgementRange Upper="1" Lower="1"/>             
      <netrm:BufferRemaining>8</netrm:BufferRemaining>  
    </wsrm:SequenceAcknowledgement>  
    ```  
  
-   B4002:即使启用可靠消息流控制时，WCF 不需要`netrm:BufferRemaining`中的元素`SequenceAcknowledgement`标头。  
  
-   B4003:WCF 可靠消息目标使用`netrm:BufferRemaining`以指示如何许多新的消息可以缓冲。  
  
-   启用 B4004:When 可靠消息流控制时，WCF 可靠消息源使用的值`netrm:BufferRemaining`遏制消息传输。  
  
-   B4005:WCF 将生成`netrm:BufferRemaining`整数值介于 0 和 4096 （含)，并读取介于 0 的整数值和`xs:int`的`maxInclusive`值 214748364 （含)。  
  
## <a name="message-exchange-patterns"></a>消息交换模式  
 WS-ReliableMessaging 用于不同消息交换模式时，本部分将介绍 WCF 的行为。 对于每个消息交换模式，可以考虑下面的两个部署方案：  
  
-   不可寻址的发起方：发起方位于防火墙;响应方可以将消息传递到发起方仅在 HTTP 响应上。  
  
-   可寻址的发起方：发起方和响应方都可以发送 HTTP 请求;换而言之，可以建立两个反向 HTTP 连接。  
  
### <a name="one-way-non-addressable-initiator"></a>单向、不可寻址的发起方  
  
#### <a name="binding"></a>绑定  
 WCF 提供了通过一个 HTTP 通道使用一个序列的单向消息交换模式。 WCF 使用 HTTP 请求传输所有消息从发起方到响应方，并使用 HTTP 响应传输到发起方从响应方的所有消息。  
  
#### <a name="createsequence-exchange"></a>CreateSequence 交换  
 WCF 发起方传输`CreateSequence`没有消息`Offer`HTTP 请求上的元素，并期望`CreateSequenceResponse`HTTP 响应上的消息。 WCF 响应方创建一个序列并传输`CreateSequenceResponse`没有消息`Accept`HTTP 响应上的元素。  
  
#### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement  
 WCF 发起方处理除之外的所有消息的确认答复`CreateSequence`消息和错误消息。 WCF 响应方始终将对所有序列的 HTTP 响应上的独立确认传输和`AckRequested`消息。  
  
#### <a name="closesequence-exchange"></a>CloseSequence 交换  
 WCF 发起方传输`CloseSequence`上的 HTTP 请求消息，并需要`CreateSequenceResponse`HTTP 响应上的消息。 WCF 响应方传输`CloseSequenceResponse`HTTP 响应上的消息。  
  
#### <a name="terminatesequence-exchange"></a>TerminateSequence 交换  
 WCF 发起方传输`TerminateSequence`上的 HTTP 请求消息，并需要`TerminateSequenceResponse`HTTP 响应上的消息。 WCF 响应方传输`TerminateSequenceResponse`HTTP 响应上的消息。  
  
### <a name="one-way-addressable-initiator"></a>单向、可寻址的发起方  
  
#### <a name="binding"></a>绑定  
 WCF 提供了通过一个使用一个序列的单向消息交换模式入站和一个出站 HTTP 通道。 WCF 使用 HTTP 请求传输所有消息。 所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### <a name="createsequence-exchange"></a>CreateSequence 交换  
 WCF 发起方传输`CreateSequence`没有消息`Offer`HTTP 请求上的元素。 WCF 响应方创建一个序列并传输`CreateSequenceResponse`没有消息`Accept`HTTP 请求上的元素。  
  
### <a name="duplex-addressable-initiator"></a>双工、可寻址的发起方  
  
#### <a name="binding"></a>绑定  
 WCF 提供了完全异步的双向消息交换模式，使用两个序列通过一个入站和一个出站 HTTP 通道。 此消息交换模式可以与 `Request/Reply`、`Addressable` 发起方消息交换模式以有限方式混合使用。 WCF 使用 HTTP 请求传输所有消息。 所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### <a name="createsequence-exchange"></a>CreateSequence 交换  
 WCF 发起方传输`CreateSequence`消息`Offer`HTTP 请求上的元素。 WCF 响应方确保`CreateSequence`已`Offer`元素，然后创建一个序列并传输`CreateSequenceResponse`消息`Accept`元素。  
  
#### <a name="sequence-lifetime"></a>序列生存期  
 WCF 将两个序列视为一个全双工会话。  
  
 在生成的错误，使一个序列，WCF 需要要故障这两个序列的远程终结点。 在读取的错误，使一个序列，WCF 会使故障这两个序列。  
  
 WCF 可以关闭其出站序列并继续处理其入站序列上的消息。 相反，WCF 可以处理入站序列的关闭和继续其出站序列上发送消息。  
  
### <a name="request-reply-and-one-way-non-addressable-initiator"></a>请求-答复和单向、不可寻址的发起方  
  
#### <a name="binding"></a>绑定  
 WCF 提供了单向和请求-答复消息交换模式使用两个序列通过一个 HTTP 通道。 WCF 使用 HTTP 请求传输所有消息从发起方到响应方，并使用 HTTP 响应传输到发起方从响应方的所有消息。  
  
#### <a name="createsequence-exchange"></a>CreateSequence 交换  
 WCF 发起方传输`CreateSequence`消息`Offer`HTTP 请求上的元素，并期望`CreateSequenceResponse`HTTP 响应上的消息。 WCF 响应方创建一个序列并传输`CreateSequenceResponse`消息`Accept`HTTP 响应上的元素。  
  
#### <a name="one-way-message"></a>单向消息  
 若要成功完成单向消息交换，WCF 发起方传输请求序列消息在 HTTP 请求和接收独立`SequenceAcknowledgement`HTTP 响应上的消息。 `SequenceAcknowledgement` 必须确认已传输的消息。  
  
 确认、 错误或正文为空且 HTTP 202 状态代码的响应与请求的 WCF 响应可能会答复。  
  
#### <a name="two-way-messages"></a>双向消息  
 若要成功地完成双向消息交换协议，WCF 发起方传输请求序列消息在 HTTP 请求和接收答复序列消息在 HTTP 响应上。 响应必须包含一个确认已传输的请求序列消息的 `SequenceAcknowledgement`。  
  
 使用应用程序答复、 错误或正文为空且 HTTP 202 状态代码的响应请求的 WCF 响应可能会答复。  
  
 由于存在单向消息和应用程序答复的计时，因此请求序列消息的序列号与响应消息的序列号不相关联。  
  
#### <a name="retrying-replies"></a>重试答复  
 WCF 依赖于双向消息交换协议关联的 HTTP 请求-答复相关。 因此，WCF 发起方不会停止重试请求序列消息，确认请求序列消息时，但而不是在 HTTP 响应携带`SequenceAcknowledgement`，应用程序答复或错误。 WCF 响应方重试次数依赖向其答复相关联的请求的 HTTP 响应。  
  
#### <a name="closesequence-exchange"></a>CloseSequence 交换  
 收到后的所有答复序列消息和所有单向请求序列消息的确认，WCF 发起方传输`CloseSequence`HTTP 请求上请求序列消息，并需要`CloseSequenceResponse`HTTP 响应上。  
  
 关闭请求序列将隐式关闭答复序列。 这意味着 WCF 发起方包括答复序列的最终`SequenceAcknowledgement`上`CloseSequence`消息和答复序列没有`CloseSequence`exchange。  
  
 WCF 响应方确保所有答复确认并传输`CloseSequenceResponse`HTTP 响应上的消息。  
  
#### <a name="terminatesequence-exchange"></a>TerminateSequence 交换  
 收到后`CloseSequenceResponse`消息时，WCF 发起方传输`TerminateSequence`上的 HTTP 请求的请求序列消息，并需要`TerminateSequenceResponse`HTTP 响应上。  
  
 与 `CloseSequence` 交换一样，终止请求序列将隐式终止答复序列。 这意味着 WCF 发起方包括答复序列的最终`SequenceAcknowledgement`上`TerminateSequence`消息和答复序列没有`TerminateSequence`exchange。  
  
 WCF 响应方传输`TerminateSequenceResponse`HTTP 响应上的消息。  
  
### <a name="requestreply-addressable-initiator"></a>请求/答复、可寻址的发起方  
  
#### <a name="binding"></a>绑定  
 WCF 提供了使用两个的请求-答复消息交换模式序列通过一个入站和一个出站 HTTP 通道。 此消息交换模式可以与 `Duplex, Addressable` 发起方消息交换模式以有限方式混合使用。 WCF 使用 HTTP 请求传输所有消息。 所有 HTTP 响应的正文都为空，并且具有 HTTP 202 状态代码。  
  
#### <a name="createsequence-exchange"></a>CreateSequence 交换  
 WCF 发起方传输`CreateSequence`消息`Offer`HTTP 请求上的元素。 WCF 响应方确保`CreateSequence`已`Offer`元素，然后创建一个序列并传输`CreateSequenceResponse`消息`Accept`元素。  
  
#### <a name="requestreply-correlation"></a>请求/答复关联  
 以下内容适用于所有关联的请求和答复：  
  
-   WCF 可确保所有应用程序请求消息都具有`ReplyTo`终结点引用和一个`MessageId`。  
  
-   WCF 为每个应用程序请求消息的应用的本地终结点引用`ReplyTo`。 本地终结点引用是发起方的 `CreateSequence` 消息的 `ReplyTo` 和响应方的 `CreateSequence` 消息的 `To`。  
  
-   WCF 可确保该传入请求消息具有`MessageId`和一个`ReplyTo`。  
  
-   WCF 可确保`ReplyTo`前面定义的所有应用程序请求消息的终结点引用的 URI 匹配的本地终结点引用。  
  
-   WCF 可确保所有答复都具有正确`RelatesTo`并`To`标头遵循`wsa`请求/答复关联规则。
