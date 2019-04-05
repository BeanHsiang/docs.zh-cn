---
title: dotnet-install 脚本
description: 了解用于安装 .NET Core CLI 工具和共享运行时的 dotnet-install 脚本。
ms.date: 01/16/2019
ms.openlocfilehash: 6404a8332a7196f0e6fdfe649c2c180970390775
ms.sourcegitcommit: e39d93d358974b9ed4541cedf4e25c0101015c3c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2019
ms.locfileid: "55204790"
---
# <a name="dotnet-install-scripts-reference"></a>dotnet-install 脚本引用

## <a name="name"></a>name

`dotnet-install.ps1` | `dotnet-install.sh` - 用于安装 .NET Core CLI 工具和共享运行时的脚本。

## <a name="synopsis"></a>摘要

Windows：

`dotnet-install.ps1 [-Channel] [-Version] [-InstallDir] [-Architecture] [-SharedRuntime] [-Runtime] [-DryRun] [-NoPath] [-Verbose] [-AzureFeed] [-UncachedFeed] [-NoCdn] [-FeedCredential] [-ProxyAddress] [-ProxyUseDefaultCredentials] [-SkipNonVersionedFiles] [-Help]`

macOS/Linux：

`dotnet-install.sh [--channel] [--version] [--install-dir] [--architecture] [--runtime] [--dry-run] [--no-path] [--verbose] [--azure-feed] [--uncached-feed] [--no-cdn] [--feed-credential] [--runtime-id] [--skip-non-versioned-files] [--help]`

## <a name="description"></a>说明​​

`dotnet-install` 脚本用于执行 .NET Core SDK 的非管理员安装，其中包含 .NET Core CLI 工具和共享运行时。

建议使用在 [.NET Core 主网站](https://dot.net)上托管的稳定版本。 脚本的直接路径为：

* <https://dot.net/v1/dotnet-install.sh>（bash、UNIX）
* <https://dot.net/v1/dotnet-install.ps1>（Powershell、Windows）

这些脚本主要用于自动化方案和非管理员安装。 有两个脚本：一个是适用于在 Windows 上工作的 PowerShell 脚本，另一个是在 Linux/macOS 上工作的 bash 脚本。 这两个脚本的行为相同。 bash 脚本也读取 PowerShell 开关。因此，可以在 Linux/macOS 系统上将 PowerShell 开关与脚本结合使用。

安装脚本从 CLI 生成放置下载 ZIP/tarball 文件，并将其安装在默认位置或 `-InstallDir|--install-dir` 所指定的位置。 默认情况下，安装脚本下载 SDK 并安装它。 如果只想获取共享的运行时，请指定 `--runtime` 参数。

默认情况下，该脚本会将安装位置添加到当前会话的 $PATH。 通过指定 `--no-path` 参数覆盖此默认行为。

运行脚本前，请安装所需的[依赖项](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)。

可以使用 `--version` 参数安装特定版本。 必须将该版本指定为一个 3 部分构成的版本（例如，1.0.0-13232）。 如果未提供，则使用 `latest` 版本。

## <a name="options"></a>选项

* **`-Channel <CHANNEL>`**

  指定安装的源通道。 可能的值为：

  * `Current` - 最新版本。
  * `LTS` - 长期支持频道（最新受支持版本）。
  * 表示特定版本的由两部分构成的 X.Y 格式的版本（例如 `2.0` 或 `1.0`）。
  * 分支名称。 例如，`release/2.0.0`、`release/2.0.0-preview2` 或 `master`（适用于每日测试版本）。

  默认值为 `LTS`。 有关 .NET 支持频道的详细信息，请参阅 [.NET 支持策略](https://www.microsoft.com/net/platform/support-policy#dotnet-core)页。

* **`-Version <VERSION>`**

  表示特定的内部版本。 可能的值为：

  * `latest` - 频道上的最新内部版本（与 `-Channel` 选项结合使用）。
  * `coherent` - 频道上的最新相干内部版本；使用最新的稳定包组合（与分支名称 `-Channel` 选项结合使用）。
  * 由三部分组成的版本，采用 X.Y.Z 格式，表示特定的内部版本；取代 `-Channel` 选项。 例如：`2.0.0-preview2-006120`。

  如果没有指定，`-Version` 默认值为 `latest`。

* **`-InstallDir <DIRECTORY>`**

  指定安装路径。 如果不存在，则会创建该目录。 默认值为 *%LocalAppData%\Microsoft\dotnet*。 会将二进制文件直接放入目录中。

* **`-Architecture <ARCHITECTURE>`**

  要安装的 .NET Core 二进制文件的体系结构。 可能值为 `<auto>`、`amd64`、`x64`、`x86`、`arm64` 以及 `arm`。 默认值为 `<auto>`，它表示当前正在运行的操作系统体系结构。

* **`-SharedRuntime`**

  > [!NOTE]
  > 此参数已过时，可能会在将来版本的脚本中删除。 建议的替代项为 `Runtime` 选项。

  仅安装共享运行时位，而非整个 SDK。 这等效于指定 `-Runtime dotnet`。

* **`-Runtime <RUNTIME>`**

  仅安装共享运行时，而非整个 SDK。 可能的值为：

  * `dotnet` - `Microsoft.NETCore.App` 共享运行时。
  * `aspnetcore` - `Microsoft.AspNetCore.App` 共享运行时。

* **`-DryRun`**

  如果设置，脚本将不会执行安装。 而会显示要使用哪个命令行来持续安装当前请求的 .NET Core CLI 版本。 例如，如果指定版本 `latest`，它将显示特定版本的链接，以便可在生成脚本中明确地使用此命令。 如果想要自行安装或下载，它还会显示二进制文件位置。

* **`-NoPath`**

  如果设定，不会将安装文件夹导出到当前会话的路径。 默认情况下，该脚本会修改 PATH，这会使 CLI 工具在安装后立即可用。

* **`-Verbose`**

  显示诊断信息。

* **`-AzureFeed`**

  指定此安装程序的 Azure 源的 URL。 建议不要更改该值。 默认值为 `https://dotnetcli.azureedge.net/dotnet`。

* **`-UncachedFeed`**

  允许更改此安装程序使用的未缓存源的 URL。 建议不要更改该值。

* **`-NoCdn`**

  禁止从 [Azure 内容分发网络 (CDN)](https://docs.microsoft.com/azure/cdn/cdn-overview) 进行下载，并直接使用未缓存源。

* **`-FeedCredential`**

  用作追加到 Azure 源的查询字符串。 这允许更改 URL 以使用非公共 blob 存储帐户。

* **`-ProxyAddress`**

  如果设置，安装程序发出 Web 请求时将使用该代理。 （仅对 Windows 有效）

* **`ProxyUseDefaultCredentials`**

  如果设置，在使用代理地址时，安装程序会使用当前用户的凭据。 （仅对 Windows 有效）

* **`-SkipNonVersionedFiles`**

  跳过安装未添加版本的文件，例如 dotnet.exe（如果它们已经存在）。

* **`-Help`**

  打印脚本帮助。

## <a name="examples"></a>示例

* 将最新的长期支持 (LTS) 版本安装到默认位置：

  Windows：

  ```powershell
  ./dotnet-install.ps1 -Channel LTS
  ```

  macOS/Linux：

  ```bash
  ./dotnet-install.sh --channel LTS
  ```

* 将 2.0 频道中的最新版本安装到指定位置：

  Windows：

  ```powershell
  ./dotnet-install.ps1 -Channel 2.0 -InstallDir C:\cli
  ```

  macOS/Linux：

  ```bash
  ./dotnet-install.sh --channel 2.0 --install-dir ~/cli
  ```

* 安装 1.1.0 版共享运行时：

  Windows：

  ```powershell
  ./dotnet-install.ps1 -Runtime dotnet -Version 1.1.0
  ```

  macOS/Linux：

  ```bash
  ./dotnet-install.sh --runtime dotnet --version 1.1.0
  ```

* 获取脚本并在公司代理后面安装 2.1.2 版本（仅限 Windows）：

  ```powershell
  Invoke-WebRequest 'https://dot.net/v1/dotnet-install.ps1' -Proxy $env:HTTP_PROXY -ProxyUseDefaultCredentials -OutFile 'dotnet-install.ps1';
  ./dotnet-install.ps1 -InstallDir '~/.dotnet' -Version '2.1.2' -ProxyAddress $env:HTTP_PROXY -ProxyUseDefaultCredentials;
  ```

* 获取脚本并安装 .NET Core CLI 单行式命令示例：

  Windows：

  ```powershell
  @powershell -NoProfile -ExecutionPolicy unrestricted -Command "[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; &([scriptblock]::Create((Invoke-WebRequest -useb 'https://dot.net/v1/dotnet-install.ps1'))) <additional install-script args>"
  ```

  macOS/Linux：

  ```bash
  curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin <additional install-script args>
  ```

## <a name="see-also"></a>请参阅

- [.NET Core 版本](https://github.com/dotnet/core/releases)
- [.NET Core 运行时和 SDK 下载存档](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md)
