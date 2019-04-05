---
title: 为 Docker 容器选择 .NET Core 还是 .NET Framework
description: 适用于容器化 .NET 应用程序的 .NET 微服务体系结构 | 为 Docker 容器选择 .NET Core 还是 .NET Framework
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/11/2018
ms.openlocfilehash: e71739b06275d4ee786d246004930d7b66fbc72b
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53151416"
---
# <a name="choosing-between-net-core-and-net-framework-for-docker-containers"></a>为 Docker 容器选择 .NET Core 还是 .NET Framework

通过 .NET 生成服务器端容器化 Docker 应用程序时，有两种支持的框架：[.NET Framework 和 .NET Core](https://www.microsoft.com/net/download)。 这两者共享许多 .NET 平台组件，可在它们之间共享代码。 但两者之间存在根本差异，可根据需要实现的目标选择框架。 本节提供有关何时选择各框架的指南。

>[!div class="step-by-step"]
>[上一页](../container-docker-introduction/docker-containers-images-registries.md)
>[下一页](general-guidance.md)