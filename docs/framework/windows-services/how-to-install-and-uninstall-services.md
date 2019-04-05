---
title: 如何：安装和卸载 Windows 服务
ms.date: 02/05/2019
helpviewer_keywords:
- Windows Service applications, deploying
- services, uninstalling
- services, installing
- installing Windows Services
- uninstalling applications, apps, Windows services
- installation, Windows services
- uninstalling Windows services
- installutil.exe tool
ms.assetid: c89c5169-f567-4305-9d62-db31a1de5481
author: ghogen
ms.openlocfilehash: 43b5ad2f346406897e8bcbcce5660a6c9524f9af
ms.sourcegitcommit: 3500c4845f96a91a438a02ef2c6b4eef45a5e2af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55826249"
---
# <a name="how-to-install-and-uninstall-windows-services"></a>如何：安装和卸载 Windows 服务
如果正使用 .NET Framework 开发 Windows 服务，可以使用 [InstallUtil.exe](../tools/installutil-exe-installer-tool.md) 的命令行实用工具快速安装服务应用。 想要发布用户可以安装和卸载的 Windows 服务的开发者，应使用 InstallShield。 有关详细信息，请参阅[创建安装程序包（Windows 客户端）](https://docs.microsoft.com/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-client)。
  
> [!WARNING]
>  如果你想要从你的计算机卸载服务，不要遵循本文中的步骤。 而是找出安装了该服务的程序或软件包，然后在“设置”中选择“应用”来卸载该程序。 请注意，许多服务是 Windows 不可或缺的部分；如果你删除它们，可能导致系统不稳定。  
  
 要使用本文中的步骤，首先需要将服务安装程序添加到 Windows 服务。 有关详细信息，请参见[演练：创建 Windows 服务应用](../windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)。  
  
 无法通过按 F5 从 Visual Studio 开发环境直接运行 Windows 服务项目。 必须先在项目中安装服务，然后才能运行该项目。  
  
> [!TIP]
>  可以使用“服务器资源管理器”验证是否已安装或卸载服务。 有关详细信息，请参阅[如何在 Visual Studio 中使用服务器资源管理器](https://support.microsoft.com/help/316649/how-to-use-the-server-explorer-in-visual-studio-net-and-visual-studio)。
  
### <a name="install-your-service-manually"></a>手动安装服务  
  
1.  从“开始”菜单中选择“Visual Studio \<版本>”目录，然后选择“VS \<版本>开发人员命令提示”。
  
     出现“Visual Studio 开发人员命令提示”。 
  
2.  访问你的项目的已编译可执行文件所在的目录。  
  
3.  将项目的可执行文件作为参数，通过命令提示运行 InstallUtil.exe：  
  
    ```console
    installutil <yourproject>.exe  
    ```  

     如果使用的是 Visual Studio 开发人员命令提示，InstallUtil.exe 应该在系统路径上。 如果不在，可以将其添加到该路径，或使用完全限定的路径来调用它。 此工具随 .NET Framework 安装在 %WINDIR%\Microsoft.NET\Framework[64]\\<framework_version> 中。
     
     例如:
     - 对于 32 位版的 .NET Framework 4 或 4.5 以及更高版本，如果 Windows 安装目录是 C: \ Windows，则默认路径是 C:\Windows\ Microsoft.NET \ Framework \ v4.0.30319 \ InstallUtil.exe。
     - 对于 64 位版的 .NET Framework 4 或 4.5 以及更高版本，默认路径是 C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe。
  
### <a name="uninstall-your-service-manually"></a>手动卸载服务  
  
1. 从“开始”菜单中选择“Visual Studio \<版本>”目录，然后选择“VS \<版本>开发人员命令提示”。
  
     出现“Visual Studio 开发人员命令提示”。  
  
2.  将项目的输出作为参数，通过命令提示运行 InstallUtil.exe：  
  
    ```console  
    installutil /u <yourproject>.exe  
    ```  
  
3. 删除服务的可执行文件后，该服务可能仍然会出现在注册表中。 如果发生这种情况下，请使用命令 [sc delete](/windows-server/administration/windows-commands/sc-delete) 从注册表中删除服务的条目。  
  
## <a name="see-also"></a>请参阅
- [Windows 服务应用程序简介](../windows-services/introduction-to-windows-service-applications.md)
- [如何：创建 Windows 服务](../windows-services/how-to-create-windows-services.md)
- [如何：将安装程序添加到服务应用程序](../windows-services/how-to-add-installers-to-your-service-application.md)
- [Installutil.exe（安装程序工具）](../tools/installutil-exe-installer-tool.md)
