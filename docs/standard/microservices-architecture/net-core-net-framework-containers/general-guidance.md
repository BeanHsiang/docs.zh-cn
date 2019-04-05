---
title: 通用指南
description: 适用于容器化 .NET 应用程序的 .NET 微服务体系结构 | 通用指南
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/11/2018
ms.openlocfilehash: 6ff6170fd1cdd0c69ecc8729cc8199cceea43ffa
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53128474"
---
# <a name="general-guidance"></a>通用指南

本部分提供有关何时选择 .NET Core 或 .NET Framework 的总结。 后面各部分将提供对上述选择的详细介绍。

将 .NET Core 与 Linux 或 Windows 容器结合使用并用于容器化 Docker 服务器应用程序的适用情况：

-   用户有跨平台需求。 例如，想同时使用 Linux 和 Windows 容器。

-   应用程序体系结构基于微服务。

-   需快速启动容器且每个容器内存占用较小，以实现更好的密度，或每个硬件单位中的容器较多，以降低成本。

简单地说，在创建新的容器化 .NET 应用程序时，应考虑将 .NET Core 作为默认选择。 它具有许多好处，并最匹配容器的基本原理和运行方式。

使用 .NET Core 的另一个好处是可在同一台计算机中并行运行 .NET 版本的应用程序。 这一优势对于不使用容器的服务器或虚拟机而言更为重要，因为容器会隔离应用所需的 .NET 版本。 （只要它们与基础操作系统兼容。）

在以下情况下，应将 .NET Framework 用于容器化 Docker 服务器应用程序：

-   应用程序当前使用 .NET Framework 并在 Windows 上具有强依赖关系。

-   需要使用 .NET Core 不支持的 Windows API。

-   用户需要使用不可用于 .NET Core 的第三方 .NET 库或 NuGet 包。

在 Docker 上使用.NET Framework 可通过最大限度地减少部署问题来提升部署体验。 此[“提升和移动”方案](https://aka.ms/liftandshiftwithcontainersebook)对于针对最初使用传统 .NET Framework（如 ASP.NET WebForms、MVC Web 应用或 WCF (Windows Communication Foundation) 服务）开发的旧应用程序实施容器化而言很重要。

### <a name="additional-resources"></a>其他资源

-   **电子书：使用 Azure 和 Windows 容器更新现有 .NET Framework 应用程序**  
    https://aka.ms/liftandshiftwithcontainersebook

-   **示例应用：使用 Windows 容器更新旧的 ASP.NET Web 应用**  
    https://aka.ms/eshopmodernizing

>[!div class="step-by-step"]
>[上一页](index.md)
>[下一页](net-core-container-scenarios.md)