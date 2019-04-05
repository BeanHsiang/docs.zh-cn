---
title: 在托管应用程序中承载
ms.date: 03/30/2017
ms.assetid: af70132d-e9e1-4f32-b20f-f0014629758a
ms.openlocfilehash: 0210f608be8ef7ff8b2af4b0cc36b308cd3ddbe8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54617234"
---
# <a name="hosting-in-a-managed-application"></a>在托管应用程序中承载
Windows Communication Foundation (WCF) 服务可以承载于任何[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]应用程序。 自承载服务是最灵活的宿主选项，因为此服务部署所需要的基础结构最少。 但是，它也是最不可靠宿主选项，因为托管应用程序不提供的高级宿主和管理功能，如 Internet 信息服务 (IIS) 和 Windows 服务在 WCF 中，其他托管选项。  
  
 若要创建自承载服务，请创建并打开 <xref:System.ServiceModel.ServiceHost>的实例以启动侦听消息的服务。 有关详细信息，请参阅[如何：承载于托管应用程序的 WCF 服务](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)。  
  
 有关如何定义协定、 实现协定，和托管应用程序内托管服务的完整示例请参阅[入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)并[自承载](../../../../docs/framework/wcf/samples/self-host.md)。  
  
 以下各部分描述了使用此宿主选项的常见情况。  
  
## <a name="console-applications"></a>控制台应用程序  
 自承载支持的常见方案是控制台应用程序内运行的 WCF 服务。 承载 WCF 服务中的控制台应用程序服务在开发阶段是通常很有用。 这使服务变得容易调试，从中跟踪信息以查明应用程序内发生的情况变得更加方便，以及通过将其复制到新的位置进行来回移动变得更加轻松。  
  
## <a name="rich-client-applications"></a>胖客户端应用程序  
 自承载支持是丰富的客户端应用程序，如基于 Windows Presentation Foundation (WPF) 或 Windows 窗体 (WinForms) 其他常见方案。 此宿主选项还使丰富客户端应用程序（如 [!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] 和 WinForms 应用程序）与外部世界的通信变得很容易。 例如，使用的对等协作客户[!INCLUDE[avalon2](../../../../includes/avalon2-md.md)]为其用户界面，并还承载 WCF 服务，允许其他客户端连接到它并共享信息。  
  
## <a name="see-also"></a>请参阅
- [托管服务](../../../../docs/framework/wcf/hosting-services.md)
- [入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)
