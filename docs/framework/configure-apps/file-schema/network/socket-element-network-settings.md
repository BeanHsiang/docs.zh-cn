---
title: <socket> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/socket
- http://schemas.microsoft.com/.NetConfiguration/v2.0#socket
helpviewer_keywords:
- <socket> element
- socket element
ms.assetid: 366c634c-7d16-478f-aedf-053eda94a1a0
ms.openlocfilehash: 3f599d6ada288db861f69fc64e6b84ee326b5830
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55256884"
---
# <a name="socket-element-network-settings"></a>\<套接字 > 元素 （网络设置）
指定套接字操作是否使用完成端口。  
  
 \<configuration>  
\<system.net>  
\<settings>  
\<socket>  
  
## <a name="syntax"></a>语法  
  
```xml  
<socket  
  alwaysUseCompletionPortsForConnect="true|false"  
  alwaysUseCompletionPortsForAccept="true|false"  
  ipProtectionLevel="EdgeRestricted|Restricted|Unrestricted|Unspecified"  
/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|**特性**|**说明**|  
|-------------------|---------------------|  
|`alwaysUseCompletionPortsForAccept`|指示是否套接字应始终使用完成端口的接受方法调用。 默认值为 `false`。|  
|`alwaysUseCompletionPortsForConnect`|指示是否套接字应始终使用完成端口的连接方法调用。 默认值为 `false`。|  
|`ipProtectionLevel`|指定的默认<xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>使用套接字。 默认值取决于 Windows 的版本。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[settings](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## <a name="remarks"></a>备注  
 `alwaysUseCompletionPortsForAccept` 和 `alwaysUseCompletionPortsForConnect` 特性用于指定 <xref:System.Net.Sockets?displayProperty=nameWithType>.namespace 中的类在使用完全端口时的默认行为。 对于高性能服务器应用程序建议使用完成端口。  
  
 默认值为`alwaysUseCompletionPortsForAccept`并`alwaysUseCompletionPortsForConnect`属性是**false**。  
  
 <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForAccept%2A>可用于获取当前值`alwaysUseCompletionPortsForAccept`适用的配置文件中的属性。 <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForConnect%2A>可用于获取当前值`alwaysUseCompletionPortsForConnect`适用的配置文件中的属性。  
  
 `ipProtectionLevel`属性指定的默认<xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>使用套接字。 <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A>属性，为指定的范围，将 IPv6 套接字的限制的配置，如具有相同的地址的链接本地或站点本地前缀。 此选项使应用程序可以限制对 IPv6 套接字的访问权限。 通过应用此类限制，可让在专用局域网上运行的应用程序能够通过简单的方式很好地增强自身的安全性，以便防范外部攻击。 此选项可以扩大或缩小侦听套接字，从而使得不受限制访问公用和专用用户如果合适，或者对同一站点中，根据需要限制的访问范围。  
  
 这`ipProtectionLevel`属性设置会影响仅初始传入流量：  
  
-   TCP 服务器侦听的套接字上的传入连接。  
  
-   一个接收套接字上的数据包的 UDP 应用程序。  
  
 此配置设置不会影响已建立的 TCP 连接 （流量不受限制的两个方向），并且不影响发送的 UDP 数据包的应用程序。  
  
 可能的值`ipProtectionLevel`属性设置中指定的已定义的保护级别与对应<xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>枚举，如下所示：  
  
|**属性值**|**说明**|  
|-|-|  
|EdgeRestricted|IP 保护级别是边缘受限。 用于在 Internet 上运行的应用程序将使用此值。 此设置不允许使用 Windows Teredo 实现的网络地址转换 (NAT) 遍历。 这些应用程序可能会绕过 IPv4 防火墙，因此必须针对开放端口的 Internet 攻击保护应用程序。 在 Windows Server 2003 和 Windows XP 上，针对套接字的 IP 保护级别的默认值是边缘受限。|  
|受限制|IP 保护级别是受限制。 未实现 Internet 方案的 intranet 应用程序将使用此值。 通常，这些应用程序不是测试或强化了抵御 Internet 样式的攻击。 此设置将限制到仅链接-本地接收的流量。|  
|不受限制|IP 保护级别是不受限制。 此值应使用的设计包括利用 IPv6 NAT 遍历功能构建的应用程序在 Internet 上运行的应用程序到 Windows (例如，Teredo)。 这些应用程序可能会绕过 IPv4 防火墙，因此必须针对开放端口的 Internet 攻击保护应用程序。 在 Windows Server 2008 R2 和 Windows Vista 上，针对套接字的 IP 保护级别的默认值是不受限制。|  
|未指定|IP 保护级别是未指定。 在 Windows 7 和 Windows Server 2008 R2，针对套接字的 IP 保护级别的默认值是未指定。|  
  
 默认值为`ipProtectionLevel`属性是**未指定**。  
  
 <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A>属性可以用于获取的当前值`ipProtectionLevel`适用的配置文件中的属性。  
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
 下面的示例演示如何指定应使用完成端口，以及默认<xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>应为不受限制。  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <socket  
        alwaysUseCompletionPortsForAccept="true"  
        alwaysUseCompletionPortsForConnect="true"  
        ipProtectionLevel="Unrestricted"  
       />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Net?displayProperty=nameWithType>
- <xref:System.Net.Configuration.SocketElement?displayProperty=nameWithType>
- <xref:System.Net.Sockets?displayProperty=nameWithType>
- <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=nameWithType>
- <xref:System.Net.Sockets.SocketOptionName.IPProtectionLevel?displayProperty=nameWithType>
- [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
