---
title: C# 和 Visual Studio Code 入门
description: 了解如何使用 Visual Studio Code 创建和调试首个 C# .NET Core 应用。
author: kendrahavens
ms.date: 12/05/2018
ms.custom: seodec18
ms.openlocfilehash: 8df26651a7b35e5b6c9bdcb54d09c97525e12426
ms.sourcegitcommit: 5d9f4b805787f890ca6e0dc7ea30a43018bc9cbb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2019
ms.locfileid: "57788331"
---
# <a name="get-started-with-c-and-visual-studio-code"></a>C# 和 Visual Studio Code 入门

.NET Core 提供了快速运行的模块化平台，用于创建在 Windows、Linux 和 macOS 上运行的应用程序。 带 C# 扩展的 Visual Studio Code 提供功能强大的编辑体验，完全支持 C# IntelliSense（智能代码填充）和调试。

## <a name="prerequisites"></a>系统必备

1. 安装 [Visual Studio Code](https://code.visualstudio.com/)。
2. 获取 [.NET Core SDK](https://www.microsoft.com/net/download/core)。
3. 安装 Visual Studio Code 的 [C# 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp)。 若要详细了解如何在 Visual Studio Code 上安装扩展，请访问 [VS Code 扩展市场](https://code.visualstudio.com/docs/editor/extension-gallery)。

## <a name="hello-world"></a>Hello World

让我们从 .NET Core 上的一个简单“Hello World”程序入手：

1. 打开项目：

    * 打开 Visual Studio Code。
    * 依次单击左侧菜单上的“资源管理器”图标和 **“打开文件夹”**。
    * 从主菜单中选择“文件” > “打开文件夹”，打开要在其中放置 C# 项目的文件夹，然后单击“选择文件夹”。 在我们的示例中，为项目创建名为“HelloWorld”的文件夹。

      ![Visual Studio Code“打开文件夹”](media/with-visual-studio-code/vs-code-open-folder.png)

2. 初始化 C# 项目：
    * 通过从主菜单中选择“视图” > “集成终端”，从 Visual Studio Code 中打开集成终端。
    * 在终端窗口中，键入“`dotnet new console`”。
    * 此命令在已编写“Hello World”简单程序的文件夹中创建 `Program.cs` 文件，以及 `HelloWorld.csproj` C# 项目文件。

      ![dotnet new 命令](media/with-visual-studio-code/dotnet-new-command.png)

3. 解析生成资产：

    * 对于 .NET Core 1.x，键入 `dotnet restore`。 运行 `dotnet restore` 后，便有权访问生成项目所需的 .NET Core 包。

      ![dotnet restore 命令](media/with-visual-studio-code/dotnet-restore-command.png)

      [!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

4. 运行“Hello World”程序：

    * 键入 `dotnet run`。

      ![dotnet run 命令](media/with-visual-studio-code/dotnet-run-command.png)

还可以观看简短的视频教程，以获取更多关于在 [Windows](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core)、[macOS](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-using-CSharp-and-NET-Core-on-MacOS) 或 [Linux](https://channel9.msdn.com/Blogs/dotnet/Get-started-with-VS-Code-Csharp-dotnet-Core-Ubuntu) 上进行安装的帮助。

## <a name="debug"></a>调试

1. 单击打开 *Program.cs*。 在 Visual Studio Code 中首次打开 C# 文件时，会在编辑器中加载 [OmniSharp](https://www.omnisharp.net/)。

    ![打开 Program.cs 文件](media/with-visual-studio-code/open-program-cs.png)

2. Visual Studio Code 会提示添加缺少的资产，以生成和调试应用。 选择 **“是”**。

    ![提示添加缺少的资产](media/with-visual-studio-code/missing-assets.png)

3. 若要打开调试视图，请单击左侧菜单上的“调试”图标。

    ![在 Visual Studio Code 中打开“调试”选项卡](media/with-visual-studio-code/open-debug-tab.png)

4. 找到窗格最上面的绿色箭头。 请确保已选择旁边下拉列表中的“`.NET Core Launch (console)`”。

    ![在 Visual Studio Code 中选择“.NET Core”](media/with-visual-studio-code/select-net-core.png)

5. 单击第 9 行旁边的编辑器边距（编辑器中行号左侧的空间）或者将文本光标移动到编辑器中的第 9 行并按 <kbd>F9</kbd>，为项目添加断点。

    ![设置断点](media/with-visual-studio-code/set-breakpoint-vs-code.png)

6. 要开始调试，请选择 <kbd>F5</kbd> 或绿色箭头。 在到达你在上一步中设置的断点时，调试器会停止执行程序。
    * 调试时，可以在左上角的窗格中查看局部变量，也可以使用调试控制台进行查看。

7. 选择最上面的蓝色箭头以继续调试，或选择最上面的红色方块以停止调试。

    ![在 Visual Studio Code 中运行并调试](media/with-visual-studio-code/run-debug-vs-code.png)

> [!TIP]
> 若要详细了解如何使用 OmniSharp 在 Visual Studio Code 中进行 .NET Core 调试，以及相关的疑难解答提示，请参阅[有关设置 .NET Core 调试器的说明](https://github.com/OmniSharp/omnisharp-vscode/blob/master/debugger.md)。

## <a name="add-a-class"></a>添加类

1. 若要添加一个新类，请右键单击 VSCode Explorer 并选择“新文件”。 此操作会将新文件添加到在 VSCode 中打开的文件夹中。
2. 将文件命名为 `Class1.cs`。 必须在末尾使用 `.cs` 扩展名保存它，以便将其识别为 csharp 文件。
3. 添加下面的代码，以创建第一个类。 确保包括正确的命名空间，以便可以从 `Program.cs` 文件引用它。
``` csharp
using System;

namespace HelloWorld
{
    public class Class1
    {
        public string ReturnMessage()
        {
            return "Happy coding!";
        }
    }
}
```

4. 通过添加下面的代码，从 `Program.cs` 中的主要方法调用新类。

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Class1 c1 = new Class1();
            Console.WriteLine($"Hello World! {c1.ReturnMessage()}");
        }
    }
}
```

5. 保存更改并再次运行程序。 新消息应显示追加的字符串。
```console
> dotnet run
Hello World! Happy coding!
```

## <a name="faq"></a>FAQ

### <a name="im-missing-required-assets-to-build-and-debug-c-in-visual-studio-code-my-debugger-says-no-configuration"></a>缺少在 Visual Studio Code 中生成和调试 C# 所需的资产。 调试器显示“无配置”。

Visual Studio Code C# 扩展可生成用于生成和调试的资产。 首次打开 C# 项目时，Visual Studio Code 会提示用户生成这些资产。 如果当时并未生成这些资产，仍可以通过打开命令面板（“视图”>“命令面板”）并键入“>.NET：生成用于生成和调试的资产”来运行此命令。 选择此方法可生成所需的 .vscode、launch.json 和 tasks.jsonn 配置文件。

## <a name="see-also"></a>请参阅

- [设置 Visual Studio Code](https://code.visualstudio.com/docs/setup/setup-overview)
- [在 Visual Studio Code 中进行调试](https://code.visualstudio.com/Docs/editor/debugging)
