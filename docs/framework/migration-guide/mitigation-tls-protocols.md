---
title: 缓解：TLS 协议
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 33f97d13-3022-43da-8b18-cdb5c88df9c2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: abfbea052072f0b90c9d018b520b67878d235701
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54506805"
---
# <a name="mitigation-tls-protocols"></a>缓解：TLS 协议
从 .NET Framework 4.6 开始，允许 <xref:System.Net.ServicePointManager?displayProperty=nameWithType> 和 <xref:System.Net.Security.SslStream?displayProperty=nameWithType> 类使用以下三种协议之一：Tls1.0、Tls1.1 或 Tls1.2。 不支持 SSL3.0 协议和 RC4 密码。  
  
## <a name="impact"></a>影响  
 此更改会影响：  
  
-   使用 SSL 与 HTTPS 服务器或与使用以下任何类型的套接字对话的任何应用：<xref:System.Net.Http.HttpClient>、<xref:System.Net.HttpWebRequest>、<xref:System.Net.FtpWebRequest>、<xref:System.Net.Mail.SmtpClient> 和 <xref:System.Net.Security.SslStream>。  
  
-   不能升级以支持 Tls1.0、Tls1.1 或 Tls 1.2 的任意服务器端应用。  
  
## <a name="mitigation"></a>缓解  
 建议的缓解操作是将服务器端应用升级到 Tls1.0、Tls1.1 或 Tls 1.2。 如果这不可行或者如果客户端应用被中断，则可以使用 <xref:System.AppContext> 类并采用如两种方式中的一种来选择退出此功能：  
  
-   以编程方式使用如下代码段：  
  
     [!code-csharp[AppCompat.SSLProtocols#1](../../../samples/snippets/csharp/VS_Snippets_CLR/appcompat.sslprotocols/cs/program.cs#1)]
     [!code-vb[AppCompat.SSLProtocols#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/appcompat.sslprotocols/vb/module1.vb#1)]  
  
     由于 <xref:System.Net.ServicePointManager> 对象仅初始化一次，因此定义这些兼容性设置必须是应用程序执行的第一件事。  
  
-   在 app.config 文件的 [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) 部分中添加下面的代码行：  
  
    ```xml  
    <AppContextSwitchOverrides value="Switch.System.Net.DontEnableSchUseStrongCrypto=true"/>  
    ```  
  
 但请注意，不建议选择退出默认行为，因为这会导致应用程序不太安全。  
  
## <a name="see-also"></a>请参阅
- [重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6.md)
