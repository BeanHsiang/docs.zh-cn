---
title: 安装问题疑难解答
ms.date: 03/30/2017
ms.assetid: 1644f885-c408-4d5f-a5c7-a1a907bc8acd
ms.openlocfilehash: 69cc6bce08f3d98d3d63570005582bc6f50240bf
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54532547"
---
# <a name="troubleshooting-setup-issues"></a>安装问题疑难解答
本主题介绍如何对 Windows Communication Foundation (WCF) 设置问题进行故障排除。  
  
## <a name="some-windows-communication-foundation-registry-keys-are-not-repaired-by-performing-an-msi-repair-operation-on-the-net-framework-30"></a>有些 Windows Communication Foundation 注册表项无法通过在 .NET Framework 3.0 上执行 MSI 修复操作来修复  
 如果您删除下面的任何注册表项：  
  
-   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelService 3.0.0.0  
  
-   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelOperation 3.0.0.0  
  
-   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelEndpoint 3.0.0.0  
  
-   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SMSvcHost 3.0.0.0  
  
-   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSDTC Bridge 3.0.0.0  
  
 不使用.NET Framework 3.0 安装程序从启动运行修复时重新创建密钥**添加/删除程序**中的小程序**控制面板**。 若要重新正确创建这些项，用户必须卸载并重新安装 .NET Framework 3.0。  
  
## <a name="wmi-service-corruption-blocks-installation-of-the-windows-communication-foundation-wmi-provider-during-installation-of-net-framework-30-package"></a>在安装 .NET Framework 3.0 软件包过程中 WMI Service Corruption 阻止 Windows Communication Foundation WMI 提供程序的安装  
 WMI Service Corruption 可能阻止 Windows Communication Foundation WMI 提供程序的安装。 在安装过程中，Windows Communication Foundation 安装程序无法使用 mofcomp.exe 组件注册 WCF .mof 文件。 下面列出了几个症状：  
  
1.  .NET Framework 3.0 安装成功完成，但未注册 WCF WMI 提供程序。  
  
2.  应用程序事件日志中显示一个错误事件，该事件指示在注册 WCF 的 WMI 提供程序或运行 mofcomp.exe 时出现问题。  
  
3.  用户的 %temp% 目录中名为 dd_wcf_retCA* 的安装日志文件包含对注册 WCF WMI 提供程序失败的引用。  
  
4.  事件日志或安装跟踪日志文件中可能会列出以下异常之一：  
  
     ServiceModelReg [11:09:59:046]:System.ApplicationException:意外的结果 3 执行 E:\WINDOWS\system32\wbem\mofcomp.exe 使用"E:\WINDOWS\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModel.mof"  
  
     或：  
  
     ServiceModelReg [07:19:33:843]:System.TypeInitializationException:System.Management.ManagementPath 的类型初始值设定项引发了异常。 ---> System.Runtime.InteropServices.COMException (0x80040154):检索具有 CLSID {CF4CC405-E2C5-4DDD-B3CE-5E7582D8C9FA} 因以下错误失败的组件的 COM 类工厂：80040154.  
  
     或：  
  
     ServiceModelReg [07:19:32:750]:System.IO.FileNotFoundException:无法加载文件或程序集 C:\WINDOWS\system32\wbem\mofcomp.exe 或其某个依赖项。 系统找不到指定的文件。  
  
     文件名：'C:\WINDOWS\system32\wbem\mofcomp.exe  
  
 若要解决前面说明的问题，必须按照以下步骤操作。  
  
1.  运行[WMI 诊断实用程序，版本 2.0](https://go.microsoft.com/fwlink/?LinkId=94685)以修复 WMI 服务。 有关使用此工具的详细信息，请参阅[WMI 诊断实用程序](https://go.microsoft.com/fwlink/?LinkId=94686)主题。  
  
 使用修复安装.NET Framework 3.0**添加/删除程序**小程序位于**控制面板**，或卸载/重新安装.NET Framework 3.0。  
  
## <a name="repairing-net-framework-30-after-net-framework-35-installation-removes-configuration-elements-introduced-by-net-framework-35-in-machineconfig"></a>在安装 .NET Framework 3.5 后修复 .NET Framework 3.0 会移除 .NET Framework 3.5 在 machine.config 中引入的配置元素  
 如果在安装 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 后修复 .NET Framework 3.0，则会从 machine.config 中移除由 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 引入的配置元素。 但是，web.config 保持不变。 解决方法是修复[!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]此后通过 ARP 或使用[工作流服务注册工具 (WFServicesReg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md)与`/c`切换。  
  
 [工作流服务注册工具 (WFServicesReg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md)位于 %windir%\Microsoft.NET\framework\v3.5\ 或 %windir%\Microsoft.NET\framework64\v3.5\  
  
## <a name="configure-iis-properly-for-wcfwf-webhost-after-installing-net-framework-35"></a>安装 .NET Framework 3.5 之后，为 WCF/WF Webhost 正确配置 IIS  
 当[!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]安装无法配置其他与 WCF 相关的 IIS 配置设置，它在安装日志中记录错误并继续。 对运行 WorkflowServices 应用程序的任何尝试都将失败，因为缺少必需的配置设置。 例如，加载 xoml 或规则服务会失败。  
  
 解决此问题，请使用[工作流服务注册工具 (WFServicesReg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md)与`/c`切换到在计算机上正确配置 IIS 脚本映射。 [工作流服务注册工具 (WFServicesReg.exe)](../../../docs/framework/wcf/workflow-service-registration-tool-wfservicesreg-exe.md)位于 %windir%\Microsoft.NET\framework\v3.5\ 或 %windir%\Microsoft.NET\framework64\v3.5\  
  
## <a name="could-not-load-type-systemservicemodelactivationhttpmodule-from-assembly-systemservicemodel-version-3000-cultureneutral-publickeytokenb77a5c561934e089"></a>无法从程序集“System.ServiceModel, Version 3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089”加载类型“System.ServiceModel.Activation.HttpModule”  
 如果发生此错误[!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]安装，然后启用 WCF HTTP 激活。 若要解决此问题，运行以下命令行从内部开发人员命令提示中为 Visual Studio:  
  
```Output  
aspnet_regiis.exe -i -enable  
```  
  
## <a name="see-also"></a>请参阅
- [设置说明](../../../docs/framework/wcf/samples/set-up-instructions.md)
