---
title: <network> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#network
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network
helpviewer_keywords:
- <network> element
- network element
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
ms.openlocfilehash: 67743ccf2fa14117814160aeb7624c2be4eea364
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55257857"
---
# <a name="network-element-network-settings"></a>\<网络 > 元素 （网络设置）
配置外部的简单邮件传输协议 (SMTP) 服务器的网络选项。  
  
 \<configuration>  
\<system.net>  
\<mailSettings>  
\<smtp>  
\<network>  
  
## <a name="syntax"></a>语法  
  
```xml  
<network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`clientDomain`|指定要使用初始 SMTP 协议请求中连接到 SMTP 邮件服务器的客户端域名。 默认值为本地计算机发送请求的本地主机名称。|  
|`defaultCredentials`|指定是否应使用默认用户凭据访问 SMTP 事务的 SMTP 邮件服务器。 默认值为 `false`。|  
|`enableSsl`|指定是否使用 SSL 访问 SMTP 邮件服务器。 默认值为 `false`。|  
|`host`|指定要用于 SMTP 事务的 SMTP 邮件服务器的主机名。 此属性具有没有默认值。|  
|`password`|指定要用于对 SMTP 邮件服务器进行身份验证的密码。 此属性具有没有默认值。|  
|`port`|指定要用于连接到 SMTP 邮件服务器的端口号。 默认值为 25。|  
|`targetName`|指定要使用的 SMTP 事务的扩展的保护时用于身份验证服务提供程序名称 (SPN)。 此属性具有没有默认值。|  
|`userName`|指定要用于对 SMTP 邮件服务器进行身份验证的用户名。 此属性具有没有默认值。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<smtp > 元素 （网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|配置简单邮件传输协议 (SMTP) 邮件发送选项。|  
  
## <a name="remarks"></a>备注  
 一些 SMTP 服务器要求您向之前使用服务器进行自行。 如果想要对自己在主机上使用的默认网络凭据进行身份验证，请将`defaultCredentials`属性为`true`。 <xref:System.Net.Configuration.SmtpNetworkElement.DefaultCredentials%2A?displayProperty=nameWithType>属性可以用于获取的当前值`defaultCredentials`适用的配置文件中的属性。  
  
 此外可以使用基本身份验证 （用户名和密码） 进行身份验证到 SMTP 服务器。 若要使用此选项，必须指定有效的用户名称和指定的 SMTP 服务器的密码。  
  
> [!NOTE]
>  基本身份验证发送`userName`和`password`到未加密的服务器的值。 监视网络流量的任何人都可以查看你的凭据，并将其用于连接到服务器。 应考虑使用更安全的身份验证机制，例如 Kerberos 或 NT LAN Manager (NTLM)。如果`defaultCredentials`是`true`，如果服务器支持这些协议，将使用 Kerberos 或 NTLM。  
  
 基本身份验证和默认网络凭据选项是互斥的;如果您设置`defaultCredentials`到`true`和指定的用户名和密码、 使用的默认网络凭据，并忽略基本身份验证数据。  
  
 如果指定的基本身份验证`userName`，还应指定`password`到身份验证自己到邮件服务器。  
  
 <xref:System.Net.Configuration.SmtpNetworkElement.UserName%2A?displayProperty=nameWithType>属性可以用于获取的当前值`userName`适用的配置文件中的属性。 <xref:System.Net.Configuration.SmtpNetworkElement.Password%2A?displayProperty=nameWithType>属性可以用于获取的当前值`password`适用的配置文件中的属性。 一个`password`属性将不正常情况下输入出于安全原因的配置文件中。  
  
 `clientDomain`属性更改对 SMTP 服务器的初始 SMTP 协议请求中使用的客户端域名。 `clientDomain`属性可以设置为本地计算机的完全限定域名而不是默认情况下使用的本地主机名称。 这提供了更好地遵守 SMTP 协议标准。 默认值为本地计算机发送请求的本地主机名称。 <xref:System.Net.Configuration.SmtpNetworkElement.ClientDomain%2A?displayProperty=nameWithType>属性可以用于获取的当前值`clientDomain`适用的配置文件中的属性。  
  
 `targetName`使用扩展的保护时，使用属性进行身份验证。 默认值是窗体的"SMTPSVC /\<主机 >"其中\<主机 > 是 SMTP 邮件服务器的主机名。 <xref:System.Net.Configuration.SmtpNetworkElement.TargetName%2A?displayProperty=nameWithType>属性可以用于获取的当前值`targetName`适用的配置文件中的属性。  
  
 `enableSsl`属性指定是否使用 SSL 访问 SMTP 邮件服务器。 <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>类仅支持 SMTP 服务扩展安全 smtp 通过传输层安全性 RFC 3207 中定义。 在此模式下，SMTP 会话开始在未加密的通道，然后 STARTTLS 命令发出客户端到服务器，以切换到使用 SSL 进行安全通信。 请参阅 RFC 3207 发布由 Internet 工程任务组 (IETF) 有关详细信息。  
  
 备用连接一个方法是在其中任何协议命令发送之前预先建立 SSL 会话。 这种连接方法有时称为 SMTPS，并且默认使用端口 465。 目前不支持使用 SSL 此备用连接方法。  
  
 <xref:System.Net.Configuration.SmtpNetworkElement.EnableSsl%2A?displayProperty=nameWithType>属性可以用于获取的当前值`enableSsl`适用的配置文件中的属性。  
  
## <a name="example"></a>示例  
 下面的示例指定适当的 SMTP 参数，以使用默认网络凭据发送电子邮件。  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="Network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
