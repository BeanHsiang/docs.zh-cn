---
title: WCF 服务主机 (WcfSvcHost.exe)
ms.date: 03/30/2017
ms.assetid: 8643a63d-a357-4c39-bd6c-cdfdf71e370e
ms.openlocfilehash: 6a8ed677ceaf9b86b67ec2558eb4e31c23d4c57e
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54505635"
---
# <a name="wcf-service-host-wcfsvchostexe"></a>WCF 服务主机 (WcfSvcHost.exe)
Windows Communication Foundation (WCF) 服务主机 (WcfSvcHost.exe) 允许您以启动 Visual Studio 调试器 (F5) 以自动承载和测试已实现的服务。 然后，您可以测试使用 WCF 测试客户端 (WcfTestClient.exe) 或自己的客户端，以查找并解决任何潜在错误的服务。  
  
## <a name="wcf-service-host"></a>WCF 服务主机  
 WCF 服务主机枚举中的 WCF 服务项目的服务、 加载项目的配置和实例化它找到的每个服务的主机。 该工具通过 WCF 服务模板集成到 Visual Studio 并开始调试项目时调用。  
  
 通过使用 WCF 服务主机，你可以无需编写额外代码或在开发过程中提交到特定的主机托管 WCF 服务 （在 WCF 服务库项目）。  
  
> [!NOTE]
>  WCF 服务主机不支持部分信任。 如果你想要在部分信任环境中使用 WCF 服务，不要使用 WCF 服务库项目模板在 Visual Studio 中生成服务。 相反，新的网站在 Visual Studio 中通过选择创建 WCF 服务网站模板，可以托管 web 服务器支持是 WCF 部分信任环境中的服务。  
  
## <a name="project-types-hosted-by-wcf-service-host"></a>WCF 服务主机承载的项目类型  
 WCF 服务主机可以承载以下 WCF 服务库项目类型：WCF 服务库、 顺序工作流服务库、 状态机工作流服务库和联合服务库。 WCF 服务主机也可以承载这些服务，可以添加到服务库项目 using**添加项**功能。 这包括 WCF 服务、 WF 状态机服务、 WF 顺序服务、 XAML WF 状态机服务和 XAML WF 顺序服务。  
  
 但是，应该注意到该工具将不会帮助您配置主机。 对于此项任务，必须手动编辑 App.config 文件。 另外，此工具也不会验证用户定义的配置文件。  
  
> [!CAUTION]
>  不应使用托管服务的 WCF 服务主机在生产环境中，因为它不设计用于此目的。  WCF 服务主机不支持可靠性、 安全性和可管理性的此类环境的要求。 请改用 IIS，因为它可以提供卓越的可靠性和监视功能，并且是承载服务的首选解决方案。 在服务开发完成后，应将服务迁移到 IIS 的 WCF 服务主机中。  
  
## <a name="scenarios-for-using-wcf-service-host-inside-visual-studio"></a>在 Visual Studio 中使用 WCF 服务主机的方案  
 下表列出了中的所有参数**命令行参数**对话框中，可以通过右键单击你的项目中找到**解决方案资源管理器**在 Visual Studio 中，选择**属性**，然后选择**调试**选项卡并单击**启动项目**。 这些参数可用于配置 WCF 服务主机。  
  
|参数|含义|  
|---------------|-------------|  
|`/client`|一个可选参数，用于指定要在承载服务后运行的可执行文件的路径。 这将启动 WCF 测试客户端承载后。|  
|`/clientArg`|将字符串指定为传递给自定义客户端应用程序的自变量。|  
|`/?`|显示帮助文本。|  
  
#### <a name="using-wcf-test-client"></a>使用 WCF 测试客户端  
 创建新的 WCF 服务项目并按 F5 启动调试器后，WCF 服务主机将开始承载它在项目中找到的所有服务。 WCF 测试客户端会自动打开并显示配置文件中定义的服务终结点的列表。 可以从主窗口中测试参数并调用服务。  
  
 若要确保使用 WCF 测试客户端，请右键单击您的项目**解决方案资源管理器**在 Visual Studio 中，选择**属性**，然后选择**调试**选项卡。单击**启动项目**，并确保在显示以下**命令行参数**对话框。  
  
 `/client:WcfTestClient.exe`  
  
#### <a name="using-a-custom-client"></a>使用自定义客户端  
 若要使用自定义客户端，请右键单击您的项目**解决方案资源管理器**在 Visual Studio 中，选择**属性**，然后选择**调试**选项卡。单击**启动项目**和编辑`/client`中的参数**命令行参数**对话框以指向自定义客户端，如下面的示例中所示。  
  
 `/client:"path/CustomClient.exe"`  
  
 当您按 F5 再次启动该服务时，WCF 服务主机将启动调试器时自动启动自定义客户端。  
  
 也可以按照以下示例中的指示使用 `/clientArg:` 参数将字符串指定为传递给自定义客户端应用程序的自变量。  
  
 `/client:"path/CustomClient.exe" /clientArg:"arguments that are passed to Client"`  
  
 例如，如果使用的是联合服务库模板，则可以使用以下命令行自变量：  
  
 `/client:iexplore.exe /clientArgs:http://localhost:8731/Design_Time_Addresses/Feed1/`  
  
#### <a name="specifying-no-client"></a>指定无客户端  
 若要指定 WCF 服务承载之后，将使用任何客户端，请右键单击您的项目**解决方案资源管理器**在 Visual Studio 中，选择**属性**，然后选择**调试**选项卡。单击**启动项目**并保留**命令行参数**对话框留空。  
  
#### <a name="using-a-custom-host"></a>使用自定义主机  
 若要使用自定义主机，请右键单击您的项目**解决方案资源管理器**在 Visual Studio 中，选择**属性**，然后选择**调试**选项卡。单击**启动外部程序**并输入自定义主机的完整路径。 此外可以使用**命令行参数**对话框可以指定要传递到主机参数。  
  
## <a name="wcf-service-host-user-interface"></a>WCF 服务主机用户界面  
 当您最初调用 WCF 服务主机 （通过按 F5 在 Visual Studio 中的）， **WCF 服务主机**窗口将自动打开。 当运行 WCF 服务主机时，该程序的图标将出现在通知区域中。 双击该图标可以打开**WCF 服务主机**窗口  
  
 如果服务驻留在过程中发生错误，将打开 WCF 服务主机对话框显示的相关信息。  
  
 **WCF 服务主机**主窗口包含两个菜单：  
  
-   **文件**:包含**关闭**并**退出**命令。 当您单击**关闭**，则**WCF 服务主机**对话框将关闭，但继续承载服务。 当您单击**退出**，WCF 服务主机也将关闭。 这还将停止所有承载的服务。  
  
-   **帮助**:包含**有关**命令包含版本信息。 它还包含**帮助**可以打开帮助文件的命令。  
  
 主**WCF 服务主机**窗口包含两个区域：  
  
-   第一个功能是**服务**。 该区域包含一个显示所有服务基本信息的列表。 这些信息包括：  
  
    -   **服务**：列出所有服务。  
  
    -   **状态**:列出了服务的状态。 有效值为"已启动"、"已停止"和"错误"。  
  
    -   **元数据地址**:显示服务的元数据地址。  
  
-   第二个区域**的其他信息**。 它将显示服务状态的详细的说明中选择特定的服务行时**服务**区域。 如果状态为“错误”，则可以在屏幕上查看完整的错误消息。  
  
## <a name="stopping-wcf-service-host"></a>停止 WCF 服务主机  
 可以通过以下四种方法来关闭 WCF 服务主机：  
  
-   停止在 Visual Studio 中的调试会话。  
  
-   选择**退出**从**文件**中的菜单**WCF 服务主机**窗口。  
  
-   选择**退出**从系统通知区域中的 WCF 服务主机任务栏图标上下文菜单。  
  
-   如果正在使用它，请退出 WCF 测试客户端。  
  
## <a name="using-service-host-without-administrator-privilege"></a>在无管理员权限的情况下使用服务主机  
 若要使不具有管理员权限的用户能够开发 WCF 服务，ACL （访问控制列表） 创建命名空间"http://+:8731/Design_Time_Addresses"在 Visual Studio 安装的过程。 该 ACL 被设置为“(UI)”，这将包括登录到此计算机的所有交互用户。 管理员可以添加或删除此 ACL 中的用户或打开其他端口。此 ACL 使用户能够使用 WCF 服务自动主机 (wcfSvcHost.exe)，而无需向其授予管理员权限。  
  
 可以使用提升的管理员帐户在 [!INCLUDE[wv](../../../includes/wv-md.md)] 中通过 netsh.exe 工具来修改访问权限。 下面是使用 netsh.exe 的示例。  
  
```  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 有关 netsh.exe 的更多信息，请参阅"[如何使用 Netsh.exe 工具和命令行开关](https://go.microsoft.com/fwlink/?LinkId=97877)"。  
  
## <a name="see-also"></a>请参阅
- [WCF 测试客户端 (WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)
