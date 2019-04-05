---
title: Windows 窗体中的安全性概述
ms.date: 03/30/2017
helpviewer_keywords:
- code access security [Windows Forms], Windows Forms
- permissions [Windows Forms], Windows Forms
- Windows Forms, security
- security [Windows Forms], about security
- access control [Windows Forms], Windows Forms
ms.assetid: 4810dc9f-ea23-4ce1-8ea1-657f0ff1d820
ms.openlocfilehash: 8a1a7fe9f7b356f318a99dfecb425a66c1f70bd6
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708194"
---
# <a name="security-in-windows-forms-overview"></a>Windows 窗体中的安全性概述
在发布 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 之前，用户计算机上运行的所有代码都有相同的权利或权限来访问该计算机的用户所拥有的资源。 例如，如果允许用户访问文件系统，则会允许代码访问文件系统；如果允许用户访问数据库，则会允许代码访问数据库。 尽管这些权利或权限对用户显式安装在本地计算机上的可执行文件中的代码来说是可接受的，但对来自 Internet 或本地 Intranet 的恶意代码来说可能是不可接受的。 此代码没有权限时应不能访问用户的计算机资源。  
  
 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 引入了称为代码访问安全性的基础结构，它让你能够区分代码拥有的权限或权利与用户拥有的权利。 默认情况下，来自 Internet 和 Intranet 的代码仅能在所谓的部分信任模式下运行。 部分信任使应用程序受一系列限制的约束：此外，应用程序被限制访问本地硬盘，且无法运行非托管代码。 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 控制允许代码基于代码标识访问的资源：它来自哪里、是否具有[强名称程序集](../app-domains/strong-named-assemblies.md)以及是否使用证书签名等等。  
  
 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 技术用于部署 Windows 窗体应用程序，有助于让你更轻松地开发可在部分信任、完全信任或具有提升的权限的部分信任中运行的应用程序。 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 提供了如“权限提升”和“受信任的应用程序部署”等功能，从而使你的应用程序能以可靠的方式从本地用户请求完全信任或提升的权限。  
  
## <a name="understanding-security-in-the-net-framework"></a>了解 .NET Framework 中的安全性  
 代码访问安全性根据代码源以及代码标识的其他方面，使代码可以获得不同等级的受信度。 若要深入了解公共语言运行时用于确定安全策略的证据，请参阅[证据](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7y5x1hcd(v=vs.100))。 它有助于保护计算机系统不受恶意代码危害，并帮助防止受信任的代码有意或无意地折损安全性。 代码访问安全性还可让你更好地控制应用程序所能执行的操作，因为你可以指定你需要应用程序拥有的哪些权限。 代码访问安全性会影响面向公共语言运行时的所有托管代码，即使该代码不执行单个代码访问安全性权限检查。 有关 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中安全性的详细信息，请参阅[关键的安全性概念](../../standard/security/key-security-concepts.md)和[代码访问安全性基础知识](../misc/code-access-security-basics.md)。  
  
 如果用户直接运行 Web 服务器或文件共享的 Windows 窗体可执行文件，则授予应用程序的信任度取决于代码所在的位置和启动方式。 当应用程序运行时，它将自动进行计算，并从公共语言运行时接收一个命名的权限集。 默认情况下，来自本地计算机的代码会被授予完全信任权限集，来自本地网络中的代码被授予本地 Intranet 权限集，而来自 Internet 的代码被授予 Internet 权限集。  
  
> [!NOTE]
>  在 1.0 版的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Service Pack 1 和 Service Pack 2 中，Internet 区域代码组接收 Nothing 权限集。 在所有其他版本的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中，Internet 区域代码组接收 Internet 权限集。  
>   
>  每个这些权限集中授予的默认权限都列在[默认安全策略](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/03kwzyfc(v=vs.100))主题中。 根据应用程序接收的权限，它会正确运行或者生成安全性异常。  
>   
>  许多 Windows 窗体应用程序都将使用 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 进行部署。 用于生成 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 部署的工具拥有不同于上述内容的安全性默认值。 有关详细信息，请参阅下列讨论。  
  
 授予给应用程序的实际权限可能不同于默认值，原因是可以修改安全策略；这意味着你的应用程序可以在一台计算机上拥有权限，但不能在另一台上也拥有权限。  
  
## <a name="developing-a-more-secure-windows-forms-application"></a>开发更安全的 Windows 窗体应用程序  
 安全性在应用程序开发的每个步骤中都非常重要。 通过查看并遵循[安全编码准则](../../standard/security/secure-coding-guidelines.md)开始。  
  
 下一步，决定你的应用程序是否必须在完全信任环境中运行或是否应在部分信任环境中运行。 在完全信任环境中运行应用程序能更轻松地访问本地计算机上的资源，但如果不严格根据安全编码指南主题来开发和设计应用程序，会使你的应用程序和其用户暴露在高安全性风险中。 在部分信任环境中运行应用程序能更轻松地开发更安全的应用程序并减少很多风险，但就如何实现某些功能方面需要进行更多规划。  
  
 如果选择部分信任环境（即，Internet 或本地 Intranet 权限集），则要决定应用程序在此环境中的工作方式。 Windows 窗体在不完全受信任的环境中提供了其他更安全的方式来实现功能。 可以同时为部分信任和完全信任环境设计并以不同的方式编写应用程序的某些部分，如数据访问。 一些 Windows 窗体功能的目的在于在部分信任环境中工作，如应用程序设置。 有关详细信息，请参阅[应用程序设置概述](./advanced/application-settings-overview.md)。  
  
 如果你的应用程序需要比部分信任所允许的更多的权限，但你不想在完全信任环境中运行，你可以在部分信任环境中运行的同时仅断言那些你需要的额外权限。 例如，如果你想要在部分信任环境中运行，但必须授予应用程序对用户文件系统上的目录的只读访问权限，则你仅可针对该目录请求 <xref:System.Security.Permissions.FileIOPermission>。 正确使用此方法可以增强应用程序的功能，并将用户的安全风险降至最低。  
  
 开发将在部分信任环境中运行的应用程序时，对应用程序必须运行什么权限以及应用程序可以选择使用什么权限进行跟踪。 当所有权限都已知时，你应在应用程序级别提出声明性的权限请求。 请求权限会通知 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 运行时应用程序所需要的权限以及具体所不需要的权限。 有关请求权限的详细信息，请参阅[请求权限](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/yd267cce(v=vs.100))。  
  
 当请求可选的权限时，如果应用程序执行一个操作，但未获得执行该操作所需的权限时会生成安全性异常，这时必须处理此安全性异常。 适当地处理 <xref:System.Security.SecurityException> 将确保你的应用程序可以继续运行。 你的应用程序可以使用异常来确定是否应对用户禁用一项功能。 例如，如果未授予所需的文件权限，应用程序可以禁用“保存”菜单选项。  
  
 有时，很难知道你是否已断言所有适当的权限。 例如，看似无关紧要的方法调用可能在其执行期间的某个点上访问文件系统。 如果未给应用程序部署所有所需的权限，它可能在桌面上调试时测试结果为正常，但在部署时失败。 这两个[!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)]SDK 和 Visual Studio 2005 包含计算应用程序所需的权限： MT.exe 分别命令行工具和 Visual Studio 的计算权限功能。  
  
 以下主题介绍其他 Windows 窗体安全功能。  
  
|主题|描述|  
|-----------|-----------------|  
|-   [Windows 窗体中更加安全的文件和数据访问](more-secure-file-and-data-access-in-windows-forms.md)|介绍如何访问部分信任环境中的文件和数据。|  
|-   [Windows 窗体中更加安全的打印](more-secure-printing-in-windows-forms.md)|介绍如何访问部分信任环境中的打印功能。|  
|-   [Windows 窗体中的其他安全注意事项](additional-security-considerations-in-windows-forms.md)|介绍在部分信任环境中执行窗口操作、使用“剪贴板”以及调用非托管代码。|  
  
-  
  
### <a name="deploying-an-application-with-the-appropriate-permissions"></a>用适当的权限部署应用程序  
 将 Windows 窗体应用程序部署到客户端电脑最常见的方式是使用 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]，它是一种描述应用程序运行所需的所有组件的部署技术。 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 使用称为清单的 XML 文件来描述组成应用程序的程序集和文件以及应用程序所需的权限。  
  
 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 有两种在客户端计算机上请求提升的权限的技术。 两种技术都依赖于验证码证书的使用。 该证书有助于为你的用户提供一些保证，保证应用程序来自受信任的源。  
  
 下表对这些技术进行了介绍。  
  
|提升的权限技术|描述|  
|------------------------------------|-----------------|  
|权限提升|应用程序第一次运行时将以“安全性”对话框来提示用户。 “权限提升”对话框告知用户应用程序的发布者，使用户能在知情的情况下决定是否向其授予其他信任|  
|受信任的应用程序部署|涉及到系统管理员在客户端计算机上执行发布者验证码证书的一次性安装。 从那一刻起，任何使用该证书签名的应用程序都视为受信任，可以在没有其他提示的情况下在本地计算机上以完全信任模式运行。|  
  
 选择哪种技术将取决于你的部署环境。 有关详细信息，请参阅[选择 ClickOnce 部署策略](/visualstudio/deployment/choosing-a-clickonce-deployment-strategy)。  
  
 默认情况下[!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]部署使用 Visual Studio 的应用程序或[!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)]SDK 工具 （Mage.exe 和 MageUI.exe） 配置为具有完全信任的客户端计算机上运行。 如果你正在使用部分信任或仅使用某些其他权限部署应用程序，则必须更改此默认设置。 可以使用 Visual Studio 来执行此操作或[!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)]SDK 工具 MageUI.exe 配置你的部署时。 有关如何使用 MageUI.exe 的详细信息，请参阅演练：部署 ClickOnce 应用程序从命令行。  另请参阅[如何：设置 ClickOnce 应用程序的自定义权限](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/hafybdaa(v=vs.110))或[如何：设置 ClickOnce 应用程序的自定义权限](/visualstudio/deployment/how-to-set-custom-permissions-for-a-clickonce-application)。  
  
 若要深入了解 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 的安全方面和权限提升，请参阅[保护 ClickOnce 应用程序](/visualstudio/deployment/securing-clickonce-applications)。 若要深入了解受信任的应用程序部署，请参阅[受信任的应用程序部署概述](/visualstudio/deployment/trusted-application-deployment-overview)。  
  
### <a name="testing-the-application"></a>测试应用程序  
 如果已通过使用 Visual Studio 部署 Windows 窗体应用程序，可以启用在部分信任或受限的权限集从开发环境中进行调试。  另请参阅[如何：使用受限权限调试 ClickOnce 应用程序](/visualstudio/deployment/how-to-debug-a-clickonce-application-with-restricted-permissions)。  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体安全](windows-forms-security.md)
- [代码访问安全性基础知识](../misc/code-access-security-basics.md)
- [ClickOnce 安全和部署](/visualstudio/deployment/clickonce-security-and-deployment)
- [受信任的应用程序部署概述](/visualstudio/deployment/trusted-application-deployment-overview)
- [Mage.exe（清单生成和编辑工具）](../tools/mage-exe-manifest-generation-and-editing-tool.md)
- [MageUI.exe（图形化客户端中的清单生成和编辑工具）](../tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)
