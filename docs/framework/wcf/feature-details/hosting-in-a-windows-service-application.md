---
title: 在 Windows 服务应用程序中承载
ms.date: 03/30/2017
ms.assetid: f4199998-27f3-4dd9-aee4-0a4addfa9f24
ms.openlocfilehash: 52c62ef1be7dafc97c5cf958f30444e47f900e92
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54621966"
---
# <a name="hosting-in-a-windows-service-application"></a>在 Windows 服务应用程序中承载
Windows 服务（以前称为 Windows NT 服务）提供了一种尤其适合于下面这样的应用程序的进程模型：必须在长时间运行的可执行程序中生存，并且不显示任何形式的用户界面。 Windows 服务应用程序的进程生存期由服务控制管理器 (SCM) 管理，您可以通过该管理器启动、停止和暂停 Windows 服务应用程序。 可以配置为在计算机启动，使其合适的托管环境的"always on"应用程序时自动启动的 Windows 服务进程。 Windows 服务应用程序的详细信息，请参阅[Windows 服务应用程序](https://go.microsoft.com/fwlink/?LinkId=89450)。  
  
 承载长时间运行的 Windows Communication Foundation (WCF) 服务的应用程序与 Windows 服务共享许多特征。 具体而言，WCF 服务是长时间运行服务器的可执行文件不直接与用户交互，因此未实现任何形式的用户界面。 在这种情况下，托管 Windows 服务应用程序内的 WCF 服务是用于构建可靠、 长时间运行的 WCF 应用程序的一个选项。  
  
 通常情况下，WCF 开发人员必须决定是否托管 Windows 服务应用程序内或在 Internet 信息服务 (IIS) 或 Windows 进程激活服务 (WAS) 宿主环境内部其 WCF 应用程序。 在下列条件下，应考虑使用 Windows 服务应用程序：  
  
-   应用程序要求显式激活。 例如，在服务器启动时应用程序必须自动启动（而不是动态启动以响应第一个传入消息）的条件下，应使用 Windows 服务。  
  
-   承载应用程序的进程必须在启动后保持运行状态。 Windows 服务进程一旦启动将一直保持运行状态，直到服务器管理员使用服务控制管理器显式关闭该进程。 在 IIS 或 WAS 中承载的应用程序可能会动态地启动和停止，以便最佳地使用系统资源。 需要显式控制其托管进程的生存期的应用程序应使用 Windows 服务而非 IIS 或 WAS。  
  
-   您的 WCF 服务必须在 Windows Server 2003 上运行，并使用非 HTTP 传输。 在 Windows Server 2003 上，[!INCLUDE[iis601](../../../../includes/iis601-md.md)] 宿主环境限制为仅可进行 HTTP 通信。 Windows 服务应用程序不受此限制的约束，可以使用任何传输 WCF 支持，包括 net.tcp、 net.pipe 和 net.msmq。  
  
### <a name="to-host-wcf-inside-of-a-windows-service-application"></a>在 Windows 服务应用程序内承载 WCF  
  
1.  创建 Windows 服务应用程序。 可以使用 <xref:System.ServiceProcess> 命名空间中的类以托管代码的形式编写 Windows 服务应用程序。 此应用程序必须包含一个继承自 <xref:System.ServiceProcess.ServiceBase> 的类。  
  
2.  链接到 Windows 服务应用程序的生存期的 WCF 服务的生存期。 通常，您希望 Windows 服务应用程序，若要在宿主服务启动时变为活动状态，请停止侦听消息时停止，并在 WCF 服务时遇到错误时关闭托管进程宿主服务中承载的 WCF 服务。 这可以通过以下操作实现：  
  
    -   重写 <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 以打开一个或多个 <xref:System.ServiceModel.ServiceHost> 实例。 单个 Windows 服务应用程序可以托管多个 WCF 服务的启动和停止作为一个组。  
  
    -   重写<xref:System.ServiceProcess.ServiceBase.OnStop%2A>来调用<xref:System.ServiceModel.Channels.CommunicationObject.Closed>上<xref:System.ServiceModel.ServiceHost>任何正在运行的 WCF 服务的过程中启动<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29>。  
  
    -   订阅 <xref:System.ServiceModel.Channels.CommunicationObject.Faulted> 的 <xref:System.ServiceModel.ServiceHost> 事件，并使用 <xref:System.ServiceProcess.ServiceController> 类以在出现错误时关闭 Windows 服务应用程序。  
  
     托管 WCF 服务的 Windows 服务应用程序部署和作为 Windows 服务应用程序，不要使用 WCF 的管理的方式相同。  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceProcess>
- [演练：在组件设计器中创建 Windows 服务应用程序](https://go.microsoft.com/fwlink/?LinkId=94875)
- [如何：主机托管的 Windows 服务中的 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)
- [Windows 服务主机](../../../../docs/framework/wcf/samples/windows-service-host.md)
- [服务应用程序编程体系结构](https://go.microsoft.com/fwlink/?LinkId=94876)
- [Windows Server App Fabric 承载功能](https://go.microsoft.com/fwlink/?LinkId=201276)
