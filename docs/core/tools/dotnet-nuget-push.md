---
title: dotnet nuget push 命令
description: dotnet nuget push 命令可将包推送到服务器并发布。
author: karann-msft
ms.date: 12/04/2018
ms.openlocfilehash: 4f0d127d8b9f37b1c381d8981f54035a2fc3b0e5
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53169347"
---
# <a name="dotnet-nuget-push"></a>dotnet nuget push

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet nuget push` - 将包推送到服务器，并将其发布。

## <a name="synopsis"></a>摘要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output] [--interactive] [-k|--api-key] [-n|--no-symbols]
    [--no-service-endpoint] [-s|--source] [-sk|--symbol-api-key] [-ss|--symbol-source] [-t|--timeout]
dotnet nuget push [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet nuget push [<ROOT>] [-d|--disable-buffering] [--force-english-output] [-k|--api-key] [-n|--no-symbols]
    [-s|--source] [-sk|--symbol-api-key] [-ss|--symbol-source] [-t|--timeout]
dotnet nuget push [-h|--help]
```
---

## <a name="description"></a>说明

`dotnet nuget push` 将包推送到服务器，并将其发布。 push 命令使用在系统的 NuGet 配置文件或配置文件链中找到的服务器和凭据详细信息。 有关配置文件的详细信息，请参阅 [Configuring NuGet Behavior](/nuget/consume-packages/configuring-nuget-behavior)（配置 NuGet 行为）。 通过加载 *%AppData%\NuGet\NuGet.config* (Windows) 或 *$HOME/.local/share* (Linux/macOS) 获得 NuGet 的默认配置，然后加载任意 *nuget.config* 或 *.nuget\nuget.config*，从驱动器的根目录开始，并在当前目录中结束。

## <a name="arguments"></a>自变量

* **`ROOT`**

  指定要推送的包的文件路径。

## <a name="options"></a>选项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

* **`-d|--disable-buffering`**

  当推送到 HTTP(S) 服务器以减少内存使用率时，禁用缓冲。

* **`--force-english-output`**

  使用固定的、基于英语的区域性强制运行应用程序。

* **`-h|--help`**

打印出有关命令的简短帮助。

* **`--interactive`**

  对于身份验证等操作，允许命令阻止并要求手动操作。 自 .NET Core 2.2 SDK 起可用的选项。

* **`-k|--api-key <API_KEY>`**

  服务器的 API 密钥。

* **`-n|--no-symbols`**

  不推送符号（即使存在）。

* **`--no-service-endpoint`**

  不将“api/v2/package”追加至源 URL。 自 .NET Core 2.1 SDK 起可用的选项。

* **`-s|--source <SOURCE>`**

  指定服务器 URL。 除非在 NuGet 配置文件中设置了 `DefaultPushSource` 配置值，否则此选项是必需的。

* **`-sk|--symbol-api-key <API_KEY>`**

  符号服务器的 API 密钥。

* **`-ss|--symbol-source <SOURCE>`**

  指定符号服务器 URL。

* **`-t|--timeout <TIMEOUT>`**

  指定推送到服务器的超时（秒）。 默认值为 300 秒（5 分钟）。 指定为 0（零秒）将应用默认值。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

* **`-d|--disable-buffering`**

  当推送到 HTTP(S) 服务器以减少内存使用率时，禁用缓冲。

* **`--force-english-output`**

  使用固定的、基于英语的区域性强制运行应用程序。

* **`-h|--help`**

  打印出有关命令的简短帮助。

* **`-k|--api-key <API_KEY>`**

  服务器的 API 密钥。

* **`-n|--no-symbols`**

  不推送符号（即使存在）。

* **`-s|--source <SOURCE>`**

  指定服务器 URL。 除非在 NuGet 配置文件中设置了 `DefaultPushSource` 配置值，否则此选项是必需的。

* **`-sk|--symbol-api-key <API_KEY>`**

  符号服务器的 API 密钥。

* **`-ss|--symbol-source <SOURCE>`**

  指定符号服务器 URL。

* **`-t|--timeout <TIMEOUT>`**

  指定推送到服务器的超时（秒）。 默认值为 300 秒（5 分钟）。 指定为 0（零秒）将应用默认值。

---

## <a name="examples"></a>示例

* 将 foo.nupkg 推送到默认推送源（指定 API 密钥）：

  ```console
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a
  ```

* 将 foo.nupkg 推送到自定义推送源 `https://customsource`（指定 API 密钥）：

  ```console
  dotnet nuget push foo.nupkg -k 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
  ```

* 将 *foo.nupkg* 推送到默认推送源：

  ```console
  dotnet nuget push foo.nupkg
  ```

* 将 *foo.symbols.nupkg* 推送到默认符号源：

  ```console
  dotnet nuget push foo.symbols.nupkg
  ```

* 将 foo.nupkg 推送到默认推送源（指定 360 秒超时时间）：

  ```console
  dotnet nuget push foo.nupkg --timeout 360
  ```

* 将当前目录中的所有 *.nupkg* 文件推送到默认推送源：

  ```console
  dotnet nuget push *.nupkg
  ```