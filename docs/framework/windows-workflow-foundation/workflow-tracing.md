---
title: 工作流跟踪
ms.date: 03/30/2017
ms.assetid: 18737989-0502-4367-b5f6-617ebfb77c96
ms.openlocfilehash: f8b454437631b4711360ddf0c1196cafca13b5ff
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54627169"
---
# <a name="workflow-tracing"></a>工作流跟踪
工作流跟踪提供了一种使用 .NET Framework 跟踪侦听器捕获诊断信息的方法。 如果检测到应用程序存在问题，可以启用跟踪，然后在解决问题之后再次禁用跟踪。 可以通过两种方法为工作流启用调试跟踪。 您可以使用事件跟踪查看器配置调试跟踪，也可以使用 <xref:System.Diagnostics> 向文件发送跟踪事件。  
  
## <a name="enabling-debug-tracing-in-etw"></a>在 ETW 中启用调试跟踪  
 若要使用 ETW 启用跟踪，请在事件查看器中启用调试通道：  
  
1.  在事件查看器中导航到分析和调试日志节点。  
  
2.  在事件查看器中树视图中，导航到**事件查看器-> 应用程序和服务日志-> Microsoft-> Windows-> 应用程序服务器-应用程序**。 右键单击**应用程序服务器-应用程序**，然后选择**视图-> 显示分析和调试日志**。 右键单击**调试**，然后选择**启用日志**。  
  
3.  当工作流运行调试并将跟踪发出到 ETW 调试通道时，即可在事件查看器中查看这些跟踪。 导航到**事件查看器-> 应用程序和服务日志-> Microsoft-> Windows-> 应用程序服务器-应用程序**。 右键单击**调试**，然后选择**刷新**。  
  
4.  默认跟踪分析缓冲区大小仅为 4 KB；建议将此大小增大到 32 KB。 为此，请执行下列步骤。  
  
    1.  在当前框架目录（例如，C:\Windows\Microsoft.NET\Framework\v4.0.21203）中执行以下命令：`wevtutil um Microsoft.Windows.ApplicationServer.Applications.man`  
  
    2.  更改\<bufferSize > 为 32 Windows.ApplicationServer.Applications.man 文件中的值。  
  
        ```xml  
        <channel name="Microsoft-Windows-Application Server-Applications/Analytic" chid="ANALYTIC_CHANNEL" symbol="ANALYTIC_CHANNEL" type="Analytic" enabled="false" isolation="Application" message="$(string.MICROSOFT_WINDOWS_APPLICATIONSERVER_APPLICATIONS.channel.ANALYTIC_CHANNEL.message)" >  
                    <publishing>  
                      <bufferSize>32</bufferSize>  
                    </publishing>  
                  </channel>  
        ```  
  
    3.  在当前框架目录（例如，C:\Windows\Microsoft.NET\Framework\v4.0.21203）中执行以下命令：`wevtutil im Microsoft.Windows.ApplicationServer.Applications.man`  
  
> [!NOTE]
>  如果使用.NET Framework 4 Client Profile，必须先从.NET Framework 4 目录运行以下命令来注册 ETW 清单： `ServiceModelReg.exe –i –c:etw`  
  
## <a name="enabling-debug-tracing-using-systemdiagnostics"></a>使用 System.Diagnostics 启用调试跟踪  
 上述侦听器可以在工作流应用程序的 App.config 文件或工作流服务的 Web.config 中配置。 在此示例中， [TextWriterTraceListener](https://go.microsoft.com/fwlink/?LinkId=165424)配置为在当前目录的 MyTraceLog.txt 文件中保存跟踪信息。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="System.Activities" switchValue="Information">  
        <listeners>  
          <add name="textListener" />  
          <remove name="Default" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="textListener"  
           type="System.Diagnostics.TextWriterTraceListener"  
           initializeData="MyTraceLog.txt"  
           traceOutputOptions="ProcessId, DateTime" />  
    </sharedListeners>  
    <trace autoflush="true" indentsize="4">  
      <listeners>  
        <add name="textListener" />  
      </listeners>  
    </trace>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [Windows Server App Fabric 监视](https://go.microsoft.com/fwlink/?LinkId=201273)
- [使用 App Fabric 监视应用程序](https://go.microsoft.com/fwlink/?LinkId=201275)
