---
title: 选择 C# 语言版本 - C# 指南
description: 配置编译器以使用特定的编译器版本执行语法验证
ms.date: 02/28/2019
ms.openlocfilehash: 6d31a757171bd2eecdcc1fbd3da765dcb3fe45c0
ms.sourcegitcommit: 79066169e93d9d65203028b21983574ad9dcf6b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57212022"
---
# <a name="select-the-c-language-version"></a>选择 C# 语言版本

C# 编译器根据项目的一个或多个目标框架确定默认语言版本。 如果你的项目是以具有相应预览语言版本的预览框架为目标，那么使用的语言版本是预览语言版本。 如果你的项目不以预览框架为目标，则使用的语言版本是最新的次要版本。

例如，在 .NET Core 3.0 的预览版期间，任何以 `netcoreapp3.0` 或 `netstandard2.1` 为目标的项目（均为预览版）都将使用 C# 8.0 语言（同样为预览版）。 以任何已发布版本为目标的项目将使用 C# 7.3（最新发布的版本）。 此行为意味着任何以 .NET Framework 为目标的项目都将使用最新版本 (C# 7.3)。 

借助此功能，在开发环境中安装新版本的 SDK 和工具时，不必选择在项目中引入新的语言功能。 可以在生成计算机上安装最新的 SDK 和工具。 每个项目可以配置为对其生成使用该语言的特定版本。 默认行为意味着只有在项目以这些框架为目标时，才会启用依赖于新类型或新 CLR 行为的任何语言功能。

可以通过指定语言版本来覆盖默认行为。 有几种方法可以设置语言版本：

- 依靠 [Visual Studio 快速操作](#visual-studio-quick-action)。
- 在 [Visual Studio UI](#set-the-language-version-in-visual-studio) 中设置语言版本。
- 手动编辑 [.csproj 文件](#edit-the-csproj-file)。
- 为[子目录中的多个项目](#configure-multiple-projects)设置语言版本。
- 配置 [`-langversion` 编译器选项](#set-the-langversion-compiler-option)。

## <a name="visual-studio-quick-action"></a>Visual Studio 快速操作

Visual Studio 可帮助你确定需要的语言版本。 如果你使用的语言功能不适合当前配置的版本，Visual Studio 会显示一项潜在修复来为项目更新语言版本。

## <a name="set-the-language-version-in-visual-studio"></a>在 Visual Studio 中设置语言版本

可以在 Visual Studio 中设置该版本。 右键单击“解决方案资源管理器”中的项目节点，然后选择“属性”。 选择**生成**选项卡并选择**高级**按钮。 在下拉列表中，选择版本。 下图显示“最新”设置：

![高级生成设置的屏幕截图，在这里可以指定语言版本](./media/configure-language-version/advanced-build-settings.png)

> [!NOTE]
> 如果使用 Visual Studio IDE 来更新 csproj 文件，IDE 将为每个生成配置创建单独的节点。 通常在所有生成配置中都设置相同的值，但你需要为每个生成配置显式地设置值，或在修改此设置时选择"所有配置"。 在 csproj 文件中，你可以看到如下内容：
>
>```xml
> <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
>  <LangVersion>latest</LangVersion>
></PropertyGroup>
>
> <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|AnyCPU'">
>  <LangVersion>latest</LangVersion>
> </PropertyGroup>
> ```
>

## <a name="edit-the-csproj-file"></a>编辑 csproj 文件

可在 .csproj 文件中设置语言版本。 添加如下元素：

```xml
<PropertyGroup>
   <LangVersion>latest</LangVersion>
</PropertyGroup>
```

`latest` 值使用 C# 语言的最新次要版本。 有效值为：

|值|含义|
|------------|-------------|
|preview|编译器接受最新预览版中的所有有效语言语法。|
|最新|编译器接受最新发布的编译器版本（包括次要版本）中的语法。|
|latestMajor|编译器接受最新发布的编译器主要版本中的语法。|
|8.0|编译器只接受 C# 8.0 或更低版本中所含的语法。|
|7.3|编译器只接受 C# 7.3 或更低版本中所含的语法。|
|7.2|编译器只接受 C# 7.2 或更低版本中所含的语法。|
|7.1|编译器只接受 C# 7.1 或更低版本中所含的语法。|
|7|编译器只接受 C# 7.0 或更低版本中所含的语法。|
|6|编译器只接受 C# 6.0 或更低版本中所含的语法。|
|5|编译器只接受 C# 5.0 或更低版本中所含的语法。|
|4|编译器只接受 C# 4.0 或更低版本中所含的语法。|
|3|编译器只接受 C# 3.0 或更低版本中所含的语法。|
|ISO-2|编译器只接受 ISO/IEC 23270:2006 C# (2.0) 中所含的语法 |
|ISO-1|编译器只接受 ISO/IEC 23270:2003 C# (1.0/1.2) 中所含的语法 |

## <a name="configure-multiple-projects"></a>配置多个项目

可以创建包含 `<LangVersion>` 元素的 Directory.build.props 文件来配置多个目录。 通常是在解决方案目录中完成这件事。 将以下内容添加到解决方案目录中的 Directory.build.props 文件：

```xml
<Project>
 <PropertyGroup>
   <LangVersion>7.3</LangVersion>
 </PropertyGroup>
</Project>
```

现在，包含该文件的目录的每个子目录中的生成都将使用 C# 版本 7.3 语法。 有关详细信息，请参阅关于[自定义生成](/visualstudio/msbuild/customize-your-build)的文章。

## <a name="set-the-langversion-compiler-option"></a>选择 langversion 编译器选项

你可以使用 `-langversion` 命令行选项。 有关详细信息，请参阅关于 [/langversion](../language-reference/compiler-options/langversion-compiler-option.md) 编译器选项的文章。 若要查看有效值的列表，请键入 `csc -langversion:?`。
