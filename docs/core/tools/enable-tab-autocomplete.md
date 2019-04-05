---
title: 启用 tab 自动补全
description: 本文介绍如何针对适用于 PowerShell、Bash 和 zsh 的 .NET Core CLI 启用 tab 自动补全。
author: thraka
ms.author: adegeo
ms.date: 12/17/2018
ms.openlocfilehash: 16574e02aa9f9167602401eef2ad7a73e07ad107
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57203332"
---
# <a name="how-to-enable-tab-completion-for-net-core-cli"></a>如何为 .NET Core CLI 启用 TAB 自动补全功能

从.NET Core 2.0 SDK 开始，NET Core CLI 支持 tab 自动补全。 本文介绍如何为三个 shell、PowerShell、Bash 和 zsh 配置 tab 自动补全。 其他 shell 可能支持自动补全功能。 请参阅有关如何配置自动补全功能的文档，这些步骤应与本文中介绍的步骤类似。

[!INCLUDE [topic-appliesto-net-core-2plus](~/includes/topic-appliesto-net-core-2plus.md)]

设置完成后，通过在 shell 中键入 `dotnet` 命令，然后按下 TAB 键来触发 .NET Core CLI 的 tab 自动补全。 当前命令行将发送到 `dotnet complete` 命令，结果将由 shell 处理。 可以通过直接向 `dotnet complete` 命令发送内容来测试结果而无需启用 tab 自动补全。 例如:

```
> dotnet complete "dotnet a"
add
clean
--diagnostics
migrate
pack
```

如果该命令不起作用，请确保已安装 .NET Core 2.0 SDK 或更高版本。 如果已安装，但该命令仍不起作用，请确保 `dotnet` 命令解析为 .NET Core 2.0 SDK 及更高版本。 使用 `dotnet --version` 命令查看当前路径解析为的 `dotnet` 的版本。 有关详细信息，请参阅[选择要使用的 .NET Core 版本](../versions/selection.md)页面。

### <a name="examples"></a>示例

下面是 tab 自动补全提供的一些示例：

输入                                | 将变为                                                                     | 因为
:------------------------------------|:----------------------------------------------------------------------------|:--------------------------------
`dotnet a⇥`                          | `dotnet add`                                                                 | `add` 是第一项子命令，按字母排序。
`dotnet add p⇥`                      | `dotnet add --help`                                                          | Tab 自动补全匹配子字符串，`--help` 首先按字母顺序排列。
`dotnet add p⇥⇥`                    | `dotnet add package`                                                          | 第二次按 Tab 将显示下一条建议。      
`dotnet add package Microsoft⇥`      | `dotnet add package Microsoft.ApplicationInsights.Web`                      | 结果按字母顺序返回。
`dotnet remove reference ⇥`          | `dotnet remove reference ..\..\src\OmniSharp.DotNet\OmniSharp.DotNet.csproj` | Tab 自动补全是可识别的项目文件。

## <a name="powershell"></a>PowerShell

要将 tab 自动补全添加到适用于 .NET Core CLI 的 PowerShell，请创建或编辑存储在变量 `$PROFILE` 中的配置文件。 有关详细信息，请参阅[如何创建配置文件](/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-6#how-to-create-a-profile)和[配置文件和执行策略](/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-6#profiles-and-execution-policy)。 

将以下代码添加到配置文件中：

```powershell
# PowerShell parameter completion shim for the dotnet CLI 
Register-ArgumentCompleter -Native -CommandName dotnet -ScriptBlock {
     param($commandName, $wordToComplete, $cursorPosition)
         dotnet complete --position $cursorPosition "$wordToComplete" | ForEach-Object {
            [System.Management.Automation.CompletionResult]::new($_, $_, 'ParameterValue', $_)
         }
 }
```

## <a name="bash"></a>Bash

要将 tab 自动补全添加到适用于 .NET Core CLI 的 bash shell，请将以下代码添加到 `.bashrc` 文件：

```bash
# bash parameter completion for the dotnet CLI

_dotnet_bash_complete()
{
  local word=${COMP_WORDS[COMP_CWORD]}

  local completions
  completions="$(dotnet complete --position "${COMP_POINT}" "${COMP_LINE}")"

  COMPREPLY=( $(compgen -W "$completions" -- "$word") )
}

complete -f -F _dotnet_bash_complete dotnet
```

## <a name="zsh"></a>Zsh

要将 tab 自动补全添加到适用于 .NET Core CLI 的 zsh shell，请将以下代码添加到 `.zshrc` 文件：

```zsh
# zsh parameter completion for the dotnet CLI

_dotnet_zsh_complete() 
{
  local completions=("$(dotnet complete "$words")")

  reply=( "${(ps:\n:)completions}" )
}

compctl -K _dotnet_zsh_complete dotnet
```
