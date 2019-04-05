---
title: WCF 分析跟踪
ms.date: 03/30/2017
ms.assetid: 6029c7c7-3515-4d36-9d43-13e8f4971790
ms.openlocfilehash: 6d4db9a8ec11e215ef18dcab6b7940526bc24927
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54748137"
---
# <a name="wcf-analytic-tracing"></a>WCF 分析跟踪
此示例演示如何将您自己的跟踪事件添加到 Windows Communication Foundation (WCF) 将写入到 ETW 中的分析跟踪流[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]。 跟踪分析是为了便于查看服务，而不会导致较高性能损失。 此示例演示如何使用<xref:System.Diagnostics.Eventing?displayProperty=nameWithType>Api 来与 WCF 服务集成的写入事件。  
  
 有关详细信息<xref:System.Diagnostics.Eventing?displayProperty=nameWithType>Api，请参阅<xref:System.Diagnostics.Eventing?displayProperty=nameWithType>。  
  
 若要了解有关在 Windows 事件跟踪的详细信息，请参阅[改善调试和性能优化使用 ETW](https://go.microsoft.com/fwlink/?LinkId=166488)。  
  
## <a name="disposing-eventprovider"></a>释放 EventProvider  
 此示例使用 <xref:System.Diagnostics.Eventing.EventProvider?displayProperty=nameWithType> 类，该类实现 <xref:System.IDisposable?displayProperty=nameWithType>。 在实现对 WCF 服务的跟踪时，很可能，您可以使用<xref:System.Diagnostics.Eventing.EventProvider>的服务的生命周期的资源。 因此，为了便于阅读，此示例永远不会释放已包装的 <xref:System.Diagnostics.Eventing.EventProvider>。 如果出于某种原因，您的服务具有不同的跟踪需求，并且必须释放此资源，则应根据释放非托管资源的最佳做法来修改此示例。 释放非托管的资源的详细信息，请参阅[实现 Dispose 方法](https://go.microsoft.com/fwlink/?LinkId=166436)。  
  
## <a name="self-hosting-vs-web-hosting"></a>自我承载与Web 承载  
 对于 Web 承载的服务，WCF 的分析跟踪提供了一个名为"HostReference"，用于标识发出这些跟踪服务的字段。 可扩展的用户跟踪可以参与此模型，此示例演示执行该操作的最佳做法。 Web 主机的格式引用时管道&#124;字符实际显示在生成字符串可以是以下之一：  
  
-   如果该应用程序不在根处。  
  
     \<SiteName>\<ApplicationVirtualPath>&#124;\<ServiceVirtualPath>&#124;\<ServiceName>  
  
-   如果该应用程序在根处。  
  
     \<SiteName>&#124;\<ServiceVirtualPath>&#124;\<ServiceName>  
  
 对于自承载服务，WCF 的分析跟踪不会填充"HostReference"字段。 此示例中的 `WCFUserEventProvider` 类在由自承载服务使用时，其行为是一致的。  
  
## <a name="custom-event-details"></a>自定义事件详细信息  
 WCF 的 ETW 事件提供程序清单定义了三个旨在由 WCF 服务作者从服务代码内发出的事件。 下表显示了这三个事件的分类。  
  
|事件|描述|事件 ID|  
|-----------|-----------------|--------------|  
|UserDefinedInformationEventOccurred|服务中发生的说明内容不是一个问题时发出此事件。 例如，可以在对数据库成功进行调用后发出一个事件。|301|  
|UserDefinedWarningOccurred|发生的问题可能导致将来出现错误时发出此事件。 例如，如果调用数据库失败，但能够通过回退到冗余数据存储区进行恢复，则可以发出一个警告事件。|302|  
|UserDefinedErrorOccurred|服务的行为方式不符合预期时发出此事件。 例如，如果调用数据库失败且无法从其他位置检索数据，则可能会发出一个事件。|303|  
  
#### <a name="to-use-this-sample"></a>使用此示例  
  
1.  使用 Visual Studio 2012 打开 WCFAnalyticTracingExtensibility.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl+Shift+B。  
  
3.  若要运行解决方案，请按 Ctrl+F5。  
  
     在 Web 浏览器中，单击**calculator.svc**。 服务的 WSDL 文档的 URI 应出现在浏览器中。 复制该 URI。  
  
4.  运行 WCF 测试客户端 (WcfTestClient.exe)。  
  
     WCF 测试客户端 (WcfTestClient.exe) 位于`\<Visual Studio 2012 Install Dir>\Common7\IDE\WcfTestClient.exe`。 默认 Visual Studio 2012 安装目录是`C:\Program Files\Microsoft Visual Studio 10.0`。  
  
5.  在 WCF 测试客户端，通过选择添加服务**文件**，然后**添加的服务**。  
  
     在输入框中添加终结点地址。  
  
6.  单击**确定**关闭对话框。  
  
     ICalculator 服务下的左窗格中添加**我的服务项目**。  
  
7.  打开事件查看器应用程序。  
  
     然后再调用该服务，启动事件查看器，并确保事件日志正在侦听从 WCF 服务发出的跟踪事件。  
  
8.  从**启动**菜单中，选择**管理工具**，然后**事件查看器**。 启用**Analytic**并**调试**日志。  
  
9. 在事件查看器中树视图中，导航到**事件查看器**，**应用程序和服务日志**， **Microsoft**， **Windows**，，然后**应用程序服务器-应用程序**。 右键单击**应用程序服务器-应用程序**，选择**视图**，然后**显示分析和调试日志**。  
  
     絋粄**显示分析和调试日志**选项处于选中状态。 启用**分析**日志。  
  
     在事件查看器中树视图中，导航到**事件查看器**，**应用程序和服务日志**， **Microsoft**， **Windows**， **应用程序服务器-应用程序**，然后**分析**。 右键单击**Analytic** ，然后选择**启用日志**。  
  
10. 使用 WCF 测试客户端来测试服务。  
  
    1.  在 WCF 测试客户端中，双击**add （)** ICalculator 服务节点下。  
  
         **Add （)** 方法将出现在右窗格中使用两个参数。  
  
    2.  为第一个参数键入 2，为第二个参数键入 3。  
  
    3.  单击**Invoke**来调用该方法。  
  
11. 转到**事件查看器**已打开的窗口。 导航到**事件查看器**，**应用程序和服务日志**， **Microsoft**， **Windows**，**应用程序服务器应用程序**。  
  
12. 右键单击**Analytic**节点，然后选择**刷新**。  
  
     事件将显示在右窗格中。  
  
13. 使用 ID 303 来查找事件，然后双击该事件将其打开，并检查其内容。  
  
     已将发出此事件`Add()`ICalculator 服务的方法和具有负载等于"2 + 3 = 5"。  
  
#### <a name="to-clean-up-optional"></a>清理（可选）  
  
1.  打开**事件查看器**。  
  
2.  导航到**事件查看器**，**应用程序和服务日志**， **Microsoft**， **Windows**，，然后**应用程序服务器-应用程序**。 右键单击**Analytic** ，然后选择**禁用日志**。  
  
3.  导航到**事件查看器**，**应用程序和服务日志**， **Microsoft**， **Windows**， **应用程序服务器-应用程序**，然后**分析**。 右键单击**Analytic** ，然后选择**清除日志**。  
  
4.  单击**清除**清除这些事件。  
  
## <a name="known-issue"></a>已知问题  
 没有中的已知的问题**事件查看器**，它可能无法解码 ETW 事件。 可能会看到错误消息，指出："事件 ID 的说明\<id > 找不到 Microsoft Windows 应用程序服务器-应用程序的源中。 本地计算机上未安装引发此事件的组件，或者安装已损坏。 你可以安装或修复本地计算机上的组件。" 如果遇到此错误，请选择**刷新**从**操作**菜单。 然后，该事件应能正确解码。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请转到[Windows Communication Foundation (WCF) 和.NET Framework 4 的 Windows Workflow Foundation (WF) 示例](https://go.microsoft.com/fwlink/?LinkId=150780)若要下载所有 Windows Communication Foundation (WCF) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ETWTrace`  
  
## <a name="see-also"></a>请参阅
- [AppFabric 监视示例](https://go.microsoft.com/fwlink/?LinkId=193959)
