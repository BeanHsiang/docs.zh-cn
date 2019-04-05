---
title: 安装F#
description: 了解如何安装F#根据你的环境。
ms.date: 08/28/2018
ms.openlocfilehash: 873d3021ba884ec81992469e5d0f3b7c18b1e0f4
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56975246"
---
# <a name="install-f"></a>安装 F\#

你可以安装F#在多个方面，具体取决于你的环境。

## <a name="install-f-with-visual-studio"></a>安装F#使用 Visual Studio

如果在下载[Visual Studio](https://visualstudio.microsoft.com/)第一次，它将首先安装 Visual Studio 安装程序。 安装程序安装在相应 SKU 的 Visual Studio。 如果你已安装，请单击**修改**。

接下来，您将看到工作负荷列表。 选择**ASP.NET 和 web 开发**哪一项将安装F#ASP.NET Core 项目的支持和.NET Core 支持。

接下来，单击**修改**右下角中。  这将安装所选的所有内容。 然后可以打开带有 Visual Studio 2017F#语言支持通过单击**启动**。

## <a name="install-f-with-visual-studio-for-mac"></a>安装F#使用 Visual Studio for Mac

F#在默认情况下安装[Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/)，无论哪种配置选择。

在安装完成后，选择"启动 Visual Studio"。 您还可以启动它通过 Finder 在 macOS 上。

## <a name="install-f-with-visual-studio-code"></a>安装F#使用 Visual Studio Code

您必须具有[安装 git](https://git-scm.com/download)且适用于你的路径以使项目模板使用。 你可以验证是否已正确安装通过键入`git --version`在命令提示符，然后按**Enter**。

### <a name="macostabmacos"></a>[macOS](#tab/macos)

[Mono](https://www.mono-project.com)用于[F#交互式](../tutorials/fsharp-interactive/index.md)支持。 通过 Homebrew 在 macOS 上安装 Mono 的最简单方法。 只需为你的终端中键入以下内容：

```console
brew install mono
```

此外安装[.NET Core SDK](https://www.microsoft.com/net/download)。

### <a name="linuxtablinux"></a>[Linux](#tab/linux)

[Mono](https://www.mono-project.com)用于[F#交互式](../tutorials/fsharp-interactive/index.md)支持。 如果您在 Debian 或 Ubuntu 上，可以使用以下：

```console
sudo apt-get update
sudo apt-get install mono-complete fsharp
```

此外安装[.NET Core SDK](https://www.microsoft.com/net/download)。

### <a name="windowstabwindows"></a>[Windows](#tab/windows)

安装[Visual Studio 中使用F#支持](#install-f-with-visual-studio)。 这将安装所有必要的组件来编写、 编译和执行F#代码。

此外安装[.NET Core SDK](https://www.microsoft.com/net/download/)。

---

然后，你将需要[Visual Studio Code](https://code.visualstudio.com)安装。

接下来，请单击扩展图标并搜索"Ionide":

唯一的插件所需的F#支持在 Visual Studio Code [ionide-fsharp](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp)。 但是，也可以安装[Ionide 虚设](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-FAKE)若要获取[FAKE](https://fsharp.github.io/FAKE/)支持并[Ionide paket 依存](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-Paket)获取[paket 依存](https://fsprojects.github.io/Paket/)支持。 虚设和 paket 依存是其他F#用于生成项目并分别管理依赖项的社区工具。
