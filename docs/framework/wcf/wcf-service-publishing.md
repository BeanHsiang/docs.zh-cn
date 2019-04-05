---
title: WCF 服务发布
ms.date: 03/30/2017
ms.assetid: c806b253-cd47-4b96-b831-e73cbf08808f
ms.openlocfilehash: 04912d94568cf144e874513395e6a6f31375fb7c
ms.sourcegitcommit: acd8ed14fe94e9d4e3a7fb685fe83d05e941073c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2019
ms.locfileid: "56441432"
---
# <a name="wcf-service-publishing"></a>WCF 服务发布

Windows Communication Foundation (WCF) 服务发布帮助您从实际部署到生产环境中以进行测试的应用程序提供的 WCF 服务主机和 WCF 测试客户端的早期开发环境。 提交到最终部署计划之前，您可以使用 Windows Communication Foundation (WCF) 服务发布来验证您的 WCF 服务正确执行，并已准备好发布。 您还可以选择将您的 WCF 服务库部署到用于测试的各种目标位置。

## <a name="supported-services-and-target-locations"></a>支持的服务和目标位置

WCF 服务发布支持发布的 WCF 服务库模板，以及其相应的项模板包括以下各项集中创建的 WCF 服务：

-   带有项模板的 WCF 服务库模板。

-   联合服务库。

可以通过选择找到这些服务模板**文件** > **新建项目**> [**Visual Basic**或**Visual C#** ] > **WCF**。 对于此位置 （包括 WCF 工作流服务应用程序和 WCF 服务应用程序） 中的其他 WCF 模板，可以发布使用[一键式发布为 web 应用程序](https://docs.microsoft.com/previous-versions/aspnet/dd465337(v=vs.110))。

可以将服务发布到以下目标位置。

-   本地 IIS。

-   文件系统。

-   FTP 站点。

## <a name="using-wcf-service-publishing"></a>使用 WCF 服务发布

若要部署服务实现，请执行以下步骤：

1.  使用提升的权限打开 Visual Studio (右键单击该可执行文件，然后选择**以管理员身份运行**以将其打开)。  如果使用 IIS 7.0 或更高版本，确保你已安装的"IIS 元数据库和 iis 6 配置兼容性"部分，在控制面板中使用"打开或关闭，请打开 Windows 功能"。

2.  打开服务项目中，选择**构建** > **发布\<项目名称 >** 从主菜单中，右键单击该项目中的或**解决方案资源管理器**并单击**发布**。

3.  **发布**窗口会显示。 单击 **...**. 按钮指定服务应部署到的目标位置。 你可以选择将应用部署到本地 IIS、 文件系统或 FTP 站点。 如果部署到本地 IIS 应用程序，可以选择你的网站，并通过单击创建 web 应用程序在其下**创建新的 Web 应用程序**在右上角的图标。

4.  单击后**发布**主窗口中，在 Visual Studio 部署到指定的目标位置的应用程序，并将 Web.config、.svc 和程序集文件复制到目标目录。 . .Svc 的名称将为"ProjectName.ServiceName.svc"。 已成功发布服务后，您可以中找到一个热 Visual Studio 输出窗口中，看起来类似于"连接到`http://localhost/WebApplicationFolderName...`"。 可在按住 Ctrl 键的同时单击该链接来打开 Visual Studio 中的浏览器页面，以便查看服务目录结构。

     如果您无法浏览到网站，这可能是因为 IIS 中未启用目录浏览器。 请按照中的"可尝试的操作"部分，若要启用它的提示。 或者，你可以直接键入`http://localhost/WebApplicationFolderName/ProjectName.ServiceName.svc`若要查看你的服务页面。

可以使用**发布**指定你想要复制的程序集、 配置和到目标位置，在项目中定义的所有服务的.svc 文件，并覆盖目标位置的现有文件。

如果选择将应用程序部署到本地 IIS，则可能会遇到与 IIS 设置有关的错误。 请确保已正确安装 IIS。 可以输入`http://localhost`在浏览器的地址栏并检查是否 IIS 默认页面显示。 在某些情况下，问题也可能引起的 ASP.NET 或 IIS 中的 WCF 不正确的注册。 你可以打开 Visual Studio 开发人员命令提示符并运行命令`aspnet_regiis.exe -ir`来解决 ASP.NET 注册问题，或运行命令`ServiceModelReg.exe –ia`来解决 WCF 注册问题。

## <a name="files-generated-for-publishing"></a>生成的待发布文件
 WCF 服务库可以由 Web 承载之前，由工具生成下列文件： 程序集文件、 Web.config 文件和.svc 文件。 这些文件全部复制到目标位置。 然后发布该服务。

### <a name="assembly-files"></a>程序集文件
 当您发布的 WCF 服务时使用此工具，首先自动生成服务和生成后，在服务项目中的程序集文件生成。

### <a name="svc-file"></a>.SVC 文件
 此文件是否存在与否，以确保版本有效性，发布操作将生成每个 WCF 服务，*.svc 文件。 有两种不同的 svc 文件： 一个用于 WCF 服务库和联合服务库，另一个用于顺序工作流和状态机工作流服务库。 生成\*.svc 文件复制到目标位置中的根文件夹。

### <a name="webconfig-file"></a>Web.config 文件
 每次将服务项目发布到特定目标位置时，都会创建一个 Web.config 文件。

 生成的 Web.config 文件包括可用于托管、 Web 和 WCF 服务库中有以下更改 App.config 的内容的 Web 部分：

-   排除了基址。

-   排除了 `<diagnostics>` 元素中的设置以保留目标平台的跟踪设置。

## <a name="publishing-wcf-services-with-non-http-bindings-to-iis"></a>将具有非 HTTP 绑定的 WCF 服务发布到 IIS
 如果你使用的是 iis 7.0 或更高版本，使用非 HTTP 绑定到 IIS 发布 WCF 服务。 需要进行一些预配置。 有关详细信息，请参阅主题[在 Windows 进程激活服务中承载](../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)。

## <a name="security"></a>安全性
 发布到本地 IIS 需要具有管理员权限，原因是 IIS 要求以 Administrator 帐户身份运行。 如果用户不具有管理员权限打开 WCF 服务发布时，IIS 不是可用作目标位置。 发布到文件系统或 FTP 站点的工作不具有管理员权限。

## <a name="see-also"></a>请参阅

- [WCF Visual Studio 模板](../../../docs/framework/wcf/wcf-vs-templates.md)
- [WCF 服务主机 (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
- [WCF 测试客户端 (WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)