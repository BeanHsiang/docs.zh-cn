---
title: 承载服务
ms.date: 03/30/2017
helpviewer_keywords:
- hosting services [WCF]
ms.assetid: 192be927-6be2-4fda-98f0-e513c4881acc
ms.openlocfilehash: 208841d880ffcbfb2bbeb9e235cc8cdf0fa2f041
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54637919"
---
# <a name="hosting-services"></a>承载服务
要变为活动状态，服务必须承载于创建它并控制它的上下文和生存期的运行时环境中。 Windows Communication Foundation (WCF) 服务设计为支持托管代码的任何 Windows 进程中运行。  
  
 WCF 提供了统一的编程模型，用于构建面向服务的应用程序。 此编程模型保持一致且独立于部署服务的运行时环境。 实际上，这意味着不管使用什么宿主选项，服务的代码看起来都非常类似。  
  
 这些宿主选项的范围是从在控制台应用程序内运行到在服务器环境（如在由 Internet 信息服务 (IIS) 或由 Windows 进程激活服务 (WAS) 管理的工作进程内运行的 Windows 服务）中运行。 开发人员选择可满足服务的部署要求的宿主环境。 这些要求可能源自部署应用程序的平台，它必须发送和接收消息的传输，或者进程回收的类型和为确保足够可用性所需的其他进程管理，或者某些其他管理或可靠性要求。 下一节提供了有关宿主选项的信息和指南。  
  
## <a name="hosting-options"></a>宿主选项  
  
#### <a name="self-hosting-in-a-managed-application"></a>托管应用程序中的自承载  
 可以在任何托管应用程序中承载 WCF 服务。 这是最灵活的选项，因为它需要部署最少的基础结构。 在托管应用程序代码内嵌入服务代码，然后创建并打开 <xref:System.ServiceModel.ServiceHost> 的实例以使服务变为可用。 有关详细信息，请参阅[如何：承载于托管应用程序的 WCF 服务](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)。  
  
 此选项可实现两个常见方案：在控制台应用程序和丰富的客户端应用程序，如基于 Windows Presentation Foundation (WPF) 或 Windows 窗体 (WinForms) 上运行的 WCF 服务。 承载在控制台应用程序的 WCF 服务应用程序的开发阶段是通常很有用。 这使服务变得容易调试，从中跟踪信息以查明应用程序内发生的情况变得更加方便，以及通过将其复制到新的位置进行来回移动变得更加轻松。 此宿主选项还使丰富客户端应用程序（如 [!INCLUDE[avalon2](../../../includes/avalon2-md.md)] 和 WinForms 应用程序）与外部世界的通信变得很容易。 例如，使用的对等协作客户[!INCLUDE[avalon2](../../../includes/avalon2-md.md)]为其用户界面，并还承载 WCF 服务，允许其他客户端连接到它并共享信息。  
  
#### <a name="managed-windows-services"></a>托管 Windows 服务  
 此宿主选项包括注册承载 WCF 服务作为托管 Windows 服务 （以前称为 NT 服务），以便该服务的进程生存期由服务控制管理器 (SCM) 控制的应用程序域 (AppDomain)Windows 服务。 与自承载选项一样，此类型的宿主环境要求作为应用程序的一部分编写某些宿主代码。 该服务实现为这两个 Windows 服务和 WCF 服务，因为它继承自<xref:System.ServiceProcess.ServiceBase>类，以及从 WCF 服务协定接口。 然后创建 <xref:System.ServiceModel.ServiceHost> ，在被重写的 <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 方法内打开它并在被重写的 <xref:System.ServiceProcess.ServiceBase.OnStop> 方法内关闭它。 还必须实现从 <xref:System.Configuration.Install.Installer> 继承的安装程序类，以允许 Installutil.exe 工具将程序安装为 Windows 服务。 有关详细信息，请参阅[如何：承载 WCF 服务中托管的 Windows 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)。 由托管 Windows 服务宿主选项启用的方案是在安全环境中没有消息激活 IIS 外部承载的长时间运行 WCF 服务。 服务的生存期改由操作系统控制。 此宿主选项在 Windows 的所有版本中都是可用的。  
  
#### <a name="internet-information-services-iis"></a>Internet 信息服务 (IIS)  
 IIS 宿主选项与 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 集成在一起，并使用这些技术提供的功能，如进程回收、空闲关闭、进程状况监视和基于消息的激活。 在 [!INCLUDE[wxp](../../../includes/wxp-md.md)] 和 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 操作系统上，这是作为必须高度可用且高度可伸缩的 Web 服务应用程序宿主的首选解决方案。 IIS 还提供了客户期望企业级服务器产品具有的集成可管理性。 此宿主选项要求正确配置 IIS，但不需要编写任何承载代码作为应用程序的一部分。 有关如何配置 IIS 承载的 WCF 服务，请参阅[如何：承载在 IIS 中的 WCF 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)。  
  
 请注意，以 IIS 为宿主的服务只能使用 HTTP 传输。 它在 IIS 5.1 中的实现在 [!INCLUDE[wxp](../../../includes/wxp-md.md)]中引入了一些限制。 提供的 WCF 服务由 IIS 5.1，在基于消息的激活[!INCLUDE[wxp](../../../includes/wxp-md.md)]阻止使用端口 80 进行通信的同一计算机上的任何其他自承载的 WCF 服务。 WCF 服务可以在与其他应用程序由托管时，相同的 AppDomain/应用程序池/工作进程中运行[!INCLUDE[iis601](../../../includes/iis601-md.md)]上[!INCLUDE[ws2003](../../../includes/ws2003-md.md)]。 但是，由于 WCF 并[!INCLUDE[iis601](../../../includes/iis601-md.md)]两者都使用内核模式 HTTP 堆栈 (HTTP.sys)，[!INCLUDE[iis601](../../../includes/iis601-md.md)]可以与同一台计算机，与 IIS 5.1 上运行的其他自承载 WCF 服务共享端口 80。  
  
#### <a name="windows-process-activation-service-was"></a>Windows 进程激活服务 (WAS)  
 Windows 进程激活服务 (WAS) 是在 [!INCLUDE[lserver](../../../includes/lserver-md.md)] 上也可用的 [!INCLUDE[wv](../../../includes/wv-md.md)]的新进程激活机制。 它保留了熟悉的 [!INCLUDE[iis601](../../../includes/iis601-md.md)] 进程模型（应用程序池和基于消息的进程激活）和承载功能（如快速失败保护、运行状况监视和回收），但是它从激活体系结构中移除了对 HTTP 的依赖。 [!INCLUDE[iisver](../../../includes/iisver-md.md)] 使用 WAS 通过 HTTP 完成基于消息的激活。 WCF 的其他组件也插入了 WAS 通过其他 WCF 支持的协议，例如 TCP、 MSMQ 和命名的管道提供基于消息的激活。 这样，使用通信协议的应用程序就可以使用 IIS 功能（如进程回收、快速失败保护）和仅对基于 HTTP 的应用程序可用的通用配置系统。  
  
 此承载选项要求正确配置 WAS，但不需要编写任何承载代码作为应用程序的一部分。 详细了解如何配置 WAS 托管，请参阅[如何：承载在 WAS 中的 WCF 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)。  
  
## <a name="choosing-a-hosting-environment"></a>选择宿主环境  
 下表汇总了与每个宿主选项关联的一些主要优点和方案。  
  
|宿主环境|常见方案|主要优点和限制|  
|-------------------------|----------------------|----------------------------------|  
|托管应用程序（“自承载”）|在开发过程中使用的控制台应用程序。<br />丰富 WinForm 和[!INCLUDE[avalon2](../../../includes/avalon2-md.md)]访问服务的客户端应用程序。|-灵活。<br />-易于部署。<br />-未服务的企业解决方案。|  
|Windows 服务（以前称为 NT 服务）|IIS 外部承载的长时间运行 WCF 服务。|服务进程生存期由操作系统，不是消息激活控制。<br />-支持的所有版本的 Windows。<br />安全环境。|  
|IIS 5.1、 [!INCLUDE[iis601](../../../includes/iis601-md.md)]|-运行 WCF 服务与并行[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]使用 HTTP 协议在 Internet 上的内容。|-进程回收。<br />-空闲时关闭。<br />-处理运行状况监视。<br />-基于消息的激活。<br />-仅限 HTTP。|  
|Windows 进程激活服务 (WAS)|-运行而无需使用各种传输协议在 Internet 上安装 IIS 的 WCF 服务。|不需要 IIS。<br />-进程回收。<br />-空闲时关闭。<br />-处理运行状况监视。<br />-基于消息的激活。<br />-适用于 HTTP、 TCP、 命名的管道和 MSMQ。|  
|IIS 7.0|-运行 WCF 服务使用[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]内容。<br />-使用各种传输协议在 Internet 上运行的 WCF 服务。|-已优势。<br />-与集成[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]和 IIS 内容。|  
  
 宿主环境的选择取决于部署它的 Windows 版本、它要求发送消息的传输以及它要求的进程和应用程序域回收的类型。 下表汇总了与这些要求相关的数据。  
  
|宿主环境|平台可用性|支持的传输|进程和 AppDomain 回收|  
|-------------------------|---------------------------|--------------------------|-------------------------------------|  
|托管应用程序（“自承载”）|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP；<br /><br /> net.tcp；<br /><br /> net.pipe；<br /><br /> net.msmq|否|  
|Windows 服务（以前称为 NT 服务）|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP；<br /><br /> net.tcp；<br /><br /> net.pipe；<br /><br /> net.msmq|否|  
|IIS 5.1|[!INCLUDE[wxp](../../../includes/wxp-md.md)]|HTTP|是|  
|[!INCLUDE[iis601](../../../includes/iis601-md.md)]|[!INCLUDE[ws2003](../../../includes/ws2003-md.md)]|HTTP|是|  
|Windows 进程激活服务 (WAS)|[!INCLUDE[wv](../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP；<br /><br /> net.tcp；<br /><br /> net.pipe；<br /><br /> net.msmq|是|  
  
 值得注意的是，从不受信任的主机运行服务或任何扩展会危害安全。 另请注意，通过模拟打开 <xref:System.ServiceModel.ServiceHost> 时，应用程序必须确保未注销用户，例如通过缓存用户的 <xref:System.Security.Principal.WindowsIdentity> 。  
  
## <a name="see-also"></a>请参阅
- [系统要求](../../../docs/framework/wcf/wcf-system-requirements.md)
- [基本编程生命周期](../../../docs/framework/wcf/basic-programming-lifecycle.md)
- [实现服务协定](../../../docs/framework/wcf/implementing-service-contracts.md)
- [如何：承载在 IIS 中的 WCF 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)
- [如何：承载在 WAS 中的 WCF 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)
- [如何：主机托管的 Windows 服务中的 WCF 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)
- [如何：承载于托管应用程序的 WCF 服务](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)
