---
title: webRequestModules -> <add> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/add
- http://schemas.microsoft.com/.NetConfiguration/v2.0#add
helpviewer_keywords:
- <webRequestModules>, add element
- webRequestModules, add element
- add element, webRequestModules
- <add> element, webRequestModules
ms.assetid: 47ec4adc-f39f-4bcd-8680-1ec21fd26890
ms.openlocfilehash: ff564571f3f606ac526c5b9efdb904d237348ffe
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55287126"
---
# <a name="add-element-for-webrequestmodules-network-settings"></a>\<添加 > webRequestModules （网络设置） 的
将自定义的 Web 请求模块添加到应用程序。  
  
 \<configuration>  
\<system.net>  
\<webRequestModules>  
\<add>  
  
## <a name="syntax"></a>语法  
  
```xml  
<add   
  prefix="URI prefix"   
  type="type_fullname, assembly_fullname"   
/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|**特性**|**说明**|  
|-------------------|---------------------|  
|`prefix`|此 Web 请求模块处理的请求 URI 前缀。|  
|`type`|完全限定的类型名 (由<xref:System.Type.FullName%2A>属性) 和程序集名称 (由<xref:System.Reflection.Assembly.FullName%2A>属性)、 分隔一个逗号，实现该 Web 请求模块。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[webRequestModules](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|指定模块用于从网络主机请求信息。|  
  
## <a name="remarks"></a>备注  
 `prefix`属性定义使用指定的 Web 请求模块的 URI 前缀。 Web 请求模块通常注册用于处理特定的协议，例如 HTTP 或 FTP，但可以注册用于处理对特定服务器或服务器上的路径的请求。  
  
 当 URI 匹配的前缀传递给创建 Web 请求模块<xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType>方法。  
  
 值为`prefix`属性应为有效的 URI 的前导字符。 例如，`http` 或 `http://www.contoso.com`。
  
 值为`type`属性应为有效的类型名称和相应的程序集名称，用逗号分隔。
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
 下面的示例为 HTTP 注册自定义的 Web 请求模块。 应使用正确的值指定模块的版本和 PublicKeyToken 替换值。  
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Net.WebRequest>
- [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
