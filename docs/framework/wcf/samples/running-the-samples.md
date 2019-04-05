---
title: 运行 Windows Communication Foundation 示例
ms.date: 03/30/2017
ms.assetid: db8a83da-95c1-4a21-a9d2-48caeb6398ea
ms.openlocfilehash: aec7d7f9ce0a6db5d20bce47ab313f4248e86c88
ms.sourcegitcommit: bef803e2025642df39f2f1e046767d89031e0304
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56304669"
---
# <a name="running-the-windows-communication-foundation-samples"></a>运行 Windows Communication Foundation 示例
可以在单一计算机或跨计算机配置中运行的 Windows Communication Foundation (WCF) 示例。 示例在提供时就可用于在单机上运行。 在跨计算机配置中，必须修改示例的配置文件设置。 下面的过程说明如何用同一计算机配置和跨计算机配置来运行示例。 请注意，Internet 信息服务 (IIS) 中承载的服务和自承载示例在步骤上有所不同。 大多数示例承载于 IIS 中，请参见示例自述文件信息以确定示例的承载方式。  
  
 在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 上，未在 IIS 中承载的示例需要提升的权限以使用 Http.sys 注册侦听器。 以服务运行所用的帐户使用 Httpcfg.exe 注册服务侦听地址，或从以管理员特权运行的命令提示符启动服务。  
  
> [!NOTE]
>  在生成或运行任何 WCF 示例之前, 请确保您已执行了[的 Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
### <a name="to-run-the-sample-on-the-same-machine"></a>在同一计算机上运行示例  
  
1.  如果服务由 IIS 承载，请确保您可以访问使用浏览器通过输入以下地址的服务： `http://localhost/servicemodelsamples/service.svc`。 在响应中应显示确认页。 如果未显示确认页，请参阅[WCF 示例的故障排除提示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
2.  如果服务是自承载的，请从 \service\bin（在语言特定文件夹内）中运行 Service.exe。 服务活动显示在服务控制台窗口上。  
  
3.  从 \client\bin 运行 Client.exe\\，从特定于语言的文件夹下。 客户端活动将显示在客户端控制台窗口上。  
  
4.  如果客户端和服务能够进行通信，请参见[WCF 示例的故障排除提示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-run-the-sample-across-machines"></a>跨计算机运行示例  
  
1.  如果服务在 IIS 中承载：  
  
    1.  在服务计算机上创建一个名为 ServiceModelSamples 的虚拟目录。 批处理文件 Setupvroot.bat 附带[的 Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)可用于创建磁盘目录和虚拟目录。  
  
    2.  从 %SystemDrive%\Inetpub\wwwroot\servicemodelsamples 中将服务程序文件复制到服务计算机上的 ServiceModelSamples 虚拟目录中。 确保在 \bin 目录中包括这些文件。  
  
    3.  测试是否可使用浏览器从客户端计算机访问服务。  
  
     如果服务是自承载的：  
  
    1.  在服务计算机上，创建一个保存服务文件的目录。  
  
    2.  将 \service\bin\ 文件夹（在语言特定文件夹内）中的服务程序文件复制到服务计算机上。  
  
    3.  在服务配置文件中，更改终结点定义的地址值以与服务的新地址相匹配。 在地址中将任何对“localhost”的引用替换为一个完全限定的域名。  
  
    4.  在命令提示符处启动 Service.exe。  
  
2.  将 \client\bin\ 文件夹（在语言特定文件夹内）中的客户端程序文件复制到客户端计算机上。  
  
3.  设置终结点地址。  
  
    1.  如果服务未在域帐户下运行，请打开客户端配置文件并更改终结点定义的地址值以与服务的新地址相匹配。 在地址中将任何对“localhost”的引用替换为一个完全限定的域名。  
  
    2.  如果服务正在域帐户下运行，则通过针对服务运行 Svcutil.exe 来重新生成客户端配置。 有关运行 Svcutil.exe 的详细信息，请参阅[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)。 使用生成的文件来代替示例中的配置文件。 生成的配置文件有附加的标识信息，并包含连接到服务终结点所需的所有设置，即使这些设置是默认设置。 有关标识信息的详细信息，请参阅[服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)，并[\<标识 >](../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)。  
  
4.  在客户端计算机上，在命令提示符下启动 Client.exe。  
  
### <a name="to-debug-a-service"></a>调试服务  
  
1.  生成解决方案 （客户端和服务） 使用**生成**菜单或 CTRL + SHIFT + B。  
  
2.  如果服务在 IIS 中承载：  
  
    1.  激活服务使用的浏览器通过输入地址`http://localhost/servicemodelsamples/service.svc`。  
  
    2.  在解决方案中，选择**调试**菜单并**附加到进程**菜单项。  
  
    3.  选择“显示所有用户的进程”复选框。  
  
    4.  选择主机辅助进程 W3wp.exe 以进行调试（在 Windows XP 上选择 ASPNet_wp.exe on）。  
  
3.  现在可以在服务代码中设置断点并启用针对异常的断点。  
  
4.  右键单击客户端项目项，然后选择**调试**，**启动新实例**。  
  
### <a name="to-clean-up-after-the-sample"></a>运行示例后进行清理  
  
-   出于安全目的，如果服务承载于 IIS 中，请在示例结束后删除虚拟目录定义和在安装步骤中授予的权限。  
  
## <a name="see-also"></a>请参阅
- [生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)
- [WCF 示例的疑难解答提示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))
