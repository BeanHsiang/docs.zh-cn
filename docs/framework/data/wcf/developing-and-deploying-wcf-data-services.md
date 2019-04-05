---
title: 开发和部署 WCF 数据服务
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- deploying [WCF Data Services
- developing applications [WCF Data Services]
ms.assetid: 6557c0e3-5aea-4f6e-bc14-77ad317a168b
ms.openlocfilehash: 826adbde9129a51f67636d51bd7714335a840525
ms.sourcegitcommit: d2ccb199ae6bc5787b4762e9ea6d3f6fe88677af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56093081"
---
# <a name="develop-and-deploy-wcf-data-services"></a>开发和部署 WCF 数据服务

本主题提供有关开发和部署 WCF 数据服务的信息。 有关 WCF 数据服务的更多基本信息，请参阅[Getting Started](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)并[概述](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)。

## <a name="develop-wcf-data-services"></a>开发 WCF 数据服务

当使用 WCF 数据服务来创建数据服务，支持[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]，必须在开发过程中执行以下基本任务：

1.  **定义数据模型**

     WCF 数据服务支持多种数据服务提供程序使您可以定义基于各种数据源，从关系数据库到后期绑定数据类型中的数据的数据模型。 有关详细信息，请参阅[数据服务提供商](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)。

2.  **创建数据服务**

     大多数基本数据服务公开一个从 <xref:System.Data.Services.DataService%601> 类继承的类和一个作为实体容器的命名空间限定名称的 `T` 类型。 有关详细信息，请参阅 [Defining WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)的信息。

3.  **配置数据服务**

     默认情况下，WCF 数据服务禁用对由实体容器公开的资源的访问。 <xref:System.Data.Services.DataServiceConfiguration>接口，您可以配置对资源的访问和服务操作，指定受支持的版本的 OData，并定义其他服务范围的行为，例如批处理行为或最大可返回的实体数在单个响应源中。 有关详细信息，请参阅[数据服务配置](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。

本主题介绍如何使用 Visual Studio 主要的开发和部署数据服务。 将数据作为 OData 馈送公开的 WCF 数据服务提供的灵活性的信息，请参阅[Defining WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)。

### <a name="choose-a-development-web-server"></a>选择开发 Web 服务器

形式的 WCF 数据服务的开发时[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]应用程序或[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]网站上使用 Visual Studio 2015，您可以在其上运行数据服务在开发过程中的 Web 服务器的选择。 以下 Web 服务器将与 Visual Studio 以使其更易于测试和调试你的本地计算机上的数据服务集成。

1.  **本地 IIS 服务器**

     创建作为在 Internet Information Services (IIS) 上运行的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序或 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 网站的数据服务时，建议使用 IIS 在本地计算机上开发和测试数据服务。 在 IIS 上运行数据服务更便于在调试过程中跟踪 HTTP 请求。 这还允许预先确定 IIS 访问数据服务所需的文件、数据库和其他资源所必须具备的权限。 若要在 IIS 上运行您的数据服务，你必须确保 IIS 和 Windows Communication Foundation (WCF) 是否安装且配置正确，并在文件系统和数据库中授予 IIS 帐户的访问权限。 有关详细信息，请参阅[如何：开发在 IIS 上运行的 WCF 数据服务](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)。

    > [!NOTE]
    > 必须使用管理员权限才能启用开发环境，以配置本地 IIS 服务器来运行 Visual Studio。

2.  **Visual Studio 开发服务器**

     Visual Studio 包括一个内置的 Web 服务器，Visual Studio 开发服务器，这是默认的 Web 服务器为[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]项目。 该 Web 服务器设计为在开发过程中在本地计算机上运行 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 项目。 [WCF Data Services 快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)演示如何创建运行在 Visual Studio 开发服务器中的数据服务。

     使用 Visual Studio 开发服务器开发数据服务时应注意以下限制：

    -   该服务器只能在本地计算机上访问。

    -   该服务器侦听 `localhost` 和特定端口，而非端口 80，后者是 HTTP 消息的默认端口。 有关详细信息，请参阅 [Visual Studio 中用于 ASP.NET Web 项目的 Web 服务器](https://docs.microsoft.com/previous-versions/aspnet/58wxa9w5(v=vs.120))。

    -   该服务器在当前用户帐户的上下文中运行数据服务。 例如，如果作为管理员级别的用户运行，在 Visual Studio 开发服务器中运行的数据服务将具有管理员级别特权。 这会导致数据服务能够访问在部署到 IIS 服务器时无权访问的资源。

    -   该服务器不包含 IIS 的额外功能，如身份验证。

    -   此服务器无法处理分块的 HTTP 流，从数据服务访问大型二进制数据时发送哪个响应是由 WCF 数据服务客户端的默认值。 有关详细信息，请参阅[流式处理提供程序](../../../../docs/framework/data/wcf/streaming-provider-wcf-data-services.md)。

    -   此服务器有问题的处理时间 (`.`) 字符在 URL 中，即使此字符支持由 WCF 数据服务中的密钥值。

    > [!TIP]
    > 即使 Visual Studio 开发服务器可用于在开发过程中测试你的数据服务，应部署到运行 IIS 的 Web 服务器之后再次对其进行测试。

3.  **Microsoft Azure 开发环境**

     Windows Azure Tools for Visual Studio 包含一组集成的工具，用于开发 Visual Studio 中的 Windows Azure 服务。 使用这些工具，可以开发可部署到 Microsoft Azure 的数据服务，并且可以在部署之前在本地计算机上测试数据服务。 使用 Visual Studio 开发 Windows Azure 平台运行的数据服务时，请使用这些工具。 您可以下载 Windows Azure Tools 从 Visual Studio [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=201848)。 有关开发 Windows Azure 运行的数据服务的详细信息，请参阅博文[部署 OData 服务在 Windows Azure 中](https://go.microsoft.com/fwlink/?LinkId=201847)。

### <a name="development-tips"></a>开发提示

开发数据服务时，应注意以下事项：

-   如果计划对用户进行身份验证或将访问权限限定给特定用户，请确定数据服务的安全要求。 有关更多信息，请参见 [Securing WCF Data Services](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)。

-   HTTP 检查程序在调试数据服务时会非常有帮助，通过它可以检查请求和响应消息的内容。 可以使用任何可显示原始数据包的网络数据包分析器检查发向数据服务的 HTTP 请求和来自数据服务的响应。

-   在调试数据服务时，你可能想要在常规操作期间从数据服务不获取有关错误的详细信息。 通过将 <xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A> 中的 <xref:System.Data.Services.DataServiceConfiguration> 属性设置为 `true` 并将数据服务类的 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A> 特性的 <xref:System.ServiceModel.Description.ServiceDebugBehavior> 属性设置为 `true`，可以从数据服务获取其他错误信息。 有关详细信息，请参阅文章[调试 WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=201868)。 你也可以在 WCF 中查看 HTTP 消息传送层中出现的异常跟踪。 有关更多信息，请参见 [Configuring Tracing](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)。

-   数据服务通常开发为[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]应用程序项目，但你也可以创建自己的数据服务作为[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Visual Studio 中的网站项目。 有关两种类型的项目之间的差异的信息，请参阅[Web 应用程序项目与 Visual Studio 中的 Web 站点项目](https://docs.microsoft.com/previous-versions/aspnet/dd547590(v=vs.110))。

-   当使用创建数据服务**添加新项**对话框中，在 Visual Studio 中，数据服务由承载[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]在 IIS 中。 虽然 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 和 IIS 是数据服务的默认宿主，但也支持其他宿主选项。 有关详细信息，请参阅[承载数据服务](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)。

## <a name="deploy-wcf-data-services"></a>部署 WCF 数据服务

WCF 数据服务在选择承载数据服务的过程方面很灵活。 Visual Studio 可用于将数据服务部署到以下平台：

-   **承载有 IIS 的 Web 服务器**

     将数据服务作为 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 项目开发时，可以使用标准 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 部署过程将其部署到 IIS Web 服务器。  Visual Studio 提供了有关以下部署技术[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]，具体类型取决于的[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]承载要部署的数据服务的项目。

    -   **ASP.NET Web 应用程序的部署技术**

        -   [如何：在 Visual Studio 中创建 Web 部署包](https://docs.microsoft.com/previous-versions/aspnet/dd465323(v=vs.110))

        -   [如何：部署 Web 项目使用一键式发布 Visual Studio 中](https://docs.microsoft.com/previous-versions/aspnet/dd465337(v=vs.110))

    -   **ASP.NET 网站的部署技术**

        -   [如何：将具有复制网站工具的网站文件复制](https://docs.microsoft.com/previous-versions/aspnet/c95809c0(v=vs.100))

        -   [如何：发布网站](https://docs.microsoft.com/previous-versions/aspnet/20yh9f1b(v=vs.100))

        -   [演练：ASP.NET Web 应用程序使用 XCOPY 部署](https://docs.microsoft.com/previous-versions/aspnet/f735abw9(v=vs.100))

     有关的部署选项的详细信息[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]应用程序，请参阅[Visual Studio 和 ASP.NET 的 Web 部署概述](https://docs.microsoft.com/previous-versions/aspnet/dd394698(v=vs.110))。

    > [!TIP]
    > 在尝试将数据服务部署到 IIS 之前，请确保已测试了向运行 IIS 的 Web 服务器的部署。 有关详细信息，请参阅[如何：开发在 IIS 上运行的 WCF 数据服务](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)。

-   **Microsoft Azure**

     您可以通过使用 Windows Azure Tools for Visual Studio 部署到 Windows Azure 数据服务。 您可以下载 Windows Azure Tools 从 Visual Studio [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=201848)。 有关数据服务部署到 Windows Azure 的详细信息，请参阅博文[部署 OData 服务在 Windows Azure 中](https://go.microsoft.com/fwlink/?LinkId=201847)。

### <a name="deployment-considerations"></a>部署注意事项

部署数据服务时，应注意以下事项：

-   当您部署使用 [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] 提供程序访问 SQL Server 数据库的数据服务时，还可能需要通过数据服务部署传播数据结构和/或数据。 Visual Studio 可以自动创建脚本 （.sql 文件） 来执行此操作在目标数据库中，并且这些脚本可以包含的 Web 部署包中[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]应用程序。 有关详细信息，请参阅[如何：部署具有 Web 应用程序项目的数据库](https://docs.microsoft.com/previous-versions/dd465343(v=vs.100))。 有关[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]网站上，你可以执行此操作使用**Database Publishing Wizard** Visual Studio 中。 有关详细信息，请参阅[发布 SQL 数据库](https://docs.microsoft.com/previous-versions/aspnet/bb907585(v=vs.100))。

-   因为 WCF 数据服务包括基本的 WCF 实现，可以使用 Windows Server AppFabric 监控数据服务部署到 Windows Server 上运行的 IIS。 有关使用 Windows Server AppFabric 监控数据服务的详细信息，请参阅博文[使用 Windows Server AppFabric 跟踪 WCF 数据服务](https://go.microsoft.com/fwlink/?LinkID=202005)。

## <a name="see-also"></a>请参阅

- [承载数据服务](../../../../docs/framework/data/wcf/hosting-the-data-service-wcf-data-services.md)
- [确保 WCF Data Services 的安全](../../../../docs/framework/data/wcf/securing-wcf-data-services.md)
- [定义 WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)
