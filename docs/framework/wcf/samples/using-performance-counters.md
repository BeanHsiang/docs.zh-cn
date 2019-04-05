---
title: 使用性能计数器
ms.date: 03/30/2017
ms.assetid: 00a787af-1876-473c-a48d-f52b51e28a3f
ms.openlocfilehash: 755d93e8165b9747f799571836d6b54e54a5fc45
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54623152"
---
# <a name="using-performance-counters"></a>使用性能计数器
此示例演示如何访问 Windows Communication Foundation (WCF) 性能计数器以及如何创建用户定义的性能计数器。 此示例基于[Getting Started](../../../../docs/framework/wcf/samples/getting-started-sample.md)。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 在此示例中，客户端调用 `ICalculator` 服务的四个方法。 客户端一直执行该操作，直到被用户中断。 该服务保持不变。  
  
 性能计数器在该服务的 Web.config 文件的诊断节中启用，如下面的示例配置所示。  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <diagnostics performanceCounters="All" />   
  </system.serviceModel>  
</configuration>  
```  
  
 也可以完成此任务使用[配置编辑器工具 (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)。  
  
 启用性能计数器后，为服务启用 WCF 性能计数器的完整套件。 .NET Framework 自动在三个级别维护性能数据：`ServiceModelService`、`ServiceModelEndpoint` 和 `ServiceModelOperation`。 其中每个级别都有“Calls”（调用）、“Calls per Second”（每秒调用次数）和“Security Calls Not Authorized”（未授权的安全调用次数）等性能计数器。  
  
### <a name="to-set-up-build-and-run-the-sample"></a>设置、生成和运行示例  
  
1.  请确保您具有执行[的 Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C# 或 Visual Basic .NET 版本的解决方案，请按照 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要在单或跨计算机配置中运行示例，请按照中的说明[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)。  
  
### <a name="to-view-performance-data"></a>查看性能数据  
  
1.  通过单击启动性能监视器工具**启动**，**运行...**，输入`perfmon`然后单击**确定，** 或从控制面板中，选择**管理工具**，然后双击**性能**。  
  
    > [!NOTE]
    >  在示例代码运行之前无法添加计数器。  
  
2.  选择列出的性能计数器并按 Delete 键以移除它们。  
  
3.  通过右键单击关系图窗格中，选择添加 WCF 计数器**添加计数器**。 在中**添加计数器**对话框中，选择**ServiceModelOperation 3.0.0.0、 ServiceModelEndpoint 3.0.0.0 或 ServiceModelService 3.0.0.0**性能对象中下拉列表框。 从列表中选择要查看的计数器。  
  
    > [!NOTE]
    >  如果不没有在计算机上运行任何 WCF 服务，则服务没有 WCF 性能计数器。  
  
### <a name="to-use-the-configuration-editor-to-enable-counters"></a>使用配置编辑器来启用计数器  
  
1.  打开 SvcConfigEditor.exe 的一个实例。  
  
2.  在文件菜单上单击**开放**，然后单击**配置文件...**.  
  
3.  导航到示例应用程序的服务文件夹并打开 Web.config 文件。  
  
4.  单击**诊断**上配置树。  
  
5.  切换**性能计数器**中**诊断**窗口以显示全部。  
  
6.  保存该配置文件并退出编辑器。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请转到[Windows Communication Foundation (WCF) 和.NET Framework 4 的 Windows Workflow Foundation (WF) 示例](https://go.microsoft.com/fwlink/?LinkId=150780)若要下载所有 Windows Communication Foundation (WCF) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\PerfCounters`  
  
## <a name="see-also"></a>请参阅
- [AppFabric 监视示例](https://go.microsoft.com/fwlink/?LinkId=193959)
