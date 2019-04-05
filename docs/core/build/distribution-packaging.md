---
title: .NET Core 分发打包
description: 了解如何为 .NET Core 打包、命名并进行版本控制以进行分发。
author: bleroy
ms.date: 06/28/2017
ms.custom: seodec18
ms.openlocfilehash: be5767351ad1cdac15c73f718f67a0d120cf65b0
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53170413"
---
# <a name="net-core-distribution-packaging"></a>.NET Core 分发打包

由于 .NET Core 现已可用于更多平台，因此了解如何为其打包、命名并进行版本控制将很有用。 这样，无论用户选择在哪里运行 .NET，包维护人员均可以帮助确保获得一致的体验。

## <a name="disk-layout"></a>磁盘布局

安装时，.NET Core 包含一些组件，这些组件在文件系统中排列如下：

```
.
├── dotnet                       (1)
├── LICENSE.txt                  (8)
├── ThirdPartyNotices.txt        (8)
├── host
│   └── fxr
│       └── <fxr version>        (2)
├── sdk
│   ├── <sdk version>            (3)
│   └── NuGetFallbackFolder      (4)
└── shared
    ├── Microsoft.NETCore.App
    │   └── <runtime version>    (5)
    └── Microsoft.AspNetCore.App
        └── <aspnetcore version> (6)
    └── Microsoft.AspNetCore.All
        └── <aspnetcore version> (7)
/
├─usr/share/man/man1
│       └── dotnet.1.gz          (9)
└─usr/bin
        └── dotnet               (10)
```

- (1) **dotnet** 主机（也称为“muxer”）有两个不同角色：激活运行时以启动应用程序，及激活 SDK 以向其分派命令。 主机是本机可执行文件 (`dotnet.exe`)。

主机只有一个，不过大部分的其他组件都在带有版本的目录中（2、3、5 和 6）。 这意味着系统上可存在多个版本，因为它们是并排安装的。

- (2) **host/fxr/\<fxr version>** 包含了主机所使用的框架解析逻辑。 主机采用已安装的最新 hostfxr。 在执行 .NET Core 应用程序时，hostfxr 负责选择合适的运行时。 例如，.NET Core 2.0.0 的应用程序会使用 2.0.5 运行时（如果可用）。 同样，hostfxr 在开发期间也会选择适当的 SDK。

- (3) **sdk/\<sdk version>** SDK（也称为“工具”）是一组托管工具，可用于编写和生成 .NET Core 库和应用程序。 SDK 包括 CLI、Roslyn 编译器、MSBuild 及相关生成任务和目标、NuGet、新项目模板等。

- (4) **sdk/NuGetFallbackFolder** 包含 `dotnet restore` 步骤中 SDK 所使用的 NuGet 包的缓存。

“共享”文件夹包含框架。 共享框架提供一组位于中心位置的库，从而让不同的应用程序使用。

- (5) **shared/Microsoft.NETCore.App/\<runtime version>** 此框架包含.NET Core 运行时和支持托管库。

- (6,7) **shared/Microsoft.AspNetCore.{App,All}/\<aspnetcore version>** 包含 ASP.NET Core 库。 已开发且支持 `Microsoft.AspNetCore.App` 下的库（作为 .NET Core 项目的一部分）。 `Microsoft.AspNetCore.All` 下的库是一个超集，其中还包含第三方库。

- (8) **LICENSE.txt,ThirdPartyNotices.txt** 是 .NET Core 许可证和 .NET Core 中使用的第三方库的许可证。

- (9,10) **dotnet.1.gz, dotnet** `dotnet.1.gz` 是 dotnet 手册页。 `dotnet` 是指向 dotnet 主机 (1) 的符号链接。 这些文件安装在已知位置用于系统集成。

## <a name="recommended-packages"></a>推荐的包

.NET Core 版本控制基于运行时组件 `[major].[minor]` 版本号。
SDK 版本采用同样的 `[major].[minor]`，并有一个独立的 `[patch]`，它为 SDK 合并了功能和修补语义。
例如:SDK 版本 2.2.302 是支持 2.2 运行时的 SDK 的第 3 个功能版本的第 2 个补丁版本。

一些包在自己的名称中就包含一部分版本号。 这能帮助最终用户安装特定版本。
版本名称中不包含版本的剩余部分。 这允许 OS 包管理器更新这些包（例如，自动安装安全修补程序）。

下表显示推荐的包。

| name                                    | 示例                | 用例：安装 ...           | 包含           | 依赖项                                   | 版本            |
|-----------------------------------------|------------------------|---------------------------------|--------------------|------------------------------------------------|--------------------|
| dotnet-sdk-[major]                      | dotnet-sdk-2           | 运行时主版本的最新 SDK    |                    | dotnet-sdk-[major].[latestminor]               | \<sdk version>     |
| dotnet-sdk-[major].[minor]              | dotnet-sdk-2.1         | 特定运行时的最新 SDK |                    | dotnet-sdk-[major].[minor].[latest sdk feat]xx | \<sdk version>     |
| dotnet-sdk-[major].[minor].[sdk feat]xx | dotnet-sdk-2.1.3xx     | 特定 SDK 的功能版本    | (3),(4)            | aspnetcore-runtime-[major].[minor]             | \<sdk version>     |
| aspnetcore-runtime-[major].[minor]      | aspnetcore-runtime-2.1 | 特定 ASP.NET Core 运行时   | (6),[(7)]          | dotnet-runtime-[major].[minor]                 | \<runtime version> |
| dotnet-runtime-[major].[minor]          | dotnet-runtime-2.1     | 特定运行时                | (5)                | host-fxr:\<runtime version>+                   | \<runtime version> |
| dotnet-host-fxr                         | dotnet-host-fxr        | _dependency_                    | (2)                | host:\<runtime version>+                       | \<runtime version> |
| dotnet-host                             | dotnet-host            | _dependency_                    | (1),(8),(9),(10)   |                                                | \<runtime version> |

大多数分发都需要从源中构建所有项目。 这对包有一些影响：

- 不能简单地从源中构建 `shared/Microsoft.AspNetCore.All` 下的第三方库。 因此 `aspnetcore-runtime` 包中省略了该文件夹。

- 使用 `nuget.org` 中的二进制项目填充了 `NuGetFallbackFolder`。 它应保留为空。

多个 `dotnet-sdk` 包可能会为 `NuGetFallbackFolder` 提供同样的文件。 要避免包管理器出现问题，这些文件应完全相同（包括校验和、修改日期等等）。

#### <a name="preview-versions"></a>预览版

包维护人员可以决定提供共享框架和 SDK 的预览版。 提供预览版可能会使用 `dotnet-sdk-[major].[minor].[sdk feat]xx`、`aspnetcore-runtime-[major].[minor]` 和 `dotnet-runtime-[major].[minor]` 包。 对于预览版，包的主版本号必须设为 0。 这样最终版本将被安装为此包的升级版。

#### <a name="patch-packages"></a>修补程序包

由于包的修补版本可能会带来重大更改，包维护人员可能要提供修补程序包。 这些包允许安装非自动升级的特定修补版本。 因为这些修补程序包不会随（安全）修补程序升级，所以只应在极少数情况使用。

下表显示推荐的包以及修补程序包。

| name                                           | 示例                  | 包含         | 依赖项                                              |
|------------------------------------------------|--------------------------|------------------|-----------------------------------------------------------|
| dotnet-sdk-[major]                             | dotnet-sdk-2             |                  | dotnet-sdk-[major].[latest sdk minor]                     |
| dotnet-sdk-[major].[minor]                     | dotnet-sdk-2.1           |                  | dotnet-sdk-[major].[minor].[latest sdk feat]xx            |
| dotnet-sdk-[major].[minor].[sdk feat]xx        | dotnet-sdk-2.1.3xx       |                  | dotnet-sdk-[major].[minor].[latest sdk patch]             |
| **dotnet-sdk-[major].[minor].[patch]**         | dotnet-sdk-2.1.300       | (3),(4)          | aspnetcore-runtime-[major].[minor].[sdk runtime patch]    |
| aspnetcore-runtime-[major].[minor]             | aspnetcore-runtime-2.1   |                  | aspnetcore-runtime-[major].[minor].[latest runtime patch] |
| **aspnetcore-runtime-[major].[minor].[patch]** | aspnetcore-runtime-2.1.0 | (6),[(7)]        | dotnet-runtime-[major].[minor].[patch]                    |
| dotnet-runtime-[major].[minor]                 | dotnet-runtime-2.1       |                  | dotnet-runtime-[major].[minor].[latest runtime patch]     |
| **dotnet-runtime-[major].[minor].[patch]**     | dotnet-runtime-2.1.0     | (5)              | host-fxr:\<runtime version>+                              |
| dotnet-host-fxr                                | dotnet-host-fxr          | (2)              | host:\<runtime version>+                                  |
| dotnet-host                                    | dotnet-host              | (1),(8),(9),(10) |                                                           |

除了使用修补程序包，还可以使用包管理器将包固定为特定版本。 要避免影响其他应用程序/用户，例如可能会在容器中生成并部署的应用程序。

## <a name="building-packages"></a>生成包

[dotnet/source-build](https://github.com/dotnet/source-build) 存储库中说明了如何生成 .NET Core SDK 的源 tarball 及其所有组件。 源版本存储库中的输出内容符合本文第一部分中所描述的布局。
