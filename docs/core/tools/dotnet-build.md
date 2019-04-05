---
title: dotnet build 命令
description: dotnet build 命令可生成项目及其所有依赖项。
ms.date: 12/04/2018
ms.openlocfilehash: 1e5e05d51f98394b2b77e3a8fc645cf9712b0a0f
ms.sourcegitcommit: e6ad58812807937b03f5c581a219dcd7d1726b1d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53169686"
---
# <a name="dotnet-build"></a>dotnet 生成

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet build` - 生成项目及其所有依赖项。

## <a name="synopsis"></a>摘要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet build [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--force] [--no-dependencies] [--no-incremental]
    [--no-restore] [-o|--output] [-r|--runtime] [-v|--verbosity] [--version-suffix]

dotnet build [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet build [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--no-dependencies] [--no-incremental] [-o|--output]
    [-r|--runtime] [-v|--verbosity] [--version-suffix]

dotnet build [-h|--help]
```
---

## <a name="description"></a>说明

`dotnet build` 命令将项目及其依赖项生成为一组二进制文件。 二进制文件包括中间语言 (IL) 文件（带 *.dll* 扩展名）和用于调试的符号文件（带 *.pdb* 扩展名）中的项目的代码。 生成依赖项 JSON 文件 (*\*.deps.json*)，该文件列出了应用程序的依赖项。 生成 *\*.runtimeconfig.json* 文件，该文件指定应用程序的共享运行时及其版本。

如果项目有第三方依赖项（如来自 NuGet 的库），将从 NuGet 缓存解析这些依赖项，并且它们不适用于项目的生成输出。 考虑到这一点，`dotnet build` 的产品还未准备好转移到另一台计算机进行运行。 这与 .NET Framework 的行为相反，后者在构建可执行项目（一个应用程序）时，将生成可在任何已安装 .NET Framework 的计算机上运行的输出。 为了能够获得相似的 .NET Core 使用体验，需要使用 [dotnet publish](dotnet-publish.md) 命令。 有关详细信息，请参阅 [.NET Core 应用程序部署](../deploying/index.md)。

构建需要 *project.assets.json* 文件，该文件列出了你的应用程序的依赖项。 此文件在 [`dotnet restore`](dotnet-restore.md) 执行时创建。 如果资产文件未就位，那么工具将无法解析引用程序集，进而导致错误生成。 使用 .NET Core 1.x SDK，需要在运行 `dotnet build` 之前显式运行 `dotnet restore`。 自 .NET Core 2.0 SDK 起，`dotnet restore` 在 `dotnet build` 运行时隐式运行。 若要在运行 build 命令时禁用隐式还原，可以传递 `--no-restore` 选项。

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

项目是否可执行由项目文件中的 `<OutputType>` 属性决定。 以下示例显示生成可执行代码的项目：

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

若要生成库，则省略 `<OutputType>` 属性。 生成输出中的主要区别在于，针对某个库的 IL DLL 不包含入口点，并且不能执行。

### <a name="msbuild"></a>MSBuild

`dotnet build` 使用 MSBuild 生成项目，因此它支持并行生成和增量生成。 有关详细信息，请参阅[增量生成](/visualstudio/msbuild/incremental-builds)。

除其自己的选项外，`dotnet build` 命令也接受 MSBuild 选项，如用来设置属性的 `-p` 或用来定义记录器的 `-l`。 有关这些选项的详细信息，请参阅 [MSBuild 命令行参考](/visualstudio/msbuild/msbuild-command-line-reference)。 或者也可以使用 [dotnet msbuild](dotnet-msbuild.md) 命令。

运行 `dotnet build` 相当于 `dotnet msbuild -restore -target:Build`。

## <a name="arguments"></a>自变量

`PROJECT | SOLUTION`

要生成的项目或解决方案文件。 如果未指定项目或解决方案文件，MSBuild 会在当前工作目录中搜索以 proj 或 sln 结尾的文件扩展名并使用该文件。

## <a name="options"></a>选项

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

* **`-c|--configuration {Debug|Release}`**

  定义生成配置。 默认值为 `Debug`。

* **`-f|--framework <FRAMEWORK>`**

  编译特定[框架](../../standard/frameworks.md)。 必须在[项目文件](csproj.md)中定义该框架。

* **`--force`**

  强制解析所有依赖项，即使上次还原已成功，也不例外。 指定此标记等同于删除 project.assets.json 文件。

* **`-h|--help`**

  打印出有关命令的简短帮助。

* **`--no-dependencies`**

  忽略项目到项目 (P2P) 引用，并仅生成指定的根项目。

* **`--no-incremental`**

  将生成标记为对增量生成不安全。 此标记关闭增量编译，并强制完全重新生成项目依赖项关系图。

* **`--no-restore`**

  在生成期间不执行隐式还原。

* **`-o|--output <OUTPUT_DIRECTORY>`**

  放置生成二进制文件的目录。 指定此选项时还需要定义 `--framework`。 如果未指定，则默认路径为 `./bin/<configuration>/<framework>/`。

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  指定目标运行时。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。

* **`-v|--verbosity <LEVEL>`**

  设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

* **`--version-suffix <VERSION_SUFFIX>`**

  在项目文件的版本字段中定义星号 (`*`) 版本后缀。 格式遵循 NuGet 的版本准则。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

* **`-c|--configuration {Debug|Release}`**

  定义生成配置。 默认值为 `Debug`。

* **`-f|--framework <FRAMEWORK>`**

  编译特定[框架](../../standard/frameworks.md)。 必须在[项目文件](csproj.md)中定义该框架。

* **`-h|--help`**

  打印出有关命令的简短帮助。

* **`--no-dependencies`**

  忽略项目到项目 (P2P) 引用，并仅生成指定的根项目。

* **`--no-incremental`**

  将生成标记为对增量生成不安全。 此标记关闭增量编译，并强制完全重新生成项目依赖项关系图。

* **`-o|--output <OUTPUT_DIRECTORY>`**

  放置生成二进制文件的目录。 指定此选项时还需要定义 `--framework`。

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  指定目标运行时。 有关运行时标识符 (RID) 的列表，请参阅 [RID 目录](../rid-catalog.md)。

* **`-v|--verbosity <LEVEL>`**

  设置命令的详细级别。 允许使用的值为 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

* **`--version-suffix <VERSION_SUFFIX>`**

  在项目文件的版本字段中定义星号 (`*`) 版本后缀。 格式遵循 NuGet 的版本准则。

---

## <a name="examples"></a>示例

* 生成项目及其依赖项：

  ```console
  dotnet build
  ```

* 使用“发布”配置生成项目及其依赖项：

  ```console
  dotnet build --configuration Release
  ```

* 针对特定运行时（本例中为 Ubuntu 16.04）生成项目及其依赖项：

  ```console
  dotnet build --runtime ubuntu.16.04-x64
  ```

* 生成项目，并在还原操作过程中使用指定的 NuGet 包源（.NET Core 2.0 SDK 及更高版本）：

  ```console
  dotnet build --source c:\packages\mypackages
  ```

* 生成项目，并将 1.2.3.4 版本设置为生成参数：

  ```console
  dotnet build -p:Version=1.2.3.4
  ```