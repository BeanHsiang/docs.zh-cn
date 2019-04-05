---
title: 服务示例的 WCF
ms.date: 03/30/2017
ms.assetid: 462a2218-f8c6-4fb7-95bc-64765459c429
ms.openlocfilehash: 3fbca09a7b50a15299cb8e805ac84c60e4b78fa7
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55268734"
---
# <a name="services"></a>Services

本节包含演示 Windows Communication Foundation (WCF) 服务的示例。

## <a name="in-this-section"></a>本节内容

- [承载](../../../../docs/framework/wcf/feature-details/hosting.md)\
演示托管 WCF 服务。

- [服务互操作性](service-interoperability.md)\
演示 WCF 和其他服务技术之间的交互。

- [行为](behaviors.md)\
演示 WCF 服务行为。

- [服务安全性](service-security.md)\
演示 WCF 服务安全。

- [WCF 服务的简化的配置](simplified-configuration-for-wcf-services.md)\
演示如何实现和配置典型的服务和客户端使用 WCF。

- [标准终结点的使用情况](usage-of-standard-endpoints.md)\
演示如何在服务配置文件中使用标准终结点。

- [扩展的保护策略](extended-protection-policy.md)\
演示扩展保护，这是一种针对中间人 (MITM) 攻击而提供保护的安全计划。

- [配置通道工厂](configuration-channel-factory.md)\
演示 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> 的用法。

- [寻址](addressing.md)\
演示终结点地址的各个方面和功能。

- [命令性](imperative.md)\
演示如何使用代码为服务定义 <xref:System.ServiceModel.WSHttpBinding>，而不是在配置中定义 `wsHttpBinding` 绑定。

- [多个协定](multiple-contracts.md)\
演示如何在一个服务上实现多个协定和如何配置终结点以便与每个实现的协定通信。

- [多个终结点](multiple-endpoints.md)\
演示如何在一个服务上配置多个终结点，以及如何从客户端与每个终结点通信。

- [在单个 listenuri 中承载的多个终结点](multiple-endpoints-at-a-single-listenuri.md)\
演示一个在单个 `ListenUri` 中承载多个终结点的服务。

- [OperationContextScope](operationcontextscope.md)\
演示如何将 WCF 调用使用标头上的额外信息发送。

- [服务说明](service-description.md)\
演示服务如何在运行时检索其服务说明信息。

- [ConcurrencyMode.Reentrant](concurrencymode-reentrant.md)\
演示如何在服务实现上使用可重入并发模式。