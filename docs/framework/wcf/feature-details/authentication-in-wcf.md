---
title: WCF 中的身份验证
ms.date: 03/30/2017
helpviewer_keywords:
- authentication [WCF]
- security [WCF], authentication
ms.assetid: 9254d873-843d-4c6e-bea4-8184ac3e44f4
ms.openlocfilehash: 22bfd7edf0ca0e9eb57e63c168c783f25782d607
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54523917"
---
# <a name="authentication-in-wcf"></a>WCF 中的身份验证
以下主题说明在 Windows Communication Foundation (WCF) 提供身份验证，例如，Windows 身份验证、 X.509 证书和用户名和密码的多种不同的机制。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：使用 ASP.NET 成员资格提供程序](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)  
 ASP.NET 功能包括成员资格和角色提供程序、用于存储用户名/密码对以供进行身份验证的数据库，以及用于身份验证的用户角色。 本主题介绍了 WCF 服务如何使用相同的数据库用户进行身份验证和授权。  
  
 [如何：使用自定义用户名和密码验证程序](../../../../docs/framework/wcf/feature-details/how-to-use-a-custom-user-name-and-password-validator.md)  
 演示如何集成自定义用户名/密码验证程序。  
  
 [服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)  
 作为额外的保护措施，客户端可以进行身份验证服务通过指定期望*标识*的服务。 如果期望的标识与服务返回的标识不匹配，则身份验证失败。  
  
 [安全性协商和超时](../../../../docs/framework/wcf/feature-details/security-negotiation-and-timeouts.md)  
 说明如何使用 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.NegotiationTimeout%2A> 类的 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> 属性。  
  
 [调试 Windows 身份验证错误](../../../../docs/framework/wcf/feature-details/debugging-windows-authentication-errors.md)  
 重点说明使用 Windows 身份验证时所遇到的常见问题。  
  
## <a name="reference"></a>参考  
 <xref:System.ServiceModel>  
  
## <a name="related-sections"></a>相关章节  
 [常用安全方案](../../../../docs/framework/wcf/feature-details/common-security-scenarios.md)  
  
## <a name="see-also"></a>请参阅
- [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [Windows Server App Fabric 的安全模型](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
