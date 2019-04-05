---
title: Visual Studio 开发人员命令提示
ms.date: 08/14/2018
helpviewer_keywords:
- command prompt, Windows SDK
- Visual Studio command prompt
- command prompt, Visual Studio
- SDK command prompt
- tools [.NET Framework], setting environment variables
- environment variables, setting for tools
- developer command prompt
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6e648cdadb567919d320ea8a12d30b7be306e67a
ms.sourcegitcommit: a36cfc9dbbfc04bd88971f96e8a3f8e283c15d42
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2019
ms.locfileid: "54221227"
---
# <a name="developer-command-prompt-for-visual-studio"></a>Visual Studio 开发人员命令提示

Visual Studio 的开发人员命令提示符使你可以更轻松地使用 .NET Framework 工具。 它是一个自动设置特定环境变量的命令提示符。

> [!div class="button"]
> [下载 Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="search-for-the-command-prompt-on-your-machine"></a>在计算机中搜索命令提示符

你可能会有多个命令提示符，具体取决于你安装的 Visual Studio 及其他任何 SDK 的版本。 例如，Visual Studio 的 64 位版本同时提供 32 位和 64 位命令提示。 （大多数工具的 32 位和 64 位版本都相同；但少数工具针对具体的 32 位和 64 位环境做了一些改变。）如果以下步骤不起作用，可以尝试[在计算机中手动查找文件](#manually-locate-the-files-on-your-machine)或[从 Visual Studio 内部运行命令提示符](#run-the-command-prompt-from-inside-visual-studio)。

### <a name="in-windows-10"></a>在 Windows 10 中

1. 在任务栏的搜索框中，开始键入工具的名称，例如 `dev` 或 `developer command prompt`。 然后显示一个列表，其中包含与搜索模式匹配的已安装应用。 如果要查找不同的命令提示，请尝试输入不同的搜索词，例如 `prompt`。

2. 选择“Visual Studio 开发人员命令提示”（或者你想使用的命令提示）。

### <a name="in-windows-81"></a>在 Windows 8.1 中

1. 通过按键盘上的 Windows 徽标键 ![Windows 徽标](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo")（举例说明），转到“开始”屏幕。

2. 在“开始”屏幕上，按 Ctrl+Tab 打开“应用程序”列表，然后输入 `V`。 然后显示一个列表，其中包含所有已安装的 Visual Studio 命令提示。

3. 选择“开发人员命令提示”（或者你想使用的命令提示）。

### <a name="in-windows-8"></a>在 Windows 8 中

1. 通过按键盘上的 Windows 徽标键 ![Windows 徽标](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo")（举例说明），转到“开始”屏幕。

2. 在“开始”屏幕上，按 Windows 徽标键 ![Windows 徽标](../get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") `+ Z`。

3. 选择屏幕底部的“应用视图”图标，然后输入 `V`。 然后显示一个列表，其中包含所有已安装的 Visual Studio 命令提示。

4. 选择“开发人员命令提示”（或者你想使用的命令提示）。

### <a name="in-windows-7"></a>在 Windows 7 中

1. 选择“开始”，展开“所有程序”，然后展开“Microsoft Visual Studio”。

2. 根据已安装的 Visual Studio 版本，选择“Visual Studio Tools”、“Visual Studio 命令提示”或你想使用的命令提示。

如果安装了其他 SDK，例如 [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 或[之前的版本](https://developer.microsoft.com/windows/downloads/sdk-archive)，则可能看到有关 ARM、x86 或 x64 体系结构的其他命令提示符。 查看单个工具的文档，以确定应使用哪个版本的命令提示。

## <a name="manually-locate-the-files-on-your-machine"></a>在计算机中手动查找文件

已安装的命令提示的快捷方式通常放在 Visual Studio 的“开始菜单”文件夹中，例如 C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Visual Studio 2017\Visual Studio Tools。 但是如果出于某种原因，搜索命令提示未产生预期的效果，你可以尝试在计算机中手动查找快捷方式。 请尝试搜索命令提示文件的名称，例如 VsDevCmd.bat，或者转到“工具”文件夹，例如 C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\Tools（该路径根据你的 Visual Studio 版本和安装位置而变化）。

## <a name="run-the-command-prompt-from-inside-visual-studio"></a>从 Visual Studio 内部运行命令提示符

为便于访问，你可以将 Visual Studio 开发人员命令提示或其他任何命令提示符添加到 Visual Studio 中的“工具”菜单中。 要使该工具可用，请将其添加到外部工具列表中。 步骤如下：

1. 打开 Visual Studio。

2. 选择“工具”菜单，然后选择“外部工具”。

3. 在“外部工具”对话框中，选择“添加”按钮。 随即出现一个新项。

4. 为新菜单项输入“标题”，例如 `Command Prompt`。

5. 在“命令”字段中，指定要启动的文件，例如 `%comspec%` 或 `C:\Windows\System32\cmd.exe`。

6. 在“参数”字段中，指定可在其中找到要使用的特定命令提示的位置，例如 `/k "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\Tools\VsDevCmd.bat"`（此命令启动随 Visual Studio 2017 Enterprise 一起安装的开发人员命令提示）。 根据 Visual Studio 版本和安装位置更改此值。

7. 为“初始目录”字段选择一个值，例如“项目目录”。

8. 选择“确定”  按钮。

   系统添加了新菜单项，并且你可以从“工具”菜单访问命令提示符。

   ![Visual Studio 中的命令提示符菜单项](media/command-prompt-vs-menu.png)

## <a name="see-also"></a>请参阅

- [工具](../../../docs/framework/tools/index.md)
- [管理外部工具](/visualstudio/ide/managing-external-tools)
