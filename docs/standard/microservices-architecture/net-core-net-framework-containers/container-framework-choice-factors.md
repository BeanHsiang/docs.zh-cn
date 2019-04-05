---
title: 决策表。 用于 Docker 的 .NET Framework
description: 适用于容器化 .NET 应用程序的 .NET 微服务体系结构 | 决策表，用于 Docker 的 .NET Framework
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/11/2018
ms.openlocfilehash: 8044e3064ac372750c174d8b47c3f7a63d6bbd0b
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53149050"
---
# <a name="decision-table-net-frameworks-to-use-for-docker"></a>决策表：用于 Docker 的 .NET Framework

下列决策表汇总了是使用 .NET Framework 还是 .NET Core。 请记住，对于 Linux 容器，你需要基于 Linux 的 Docker 主机（VM 或服务器）；对于 Windows 容器，你需要基于 Windows Server 的 Docker 主机（VM 或服务器）。

> [!IMPORTANT]
> 开发计算机将运行一个 Docker 主机，Linux 或 Windows 均可。 想在一个解决方案中一起运行和测试的相关微服务都需要在同一容器平台上运行。

<table>
<thead>
<tr class="header">
<th><strong>体系结构/应用类型</strong></th>
<th><strong>Linux 容器</strong></th>
<th><strong>Windows 容器</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>容器上的微服务</td>
<td>.NET Core</td>
<td>.NET Core</td>
</tr>
<tr class="even">
<td>单一应用程序</td>
<td>.NET Core</td>
<td><p>.NET Framework</p>
<p>.NET Core</p></td>
</tr>
<tr class="odd">
<td>一流性能和可扩展性</td>
<td>.NET Core</td>
<td>.NET Core</td>
</tr>
<tr class="even">
<td>到容器的 Windows Server 旧应用程序（“棕色字段”）迁移</td>
<td>--</td>
<td>.NET Framework</td>
</tr>
<tr class="odd">
<td>基于容器的新开发（“绿色字段”）</td>
<td>.NET Core</td>
<td>.NET Core</td>
</tr>
<tr class="even">
<td>ASP.NET Core</td>
<td>.NET Core</td>
<td><p>.NET Core（推荐）</p>
<p>.NET Framework</p></td>
</tr>
<tr class="odd">
<td>ASP.NET 4（MVC 5、Web API 2 和 Web 窗体）</td>
<td>--</td>
<td>.NET Framework</td>
</tr>
<tr class="even">
<td>SignalR 服务</td>
<td>.NET Core 2.1 或更高版本</td>
<td><p>.NET Framework</p>
<p>.NET Core 2.1 或更高版本</p></td>
</tr>
<tr class="odd">
<td>WCF、WF 和其他旧框架</td>
<td>.NET Core 中的 WCF（仅 WCF 客户端库）</td>
<td><p>.NET Framework</p>
<p>.NET Core 中的 WCF（仅 WCF 客户端库）</p></td>
</tr>
<tr class="even">
<td>Azure 服务的消耗</td>
<td><p>.NET Core</p>
<p>（最终所有 Azure 服务都将为 .NET Core 提供客户端 SDK）。</p></td>
<td><p>.NET Framework</p>
<p>.NET Core</p>
<p>（最终所有 Azure 服务都将为 .NET Core 提供客户端 SDK）。</p></td>
</tr>
</tbody>
</table>

>[!div class="step-by-step"]
>[上一页](net-framework-container-scenarios.md)
>[下一页](net-container-os-targets.md)