---
title: 构建 ASP.NET Core 2.1 应用程序部署到 AKS/Kubernetes 群集与 Linux 容器
description: 使用 Microsoft 平台和工具的容器化 Docker 应用程序的生命周期
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/25/2019
ms.openlocfilehash: c6d778d345466b1b852d06bc01ce40ccfdebf964
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57676650"
---
# <a name="build-aspnet-core-21-applications-deployed-as-linux-containers-into-an-akskubernetes-orchestrator"></a>构建 ASP.NET Core 2.1 应用程序与 Linux 容器部署到 AKS/Kubernetes 业务流程协调程序

Azure Kubernetes 服务 (AKS) 是 Azure 的托管的 Kubernetes 业务流程服务可简化容器部署和管理。

AKS 主要功能如下：

- Azure 托管的控制平面
- 自动的升级
- 自我修复
- 用户可配置缩放
- 简单的用户体验的开发人员和群集操作员。

下面的示例探索的 ASP.NET Core 2.1 应用程序在 Linux 上运行并完成开发时，将部署到 AKS 群集在 Azure 中，创建使用 Visual Studio 2017。

## <a name="creating-the-aspnet-core-21-project-using-visual-studio-2017"></a>创建 ASP.NET Core 2.1 项目使用 Visual Studio 2017

ASP.NET Core 是由 Microsoft 和 GitHub 上的.NET 社区维护一个通用开发平台。 它是跨平台，支持 Windows、 macOS 和 Linux，并且可以用在设备、 云和嵌入式 /iot 方案。

此示例使用一个简单的项目的 Visual Studio Web API 模板，因此您无需任何其他的知识来创建此示例为基础的。 只需使用一个包含所有要使用 REST API，使用 ASP.NET Core 2.1 技术运行一个小的项目的元素的标准模板创建项目。

![在 Visual Studio 中，选择 ASP.NET Core Web 应用程序中添加新项目窗口。](media/create-aspnet-core-application.png)

**图 4-36**。 创建 ASP.NET Core 应用程序

若要在 Visual Studio 中创建示例项目，选择**文件** > **新建** > **项目**，选择**Web**项目类型的左窗格中后, 跟**ASP.NET Core Web 应用程序**。

Visual Studio 列出了 web 项目的模板。 对于本示例中，选择**API**创建 ASP.NET Web API 应用程序。

验证已选择 ASP.NET Core 2.1 作为框架。 .NET core 2.1 中的最后一个版本的 Visual Studio 2017 包含和自动安装和安装 Visual Studio 2017 时为你配置。

![Visual Studio 对话框用于选择的 API 选项中选择的 ASP.NET Core Web 应用程序的类型。](media/create-web-api-application.png)

**图 4 37**。 选择 ASP.NET CORE 2.1 和 Web API 项目类型

如果有任何以前版本的.NET Core，您可以下载并安装中的 2.1 版本<https://www.microsoft.com/net/download/core#/sdk>。

创建项目时，可以添加 Docker 支持或之后，因此您可以 Docker 项目在任何时间。 若要创建项目后添加 Docker 支持，请右键单击解决方案资源管理器中的项目节点并选择**外** > **Docker 支持**上下文菜单上。

![若要向现有项目添加 Docker 支持的上下文菜单选项：右键单击 （项目） > 添加 > Docker 支持。](media/add-docker-support-to-project.png)

**图 4-38**。 向现有项目添加 Docker 支持

若要完成添加 Docker 支持，可以选择 Windows 或 Linux。 在这种情况下，选择**Linux**，这是因为 AKS 不支持 Windows 容器 （作为后期 2018)。

![选项对话框，可选择目标 OS 的 Dockerfile。](media/select-linux-docker-support.png)

**图 4-39**。 选择 Linux 容器。

使用这些简单的步骤，可以在 Linux 容器上运行 ASP.NET Core 2.1 应用程序。

正如您所看到的 Visual Studio 2017 和 Docker 之间的集成是完全面向开发人员工作效率。

现在可以运行应用程序**F5**密钥或通过使用**播放**按钮。

在运行该项目之后, 可以列出使用的映像`docker images`命令。 应会看到`mssampleapplication`创建自动部署我们的项目使用 Visual Studio 2017 的映像。

```console
docker images
```

![控制台输出 docker 映像命令，从显示的列表：存储库、 标记、 映像 ID、 Created （日期） 和大小。](media/docker-images-command.png)

**图 4-40**。 Docker 映像的视图

## <a name="register-the-solution-in-the-azure-container-registry"></a>在 Azure 容器注册表中注册解决方案

将图像上传到任何 Docker 注册表，如[Azure 容器注册表 (ACR)](https://azure.microsoft.com/services/container-registry/)或 Docker 中心，以便映像可以从该注册表部署到 AKS 群集。 在这种情况下，我们正在正在映像上载到 Azure 容器注册表。

### <a name="create-the-image-in-release-mode"></a>在发布模式下创建的映像

现在，我们将创建中的图像**发行**模式 （可用于生产） 更改为**发行**，如下所示图 4: 41，并像之前那样运行应用程序。

![工具栏在 VS 中的选项以在发布模式下生成。](media/select-release-mode.png)

**图 4: 41**。 选择发布模式下

如果您执行`docker image`命令，你将看到这两个映像创建，另一个用于`debug`，另一个用于`release`模式。

### <a name="create-a-new-tag-for-the-image"></a>为映像创建新标记

需要使用标记每个容器映像`loginServer`注册表的名称。 此标记用于路由时将容器映像推送到映像注册表。

您可以查看`loginServer`名称在 Azure 门户中，Azure 容器注册表中提取信息

![在右上角的 Azure 容器注册表名称，浏览器视图。](media/loginServer-name.png)

**图 4-42**。 注册表名称的视图

或通过运行以下命令：

```console
az acr list --resource-group MSSampleResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

![控制台输出从上面的命令。](media/az-cli-loginServer-name.png)

**图 4-43**。 获取使用 PowerShell 的注册表的名称

在这两种情况下，将获取的名称。 在本例中为`mssampleacr.azurecr.io`。

现在你可以标记该映像，采用最新映像 （版本映像），使用命令：

```console
docker tag mssampleaksapplication:latest mssampleacr.azurecr.io/mssampleaksapplication:v1
```

运行之后`docker tag`命令，列出与映像`docker images`命令，并且应可以看到具有新的标记的图像。

![控制台输出从 docker images 命令。](media/tagged-docker-images-list.png)

**图 4-44**。 带标记的图像的视图

### <a name="push-the-image-into-the-azure-acr"></a>将映像推送到 Azure ACR

将映像推送到 Azure ACR，使用以下命令：

```console
docker push mssampleacr.azurecr.io/mssampleaksapplication:v1
```

此命令需要一段时间上载图像，但在该过程为您提供反馈。

![控制台从 docker push 命令的输出： 显示了每个层的基于字符的进度条。](media/uploading-image-to-acr.png)

**图 4-45**。 将图像上传到 ACR

如下所示结果过程完成时应显示：

![控制台输出从 docker push 命令，完成后，显示所有层或多个节点。](media/uploading-docker-images-complete.png)

**图 4 46**。 节点视图

下一步是将容器部署到 AKS 的 Kubernetes 群集。 为此，需要一个文件 (**.yml 文件部署**) 包含以下：

```yml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: mssamplesbook
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: mssample-kub-app
    spec:
      containers:
        - mane: mssample-services-app
          image: mssampleacr.azurecr.io/mssampleaksapplication:v1
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
    name: mssample-kub-app
spec:
  ports:
    - name: http-port
      port: 80
      targetPort: 80
  selector:
    app: mssample-kub-app
  type: LoadBalancer
```

> [!NOTE]
> 使用 Kubernetes 部署的详细信息请参阅： <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>

现在您已基本准备好使用部署**Kubectl**，但首先必须获取到 AKS 群集使用此命令的凭据：

```console
az aks get-credentials --resource-group MSSampleResourceGroupAKS --name mssampleclusterk801
```

![控制台输出从上面的命令：合并"MSSampleK8Cluster 作为当前上下文中 /root/.kube/config](media/getting-aks-credentials.png)

**图 4-47**。 获取凭据

然后，使用`kubectl create`命令来启动部署。

```console
kubectl create -f mssample-deploy.yml
```

![控制台从上面的命令的输出:"mssamplesbook"创建部署。 服务"mssample-kub-"创建应用。](media/kubectl-create-command.png)

**图 4-48**。 将部署到 Kubernetes

部署完成后，可以使用你可以使用此命令按时间顺序访问的本地代理来访问 Kubernetes 控制台：

```console
az aks browse --resource-group MSSampleResourceGroupAKS --name mssampleclusterk801
```

并访问 url `http://127.0.0.1:8001`。

![Kubernetes 仪表板，显示部署、 Pod、 副本集和服务的浏览器视图。](media/kubernetes-cluster-information.png)

**图 4 49**。 查看 Kubernetes 群集的信息

现在可以使用 Linux 容器和 AKS Kubernetes 群集的 Azure 上部署的应用程序。 您可以访问您的应用程序浏览到你的服务，你可以从 Azure 门户获取的公共 IP。

> [!NOTE]
> 您可以了解如何在部分中创建此示例在 AKS 群集[**部署到 Azure Kubernetes 服务 (AKS)** ](deploy-azure-kubernetes-service.md)有关本指南。

>[!div class="step-by-step"]
>[上一页](set-up-windows-containers-with-powershell.md)
>[下一页](../docker-devops-workflow/index.md)
