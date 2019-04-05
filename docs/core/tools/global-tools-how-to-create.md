---
title: 如何创建 .NET Core 全局工具
description: 介绍如何创建全局工具。 全局工具是一个通过 .NET Core CLI 安装的控制台应用程序。
author: Thraka
ms.author: adegeo
ms.date: 08/22/2018
ms.openlocfilehash: a54cb0a8c32da6a89ab1c3b7757df10fd9adf5cf
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57677859"
---
# <a name="create-a-net-core-global-tool-using-the-net-core-cli"></a>使用 .NET Core CLI 创建 .NET Core 全局工具

本文介绍如何创建和打包 .NET Core 全局工具。 使用 .NET Core CLI，可以创建一个控制台应用程序作为全局工具，便于其他人轻松地安装并运行。 .NET core 全局工具是从 .NET Core CLI 安装的 NuGet 包。 有关全局工具的详细信息，请参阅 [.NET Core 全局工具概述](global-tools.md)。

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

## <a name="create-a-project"></a>创建项目

本文使用 .NET Core CLI 创建和管理项目。

我们的示例工具是一个可以生成 ASCII 自动程序并打印消息的控制台应用程序。 首先，创建新的 .NET Core 控制台应用程序。

```console
dotnet new console -o botsay
```

导航到由先前命令创建的 `botsay` 目录。

## <a name="add-the-code"></a>添加代码

使用喜欢的文本编辑器（如 `vim` 或 [Visual Studio Code](https://code.visualstudio.com/)）打开 `Program.cs` 文件。

将以下 `using` 指令添加到文件顶部，这有助于缩短代码以显示应用程序的版本信息。

```csharp
using System.Reflection;
```

接下来，向下移动到 `Main` 方法。 将方法替换为以下代码，以便处理应用程序的命令行参数。 如果未传递任何参数，将显示简短的帮助消息。 否则，所有这些参数都将转换为字符串并使用自动程序打印。

```csharp
static void Main(string[] args)
{
    if (args.Length == 0)
    {
        var versionString = Assembly.GetEntryAssembly()
                                .GetCustomAttribute<AssemblyInformationalVersionAttribute>()
                                .InformationalVersion
                                .ToString();

        Console.WriteLine($"botsay v{versionString}");
        Console.WriteLine("-------------");
        Console.WriteLine("\nUsage:");
        Console.WriteLine("  botsay <message>");
        return;
    }

    ShowBot(string.Join(' ', args));
}
```

### <a name="create-the-bot"></a>创建自动程序

接下来，添加一个名为 `ShowBot` 的新方法，该方法采用一个字符串参数。 此方法将输出消息和 ASCII 自动程序。 ASCII 自动程序代码摘自 [dotnetbot](https://github.com/dotnet/core/blob/master/samples/dotnetsay/Program.cs) 示例。

```csharp
static void ShowBot(string message)
{
    string bot = $"\n        {message}";
    bot += @"
    __________________
                      \
                       \
                          ....
                          ....'
                           ....
                        ..........
                    .............'..'..
                 ................'..'.....
               .......'..........'..'..'....
              ........'..........'..'..'.....
             .'....'..'..........'..'.......'.
             .'..................'...   ......
             .  ......'.........         .....
             .    _            __        ......
            ..    #            ##        ......
           ....       .                 .......
           ......  .......          ............
            ................  ......................
            ........................'................
           ......................'..'......    .......
        .........................'..'.....       .......
     ........    ..'.............'..'....      ..........
   ..'..'...      ...............'.......      ..........
  ...'......     ...... ..........  ......         .......
 ...........   .......              ........        ......
.......        '...'.'.              '.'.'.'         ....
.......       .....'..               ..'.....
   ..       ..........               ..'........
          ............               ..............
         .............               '..............
        ...........'..              .'.'............
       ...............              .'.'.............
      .............'..               ..'..'...........
      ...............                 .'..............
       .........                        ..............
        .....
";
    Console.WriteLine(bot);
}
```

### <a name="test-the-tool"></a>测试工具

运行项目并观察输出。 尝试使用命令行的这些变体来查看不同的结果：

```csharp
dotnet run
dotnet run -- "Hello from the bot"
dotnet run -- hello from the bot
```

位于 `--` 分隔符后的所有参数均会传递给应用程序。

## <a name="setup-the-global-tool"></a>安装全局工具

在将应用程序作为全局工具打包并分发之前，你需要修改项目文件。 打开 `botsay.csproj` 文件，并向 `<Project><PropertyGroup>` 节点添加三个新的 XML 节点：

- `<PackAsTool>`\
[必需] 表示将打包应用程序以作为全局工具进行安装。

- `<ToolCommandName>`\
[可选] 工具的替代名称，否则工具的命令名称将以项目文件命名。 一个包中可以有多个工具，选择一个唯一且友好的名称有助于与同一包中的其他工具区别开来。

- `<PackageOutputPath>`\
[可选] 将生成 NuGet 包的位置。 NuGet 包是.NET Core CLI 全局工具用于安装你的工具的包。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>

    <PackAsTool>true</PackAsTool>
    <ToolCommandName>botsay</ToolCommandName>
    <PackageOutputPath>./nupkg</PackageOutputPath>

  </PropertyGroup>

</Project>
```

虽然 `<PackageOutputPath>` 不是必选的，请在本示例中使用它。 请务必将其设置为：`<PackageOutputPath>./nupkg</PackageOutputPath>`。

接下来，创建应用程序的 NuGet 包。

```console
dotnet pack
```

`botsay.1.0.0.nupkg` 文件在由 `botsay.csproj` 文件的 `<PackageOutputPath>` XML 值标识的文件夹中创建，在本示例中为 `./nupkg` 文件夹。 这样，就可以轻松地安装和测试了。 如果想要公开发布一个工具，请将其上传到 [https://www.nuget.org](https://www.nuget.org)。该工具在 NuGet 上可用后，开发人员就可以使用 [dotnet tool install](dotnet-tool-install.md) 命令的 `--global` 选项在用户范围内安装该工具。

现在你已有一个包，请通过该包安装工具：

```console
dotnet tool install --global --add-source ./nupkg botsay
```

`--add-source` 参数指示 .NET Core CLI 临时使用 `./nupkg` 文件夹（我们的 `<PackageOutputPath>` 文件夹）作为 NuGet 包的附加源数据源。 有关安装全局工具的详细信息，请参阅 [.NET Core 全局工具概述](global-tools.md)。

如果安装成功，会出现一条消息，显示用于调用工具的命令以及所安装的版本，类似于以下示例：

```
You can invoke the tool using the following command: botsay
Tool 'botsay' (version '1.0.0') was successfully installed.
```

现在应能够键入 `botsay`，并获得来自工具的响应。

> [!NOTE]
> 如果安装已成功，但无法使用 `botsay` 命令，可能需要打开新的终端来刷新 PATH。

## <a name="remove-the-tool"></a>删除工具

完成工具的试验后，可以使用以下命令将其删除：

```console
dotnet tool uninstall -g botsay
```
