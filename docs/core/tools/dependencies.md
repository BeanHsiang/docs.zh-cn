---
title: 在 .NET Core 工具中管理依赖项
description: 介绍如何使用 .NET Core 工具管理依赖项。
ms.date: 03/06/2017
ms.custom: seodec18
ms.openlocfilehash: 701100476b8b08aa4b0229bd0de30d02c54ddce9
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57673868"
---
# <a name="managing-dependencies-with-net-core-sdk-10"></a>使用 .NET Core SDK 1.0 管理依赖项

在 .NET Core 项目从 project.json 移动到 csproj 和 MSBuild 的同时，还投入了大笔资金将项目文件和资产统一，以便跟踪依赖项。 对于 .NET Core 项目，这与 project.json 的做法类似。 没有单独的 JSON 或 XML 文件来跟踪 NuGet 依赖项。 通过这种改变，我们还在名为 `<PackageReference>` 的 csproj 语法中引入了另一种类型的引用。 

本文档介绍了新的引用类型。 它还演示了如何使用此新引用类型将包依赖项添加到项目。 

## <a name="the-new-packagereference-element"></a>新 \<PackageReference> 元素
`<PackageReference>` 具有下列基本结构：

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" />
```

如果你熟悉 MSBuild，则它看起来和已有的引用类型很相似。 关键是 `Include` 语句，它指定要添加到项目的包 ID。 `<Version>` 子元素指定要获取的版本。 根据 [NuGet 版本规则](/nuget/create-packages/dependency-versions#version-ranges)指定版本。

> [!NOTE]
> 如果不熟悉整体 `csproj` 语法，可参阅 [MSBuild 项目参考](/visualstudio/msbuild/msbuild-project-file-schema-reference)文档了解详细信息。  

使用类似以下示例中的条件添加仅在特定目标中可用的依赖项：

```xml
<PackageReference Include="PACKAGE_ID" Version="PACKAGE_VERSION" Condition="'$(TargetFramework)' == 'netcoreapp2.1'" />
```

上面的意思是，依赖项只有在对给定目标生成时才有效。 条件中的 `$(TargetFramework)` 是将在项目中设置的 MSBuild 属性。 对于大多数常见的 .NET Core 应用程序，无需这样做。 

## <a name="adding-a-dependency-to-your-project"></a>向项目添加依赖项
向项目添加依赖项非常简单。 下面是如何向项目添加 Json.NET 版本 `9.0.1` 的示例。 当然，它也适用于其他任意 NuGet 依赖项。 

打开项目文件时，将看到两个或多个 `<ItemGroup>` 节点。 你会注意到其中一个节点已有 `<PackageReference>` 元素。 可以向此节点添加新的依赖项，或创建一个新的依赖项；这完全取决于你，因为其结果将是一样的。 

在本示例中，将使用被 `dotnet new console` 删除的默认模板。 这是一个简单的控制台应用程序。 打开项目时，首先找到 `<ItemGroup>`，其中包含已存在的 `<PackageReference>`。 然后将下列内容添加进去：

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
```
之后，保存项目并运行 `dotnet restore` 命令以安装依赖项。 

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

完整项目如下所示：

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
  </ItemGroup>
</Project>
```

## <a name="removing-a-dependency-from-the-project"></a>从项目中删除依赖项
从项目文件中删除依赖项仅包含从项目文件中删除 `<PackageReference>`。
