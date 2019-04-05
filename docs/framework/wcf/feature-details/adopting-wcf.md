---
title: 采用 Windows Communication Foundation
ms.date: 03/30/2017
ms.assetid: 49ba71e2-9468-4082-84c5-cf8daf95e34a
ms.openlocfilehash: 58a51f7ea0db2297c7151a752de3f54307e0c5fd
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54643346"
---
# <a name="adopting-windows-communication-foundation"></a>采用 Windows Communication Foundation

您可以选择要用于新开发的 Windows Communication Foundation (WCF)，同时继续维护现有应用程序开发使用 ASP.NET。 因为 WCF 将是最合适的选择与在任何情况下.NET framework 构建应用程序之间的通信，所以它可以充当以解决各种软件通信问题的方式的标准工具 ASP.NET不能。

新的 WCF 应用程序可以部署在作为现有的 ASP.NET Web 服务在同一台计算机上。 如果现有的 ASP.NET Web 服务使用的.NET Framework 2.0 版之前的版本，然后可以使用 ASP.NET IIS 注册工具来有选择地将.NET Framework 2.0 部署到 IIS 应用程序是用来托管新的 WCF 应用程序。 该工具所述[ASP.NET IIS 注册工具 (Aspnet_regiis.exe)](https://go.microsoft.com/fwlink/?LinkId=94687)，并具有内置于 IIS 6.0 管理控制台用户界面。

WCF 可以用于通过添加 WCF 服务配置为在 ASP.NET 兼容性模式下运行在 IIS 中的现有 ASP.NET Web 服务应用程序添加到现有的 ASP.NET Web 服务的新功能。 由于 ASP.NET 兼容模式下，新的 WCF 服务的代码可以访问和使用更新预先存在的 ASP.NET 代码，与相同的应用程序状态信息<xref:System.Web.HttpContext>类。 这些应用程序还可以共享相同的类库。

WCF 客户端可以使用 ASP.NET Web 服务。 使用配置的 WCF 服务<xref:System.ServiceModel.BasicHttpBinding>可由 ASP.NET Web 服务客户端。 ASP.NET Web 服务可以与 WCF 应用程序共存，WCF 甚至可以用于将功能添加到现有的 ASP.NET Web 服务。 有了所有的 WCF 和 ASP.NET Web 服务可以一起使用这些方法，您可能想要将 ASP.NET Web 服务迁移到 WCF 中，仅当需要由 WCF 并不是 ASP.NET Web 服务提供的功能。

甚至在少数的情况下有必要，将代码从一种技术迁移到另一个很少是正确的方法。 采用新技术的原因是为了满足早期技术无法满足的新需求。在上述情况下，正确的做法是设计一个新的解决方案来满足刚刚扩展的需求集。 新的设计将受益于您对现有系统所拥有的经验以及您自该系统被设计以来获得的智慧。 此外，新设计还可以利用新技术的所有功能，而不是在新平台上再现旧设计。 在建立新设计的关键元素的原型之后，可以更轻松地在新系统中重用现有系统中的代码。

## <a name="see-also"></a>请参阅

- [如何：检索元数据并实现兼容服务](../../../../docs/framework/wcf/feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md)
