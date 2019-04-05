---
title: <proxy> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/proxy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#proxy
helpviewer_keywords:
- <proxy> element
- proxy element
ms.assetid: 37a548d8-fade-4ac5-82ec-b49b6c6cb22a
ms.openlocfilehash: a6c6d85d8ec1b79f6b3ddf53af0a4b289289dd6a
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55256858"
---
# <a name="proxy-element-network-settings"></a>\<代理 > 元素 （网络设置）
定义代理服务器。  
  
 \<configuration>  
\<system.net>  
\<defaultProxy >  
\<proxy>  
  
## <a name="syntax"></a>语法  
  
```xml  
<proxy
  autoDetect="true|false|unspecified" 
  bypassonlocal="true|false|unspecified"
  proxyaddress="uriString"
  scriptLocation="uriString"
  usesystemdefault="true|false|unspecified"
/>
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|**特性**|**说明**|  
|-------------------|---------------------|  
|`autoDetect`|指定是否自动检测代理。 默认值为 `unspecified`。|  
|`bypassonlocal`|指定对于本地资源是否跳过代理。 本地资源包括本地服务器 (`http://localhost`， `http://loopback`，或`http://127.0.0.1`) 和不带句点的 URI (`http://webserver`)。 默认值为 `unspecified`。|  
|`proxyaddress`|指定代理要使用的 URI。|  
|`scriptLocation`|指定的配置脚本的位置。 不要使用`bypassonlocal`具有此特性的属性。 |  
|`usesystemdefault`|指定是否使用 Internet Explorer 代理设置。 如果设置为`true`，后续属性将替代 Internet Explorer 代理设置。 默认值为 `unspecified`。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[defaultProxy](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|配置超文本传输协议 (HTTP) 代理服务器。|  
  
## <a name="text-value"></a>文本值  
  
## <a name="remarks"></a>备注  
 `proxy`元素定义为应用程序代理服务器。 如果从配置文件缺少此元素，然后.NET Framework 将使用的代理设置在 Internet Explorer 中。  
  
 值为`proxyaddress`属性应为格式正确的统一资源标识符 (URI)。  
  
 `scriptLocation`特性引用了自动检测代理配置脚本。 <xref:System.Net.WebProxy>类将尝试查找配置脚本 (通常命名 Wpad.dat) 时**使用自动配置脚本**Internet 资源管理器中选择选项。 如果`bypassonlocal`设置为任何值，`scriptLocation`将被忽略。
  
 使用`usesystemdefault`要迁移到版本 2.0 的.NET Framework 版本 1.1 应用程序的属性。  
  
 如果引发异常`proxyaddress`属性指定了无效的默认代理。 异常的 <xref:System.Exception.InnerException%2A> 属性应具有错误根本原因的详细信息。  
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
 以下示例使用从 Internet 资源管理器代理的默认值，指定代理地址，并跳过本地访问的代理。  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="true"  
      />  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
