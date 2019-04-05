---
title: dotnet new 命令
description: dotnet new 命令可根据指定模板新建 .NET Core 项目。
ms.date: 10/24/2018
ms.openlocfilehash: 5177c920fee6fa946d2bf5d96644f26309ed0a99
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54516143"
---
# <a name="dotnet-new"></a>dotnet new

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet new` - 根据指定的模板，创建新的项目、配置文件或解决方案。

## <a name="synopsis"></a>摘要

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

```console
dotnet new <TEMPLATE> [--force] [-i|--install] [-lang|--language] [-n|--name] [--nuget-source] [-o|--output]
    [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

```console
dotnet new <TEMPLATE> [--force] [-i|--install] [-lang|--language] [-n|--name] [-o|--output] [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```console
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template options]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```

---

## <a name="description"></a>说明

`dotnet new` 命令为初始化有效的 .NET Core 项目提供了便捷方法。

命令调用[模板引擎](https://github.com/dotnet/templating)，以根据指定的模板和选项在磁盘上创建项目。

## <a name="arguments"></a>自变量

`TEMPLATE`

调用命令时要实例化的模板。 每个模板可能具有可传递的特定选项。 有关详细信息，请参阅[模板选项](#template-options)。

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

此命令包含默认的模板列表。 使用 `dotnet new -l` 获取可用模板的列表。 下表列出了随 .NET Core SDK 2.1.300 一起预安装的模板。 模板的默认语言显示在括号内。

|模板描述                          | 模板名称    | 语言     |
|----------------------------------------------|------------------|---------------|
| 控制台应用程序                          | `console`        | [C#]、F#、VB  |
| 类库                                | `classlib`       | [C#]、F#、VB  |
| 单元测试项目                            | `mstest`         | [C#]、F#、VB  |
| xUnit 测试项目                           | `xunit`          | [C#]、F#、VB  |
| NUnit 试项目                           | `nunit`          | [C#]、F#、VB  |
| Razor 页                                   | `page`           | [C#]          |
| MVC ViewImports                              | `viewimports`    | [C#]          |
| MVC ViewStart                                | `viewstart`      | [C#]          |
| ASP.NET Core 空                           | `web`            | [C#]，F#      |
| ASP.NET Core Web 应用程序 (Model-View-Controller) | `mvc`            | [C#]，F#      |
| ASP.NET Core Web 应用程序                         | `razor`， `webapp`| [C#]          |
| 含 Angular 的 ASP.NET Core                    | `angular`        | [C#]          |
| 含 React.js 的 ASP.NET Core                   | `react`          | [C#]          |
| 含 React.js 和 Redux 的 ASP.NET Core         | `reactredux`     | [C#]          |
| ASP.NET Core Web API                         | `webapi`         | [C#]，F#      |
| Razor 类库                          | `razorclasslib`  | [C#]          |
| global.json 文件                             | `globaljson`     |               |
| NuGet 配置                                 | `nugetconfig`    |               |
| Web 配置                                   | `webconfig`      |               |
| 解决方案文件                                | `sln`            |               |

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

此命令包含默认的模板列表。 使用 `dotnet new -l` 获取可用模板的列表。 下表列出了随 .NET Core SDK 2.0 一起预安装的模板。 模板的默认语言显示在括号内。

|模板描述                          | 模板名称 | 语言     |
|----------------------------------------------|---------------|---------------|
| 控制台应用程序                          | `console`     | [C#]、F#、VB  |
| 类库                                | `classlib`    | [C#]、F#、VB  |
| 单元测试项目                            | `mstest`      | [C#]、F#、VB  |
| xUnit 测试项目                           | `xunit`       | [C#]、F#、VB  |
| ASP.NET Core 空                           | `web`         | [C#]，F#      |
| ASP.NET Core Web 应用程序 (Model-View-Controller) | `mvc`         | [C#]，F#      |
| ASP.NET Core Web 应用程序                         | `razor`       | [C#]          |
| 含 Angular 的 ASP.NET Core                    | `angular`     | [C#]          |
| 含 React.js 的 ASP.NET Core                   | `react`       | [C#]          |
| 含 React.js 和 Redux 的 ASP.NET Core         | `reactredux`  | [C#]          |
| ASP.NET Core Web API                         | `webapi`      | [C#]，F#      |
| global.json 文件                             | `globaljson`  |               |
| NuGet 配置                                 | `nugetconfig` |               |
| Web 配置                                   | `webconfig`   |               |
| 解决方案文件                                | `sln`         |               |
| Razor 页                                   | `page`        |               |
| MVC ViewImports                              | `viewimports` |               |
| MVC ViewStart                                | `viewstart`   |               |

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

此命令包含默认的模板列表。 使用 `dotnet new -all` 获取可用模板的列表。 下表列出了随 .NET Core SDK 1.x 一起预安装的模板。 模板的默认语言显示在括号内。

|模板描述  | 模板名称 | 语言 |
|----------------------|---------------|-----------|
| 控制台应用程序  | `console`     | [C#]，F#  |
| 类库        | `classlib`    | [C#]，F#  |
| 单元测试项目    | `mstest`      | [C#]，F#  |
| xUnit 测试项目   | `xunit`       | [C#]，F#  |
| ASP.NET Core 空   | `web`         | [C#]      |
| ASP.NET Core Web 应用程序 | `mvc`         | [C#]，F#  |
| ASP.NET Core Web API | `webapi`      | [C#]      |
| NuGet 配置         | `nugetconfig` |           |
| Web 配置           | `webconfig`   |           |
| 解决方案文件        | `sln`         |           |

---

## <a name="options"></a>选项

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--force`

强制生成内容，即使会更改现有文件，也不例外。 输出目录已包含一个项目时，可能需要此操作。

`-h|--help`

打印命令帮助。 可针对 `dotnet new` 命令本身或任何模板（如 `dotnet new mvc --help`）调用它。

`-i|--install <PATH|NUGET_ID>`

从提供的 `PATH` 或 `NUGET_ID` 安装源或模板包。 若要安装模板包的预发布版本，需要以 `<package-name>::<package-version>` 格式指定该版本。 默认情况下，`dotnet new` 为该版本传递 \*，表示最后一个稳定的包版本。 请在[示例](#examples)部分查看示例。

若要了解如何创建自定义模板，请参阅 [dotnet new 自定义模板](custom-templates.md)。

`-l|--list`

列出包含指定名称的模板。 如果针对 `dotnet new` 命令调用，则它列出可能对给定的目录可用的模板。 例如，如果该目录已包含一个项目，则它不会列出所有项目模板。

`-lang|--language {C#|F#|VB}`

要创建的模板的语言。 接受的语言因模板而异（请参阅[参数](#arguments)部分中的默认值）。 对于某些模板无效。

> [!NOTE]
> 某些 shell 将 `#` 解释为特殊字符。 在这些情况下，需要括住语言参数值，如 `dotnet new console -lang "F#"`。

`-n|--name <OUTPUT_NAME>`

所创建的输出的名称。 如果未指定名称，使用的是当前目录的名称。

`--nuget-source`

指定在安装期间要使用的 NuGet 源。

`-o|--output <OUTPUT_DIRECTORY>`

用于放置生成的输出的位置。 默认为当前目录。

`--type`

根据可用类型筛选模板。 预定义值为“project”、“item”或“other”。

`-u|--uninstall <PATH|NUGET_ID>`

从提供的 `PATH` 或 `NUGET_ID` 卸载源或模板包。

> [!NOTE]
> 若要使用 `PATH` 卸载模板，需要完全限定路径。 例如，C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp 有效，但是包含文件夹中的 ./GarciaSoftware.ConsoleTemplate.CSharp 无效。
> 此外，模板路径中不要包含最后的终止目录斜杠。

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--force`

强制生成内容，即使会更改现有文件，也不例外。 输出目录已包含一个项目时，可能需要此操作。

`-h|--help`

打印命令帮助。 可针对 `dotnet new` 命令本身或任何模板（如 `dotnet new mvc --help`）调用它。

`-i|--install <PATH|NUGET_ID>`

从提供的 `PATH` 或 `NUGET_ID` 安装源或模板包。 若要安装模板包的预发布版本，需要以 `<package-name>::<package-version>` 格式指定该版本。 默认情况下，`dotnet new` 为该版本传递 \*，表示最后一个稳定的包版本。 请在[示例](#examples)部分查看示例。

若要了解如何创建自定义模板，请参阅 [dotnet new 自定义模板](custom-templates.md)。

`-l|--list`

列出包含指定名称的模板。 如果针对 `dotnet new` 命令调用，则它列出可能对给定的目录可用的模板。 例如，如果该目录已包含一个项目，则它不会列出所有项目模板。

`-lang|--language {C#|F#|VB}`

要创建的模板的语言。 接受的语言因模板而异（请参阅[参数](#arguments)部分中的默认值）。 对于某些模板无效。

> [!NOTE]
> 某些 shell 将 `#` 解释为特殊字符。 在这些情况下，需要括住语言参数值，如 `dotnet new console -lang "F#"`。

`-n|--name <OUTPUT_NAME>`

所创建的输出的名称。 如果未指定名称，使用的是当前目录的名称。

`-o|--output <OUTPUT_DIRECTORY>`

用于放置生成的输出的位置。 默认为当前目录。

`--type`

根据可用类型筛选模板。 预定义值为“project”、“item”或“other”。

`-u|--uninstall <PATH|NUGET_ID>`

从提供的 `PATH` 或 `NUGET_ID` 卸载源或模板包。

> [!NOTE]
> 若要使用源 `PATH` 卸载模板，需要完全限定路径。 例如，C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp 有效，但是包含文件夹中的 ./GarciaSoftware.ConsoleTemplate.CSharp 无效。 此外，模板路径中不要包含最后的终止目录斜杠。
> 
> 如果无法确定卸载模板所需的 `PATH` 或 `NUGET_ID` 参数，则在没有参数的情况下运行 `dotnet new --uninstall` 将列出所有已安装的模板以及卸载它们所需的参数。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-all|--show-all`

单独在 `dotnet new` 命令的上下文中运行时，显示特定类型的项目的所有模板。 在特定模板（如 `dotnet new web -all`）的上下文中运行时，`-all` 解释为一个强制创建标记。 输出目录已包含一个项目时，可能需要此操作。

`-h|--help`

打印命令帮助。 可针对 `dotnet new` 命令本身或任何模板（如 `dotnet new mvc --help`）调用它。

`-l|--list`

列出包含指定名称的模板。 如果针对 `dotnet new` 命令调用，则它列出可能对给定的目录可用的模板。 例如，如果该目录已包含一个项目，则它不会列出所有项目模板。

`-lang|--language {C#|F#}`

要创建的模板的语言。 接受的语言因模板而异（请参阅[参数](#arguments)部分中的默认值）。 对于某些模板无效。

> [!NOTE]
> 某些 shell 将 `#` 解释为特殊字符。 在这些情况下，需要括住语言参数值，如 `dotnet new console -lang "F#"`。

`-n|--name <OUTPUT_NAME>`

所创建的输出的名称。 如果未指定名称，使用的是当前目录的名称。

`-o|--output <OUTPUT_DIRECTORY>`

用于放置生成的输出的位置。 默认为当前目录。

---

## <a name="template-options"></a>模板选项

每个项目模板都可能有附加选项。 核心模板有以下附加选项：

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

console、angular、react、reactredux、razorclasslib

  `--no-restore` - 在项目创建期间不执行隐式还原。

**classlib**

`-f|--framework <FRAMEWORK>` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp2.0`（要创建 .NET Core 类库的话）或 `netstandard2.0`（要创建 .NET Standard 类库的话）。 默认值为 `netstandard2.0`。

`--no-restore` - 在项目创建期间不执行隐式还原。

**mstest、xunit**

`-p|--enable-pack` - 允许使用 [dotnet pack](dotnet-pack.md) 为项目打包。

`--no-restore` - 在项目创建期间不执行隐式还原。

**globaljson**

`--sdk-version <VERSION_NUMBER>` - 指定要在 global.json 文件中使用的 .NET Core SDK 版本。

**web**

`--exclude-launch-settings` - 从生成的模板中排除 launchSettings.json。

`--no-restore` - 在项目创建期间不执行隐式还原。

`--no-https` - 项目不需要 HTTPS。 此选项仅适用于未使用 `IndividualAuth` 或 `OrganizationalAuth` 的情况。

**webapi**

`-au|--auth <AUTHENTICATION_TYPE>` - 要使用的身份验证类型。 可能的值为：

- `None` - 不进行身份验证（默认）。
- `IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。
- `SingleOrg` - 对一个租户进行组织身份验证。
- `Windows` - Windows 身份验证。

`--aad-b2c-instance <INSTANCE>` - 要连接到的 Azure Active Directory B2C 实例。 与 `IndividualB2C` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/tfp/`。

`-ssp|--susi-policy-id <ID>` - 此项目的登录和注册策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`--aad-instance <INSTANCE>` - 要连接到的 Azure Active Directory 实例。 与 `SingleOrg` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/`。

`--client-id <ID>` - 此项目的客户端 ID。 与 `IndividualB2C` 或 `SingleOrg` 身份验证结合使用。 默认值为 `11111111-1111-1111-11111111111111111`。

`--domain <DOMAIN>` - 目录租户的域。 与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。 默认值为 `qualified.domain.name`。

`--tenant-id <ID>` - 要连接到的目录的 TenantId ID。 与 `SingleOrg` 身份验证结合使用。 默认值为 `22222222-2222-2222-2222-222222222222`。

`-r|--org-read-access` - 允许此应用程序对目录进行读取访问。 仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。

`--exclude-launch-settings` - 从生成的模板中排除 launchSettings.json。

`-uld|--use-local-db` - 指定应使用 LocalDB，而不使用 SQLite。 仅适用于 `Individual` 或 `IndividualB2C` 身份验证。

`--no-restore` - 在项目创建期间不执行隐式还原。

`--no-https` - 项目不需要 HTTPS。 `app.UseHsts` 和 `app.UseHttpsRedirection` 未添加到 `Startup.Configure` 中。 此选项仅适用于未使用 `Individual`、`IndividualB2C``SingleOrg` 和 `MultiOrg` 的情况。

**mvc、razor**

`-au|--auth <AUTHENTICATION_TYPE>` - 要使用的身份验证类型。 可能的值为：

- `None` - 不进行身份验证（默认）。
- `Individual` - 个人身份验证。
- `IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。
- `SingleOrg` - 对一个租户进行组织身份验证。
- `MultiOrg` - 对多个租户进行组织身份验证。
- `Windows` - Windows 身份验证。

`--aad-b2c-instance <INSTANCE>` - 要连接到的 Azure Active Directory B2C 实例。 与 `IndividualB2C` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/tfp/`。

`-ssp|--susi-policy-id <ID>` - 此项目的登录和注册策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`-rp|--reset-password-policy-id <ID>` - 此项目的重置密码策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`-ep|--edit-profile-policy-id <ID>` - 此项目的编辑配置文件策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`--aad-instance <INSTANCE>` - 要连接到的 Azure Active Directory 实例。 与 `SingleOrg` 或 `MultiOrg` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/`。

`--client-id <ID>` - 此项目的客户端 ID。 与 `IndividualB2C`、`SingleOrg` 或 `MultiOrg` 身份验证结合使用。 默认值为 `11111111-1111-1111-11111111111111111`。

`--domain <DOMAIN>` - 目录租户的域。 与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。 默认值为 `qualified.domain.name`。

`--tenant-id <ID>` - 要连接到的目录的 TenantId ID。 与 `SingleOrg` 身份验证结合使用。 默认值为 `22222222-2222-2222-2222-222222222222`。

`--callback-path <PATH>` - 重定向 URI 的应用程序基路径中的请求路径。 与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。 默认值为 `/signin-oidc`。

`-r|--org-read-access` - 允许此应用程序对目录进行读取访问。 仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。

`--exclude-launch-settings` - 从生成的模板中排除 launchSettings.json。

`--use-browserlink` - 在项目中添加 BrowserLink。

`-uld|--use-local-db` - 指定应使用 LocalDB，而不使用 SQLite。 仅适用于 `Individual` 或 `IndividualB2C` 身份验证。

`--no-restore` - 在项目创建期间不执行隐式还原。

`--no-https` - 项目不需要 HTTPS。 `app.UseHsts` 和 `app.UseHttpsRedirection` 未添加到 `Startup.Configure` 中。 此选项仅适用于未使用 `Individual`、`IndividualB2C``SingleOrg` 和 `MultiOrg` 的情况。

**page**

`-na|--namespace <NAMESPACE_NAME>` - 生成的代码的命名空间。 默认值为 `MyApp.Namespace`。

`-np|--no-pagemodel` - 创建不含 PageModel 的页。

**viewimports**

`-na|--namespace <NAMESPACE_NAME>` - 生成的代码的命名空间。 默认值为 `MyApp.Namespace`。

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

**console、angular、react、reactredux**

  `--no-restore` - 在项目创建期间不执行隐式还原。

**classlib**

`-f|--framework <FRAMEWORK>` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp2.0`（要创建 .NET Core 类库的话）或 `netstandard2.0`（要创建 .NET Standard 类库的话）。 默认值为 `netstandard2.0`。

`--no-restore` - 在项目创建期间不执行隐式还原。

**mstest、xunit**

`-p|--enable-pack` - 允许使用 [dotnet pack](dotnet-pack.md) 为项目打包。

`--no-restore` - 在项目创建期间不执行隐式还原。

**globaljson**

`--sdk-version <VERSION_NUMBER>` - 指定要在 global.json 文件中使用的 .NET Core SDK 版本。

**web**

`--use-launch-settings` - 在生成的模板输出中添加 launchSettings.json。

`--no-restore` - 在项目创建期间不执行隐式还原。

**webapi**

`-au|--auth <AUTHENTICATION_TYPE>` - 要使用的身份验证类型。 可能的值为：

- `None` - 不进行身份验证（默认）。
- `IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。
- `SingleOrg` - 对一个租户进行组织身份验证。
- `Windows` - Windows 身份验证。

`--aad-b2c-instance <INSTANCE>` - 要连接到的 Azure Active Directory B2C 实例。 与 `IndividualB2C` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/tfp/`。

`-ssp|--susi-policy-id <ID>` - 此项目的登录和注册策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`--aad-instance <INSTANCE>` - 要连接到的 Azure Active Directory 实例。 与 `SingleOrg` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/`。

`--client-id <ID>` - 此项目的客户端 ID。 与 `IndividualB2C` 或 `SingleOrg` 身份验证结合使用。 默认值为 `11111111-1111-1111-11111111111111111`。

`--domain <DOMAIN>` - 目录租户的域。 与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。 默认值为 `qualified.domain.name`。

`--tenant-id <ID>` - 要连接到的目录的 TenantId ID。 与 `SingleOrg` 身份验证结合使用。 默认值为 `22222222-2222-2222-2222-222222222222`。

`-r|--org-read-access` - 允许此应用程序对目录进行读取访问。 仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。

`--use-launch-settings` - 在生成的模板输出中添加 launchSettings.json。

`-uld|--use-local-db` - 指定应使用 LocalDB，而不使用 SQLite。 仅适用于 `Individual` 或 `IndividualB2C` 身份验证。

`--no-restore` - 在项目创建期间不执行隐式还原。

**mvc、razor**

`-au|--auth <AUTHENTICATION_TYPE>` - 要使用的身份验证类型。 可能的值为：

- `None` - 不进行身份验证（默认）。
- `Individual` - 个人身份验证。
- `IndividualB2C` - 使用 Azure AD B2C 进行个人身份验证。
- `SingleOrg` - 对一个租户进行组织身份验证。
- `MultiOrg` - 对多个租户进行组织身份验证。
- `Windows` - Windows 身份验证。

`--aad-b2c-instance <INSTANCE>` - 要连接到的 Azure Active Directory B2C 实例。 与 `IndividualB2C` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/tfp/`。

`-ssp|--susi-policy-id <ID>` - 此项目的登录和注册策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`-rp|--reset-password-policy-id <ID>` - 此项目的重置密码策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`-ep|--edit-profile-policy-id <ID>` - 此项目的编辑配置文件策略 ID。 与 `IndividualB2C` 身份验证结合使用。

`--aad-instance <INSTANCE>` - 要连接到的 Azure Active Directory 实例。 与 `SingleOrg` 或 `MultiOrg` 身份验证结合使用。 默认值为 `https://login.microsoftonline.com/`。

`--client-id <ID>` - 此项目的客户端 ID。 与 `IndividualB2C`、`SingleOrg` 或 `MultiOrg` 身份验证结合使用。 默认值为 `11111111-1111-1111-11111111111111111`。

`--domain <DOMAIN>` - 目录租户的域。 与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。 默认值为 `qualified.domain.name`。

`--tenant-id <ID>` - 要连接到的目录的 TenantId ID。 与 `SingleOrg` 身份验证结合使用。 默认值为 `22222222-2222-2222-2222-222222222222`。

`--callback-path <PATH>` - 重定向 URI 的应用程序基路径中的请求路径。 与 `SingleOrg` 或 `IndividualB2C` 身份验证结合使用。 默认值为 `/signin-oidc`。

`-r|--org-read-access` - 允许此应用程序对目录进行读取访问。 仅适用于 `SingleOrg` 或 `MultiOrg` 身份验证。

`--use-launch-settings` - 在生成的模板输出中添加 launchSettings.json。

`--use-browserlink` - 在项目中添加 BrowserLink。

`-uld|--use-local-db` - 指定应使用 LocalDB，而不使用 SQLite。 仅适用于 `Individual` 或 `IndividualB2C` 身份验证。

`--no-restore` - 在项目创建期间不执行隐式还原。

**page**

`-na|--namespace <NAMESPACE_NAME>` - 生成的代码的命名空间。 默认值为 `MyApp.Namespace`。

`-np|--no-pagemodel` - 创建不含 PageModel 的页。

**viewimports**

`-na|--namespace <NAMESPACE_NAME>` - 生成的代码的命名空间。 默认值为 `MyApp.Namespace`。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**console、xunit、mstest、web、webapi**

`-f|--framework` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp1.0` 或 `netcoreapp1.1`。 默认值为 `netcoreapp1.0`。

**classlib**

`-f|--framework` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp1.0`、`netcoreapp1.1` 或 `netstandard1.0` 到 `netstandard1.6`。 默认值为 `netstandard1.4`。

**mvc**

`-f|--framework` - 指定目标[框架](../../standard/frameworks.md)。 值：`netcoreapp1.0` 或 `netcoreapp1.1`。 默认值为 `netcoreapp1.0`。

`-au|--auth` - 要使用的身份验证类型。 值：`None` 或 `Individual`。 默认值为 `None`。

`-uld|--use-local-db` - 指定是否使用 LocalDB，而不是 SQLite。 值：`true` 或 `false`。 默认值为 `false`。

---

## <a name="examples"></a>示例

在当前目录中创建 F# 控制台应用程序项目：

`dotnet new console -lang F#`

在指定目录中创建 .NET Standard 类库项目（仅适用于 .NET Core SDK 2.0 或更高版本）：

`dotnet new classlib -lang VB -o MyLibrary`

在当前目录中新建没有设置身份验证的 ASP.NET Core C# MVC 应用程序项目：

`dotnet new mvc -au None`

创建新的 xUnit 应用程序：

`dotnet new xunit`

列出适用于 MVC 的所有模板：

`dotnet new mvc -l`

安装适用于 ASP.NET Core 的单页应用程序模板 2.0 版（命令选项仅可用于 .NET Core SDK 1.1 及更高版本）：

`dotnet new -i Microsoft.DotNet.Web.Spa.ProjectTemplates::2.0.0`

在当前目录中创建 global.json，将 SDK 版本设为 2.0.0（仅适用于 .NET Core SDK 2.0 或更高版本）：

`dotnet new globaljson --sdk-version 2.0.0`

## <a name="see-also"></a>请参阅

- [dotnet new 自定义模板](custom-templates.md)
- [创建 dotnet new 自定义模板](~/docs/core/tutorials/create-custom-template.md)
- [dotnet/dotnet-template-samples GitHub 存储库](https://github.com/dotnet/dotnet-template-samples)
- [dotnet new 可用模板](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)
