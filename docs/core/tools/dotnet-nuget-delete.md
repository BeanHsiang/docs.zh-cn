---
title: dotnet nuget delete 命令
description: dotnet-nuget-delete 命令从服务器删除或取消列出包。
author: karann-msft
ms.date: 12/04/2018
ms.openlocfilehash: 827d295d7a52b6c9c82adbcf3d25281bd1cc98fd
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53168307"
---
# <a name="dotnet-nuget-delete"></a>dotnet nuget delete

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet nuget delete` - 从服务器删除或取消列出包。

## <a name="synopsis"></a>摘要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [--interactive] [-k|--api-key] [--no-service-endpoint]
    [--non-interactive] [-s|--source]
dotnet nuget delete [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [-k|--api-key] [--non-interactive]
    [-s|--source]
dotnet nuget delete [-h|--help]
```
---

## <a name="description"></a>说明

`dotnet nuget delete` 命令从服务器删除或取消列出包。 对于 [NuGet.org](https://www.nuget.org/)，该操作将取消列出包。

## <a name="arguments"></a>自变量

* **`PACKAGE_NAME`**

  要删除的包的名称/ID。

* **`PACKAGE_VERSION`**

  要删除的包的版本。

## <a name="options"></a>选项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

* **`--force-english-output`**

  使用固定的、基于英语的区域性强制运行应用程序。

* **`-h|--help`**

  打印出有关命令的简短帮助。

* **`--interactive`**

  对于身份验证等操作，允许命令阻止并要求手动操作。 自 .NET Core 2.2 SDK 起可用的选项。

* **`-k|--api-key <API_KEY>`**

  服务器的 API 密钥。

* **`--no-service-endpoint`**

  不将“api/v2/package”追加至源 URL。 自 .NET Core 2.1 SDK 起可用的选项。

* **`--non-interactive`**

  不提示用户输入或确认。

* **`-s|--source <SOURCE>`**

  指定服务器 URL。 Nuget.org 的支持 URL 包括 `https://www.nuget.org`、`https://www.nuget.org/api/v3` 和 `https://www.nuget.org/api/v2/package`。 对于专用源，请替换主机名（例如，`%hostname%/api/v3`）。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

* **`--force-english-output`**

  使用固定的、基于英语的区域性强制运行应用程序。

* **`-h|--help`**

  打印出有关命令的简短帮助。

* **`-k|--api-key <API_KEY>`**

  服务器的 API 密钥。

* **`--non-interactive`**

  不提示用户输入或确认。

* **`-s|--source <SOURCE>`**

  指定服务器 URL。 Nuget.org 的支持 URL 包括 `https://www.nuget.org`、`https://www.nuget.org/api/v3` 和 `https://www.nuget.org/api/v2/package`。 对于专用源，请替换主机名（例如，`%hostname%/api/v3`）。

---

## <a name="examples"></a>示例

* 删除包 `Microsoft.AspNetCore.Mvc` 的 1.0 版：

  ```console
  dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0
  ```

* 删除包 `Microsoft.AspNetCore.Mvc` 的 1.0 版（不提示用户需要凭据或其他输入）：

  ```console
  dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0 --non-interactive
  ```