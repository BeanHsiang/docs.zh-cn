---
title: 了解 HTTP 身份验证
ms.date: 03/30/2017
ms.assetid: 9376309a-39e3-4819-b47b-a73982b57620
ms.openlocfilehash: 77fbed8cae070285925bcdc13c76fe28c3cb13cb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54525789"
---
# <a name="understanding-http-authentication"></a>了解 HTTP 身份验证
身份验证是判断客户端是否有资格访问资源的过程。 HTTP 协议支持将身份验证作为协商访问安全资源的一种方式。  
  
 来自客户端的初始请求通常是匿名请求，不包含任何身份验证信息。 HTTP 服务器应用程序可以拒绝匿名请求，而同时指示必须进行身份验证。 服务器应用程序发送 WWW-Authentication 头来指示受支持的身份验证方案。 本文档介绍了 HTTP 多个身份验证方案，并讨论其支持 Windows Communication Foundation (WCF) 中。  
  
## <a name="http-authentication-schemes"></a>HTTP 身份验证方案  
 服务器可以指定多个身份验证方案供客户端，可供选择。 下表介绍了一些常见的 Windows 应用程序中的身份验证方案。  
  
|身份验证方案|描述|  
|---------------------------|-----------------|  
|匿名|匿名请求不包含任何身份验证信息。 这就相当于授予所有人访问资源的权限。|  
|Basic|基本身份验证发送包含客户端的用户名和密码的 Base64 编码字符串。 Base64 不是一种加密形式，应将其视为相当于以明文形式发送用户名和密码。 如果需要保护资源，请务必考虑使用基本身份验证之外的身份验证方案。|  
|摘要|摘要式身份验证是质询-响应方案，用于替换基本身份验证。 服务器发送的名为的随机数据字符串*nonce*到客户端作为一项挑战。 客户端使用在其他信息中包括用户名、密码和 Nonce 的哈希进行响应。 该交换所引入的复杂程度和数据哈希增加了窃取和重用具有此身份验证方案的用户凭据的难度。<br /><br /> 摘要式身份验证需要使用 Windows 域帐户。 摘要式*领域*是 Windows 域名。 因此，不能使用不支持 Windows 域，例如 Windows XP Home Edition，摘要式身份验证的操作系统上运行的服务器。 反而言之，如果客户端运行在不支持 Windows 域的操作系统上，则必须在身份验证过程中显式指定域帐户。|  
|NTLM|NT LAN Manager (NTLM) 身份验证是质询-响应方案，是摘要式身份验证的一种更安全的变体。 NTLM 使用 Windows 凭据（而不是未编码的用户名和密码）来转换质询数据。 NTLM 身份验证需要客户端和服务器之间的多次交换。 服务器和所有参与代理都必须支持持久连接，才能成功完成身份验证。|  
|协商|协商身份验证自动在 Kerberos 协议和 NTLM 身份验证间选择，具体取决于可用性。 如果 Kerberos 协议可用，则使用 Kerberos 协议；否则，尝试使用 NTLM。 Kerberos 身份验证比 NTLM 具有更多优势。 Kerberos 身份验证既快于 NTLM，又允许使用相互身份验证和将凭据委托至远程计算机。|  
|Windows Live ID|基础 Windows HTTP 服务包括使用联合协议的身份验证。 但是，在 WCF 中的标准 HTTP 传输不支持使用联合身份验证方案，例如 Microsoft Windows Live id。 当前，可以通过使用消息安全来获得对此功能的支持。 有关详细信息，请参阅[联合身份验证和颁发令牌](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)。|  
  
## <a name="choosing-an-authentication-scheme"></a>选择身份验证方案  
 为 HTTP 服务器选择可能的身份验证方案时，需要考虑的事项包括以下几点：  
  
-   考虑是否需要保护资源。 使用 HTTP 身份验证需要传输更多数据，并可以限制与客户端的互操作性。 允许匿名访问不需要保护的资源。  
  
-   如果资源需要保护，则要考虑哪种身份验证方案可以提供所需的安全级别。 此处讨论的安全级别最低的标准身份验证方案是基本身份验证。 基本身份验证不保护用户的凭据。 安全级别最高的标准身份验证方案是协商身份验证，它将使用 Kerberos 协议。  
  
-   服务器不应（在 WWW-Authentication 头中）提供任何它不准备接受或不足以保护受保护资源安全的方案。 客户端可以在服务器提供的任何身份验证方案间自由选择。 某些客户端默认选择安全级别低的身份验证方案，或选择服务器列表中的第一个身份验证方案。  
  
## <a name="see-also"></a>请参阅
- [传输安全性概述](../../../../docs/framework/wcf/feature-details/transport-security-overview.md)
- [将模拟用于传输安全性](../../../../docs/framework/wcf/feature-details/using-impersonation-with-transport-security.md)
- [委托和模拟](../../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)
