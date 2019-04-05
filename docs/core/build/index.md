---
title: 从源生成 .NET Core
description: 了解如何从源代码生成 .NET Core 和 .NET Core CLI。
author: bleroy
ms.date: 06/28/2017
ms.custom: seodec18
---

# <a name="build-net-core-from-source"></a>从源生成 .NET Core

能从 .NET Core 的源代码生成它在多个方面都体现出其重要性：能更轻松地将 .NET Core 移植到新平台；可实现对产品做出贡献和修复；并支持创建自定义版本的 .NET。
本文为想生成和分发自己的 .NET Core 版本的开发人员提供指导。

## <a name="build-the-clr-from-source"></a>从源生成 CLR

有关 .NET CoreCLR 的源代码，可以访问 GitHub 上的 [dotnet/coreclr](https://github.com/dotnet/coreclr/) 存储库。

生成目前依赖于以下系统必备组件：

* [Git](https://git-scm.com/)
* [CMake](https://cmake.org/)
* [Python](https://www.python.org/)
* C++ 编译器。

安装完这些必备组件后，可以 [dotnet/coreclr](https://github.com/dotnet/coreclr/) 存储库为基础，调用生成脚本（Windows 中的 `build.cmd`，或 Linux 和 macOS 中的 `build.sh`）生成 CLR。

组件的安装因操作系统 (OS) 而异。 请参阅特定 OS 的生成说明：

* [Windows](https://github.com/dotnet/coreclr/blob/master/Documentation/building/windows-instructions.md)
* [Linux](https://github.com/dotnet/coreclr/blob/master/Documentation/building/linux-instructions.md)
* [macOS](https://github.com/dotnet/coreclr/blob/master/Documentation/building/osx-instructions.md)
* [FreeBSD](https://github.com/dotnet/coreclr/blob/master/Documentation/building/freebsd-instructions.md)
* [NetBSD](https://github.com/dotnet/coreclr/blob/master/Documentation/building/netbsd-instructions.md)

不能跨 OS 进行交叉生成（仅适用于基于 X64 的 ARM）。  
必须在特定的平台上生成该平台。  

生成具有两个主要的 `buildTypes`：

* 调试（默认）- 以最低优化水平编译运行时并进行额外的运行时检查（断言）。 这种优化级别的降低和额外的检查会减慢运行时的执行速度，但对于调试来说是很有价值的。 这是开发和测试环境的推荐设置。
* 发布 - 以完全优化水平编译运行时，无需进行额外的运行时检查。 这将产生更快的运行时性能，但需要更长时间进行生成，并且难以进行调试。 将 `release` 传递给生成脚本以选择此生成类型。

此外，默认情况下，生成不仅会创建运行时可执行文件，还会生成所有测试。
这其中有不少测试都需花费大量时间，但如果只想试验一下更改，则不必执行此操作。
可以通过向生成脚本添加 `skiptests` 参数来跳过测试生成，如下例所示（在 Unix 计算机上将 `.\build` 替换为 `./build.sh`）：

```bat
    .\build skiptests
```

之前的示例演示了如何生成 `Debug` 风格，该风格启用了开发时间检查（断言）并禁用优化。 若要生成发布（全速）风格，请执行以下操作：

```bat
    .\build release skiptests
```

可使用 -? 或 -help 限定符找到 更多生成选项。

### <a name="using-your-build"></a>使用生成

生成将其所有生成的文件放在存储库底部的 `bin` 目录下。
bin\Log 目录包含生成期间生成的日志文件（生成失败时这些日志最为有用）。
实际输出位于bin\Product\[平台].[CPU 体系结构].[生成类型] 目录中，如 bin\Product\Windows_NT.x64.Release。

虽然生成的“原始”输出有时很有用，但通常只需要 NuGet 包，这些包位于之前输出目录的 `.nuget\pkg` 子目录中。

可通过两种基本方法使用新的运行时：

 1. 使用 dotnet.exe 和 NuGet 撰写应用程序。
    请参阅[使用生成](https://github.com/dotnet/coreclr/blob/master/Documentation/workflow/UsingYourBuild.md)了解如何通过使用刚创建的 NuGet 包和“dotnet”命令行接口 (CLI) 来创建使用你的新运行时的程序。 非运行时开发人员常通过此方法使用你的新运行时。

 2. 使用 corerun.exe 运行通过未打包的 DLL 运行应用程序。
    此存储库还定义了一个名为 corerun.exe 的简单主机，它与 NuGet 没有任何依赖关系。
    需要告诉主机在何处获取实际使用的所需 DLL，且必须手动将它们聚集在一起。
    [dotnet/coreclr 存储库](https://github.com/dotnet/coreclr)中的所有测试都使用这种方式，可用于快速本地“编辑-编译-调试”循环（如初步单元测试）。
    有关使用此方法的详细信息，请参阅[使用 CoreRun.exe 执行 .NET Core 应用](https://github.com/dotnet/coreclr/blob/master/Documentation/workflow/UsingCoreRun.md)。

## <a name="build-the-cli-from-source"></a>从源生成 CLI

有关 .NET Core CLI 的源代码，可以访问 GitHub 上的 [dotnet/cli](https://github.com/dotnet/cli/) 存储库。

为了生成 .NET Core CLI，需要在计算机上安装以下项。

* Windows 和 Linux：
  * PATH 上的 git
* macOS：
  * PATH 上的 git
  * Xcode
  * OpenSSL

若要进行生成，请在 Windows 上从根运行 `build.cmd`，在 Linux 和 macOS 上从根运行 `build.sh`。 如果不希望执行测试，请运行 `build.cmd -t:Compile` 或 `./build.sh -t:Compile`。 若要在 macOS Sierra 中生成 CLI，需通过运行 `export DOTNET_RUNTIME_ID=osx.10.11-x64` 设置 DOTNET_RUNTIME_ID 环境变量。

### <a name="using-your-build"></a>使用生成

使用 artifacts/{os}-{arch}/stage2 中的 `dotnet` 可执行文件来试用新生成的 CLI。 如果想在从当前控制台调用 `dotnet` 时使用生成输出，也可以将 artifacts/{os}-{arch}/stage2 添加到 PATH。

## <a name="see-also"></a>另请参阅

- [.NET Core 公共语言运行时 (CoreCLR)](https://github.com/dotnet/coreclr/blob/master/README.md)
- [.NET Core CLI 开发人员指南](https://github.com/dotnet/cli/blob/master/Documentation/project-docs/developer-guide.md)
- [.NET Core 分发打包](./distribution-packaging.md)
