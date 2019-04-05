---
title: 承载工作流服务
ms.date: 03/30/2017
ms.assetid: 2d55217e-8697-4113-94ce-10b60863342e
ms.openlocfilehash: c933fd2bd46588ccd5c6115fbc2efca72bfadca4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54594507"
---
# <a name="hosting-workflow-services"></a>承载工作流服务
工作流服务在承载后才能对传入消息做出响应。 工作流服务使用的是 WCF 消息传递基础结构，因此承载的方式也类似。 类似于 WCF 服务，工作流服务可以托管在任何托管应用程序在 Internet 信息服务 (IIS) 或 Windows 进程激活服务 (WAS) 下。 此外，可以在 Windows Server App Fabric 下承载工作流服务。 有关 Windows Server App Fabric 的详细信息请参阅[Windows Server App Fabric 文档](https://go.microsoft.com/fwlink/?LinkId=193037)， [AppFabric 承载功能](https://go.microsoft.com/fwlink/?LinkId=196494)，并[AppFabric 承载概念](https://go.microsoft.com/fwlink/?LinkId=196495)。 服务承载 WCF 的各种不同方法的详细信息，请参阅[托管服务](../../../../docs/framework/wcf/hosting-services.md)。

## <a name="hosting-in-a-managed-application"></a>在托管应用程序中承载
 若要在托管应用程序中承载工作流服务，请使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 类。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 构造函数可用于指定单一工作流服务实例、工作流服务定义或使用工作流消息传递活动的活动。 调用 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 将导致服务开始侦听传入消息。

## <a name="hosting-under-iis-or-was"></a>在 IIS 或 WAS 下承载
 在 IIS 或 WAS 下承载工作流服务时，涉及到创建虚拟目录以及将定义服务及其行为的文件放在该虚拟目录中。 此时可能出现以下几种情况：

-   将定义工作流服务的 .xamlx 文件放在 IIS/WAS 虚拟目录中，同时放入指定服务行为、终结点和其他配置元素的 Web.config 文件。

-   将定义工作流服务的 .xamlx 文件放在一个 IIS/WAS 虚拟目录中。 .xamlx 文件指定要公开的终结点。 终结点将在 `WorkflowService.Endpoints` 元素中指定，如下面的示例所示。

    ```xml
    <WorkflowService xmlns="http://schemas.microsoft.com/netfx/2009/xaml/servicemodel"  xmlns:p1="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:sad="clr-namespace:System.Activities.Debugger;assembly=System.Activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
      <WorkflowService.Endpoints>
        <Endpoint ServiceContractName="IWorkFlowEchoService" AddressUri="">
          <Endpoint.Binding>
            <BasicHttpBinding />
          </Endpoint.Binding>
        </Endpoint>
      </WorkflowService.Endpoints>
    <!-- ... -->
    </WorkflowService>
    ```

    > [!NOTE]
    > 不能在 .xamlx 文件中指定行为，因此，如果需要指定行为设置，则必须使用 Web.config。

-   将定义工作流服务的 .xamlx 文件放在一个 IIS/WAS 虚拟目录中。 另外，将一个 .svc 文件放在该虚拟目录中。 使用 .svc 文件可以指定自定义 Web 服务主机工厂、应用自定义行为或者从自定义位置加载配置。

-   将一个程序集放在 IIS/WAS 虚拟目录中，该程序集包含一个使用 WCF 消息传递活动的活动。

 定义工作流服务的.xamlx 文件必须包含 <`Service`> 根元素或包含派生自任何类型的根元素<xref:System.Workflow.ComponentModel.Activity>。 使用 Visual Studio 活动模板时，将创建.xamlx 文件。 使用 WCF 工作流服务模板时，将创建.xamlx 文件。

## <a name="hosting-workflow-services-under-windows-server-app-fabric"></a>在 Windows Server App Fabric 下承载工作流服务
 在 Windows Server App Fabric 下承载工作流服务的方式与在 IIS/WAS 下的承载方式相同。 唯一区别在于会安装 Windows Server App Fabric。 Windows Server App Fabric 提供了添加到 Internet 信息服务管理器的工具，以及 powershell commandlets。 这些工具可简化工作流服务和 WCF 服务的部署、管理和跟踪。

## <a name="referencing-custom-activities"></a>引用自定义活动
 必须将对自定义活动的引用添加到 <`Assemblies`> 部分下 <`System.Web.Compilation`>，以便加载到应用程序域，并且 XAML 反序列化程序能够找到各类型。 可以在应用程序级别进行这些设置；如果要将这些设置应用于计算机上的所有应用程序，则可在根 Web.config 中进行这些设置。

## <a name="deployment"></a>部署
 系统中已经创建 Web 部署工具，以方便部署作业。 通过使用该工具，可以在 IIS 6.0 和 IIS 7.0 之间迁移应用程序，同步服务器场，并打包、存档和部署 Web 应用程序。 有关详细信息，请参阅[MS 部署工具](https://go.microsoft.com/fwlink/?LinkId=178690)。

## <a name="see-also"></a>请参阅

- [工作流服务主机内部机制](../../../../docs/framework/wcf/feature-details/workflow-service-host-internals.md)
- [配置 WorkflowServiceHost](../../../../docs/framework/wcf/feature-details/configuring-workflowservicehost.md)