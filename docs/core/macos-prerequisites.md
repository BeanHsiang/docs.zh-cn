---
title: Mac 上 .NET Core 的先决条件
description: 在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所支持的 macOS 版本和 .NET Core 依赖项。
author: guardrex
ms.author: adegeo
ms.date: 12/14/2018
ms.openlocfilehash: e895306164b93cb94dab2161971f99eae3138be9
ms.sourcegitcommit: 90775b20343b6ad831af6f5380f8ab7553abb16b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2019
ms.locfileid: "54186171"
---
# <a name="prerequisites-for-net-core-on-macos"></a>macOS 上 .NET Core 的先决条件

本文介绍了在 macOS 计算机上开发、部署和运行 .NET Core 应用程序所需的受支持的 macOS 版本和 .NET Core 依赖项。 支持的操作系统版本和随附的依赖项适用于在 Mac 上开发 .NET Core 应用的三种方法：[结合使用常用编辑器和命令行](tutorials/using-with-xplat-cli.md)、[Visual Studio Code](https://code.visualstudio.com/) 和 [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/visual-studio-mac/)。

## <a name="supported-macos-versions"></a>支持的 macOS 版本

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

以下 macOS 版本支持 .NET Core 2.x：

* macOS 10.12“Sierra”及更高版本

有关 .NET Core 2.1 和 .NET Core 2.2 支持的操作系统、发行版本和版本、不支持的 OS 版本和生命周期策略链接的完整列表，请参阅 [.NET Core 2.1 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md)和 [.NET Core 2.2 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md)。

有关下载链接和详细信息，请参阅 [.NET Core 2.2 下载](https://www.microsoft.com/net/download/dotnet-core/2.2)或 [.NET Core 2.1 下载](https://www.microsoft.com/net/download/dotnet-core/2.1)。


# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

以下 macOS 版本支持 .NET Core 1.x：

* macOS 10.12“Sierra”
* macOS 10.11“El Capitan”

有关 .NET Core 1.1 和 .NET Core 1.0 支持的操作系统、发行版本和版本、不支持的 OS 版本和生命周期策略链接的完整列表，请参阅 [.NET Core 1.1 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/1.1/1.1.md)和 [.NET Core 1.0 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0-supported-os.md)。

有关下载链接和详细信息，请参阅 [.NET Core 1.1 下载](https://www.microsoft.com/net/download/dotnet-core/1.1)或 [.NET Core 1.0 下载](https://www.microsoft.com/net/download/dotnet-core/1.0)。

# <a name="net-core-30-preview-1tabnetcore30"></a>[.NET Core 3.0 预览版 1](#tab/netcore30)

以下 macOS 版本支持 .NET Core 3.0 预览版 1：

* macOS 10.12“Sierra”及更高版本

有关 .NET Core 3.0 支持的操作系统、发行版本和版本、不支持的 OS 版本和生命周期策略链接的完整列表，请参阅 [.NET Core 3.0 支持的 OS 版本](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md)。

有关下载链接和详细信息，请参阅 [.NET Core 3.0 下载](https://www.microsoft.com/net/download/dotnet-core/3.0)。

---

## <a name="net-core-dependencies"></a>.NET Core 依赖项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

从 [.NET 下载](https://www.microsoft.com/net/download/core)下载并安装 .NET Core SDK。 如果在 macOS 上安装时遇到问题，请查阅适用于已安装的版本的[已知问题](https://github.com/dotnet/core/tree/master/release-notes/2.1)主题。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

在 macOS 上运行时，.NET Core 1.x 需要 OpenSSL。 获取 OpenSSL 的一个简单方法是使用适用于 macOS 的 [Homebrew (“brew”)](https://brew.sh/) 包。 在安装 *brew* 后，通过在终端（命令）提示符处执行以下命令来安装 OpenSSL：

```console
brew update
brew install openssl
mkdir -p /usr/local/lib
ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
```

从 [.NET 下载](https://www.microsoft.com/net/download/core)下载并安装 .NET Core SDK。 如果在 macOS 上安装时遇到问题，请查阅 [1.0.0 已知问题](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0-known-issues.md)和 [1.0.1 已知问题](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.1-known-issues.md)主题。

# <a name="net-core-30-preview-1tabnetcore30"></a>[.NET Core 3.0 预览版 1](#tab/netcore30)

从 [.NET 下载](https://www.microsoft.com/net/download/core)下载并安装 .NET Core SDK。 如果在 macOS 上进行安装时遇到问题，请查阅[发行说明](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md)主题以了解所安装的版本。

---

## <a name="increase-the-maximum-open-file-limit-net-core-versions-before-net-core-sdk-202"></a>提高开放文件上限（低于 .NET Core SDK 2.0.2 的 .NET Core 版本） 

在低于 .NET Core SDK 2.0.2 的旧版 .NET Core 中，macOS 上的默认开放文件上限可能对某些 .NET Core 工作负荷（如还原项目或运行单元测试）不够用。

可通过执行以下步骤来增大此限制：

1. 使用文本编辑器创建新文件 _/Library/LaunchDaemons/limit.maxfiles.plist_，并在文件中保存以下内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>limit.maxfiles</string>
    <key>ProgramArguments</key>
    <array>
      <string>launchctl</string>
      <string>limit</string>
      <string>maxfiles</string>
      <string>2048</string>
      <string>4096</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>ServiceIPC</key>
    <false/>
  </dict>
</plist>
```

2. 在终端窗口中运行以下命令：

   ```console
   echo 'ulimit -n 2048' | sudo tee -a /etc/profile
   ```

3. 需要重启 Mac 才能应用这些设置。

## <a name="visual-studio-for-mac"></a>Visual Studio for Mac

可以使用任何编辑器，通过 .NET Core SDK 开发 .NET Core 应用程序。 但是，若要在集成的开发环境中的 Mac 上开发 .NET Core 应用程序，可以使用 [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/visual-studio-mac/)。 

使用 Visual Studio for Mac 在 macOS 上进行 .NET Core 开发需要：

* macOS 操作系统的受支持版本
* OpenSSL（仅 .NET Core 1.x；.NET Core 2.x 使用 macOS 上本机可用的安全服务）
* .NET Core SDK for Mac
* [Visual Studio for Mac](https://visualstudio.microsoft.com/vs/visual-studio-mac/)
