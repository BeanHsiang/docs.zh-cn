---
title: WIF API 参考
ms.date: 03/30/2017
ms.assetid: a027d902-9314-4bfd-b172-4e81847b1d68
author: BrucePerlerMS
ms.openlocfilehash: 21b294a58efcad6c3eb7c74e643a2ac3e0ea23fd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54663591"
---
# <a name="wif-api-reference"></a>WIF API 参考
Windows Identity Foundation (WIF) 类可分为以下程序集：`mscorlib` (mscorlib.dll)、`System.IdentityModel` (System.IdentityModel.dll)、`System.IdentityModel.Services` (System.IdentityModel.Services.dll) 和 `System.ServiceModel` (System.ServiceModel.dll)。 本主题提供指向 WIF 命名空间的链接和每个命名空间包含的类的简短说明。  
  
> [!IMPORTANT]
>  以下 `System.IdentityModel` 命名空间包含实现 WCF 基于声明的标识模型的类：<xref:System.IdentityModel.Claims?displayProperty=nameWithType>、<xref:System.IdentityModel.Policy?displayProperty=nameWithType> 和 <xref:System.IdentityModel.Selectors?displayProperty=nameWithType>。 从 .NET Framework 4.5 开始，WCF 基于声明的标识模型已被 WIF 取代。 在基于 WIF 生成解决方案时，不应该使用这三个命名空间中的类。  
  
 <xref:System.IdentityModel?displayProperty=nameWithType>  
 包含表示 cookie 转换、安全令牌服务和专业 XML 字典读取器的类。  
  
 <xref:System.IdentityModel.Configuration?displayProperty=nameWithType>  
 包含为使用 Windows Identity Foundation (WIF) 生成的应用程序和服务提供配置的类。 此命名空间中的类表示 [\<identityConfiguration>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md) 元素下的设置。  
  
 <xref:System.IdentityModel.Metadata?displayProperty=nameWithType>  
 包含表示联合元数据文档中的元素。  
  
 <xref:System.IdentityModel.Protocols.WSTrust?displayProperty=nameWithType>  
 包含表示 WS-Trust 项目的类。  
  
 <xref:System.IdentityModel.Services?displayProperty=nameWithType>  
 包含被动（WS 联合身份验证）方案中使用的类。 还包含表示 [\<system.identityModel.services>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 元素下的设置的某些类。 此元素下的设置为应用程序配置 WS 联合身份验证。 `System.IdentityModel.Services.Configuration` 命名空间包含用于配置 WS 联合身份验证的大多数类。  
  
 <xref:System.IdentityModel.Services.Configuration?displayProperty=nameWithType>  
 包含为使用 WS 联合身份验证协议的 WIF 应用程序提供配置的类。 此命名空间中的类表示 [\<system.identityModel.services>](../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/system-identitymodel-services.md) 元素下的设置。 `System.IdentityModel.Services` 命名空间还包含用于配置 WS 联合身份验证的某些类。  
  
 <xref:System.IdentityModel.Services.Tokens?displayProperty=nameWithType>  
 包含 Web 场方案专用的安全令牌处理程序。  
  
 <xref:System.IdentityModel.Tokens?displayProperty=nameWithType>  
 包含表示安全令牌、安全令牌处理程序和其他安全令牌项目的类。  
  
 <xref:System.Security.Claims?displayProperty=nameWithType>  
 包含表示声明、基于声明的标识、基于声明的主体和其他基于声明的标识模型项目。  
  
 <xref:System.ServiceModel.Security?displayProperty=nameWithType>  
 包含表示 WCF 协定、通道、服务主机和主动 (WS-Trust) 方案中使用的其他项目的类。 命名空间还包括特定于 Windows Communication Foundation (WCF) 并不被 WIF 使用的类。  
  
## <a name="see-also"></a>请参阅
- [WIF 配置参考](../../../docs/framework/security/wif-configuration-reference.md)
- [WIF 3.5 和 WIF 4.5 之间的命名空间映射](../../../docs/framework/security/namespace-mapping-between-wif-3-5-and-wif-4-5.md)
