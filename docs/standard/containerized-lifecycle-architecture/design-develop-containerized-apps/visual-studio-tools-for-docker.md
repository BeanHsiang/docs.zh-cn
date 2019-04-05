---
title: Visual Studio Tools for Windows 上的 Docker
description: 初步了解 Visual Studio 2017 版本 15.7 及更高版本中提供的 Docker 工具。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.custom: vs-dotnet
ms.openlocfilehash: 431a0f34ba913c18c35e28ca45660495403bf688
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57844244"
---
# <a name="use-docker-tools-in-visual-studio-2017-on-windows"></a>在 Windows 上的 Visual Studio 2017 中使用 Docker 工具

开发人员工作流时使用 Docker 工具包含在 Visual Studio 2017 版本 15.7 及更高版本，是类似于使用 Visual Studio Code 和 Docker CLI （实际上，它基于相同的 Docker CLI），但它是更轻松地开始，可以简化过程、 和提供了提高工作效率生成、 运行和组合任务。 它还可以运行和调试你的容器通过常用`F5`和`Ctrl+F5`Visual Studio 中的密钥。 如果在同一个定义了其容器，甚至可以调试整个解决方案`docker-compose.yml`解决方案级文件。

## <a name="configure-your-local-environment"></a>配置在本地环境

使用 Docker 的 Windows 的最新版本，它是比以往要开发 Docker 应用程序的以下参考中所述，安装程序非常简单，因为更容易。

> [!TIP]
> 若要了解有关安装 Windows 的 Docker 的详细信息，请转到 (<https://docs.docker.com/docker-for-windows/>)。

## <a name="docker-support-in-visual-studio-2017"></a>Visual Studio 2017 中的 docker 支持

有两个级别的可以向项目添加 Docker 支持。 在 ASP.NET Core 项目中，您可以只需添加`Dockerfile`项目，方法是启用 Docker 支持的文件。 下一级别是容器业务流程支持，这会增加`Dockerfile`到项目 （如果它尚不存在） 和一个`docker-compose.yml`解决方案级文件。 默认情况下，在 Visual Studio 2017 版本 15.0 到 15.7 中添加容器业务流程支持，通过 Docker Compose。 容器业务流程支持是在 Visual Studio 2017 版本 15.8 或更高版本中选择的功能。 版本 15.8 的更高版本支持 Docker Compose 和 Service Fabric。

**添加 > Docker 支持**并**添加 > 容器业务流程协调程序支持**命令位于中的 ASP.NET Core 项目的项目节点的右键单击菜单 （或上下文菜单） 上**解决方案资源管理器**，如图 4-31 所示：

![在 Visual Studio 中添加 Docker 支持菜单选项](./media/add-docker-support-menu.png)

**图 4-31**。 向 Visual Studio 2017 项目添加 Docker 支持

### <a name="add-docker-support"></a>添加 Docker 支持

可以通过选择向现有的 ASP.NET Core 项目添加 Docker 支持**外** > **Docker 支持**中**解决方案资源管理器**。 您还可以启用 Docker 支持在项目创建期间通过选择**启用 Docker 支持**中**新的 ASP.NET Core Web 应用程序**在单击后打开的对话框**确定**中**新建项目**对话框中，图 4-32 所示。

![在 Visual Studio 中的新 ASP.NET Core web 应用的启用 Docker 支持](./media/enable-docker-support-visual-studio.png)

**图 4-32**。 Visual Studio 2017 中的项目创建过程中启用 Docker 支持

在添加或启用 Docker 支持，Visual Studio 添加*Dockerfile*到项目文件。

> [!NOTE]
> 图 4-33 所示，可以在 ASP.NET 项目 (.NET Framework，.NET Core 项目) 的项目创建期间启用 Docker Compose 支持，还添加容器业务流程支持。

![启用 Docker compose 的 ASP.NET 项目的支持](media/enable-docker-compose-support.png)

**图 4-33**。 在 Visual Studio 2017 中的 ASP.NET 项目的启用 Docker Compose 支持

### <a name="add-container-orchestration-support"></a>添加容器业务流程的支持

当你想要编写多容器解决方案时，请向项目添加容器业务流程支持。 这样就可以运行和调试容器 （整个解决方案） 的一组在同一时间，如果在同一个定义*docker compose.yml*文件。

若要添加容器业务流程支持，请右键单击中的解决方案或项目节点**解决方案资源管理器**，然后选择**添加 > 容器业务流程支持**。 然后选择**Docker Compose**或**Service Fabric**管理容器。

将容器业务流程支持添加到你的项目后，你将看到添加到项目中的 Dockerfile 和一个**docker compose**添加到解决方案中的文件夹**解决方案资源管理器**，如图 4-34 中所示：

![在解决方案资源管理器在 Visual Studio 中的 docker 文件](media/docker-support-solution-explorer.png)

**图 4-34**。 在 Visual Studio 2017 中的解决方案资源管理器中的 docker 文件

如果*docker compose.yml*已存在，Visual Studio 只需向其添加的配置代码所需的行。

## <a name="configure-docker-tools"></a>配置 Docker 工具

从主菜单中，选择**工具 > 选项**，然后展开**容器工具 > 设置**。 显示容器工具设置。

![Visual Studio Docker 工具选项，显示：自动拉取所需的 Docker 图像在项目负载上、 在后台自动启动容器、 自动终止上关闭，解决方案的容器和不提示信任 SSL 证书。](./media/visual-studio-docker-tools-options.png)

**图 4-35**。 Docker 工具选项

下表可能会帮助你决定如何设置这些选项。

| name | 默认设置 | 适用于 | 描述 |
| -----|:---------------:|:----------:| ----------- |
| 自动在项目负载上拉取所需的 Docker 图像 | On | Docker Compose | 为了加快运行速度加载项目时，Visual Studio 会启动 Docker pull 操作在后台，以便准备好运行你的代码时，该图像已下载或下载过程中。 如果只是加载项目，并浏览代码，您可以关闭此以避免下载不需要的容器映像。 |
| 在后台自动启动容器 | On | Docker Compose | 再次以提高性能，Visual Studio 创建一个容器使用卷装载供当生成并运行你的容器。 如果你想要控制创建容器时，关闭此功能。 |
| 在解决方案上的终止容器自动关闭 | On | Docker Compose | 关闭此功能如果您想要为解决方案之后关闭解决方案或关闭 Visual Studio 继续运行的容器。 |
| 不提示信任 localhost SSL 证书 | Off | ASP.NET Core 2.1 项目 | 如果不信任 localhost SSL 证书，则 Visual Studio 将提示每次运行你的项目，除非选中此复选框。 |

> [!WARNING]
> 如果 localhost SSL 证书不受信任，并选中复选框后，若要禁止显示提示，然后 HTTPS web 请求可能会在你的应用程序或服务中的运行时失败。 在这种情况下，取消选中**不会提示**复选框，会运行你的项目，并指示在提示符下的信任。

> [!TIP]
> 有关服务实现和使用的 Visual Studio Tools for Docker 的详细信息，请阅读以下文章：
>
>在本地 Docker 容器中调试应用程序： <https://docs.microsoft.com/azure/vs-azure-tools-docker-edit-and-refresh>
>
>将 ASP.NET 容器部署到使用 Visual Studio 的容器注册表： <https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker>

>[!div class="step-by-step"]
>[上一页](docker-apps-inner-loop-workflow.md)
>[下一页](set-up-windows-containers-with-powershell.md)
