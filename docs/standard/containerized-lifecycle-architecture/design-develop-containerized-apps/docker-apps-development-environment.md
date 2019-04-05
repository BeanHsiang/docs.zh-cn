---
title: Docker 应用的开发环境
description: 初步了解支持 Docker 开发生命周期的最重要的开发工具选项。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 02/15/2019
ms.openlocfilehash: 38a9f8209200635c752f60af90e22ef916796525
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57677235"
---
# <a name="development-environment-for-docker-apps"></a>Docker 应用的开发环境

## <a name="development-tools-choices-ide-or-editor"></a>开发工具选择：IDE 或编辑器

无论如果更喜欢完整且功能强大的 IDE 或轻巧便捷编辑器，Microsoft 拥有你的需求时涉及到开发 Docker 应用程序。

### <a name="visual-studio-code-and-docker-cli-cross-platform-tools-for-mac-linux-and-windows"></a>Visual Studio Code 和 Docker CLI （适用于 Mac、 Linux 和 Windows 的跨平台工具）

如果你更青睐支持任何开发语言的轻型、 跨平台编辑器，可以使用 Visual Studio Code 和 Docker CLI。 这些产品提供简单而稳定可靠的体验，这很关键的简化开发人员工作流。 通过安装"Docker for Mac"或"Docker 的 Windows"（开发环境），Docker 开发人员可以使用单个 Docker CLI 为 Windows 或 Linux （运行时环境） 构建应用程序。 此外，Visual Studio Code 支持适用于 Dockerfile 和快捷任务以在编辑器中运行 Docker 命令的 IntelliSense 使用的 Docker 扩展。

> [!NOTE]
>
> 若要下载 Visual Studio Code，请转到<https://code.visualstudio.com/download>。
>
> 若要下载适用于 Mac 和 Windows 的 Docker，请转到<https://www.docker.com/products/docker>。

### <a name="visual-studio-with-docker-tools-windows-development-machine"></a>Visual Studio 中使用 Docker 工具 （Windows 开发计算机）

我们建议你使用 Visual Studio 2017 （或更高版本） 启用的内置 Docker 工具。 使用 Visual Studio 可以开发、 运行和验证应用程序直接在所选的 Docker 环境中。 按 F5 调试应用程序 （单个容器或多个容器） 直接在 Docker 主机时，或按 Ctrl + F5 编辑和刷新应用，而无需重新生成容器。 Windows 开发人员能够创建适用于 Linux 或 Windows 的 Docker 容器的最简单且最强大选择它。

### <a name="visual-studio-for-mac-mac-development-machine"></a>Visual Studio for Mac （Mac 开发计算机）

可以使用[Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/)开发基于 Docker 的应用程序时。 Visual Studio for Mac 提供更丰富的 IDE 与 Visual Studio Code 相比 for mac。

## <a name="language-and-framework-choices"></a>选择语言和框架

你可以开发 Docker 应用程序使用 Microsoft 工具和大多数流行语言。 下面是一个初始的列表，但您并不仅限于它：

- .NET Core 和 ASP.NET Core
- Node.js
- 前往
- Java
- Ruby
- Python

基本上，您可以使用支持 Docker Linux 或 Windows 中的任何现代语言。

>[!div class="step-by-step"]
>[上一页](deploy-azure-kubernetes-service.md)
>[下一页](docker-apps-inner-loop-workflow.md)
