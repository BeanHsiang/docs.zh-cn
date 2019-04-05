---
title: 支持的部署方案的 WCF
ms.date: 03/30/2017
ms.assetid: 3399f208-3504-4c70-a22e-a7c02a8b94a6
ms.openlocfilehash: c9b56bfd95717202d4ffade443cb88d1884a453d
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55284838"
---
# <a name="supported-deployment-scenarios"></a>支持的部署方案

支持在部分受信任的应用程序中使用的 Windows Communication Foundation (WCF) 功能子集旨在满足使用 WCF 部分，而不是所有方案的要求。 在服务器上，WCF 满足 Internet 规模的要求共享宿主提供程序运行第三方应用程序中[!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)]中等信任权限集出于安全原因。 在客户端，WCF 部分信任支持旨在满足的要求的部署技术如[ClickOnce 部署](/visualstudio/deployment/clickonce-security-and-deployment)或[!INCLUDE[avalon2](../../../../includes/avalon2-md.md)]的 XAML 浏览器应用程序技术，允许无缝和安全来自不受信任的站点的桌面应用程序的部署。

## <a name="minimum-permission-requirements"></a>最小权限要求

WCF 支持以下标准命名的权限集下运行的应用程序中的功能子集：

- “中等信任”权限

- “Internet 区域”权限

尝试使用 WCF 在部分受信任应用程序中使用限制性更强的权限可能会导致在运行时的安全异常。

有关这些权限集支持的功能的详细信息，请参阅 [Partial Trust Feature Compatibility](partial-trust-feature-compatibility.md)。

## <a name="partial-trust-on-the-server"></a>在服务器上的部分信任

[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序宿主服务的许多商业提供程序要求在其服务器上的应用程序以 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 中等信任权限集来运行。 WCF 服务可以在这些环境中运行，前提是它们使用<xref:System.ServiceModel.BasicHttpBinding>，则<xref:System.ServiceModel.WebHttpBinding>，或<xref:System.ServiceModel.WSHttpBinding>具有传输级安全性。

在中等信任宿主环境中运行的 WCF 服务也可用作中间层服务通过将消息发送到客户端请求的响应中的其他服务器。 如果宿主环境已授予应用程序适当的 <xref:System.Net.WebPermission> 以向所需服务器发出出站请求，则支持服务器上的中间层方案。

除了 SOAP 消息使用的受支持的 SOAP 绑定之一，WCF 还支持<xref:System.ServiceModel.WebHttpBinding>构建在部分受信任的应用程序中的 Web 样式服务。 [WCF Web HTTP 编程模型](wcf-web-http-programming-model.md)， [WCF 联合](wcf-syndication.md)，并[AJAX 集成和 JSON 支持](ajax-integration-and-json-support.md)WCF 的功能支持在部分信任环境中。

工作流服务需要完全信任权限并且不能在部分受信任的应用程序中使用。

有关详细信息，请参阅[如何：ASP.NET 2.0 中使用中等信任](https://go.microsoft.com/fwlink/?LinkId=84603)。

## <a name="partial-trust-on-the-client"></a>在客户端上的部分信任

在从不受信任的 Internet 网站上下载和运行代码时必须采用某些安全预防措施。 [ClickOnce Deployment](/visualstudio/deployment/clickonce-security-and-deployment) （ClickOnce 部署）和 [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)]的 XAML 浏览器应用程序 (XBAP) 技术都可以使用部分信任以对不受信任的代码授予受限权限（Internet 区域）。

可以使用 WCF 与从部分受信任通过以下任一方法部署的应用程序中的远程服务器进行通信[ClickOnce 部署](/visualstudio/deployment/clickonce-security-and-deployment)或 xbap 技术。 在 Internet 区域权限集中包含<xref:System.Net.WebPermission>发起主机的允许这些应用程序与使用任何支持的 WCF 绑定中所述与其源服务器进行通信[Partial Trust Feature Compatibility](partial-trust-feature-compatibility.md).

## <a name="see-also"></a>请参阅

- [代码访问安全性](../../misc/code-access-security.md)
- [Windows Presentation Foundation 浏览器承载的应用程序概述](../../wpf/app-development/wpf-xaml-browser-applications-overview.md)
- [部分信任](partial-trust.md)
- [ASP.NET 信任级别和策略文件](https://docs.microsoft.com/previous-versions/wyts434y(v=vs.140))