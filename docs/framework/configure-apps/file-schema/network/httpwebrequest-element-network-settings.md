---
title: <httpWebRequest> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest
- http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest
helpviewer_keywords:
- <httpWebRequest> element
- httpWebRequest element
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
ms.openlocfilehash: f19c39922105cebe179dd9f26fdc6beac8ddc0ef
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55268270"
---
# <a name="httpwebrequest-element-network-settings"></a>\<httpWebRequest > 元素 （网络设置）
自定义 Web 请求参数。  
  
 \<configuration>  
\<system.net>  
\<settings>  
\<httpWebRequest>  
  
## <a name="syntax"></a>语法  
  
```xml  
<httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|**特性**|**说明**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|指定以千字节为单位的响应标头的最大长度。 默认值为 64。 值为-1 指示没有大小限制将施加的响应标头。|  
|`maximumErrorResponseLength`|指定的最大长度的错误响应，以千字节为单位。 默认值为 64。 值为-1 指示没有大小限制将施加的错误响应。|  
|`maximumUnauthorizedUploadLength`|在响应未经授权的错误代码，以字节为单位指定上传的最大长度。 默认值为 -1。 值为-1 指示，将对上载施加没有大小限制。|  
|`useUnsafeHeaderParsing`|指定是否启用不安全标题解析。 默认值为 `false`。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|**元素**|**说明**|  
|-----------------|---------------------|  
|[settings](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## <a name="remarks"></a>备注  
 默认情况下，.NET Framework 将严格强制执行 RFC 2616 的 URI 分析。 某些服务器响应可能包含控制字符，在被禁止字段中，这将导致<xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType>方法会引发<xref:System.Net.WebException>。 如果**useUnsafeHeaderParsing**设置为**true**，<xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType>不会引发这种情况下; 但是，你的应用程序将很容易受到几种形式的 URI 分析攻击。 最佳解决方案是更改的服务器，以便响应不包含控制字符。  
  
## <a name="configuration-files"></a>配置文件  
 此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。  
  
## <a name="example"></a>示例  
 下面的示例演示如何指定一个较大比正常的最大标头长度。  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>
- [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
