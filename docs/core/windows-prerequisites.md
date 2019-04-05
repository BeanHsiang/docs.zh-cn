---
title: Windows 上 .NET Core 的先决条件
description: 了解在 Windows 计算机上开发和运行 .NET Core 应用程序所需的依赖项。
ms.date: 12/14/2018
ms.openlocfilehash: 2209c6e74413204c38ba54ffc538846f27d0bdf6
ms.sourcegitcommit: 3d0c29b878f00caec288dfecb3a5c959de5aa629
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53656110"
---
# <a name="prerequisites-for-net-core-on-windows"></a>Windows 上 .NET Core 的先决条件

本文介绍在 Windows 上运行 .NET Core 应用程序所支持的 OS 版本。 支持的 OS 版本和依赖项适用于在 Windows 上开发 .NET Core 应用程序的三种方法：

* [命令行](tutorials/using-with-xplat-cli.md)
* [Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [Visual Studio Code](https://code.visualstudio.com/)

此外，如果你正在使用 Visual Studio 2017 开发 Windows，[使用 Visual Studio 2017 的先决条件](#prerequisites-with-visual-studio-2017)部分更详细地介绍了有关支持 .NET Core 开发的最小版本。

## <a name="net-core-supported-windows-versions"></a>支持 .NET Core 的 Windows 版本

以下版本支持 .NET Core：

* Windows 7 SP1
* Windows 8.1
* Windows 10 周年更新（版本 1607）或更高版本
* Windows Server 2008 R2 SP1（完全服务器或服务器核心）
* Windows Server 2012 SP1（完全服务器或服务器核心）
* Windows Server 2012 R2（完全服务器或服务器核心）
* Windows Server 2016 或更高版本（完全服务器、服务器核心或 Nano Server）

## <a name="net-core-supported-operating-systems"></a>.NET Core 支持的操作系统

以下文章提供了 .NET Core 针对每个版本所支持的操作系统的完整列表：

* [.NET Core 3.0（预览版）](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md)
* [.NET Core 2.2](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md)
* [.NET Core 2.1](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md)
* [.NET Core 1.0](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0-supported-os.md)

有关下载链接和详细信息，请参阅 [.NET 下载](https://dotnet.microsoft.com/download)下载最新版本或 [.NET 下载存档](https://dotnet.microsoft.com/download/archives#dotnet-core)下载较旧版本。

## <a name="net-core-dependencies"></a>.NET Core 依赖项

在早于 Windows 10 和 Windows Server 2016 的 Windows 版本上运行 .NET Core 1.1 及更低版本时，需要 Visual C++ Redistributable。 .NET Core 安装程序自动安装此依赖项。

如果出现以下情况，必须手动安装 [Microsoft Visual C++ 2015 Redistributable 更新 3](https://www.microsoft.com/download/details.aspx?id=52685)：

* 使用[安装程序脚本](./tools/dotnet-install-script.md)安装 .NET Core。
* 部署独立式 .NET Core 应用程序。
* 从源中生成产品。
* 通过 .zip 文件安装 .NET Core。 这可能包括 build/CI/CD 服务器。

> [!NOTE]
> 对于 Windows 8.1 和更早版本，或 Windows Server 2012 R2 和更早版本：
>
> 确保 Windows 安装是最新版本，并且包括可通过 Windows 更新安装的 [KB2999226](https://support.microsoft.com/en-us/help/2999226/update-for-universal-c-runtime-in-windows)。 如果没有安装此更新，则在启动 .NET Core 应用程序时会看到如下错误：`The program can't start because api-ms-win-crt-runtime-1-1-0.dll is missing from your computer. Try reinstalling the program to fix this problem.`
>
> 对于 Windows 7 或 Windows Server 2008 R2：
>
> 除 KB2999226 以外，请确保还安装了 [KB2533623](https://support.microsoft.com/en-us/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot)。 如果没有安装此更新，则在启动 .NET Core 应用程序时会看到如下错误：`The library hostfxr.dll was found, but loading it from C:\<path_to_app>\hostfxr.dll failed`。

## <a name="prerequisites-for-net-core-30-preview-1"></a>.NET Core 3.0 预览版 1 的先决条件

.NET core 3.0 预览版 1 与其他版本的 .NET Core 具有相同的先决条件。 但是，如果要使用 Visual Studio 创建 .NET Core 3.0 项目，则必须使用 [Visual Studio 2019 预览版](https://visualstudio.microsoft.com/vs/preview/)。 Visual Studio 2019 预览版可与其他版本的 Visual studio 并行安装，不会发生冲突。

## <a name="prerequisites-with-visual-studio-2017"></a>Visual Studio 2017 的先决条件
    
可以使用任何编辑器，通过 .NET Core SDK 开发 .NET Core 应用程序。 Visual Studio 2017 提供了用于在 Windows 上开发 .NET Core 应用程序的集成开发环境。

在[发行说明](/visualstudio/releasenotes/vs2017-relnotes)中可以详细了解 Visual Studio 2017 中的更改。

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

若要使用 .NET Core 2.2 SDK 在 Visual Studio 2017 中开发 .NET Core 应用：

 1. [下载并安装 Visual Studio 2017 版本 15.9.0 或更高版本](/visualstudio/install/install-visual-studio)，并选择“其他工具集”部分中的“.NET Core 跨平台开发”工作负载。

![选中“.NET Core 跨平台开发”工作负荷的 Visual Studio 2017 安装的屏幕截图](./media/windows-prerequisites/vs-2017-workloads.jpg)

安装“.NET Core 跨平台开发”工具集后，Visual Studio 通常会安装以前版本的 .NET Core SDK。
例如，Visual Studio 2017 15.9 在安装工作负载后默认使用 .NET Core 2.1 SDK。

若要更新 Visual Studio 以使用 .NET Core 2.2 SDK：

 1. 安装 [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download)。

 1. 如果希望项目使用最新的 .NET Core 运行时，请使用以下说明将现有或新的 .NET Core 项目重定目标到 .NET Core 2.2：

    * 在 **“项目”** 菜单上，选择 **“属性”**。
    * 在“目标框架”选择菜单上，将值设置为“.NET Core 2.2”。

![已选择“.NET Core 2.2”目标框架菜单项的 Visual Studio 2017 应用程序项目属性屏幕截图](./media/windows-prerequisites/targeting-dotnet-core.jpg)

使用 .NET Core 2.2 SDK 配置 Visual Studio 后，可执行以下操作：

* 打开、生成和运行现有 .NET Core 1.x 和 2.x 项目。
* 将 .NET Core 1.x 和 2.x 项目重定目标到 .NET Core 2.2，再生成并运行。
* 新建 .NET Core 2.2 项目。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

若要在 Visual Studio 中开发 .NET Core 1.x 应用程序，请[下载并安装 Visual Studio 2017](/visualstudio/install/install-visual-studio)，并选择“其他工具集”部分中的“.NET Core 跨平台开发”工作负载。

![选中“.NET Core 跨平台开发”工作负荷的 Visual Studio 2017 安装的屏幕截图](./media/windows-prerequisites/vs-workloads.jpg)

> [!IMPORTANT]
> 可以使用 Visual Studio 2015 进行 .NET Core 1.x 开发，但不建议这么做，原因如下：
  > * .NET Core 工具是预览版，并不受支持。
  > * 项目依据的 project.json 已遭弃用。
>
> 若要详细了解项目格式更改，请参阅[变更的简要概览](./tools/cli-msbuild-architecture.md)。

---

<a name="vs-mapping"></a>

> [!TIP]
> 若要验证 Visual Studio 版本，请执行以下操作：
>
> * 在“帮助”菜单上，选择“关于 Microsoft Visual Studio”。
> * 在“关于 Microsoft Visual Studio”对话框中，验证版本号。
>   * 对于 .NET Core 3.0 Preview 1 应用，Visual Studio 2019 版本应为预览版 1 或更高版本。
>   * 对于 .NET Core 2.2 应用，Visual Studio 2017 版本应为 15.9 或更高版本。
>   * 对于 .NET Core 2.1 应用，Visual Studio 2017 版本应为 15.7 或更高版本。
>   * 对于 .NET Core 1.x 应用，Visual Studio 2017 版本应为 15.0 或更高版本。
