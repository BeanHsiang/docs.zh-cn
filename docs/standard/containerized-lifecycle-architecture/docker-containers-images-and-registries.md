---
title: Docker 容器、映像和注册表
description: 了解注册表播放以 Docker 方式部署应用程序的整体的关键角色。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: e69490734a03cf58bf8534bc9e31110a11d44c58
ms.sourcegitcommit: 07c4368273b446555cb2c85397ea266b39d5fe50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2019
ms.locfileid: "56583311"
---
# <a name="docker-containers-images-and-registries"></a>Docker 容器、映像和注册表

使用 Docker 时，可以创建应用和服务并将它们及其依赖项打包到容器映像中。 映像是应用或服务及其配置和依赖项的静态表示形式。

若要运行应用或服务，应用的映像会被实例化，从而创建一个在 Docker 主机上运行的容器。 容器最初在开发环境或 PC 中进行测试。

在注册表中，作为映像库中存储图像。 需要注册表才可部署到生产协调程序。 Docker 通过 [Docker Hub](https://hub.docker.com/)维护一个公共注册表；其他供应商为不同映像集合提供注册表，包括 [Azure 容器注册表](https://azure.microsoft.com/services/container-registry/)。 或者，企业可以在本地为自己的 Docker 映像建立一个专用注册表。

图 1-4 显示了 Docker 中的映像和注册表如何与其他组件相关联。 图中还显示了供应商提供的多个注册表产品/服务。

![在 Docker 中的基本分类：注册表就像书架映像的存储，并可用于提取用于生成要运行服务或 web 应用容器。 有专用 Docker 注册表的本地和公有云上。 Docker 中心是由 Docker 维护的公共注册表，除了 Docker 信任的注册表（企业级解决方案），Azure 还提供了 Azure 容器注册表。 AWS、Google 和其他产品也有容器注册表。](./media/image4.png)

**图 1-4**。 Docker 术语和概念的分类

通过将图像放在注册表中，您可以存储静态和不可变的应用程序，包括所有依赖项，在框架级别。 然后，可在多个环境中对映像进行版本管理和部署，从而提供一致的部署单元。

无论是托管在本地还是托管在云中，在下列情况下都建议使用私有映像注册表：

- 由于保密性，映像不能被公开分享。

- 希望映像与所选部署环境之间的网络延迟最小。 例如，如果生产环境是 Azure，你可能想要存储在映像[Azure 容器注册表](https://azure.microsoft.com/services/container-registry/)，以便网络延迟很小。 同样，如果生产环境为本地，则你可能希望在同一本地网络中提供一个本地 Doker 可信注册表。

>[!div class="step-by-step"]
>[上一页](docker-terminology.md)
>[下一页](road-to-modern-applications-based-on-containers.md)
