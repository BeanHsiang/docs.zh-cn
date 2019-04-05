---
title: Docker 应用的内部循环开发工作流
description: 了解开发 Docker 应用程序的"内部循环"工作流。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 1ed0feeec682f5a79bc38db6a101b751ea4dbc3a
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57676663"
---
# <a name="inner-loop-development-workflow-for-docker-apps"></a>Docker 应用的内部循环开发工作流

触发跨越整个 DevOps 的外部循环工作流之前循环，开始整个过程的每个开发人员的计算机上，应用本身进行编码、 使用其首选的语言或平台，以及本地测试 (图 4-21)。 但在所有情况下，您必须很重要的一点共同点，无论选择何种语言、 框架或平台。 在此特定的工作流，你始终在开发和测试 Docker 容器，但却在本地。

![步骤 1-代码/运行/调试](./media/image18.png)

图 4-21。 内部循环开发上下文

容器或 Docker 映像的实例将包含这些组件：

-   选择 （例如，Linux 分发版或 Windows） 的操作系统

- 由开发人员 （例如，应用程序二进制文件） 添加的文件

-   配置 （例如，环境设置和依赖项）

- 哪些过程操作即可运行 Docker 的说明

您可以将设置为 （下一节中所述） 的过程中使用 Docker 的内部循环开发工作流。 考虑设置环境的初始步骤不包括在内，因为只需执行一次此操作。

## <a name="building-a-single-app-within-a-docker-container-using-visual-studio-code-and-docker-cli"></a>构建单个应用程序中使用 Visual Studio Code 和 Docker CLI 的 Docker 容器

应用是从你自己的服务和附加库 （依赖项） 组成。

图 4-22 显示了通常需要构建 Docker 应用程序后, 跟每个步骤的详细说明时要执行的基本步骤。

![工作流概述：步骤 1-代码中，第 2 步-编写 Dockerfile，第 3 步-创建映像的 Dockerfile，步骤 4 中使用定义-使用 docker-compose 文件，步骤 5-运行容器定义的服务或组合式的应用，第 6 步-测试应用程序，第 7 步-推送开始外部循环 （CI/CD 管道），或继续 developing。](./media/image19.png)

**图 4-22**。 使用 Docker CLI 适用于容器化 Docker 应用程序生命周期的高级工作流

### <a name="step-1-start-coding-in-visual-studio-code-and-create-your-initial-appservice-baseline"></a>步骤 1：开始在 Visual Studio Code 中编写代码并创建初始应用/服务基线

开发应用程序的方法是执行不带 Docker 的方式类似。 不同之处是，在开发时，你在部署和测试应用程序或服务 （如 Windows 或 Linux VM） 在本地环境中放置的 Docker 容器中运行。

**设置本地环境**

使用适用于 Mac 和 Windows 的 Docker 的最新版本，比以往要开发 Docker 应用程序更容易和安装程序非常简单。

> [!INFORMATION]
>
> 有关 Docker 的 Windows 设置的说明，请转到<https://docs.docker.com/docker-for-windows/>。
>
>有关设置 Docker for Mac 的说明，请转到<https://docs.docker.com/docker-for-mac/>。

此外，还需要代码编辑器，以便您可以实际开发正在使用 Docker CLI 的应用程序。

Microsoft 提供了 Visual Studio Code 中，这是一个轻量级代码编辑器，支持在 Mac、 Windows、 和 Linux，并提供与 IntelliSense[支持多种语言](https://code.visualstudio.com/docs/languages/overview)(JavaScript、.NET、 Go、 Java、 Ruby、 Python 和大部分现代语言）、[调试](https://code.visualstudio.com/Docs/editor/debugging)，[与 Git 集成](https://code.visualstudio.com/Docs/editor/versioncontrol)并[扩展插件支持](https://code.visualstudio.com/docs/extensions/overview)。 此编辑器是非常适合用于 Mac 和 Linux 的开发人员。 在 Windows 中，您还可以使用完整的 Visual Studio 应用程序。

> [!INFORMATION]
>
> 有关安装 Visual Studio 代码的 Windows、 Mac 或 Linux 的说明，请转到<https://code.visualstudio.com/docs/setup/setup-overview/>。
>
> 有关设置 Docker for Mac 的说明，请转到<https://docs.docker.com/docker-for-mac/>。

可以使用 Docker CLI 和写入你的代码使用任何代码编辑器中，但 Docker 扩展中使用 Visual Studio Code，可轻松作者`Dockerfile`和`docker-compose.yml`工作区中的文件。 您还可以从 Visual Studio 代码 IDE 执行 Docker 命令使用 Docker CLI 下运行的任务和脚本。

适用于 VS Code 的 Docker 扩展提供了以下功能：

- 自动`Dockerfile`和`docker-compose.yml`文件生成

- 语法突出显示并将鼠标悬停提示`docker-compose.yml`和`Dockerfile`文件

- （完成） 适用于 IntelliSense`Dockerfile`和`docker-compose.yml`文件

- Linting （错误和警告） 的`Dockerfile`文件

- 最常见的 Docker 命令的命令面板 (F1) 集成

- 用于管理映像和容器的资源管理器集成

- 部署到 Azure 应用服务从 DockerHub 和 Azure 容器注册表的映像

若要安装 Docker 扩展，按 Ctrl + Shift + P，键入`ext install`，然后运行安装扩展命令以打开 Marketplace 扩展列表。 接下来，键入**docker**对结果进行筛选，然后选择 Docker 支持扩展中，如下图所示图 4-23。

![VS Code 的 Docker 扩展视图。](./media/image20.png)

图 4-23。 在 Visual Studio Code 中安装 Docker 扩展

### <a name="step-2-create-a-dockerfile-related-to-an-existing-image-plain-os-or-dev-environments-like-net-core-nodejs-and-ruby"></a>步骤 2：创建到现有映像 （普通 OS 或开发环境，如.NET Core、 Node.js 和 Ruby） 相关的 DockerFile

你将需要`DockerFile`每个要生成的自定义映像和每个要部署的容器。 如果您的应用程序由一个自定义服务组成，则需要将单个`DockerFile`。 但是如果您的应用程序组成 （如中所示的微服务体系结构） 的多个服务，您将需要一个`Dockerfile`每个服务。

`DockerFile`通常位于应用或服务的根文件夹中并包含所需的命令，以便 Docker 知道如何设置和运行该应用程序或服务。 可以创建你`DockerFile`并将其添加到你的项目以及你的代码 (.NET Core、 node.js 等)，或者，如果您是初次接触环境，请看看以下提示。

> [!TIP]
>
> 可以使用 Docker 扩展时使用指导您`Dockerfile`和`docker-compose.yml`与 Docker 容器相关的文件。 最终，可能将编写这些种类的文件而无需此工具，但使用 Docker 扩展是很好的起点，可加快学习曲线。

在图 4 至 24 日，您可以看到如何 docker-compose 文件添加通过使用适用于 VS Code Docker 扩展。

![用于 VS Code Docker 扩展控制台视图。](./media/image24.png)

图 4-24。 添加使用 docker 文件**添加 Docker 文件复制到工作区命令**

当添加 DockerFile 时，指定要使用的基础 Docker 映像 (如使用`FROM microsoft/aspnetcore`)。 你通常将生成自定义映像从在任何官方存储库获取的基本映像之上[Docker Hub 注册表](https://hub.docker.com/)(如[适用于.NET Core 映像](https://hub.docker.com/r/microsoft/dotnet/)或一个[适用于 Node.js](https://hub.docker.com/_/node/)).

***使用现有的官方 Docker 映像***

语言堆栈的官方存储库中使用版本号可确保相同的语言功能 （包括开发、 测试和生产） 的所有计算机上可用。

下面是.NET Core 容器的示例 DockerFile:

```Dockerfile
# Base Docker image to use  
FROM microsoft/dotnet:2.1-aspnetcore-runtime
  
# Set the Working Directory and files to be copied to the image  
ARG source  
WORKDIR /app  
COPY ${source:-bin/Release/PublishOutput} .  
  
# Configure the listening port to 80 (Internal/Secured port within Docker host)  
EXPOSE 80  
  
# Application entry point  
ENTRYPOINT ["dotnet", "MyCustomMicroservice.dll"]
```

在这种情况下，映像基于根据行的官方 ASP.NET Core Docker 映像 （多体系结构适用于 Linux 和 Windows），版本 2.1 `FROM microsoft/dotnet:2.1-aspnetcore-runtime`。 (有关此主题的详细信息，请参阅[ASP.NET Core Docker 映像](https://hub.docker.com/r/microsoft/aspnetcore/)页并[.NET Core Docker 映像](https://hub.docker.com/r/microsoft/dotnet/)页)。

在 DockerFile，还可以指示 Docker 侦听在运行时 （如端口 80） 将使用的 TCP 端口。

可在 Dockerfile 中指定其他配置设置，具体取决于使用的语言和框架。 例如，`ENTRYPOINT`行与`["dotnet", "MySingleContainerWebApp.dll"]`指示 Docker 运行.NET Core 应用程序。 如果在使用 SDK 和.NET Core CLI (`dotnet CLI`) 生成并运行.NET 应用程序，此设置会有所不同。 此处的关键点是 ENTRYPOINT 行和其他设置的依赖于为应用程序选择的语言和平台。

> [!INFORMATION]
>
> 有关生成.NET Core 应用程序的 Docker 映像的详细信息，请转到<https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images>。
>
> 若要了解有关构建你自己的映像的详细信息，请转到<https://docs.docker.com/engine/tutorials/dockerimages/>。

**使用多体系结构映像存储库**

存储库中的单一映像名称可以包含平台变量，如 Linux 映像和 Windows 映像。 此功能允许 Microsoft （基础映像创建者） 等供应商创建涵盖多个平台 （Linux 和 Windows） 的单个存储库。 例如， [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) Docker 中心注册表中的可用存储库使用的同一映像名称提供适用于 Linux 和 Windows Nano Server 的支持。

拉取[microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/)映像从 Windows 主机拉取 Windows 变体，而从 Linux 主机拉取同一映像名称拉取 Linux 变体。

***从头开始创建您的基础映像***

您可以从头开始创建您自己的 Docker 基础映像在此所述[一文](https://docs.docker.com/engine/userguide/eng-image/baseimages/)从 Docker。 如果你刚开始使用 Docker，但如果你想要设置的基础映像的特定位，您可以执行此操作，这种情况下可能不是最适合您。

### <a name="step-3-create-your-custom-docker-images-embedding-your-service-in-it"></a>步骤 3：创建自定义 Docker 映像中嵌入你的服务

对于每个包含您的应用程序的自定义服务，你将需要创建一个相关的映像。 如果您的应用程序由单个服务或 web 应用的组成，将需要一个映像。

> [!NOTE]
>
> 每当你将源代码推送到 Git 存储库 （持续集成），以便将该全局环境中创建映像从时考虑到"外部循环 DevOps 工作流"，将通过自动的生成过程中创建映像应用源代码。
>
> 但我们考虑转到该外部循环路由之前，我们需要确保，Docker 应用程序工作正常，以便它们不推送到源代码管理系统 （Git 等） 可能无法正常工作的代码。
>
> 因此，每个开发人员首先需要执行整个的内部循环过程，以在本地测试，继续开发直到他们想要推送完整的功能或将更改为源代码管理系统。

若要在本地环境和使用 DockerFile 创建映像，您可以使用 docker 生成命令，在图 4-25 所示 (还可以运行`docker-compose up --build`的应用程序由多个容器/服务)。

![Docker-compose build，显示下载进度的映像的控制台输出。](./media/image25.png)

图 4-25。 正在运行的 docker 生成

（可选） 而不是直接运行`docker build`项目文件夹中，首先可以从生成的可部署文件夹使用运行所需的.NET 库`dotnet publish`命令，然后再运行`docker build`。

此示例中使用的名称创建 Docker 映像`cesardl/netcore-webapi-microservice-docker:first`(`:first`一个标记，如特定版本)。 可能需要此步骤中的每个自定义映像需要创建组合 Docker 应用程序与多个容器。

你可以找到现有的映像在本地存储库中 （在开发计算机） 使用 docker 映像命令，在图 4-26 所示。

![控制台输出中显示现有的映像的命令 docker 图像。](./media/image26.png)

**图 4-26**。 查看现有的映像使用的 docker 映像

### <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-composed-docker-app-with-multiple-services"></a>步骤 4：生成包含多个服务的组合的 Docker 应用程序时在 docker-compose.yml 中定义服务

使用`docker-compose.yml`文件中，可以定义一组相关服务部署为组合应用程序与下一步的步骤部分所述的部署命令。

创建该文件在主或根解决方案文件夹;它应该类似于在此显示内容`docker-compose.yml`文件：

```yml
version: '3.4'
services:
  web:
    build: .
    ports:
     - "81:80"
    volumes:
     - .:/code
    depends_on:
     - redis
  redis:
    image: redis
```

在此特定情况下，此文件定义两个服务： web 服务 （自定义的服务） 和 redis 服务 （受欢迎的缓存服务）。 每个服务将部署为一个容器，因此我们需要为每个使用具体的 Docker 映像。 对于此特定的 web 服务，该映像将需要执行以下操作：

- 中的当前目录中的 DockerFile 生成

- 转发的公开的端口 80 上向主机计算机上的端口 81 容器

- 到 /code 在容器中，使你能够修改代码，而无需重新生成映像可能在主机上装载项目目录

- Web 服务链接到 redis 服务

Redis 服务使用[最新的公共 redis 映像](https://hub.docker.com/_/redis/)从 Docker 中心注册表中拉取。 [redis](https://redis.io/)是用于服务器端应用程序的受欢迎的缓存。

### <a name="step-5-build-and-run-your-docker-app"></a>步骤 5：生成并运行 Docker 应用

如果您的应用程序具有单个容器，只需通过将其部署到 Docker 主机 （VM 或物理服务器） 运行。 但是，如果您的应用程序由多个服务组成，则需要*compose 它*、 过。 让我们查看不同的选项。

***选项 a:运行单个容器或服务***

可以通过使用 docker 运行命令，如下所示运行 Docker 映像：

```console
docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

为此特定部署中，我们将重定向请求发送到端口 80 到内部端口 5000。 现在该应用程序侦听的外部端口 80 主机级别。

***选项 b:编写和运行多容器应用程序***

在大多数企业方案中，将多个服务组成的 Docker 应用程序。 对于这些情况下，可以运行`docker-compose up`命令 (图 4-27)，将使用可能在之前创建的 docker-compose.yml 文件。 运行此命令将部署及其相关容器的所有组合应用程序。

![控制台输出中的的 docker-compose up 命令。](./media/image27.png)

**图 4-27**。 运行"docker compose up"命令的结果

在您运行`docker-compose up`，部署你的应用程序和其相关的容器到 Docker 主机，如图 4-28 所示的 VM 表示形式。

![运行多容器应用程序的虚拟机。](./media/image28.png)

**图 4-28**。 部署了 Docker 容器的 VM

### <a name="step-6-test-your-docker-application-locally-in-your-local-cd-vm"></a>步骤 6：测试 Docker 应用程序 （在本地，本地 CD VM)

根据您的应用程序正在执行什么操作，此步骤会有所不同。

在简单.NET Core Web API"Hello World"部署为单个容器或服务，只需要通过提供的 DockerFile 中指定的 TCP 端口来访问该服务。

如果 localhost 未开启，若要导航到你的服务，通过使用此命令为机查找 IP 地址：

```console
docker-machine {IP} {YOUR-CONTAINER-NAME}
```

在 Docker 主机上，打开浏览器并导航到该站点;您应该看到你的应用/服务运行，在图 4-29 所示。

![来自 localhost/API/values 的响应的浏览器视图。](./media/image29.png)

**图 4-29**。 测试 Docker 应用程序使用 localhost 在本地

请注意，则使用端口 80，但在内部它将被重定向到端口 5000，因为这是使用的部署方式`docker run`，如前面所述。

您可以从终端使用 CURL 进行测试。 在 Windows 上的 Docker 安装，默认 IP 是为 10.0.75.1，如下图中图 4-30 所示。

![控制台输出中获取 http://10.0.75.1/API/values使用 curl](./media/image30.png)

**图 4-30**。 通过使用 CURL 在本地测试 Docker 应用程序

**调试在 Docker 上运行的容器**

Visual Studio Code 支持调试 Docker，如果您使用的 Node.js 和其他平台，如.NET Core 容器。

您还可以调试在 Docker 中的.NET Core 或.NET Framework 的容器时使用 Visual Studio 的 Windows 或 Mac 下, 一节中所述。

> [!INFORMATION]
>
> 若要了解有关调试 Node.js Docker 容器的详细信息，请转到<https://blog.docker.com/2016/07/live-debugging-docker/>和<https://blogs.msdn.microsoft.com/user_ed/2016/02/27/visual-studio-code-new-features-13-big-debugging-updates-rich-object-hover-conditional-breakpoints-node-js-mono-more/>。

>[!div class="step-by-step"]
>[上一页](docker-apps-development-environment.md)
>[下一页](visual-studio-tools-for-docker.md)
