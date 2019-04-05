---
title: 开始使用F#使用命令行工具
description: 了解如何构建简单的多项目解决方案F#在任何操作系统 （Windows、 macOs 或 Linux） 上使用.NET Core CLI。
ms.date: 03/26/2018
ms.openlocfilehash: bc9b223fcf133ffe8b19d5284dcbd3c14a426235
ms.sourcegitcommit: 4ac80713f6faa220e5a119d5165308a58f7ccdc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54152094"
---
# <a name="get-started-with-f-with-the-net-core-cli"></a>要开始使用 F # 使用.NET Core CLI

本文介绍如何你可以开始使用 F # 在任何操作系统上 （Windows、 macOS 或 Linux） 使用.NET Core  CLI。 它将经历构建使用由一个控制台应用程序调用的类库的多项目解决方案。

## <a name="prerequisites"></a>系统必备

若要开始，你必须安装最新[.NET Core SDK](https://www.microsoft.com/net/download/)。

本文假定，您知道如何使用命令行，并且包含首选的文本编辑器。 如果还没有使用它， [Visual Studio Code](get-started-vscode.md)是实用的选项，文本编辑器，以作为F#。

## <a name="build-a-simple-multi-project-solution"></a>构建简单的多项目解决方案

打开命令提示符处/终端，并使用[dotnet 新](../../core/tools/dotnet-new.md)命令创建名为的新解决方案文件`FSNetCore`:

```console
dotnet new sln -o FSNetCore
```

运行上述命令后会生成以下目录结构：

```console
FSNetCore
    ├── FSNetCore.sln
```

### <a name="write-a-class-library"></a>编写类库

将目录更改为*FSNetCore*。

使用`dotnet new`命令，创建一个在类库项目**src**名为库的文件夹。

```console
dotnet new classlib -lang F# -o src/Library
```

运行上述命令后会生成以下目录结构：

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

内容替换为`Library.fs`使用以下代码：

```fsharp
module Library

open Newtonsoft.Json

let getJsonNetJson value =
    sprintf "I used to be %s but now I'm %s thanks to JSON.NET!" value (JsonConvert.SerializeObject(value))
```

将 Newtonsoft.Json NuGet 包添加到类库项目。

```console
dotnet add src/Library/Library.fsproj package Newtonsoft.Json
```

添加`Library`投影到`FSNetCore`解决方案： 使用[dotnet sln 添加](../../core/tools/dotnet-sln.md)命令：

```console
dotnet sln add src/Library/Library.fsproj
```

运行`dotnet build`以生成项目。 在生成时，将还原未解析的依赖项。

### <a name="write-a-console-application-that-consumes-the-class-library"></a>编写的控制台应用程序使用类库

使用`dotnet new`命令，创建一个控制台应用程序中的**src**名为应用程序的文件夹。

```console
dotnet new console -lang F# -o src/App
```

运行上述命令后会生成以下目录结构：

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        ├── App
        │   ├── App.fsproj
        │   ├── Program.fs
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

内容替换为`Program.fs`文件使用以下代码：

```fsharp
open System
open Library

[<EntryPoint>]
let main argv =
    printfn "Nice command-line arguments! Here's what JSON.NET has to say about them:"

    argv
    |> Array.map getJsonNetJson
    |> Array.iter (printfn "%s")

    0 // return an integer exit code
```

添加对的引用`Library`使用的项目[dotnet 添加引用](../../core/tools/dotnet-add-reference.md)。

```console
dotnet add src/App/App.fsproj reference src/Library/Library.fsproj
```

添加`App`投影到`FSNetCore`解决方案： 使用`dotnet sln add`命令：

```console
dotnet sln add src/App/App.fsproj
```

还原 NuGet 依赖项，`dotnet restore`并运行`dotnet build`以生成项目。

将目录更改为`src/App`控制台项目并运行项目传递`Hello World`作为自变量：

```console
cd src/App
dotnet run Hello World
```

你应看到以下结果：

```console
Nice command-line arguments! Here's what JSON.NET has to say about them:

I used to be Hello but now I'm ""Hello"" thanks to JSON.NET!
I used to be World but now I'm ""World"" thanks to JSON.NET!
```

## <a name="next-steps"></a>后续步骤

接下来，请查看[概览F#](../tour.md)若要详细了解不同F#功能。
