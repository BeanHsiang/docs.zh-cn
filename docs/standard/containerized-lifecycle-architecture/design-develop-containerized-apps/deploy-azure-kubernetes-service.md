---
title: 协调安排微服务和多容器应用程序，实现高可伸缩性和高可用性
description: 了解如何使用 Azure Kubernetes 服务部署应用。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 82a1cf7f3cc367bfb8b8f67a130600815f2a21c4
ms.sourcegitcommit: 2b986afe4ce9e13bbeec929c9737757eb61de60e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2019
ms.locfileid: "56664960"
---
# <a name="deploy-to-azure-kubernetes-service-aks"></a>将部署到 Azure Kubernetes 服务 (AKS)

可以与 AKS 使用您首选的客户端的操作系统进行交互，下面我们介绍如何使用 Microsoft Windows 和 Windows，在 Ubuntu Linux 的嵌入式的版本使用 Bash 命令。

使用 AKS 之前，有的先决条件是：

- Linux 或 Mac 开发计算机
- Windows 开发计算机
  - 在 Windows 上启用了开发人员模式
  - 适用于 Linux 的 Windows 子系统
- Azure CLI 上安装[Windows、 Mac 或 Linux](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)

> [!NOTE]
> 若要查找有关完整信息：
>
> Azure CLI: <https://docs.microsoft.com/cli/azure/index?view=azure-cli-latest>
>
> 适用于 Linux 的 Windows 子系统： <https://docs.microsoft.com/windows/wsl/about>

## <a name="create-the-aks-environment-in-azure"></a>在 Azure 中创建的 AKS 环境

有几种方法来创建 AKS 环境。 它可以通过使用 Azure CLI 命令或使用 Azure 门户完成。

这里，可以探讨一些示例使用 Azure CLI 创建群集和 Azure 门户以查看结果。 此外需要具有 Kubectl 和 Docker 在开发计算机。  

## <a name="create-the-aks-cluster"></a>创建 AKS 群集

创建 AKS 群集使用此命令：

```console
az aks create --resource-group MSSampleResourceGroup --name MSSampleClusterK801 --agent-count 1 --generate-ssh-keys --location westus2
```

创建作业完成后，可以看到在 Azure 门户中创建 AKS:

资源组中：

![Azure AKS 资源组的浏览器视图。](media/aks-resource-group-view.png)

**图 4-17**。 从 Azure AKS 资源组视图。

AKS 群集：

![AKS 资源组的浏览器视图。](media/aks-cluster-view.png)

**图 4-18**. 从 Azure AKS 视图。

你还可以查看使用创建的节点`Azure-CLI`和`Kubectl`。

首先，获取凭据：

```console
az aks get-credentials --resource-group MSSampleK8ClusterRG --name MSSampleK8Cluster
```

![控制台输出从上面的命令：合并"作为当前上下文中 /root/.kube/config MsSampleK8Cluster。](media/get-credentials-command-result.png)

**图 4-19**. `aks get-credentials` 命令的结果。

然后，从 Kubectl 获取节点：

```console
kubectl get nodes
```

![控制台输出通过命令：包括状态、 年龄 （运行的时间） 和版本的节点的列表](media/kubectl-get-nodes-command-result.png)

图 4-20。 `kubectl get nodes` 命令的结果。

>[!div class="step-by-step"]
>[上一页](orchestrate-high-scalability-availability.md)
>[下一页](docker-apps-development-environment.md)
