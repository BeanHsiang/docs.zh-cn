---
title: bypasslist -> <remove> 元素（网络设置）
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- <bypasslist>, remove element
- remove element, bypasslist
- bypasslist, remove element
- remove element, bypasslist
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
ms.openlocfilehash: a04cca3e57af5cc422776c5b2444a140e86f98b9
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57354253"
---
# <a name="remove-element-for-bypasslist-network-settings"></a>\<删除 > bypasslist （网络设置） 的元素

从代理跳过列表中删除 IP 地址或 DNS 名称。

\<configuration>\
\<system.net>\
\<defaultProxy>\
\<bypasslist>\
\<remove>

## <a name="syntax"></a>语法

```xml
<remove
  address="regular expression"
/>
```

## <a name="attributes-and-elements"></a>特性和元素

下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|**特性**|**说明**|
|-------------------|---------------------|
|`address`|正则表达式描述 IP 地址或 DNS 名称。|

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|**元素**|**说明**|
|-----------------|---------------------|
|[bypasslist](../../../../../docs/framework/configure-apps/file-schema/network/bypasslist-element-network-settings.md)|提供一组描述不使用代理的地址的正则表达式。|

## <a name="remarks"></a>备注

`remove`元素中删除描述 IP 地址或 DNS 服务器名称，从列表中的绕过代理服务器的地址的正则表达式。 配置文件中或在配置层次结构中较高级别上，前面已定义地址。

值为`address`属性应为描述一组 IP 地址或主机名的正则表达式。

有关正则表达式的详细信息，请参阅。[.NET framework 正则表达式](../../../../../docs/standard/base-types/regular-expressions.md)。

## <a name="configuration-files"></a>配置文件

此元素可在应用程序配置文件或计算机配置文件 (Machine.config) 中使用。

## <a name="example"></a>示例

下面的示例删除 adventure-works.com 域中，任何以前定义，然后将 contoso.com 域添加到忽略列表。

```xml
<configuration>
  <system.net>
    <defaultProxy>
      <bypasslist>
        <remove address="[a-z]+\.adventure-works\.com$" />
        <add address="[a-z]+\.contoso\.com$" />
      </bypasslist>
    </defaultProxy>
  </system.net>
</configuration>
```

## <a name="see-also"></a>请参阅

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
