---
title: 使用 Visual Studio 2017 生成 C# .NET Standard 库
description: 了解如何使用 Visual Studio 2017 创建 C# .NET Standard 类库。
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
ms.custom: vs-dotnet, seodec18
ms.openlocfilehash: 6228cd93b275a059da63a8b8e3408032d78c5e39
ms.sourcegitcommit: 542aa405b295955eb055765f33723cb8b588d0d0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2019
ms.locfileid: "54362010"
---
# <a name="build-a-net-standard-library-with-c-and-the-net-core-sdk-in-visual-studio-2017"></a>在 Visual Studio 2017 中使用 C# 和 .NET Core SDK 生成 .NET Standard 库

类库定义的是可以由应用程序调用的类型和方法。 借助定目标到 .NET Standard 2.0 的类库，任何支持相应版本 .NET Standard 的 .NET 实现都可以调用库。 完成类库时，可以决定是要将其作为第三方组件进行分布，还是要将其作为与一个或多个应用程序捆绑在一起的组件进行添加。

> [!NOTE]
> 有关 .NET Standard 版本及其支持的平台列表，请参阅 [.NET Standard](../../standard/net-standard.md)。

在本主题中，将创建包含一个字符串处理方法的简单实用工具库。 我们将把它作为[扩展方法](../../csharp/programming-guide/classes-and-structs/extension-methods.md)进行实现，这样就可以把它作为 <xref:System.String> 类成员进行调用。

## <a name="creating-a-class-library-solution"></a>创建类库解决方案

首先为类库项目及其相关项目创建解决方案。 Visual Studio 解决方案只用作一个或多个项目的容器。 若要创建解决方案，请执行以下操作：

1. 在 Visual Studio 菜单栏上，选择“文件” > “新建” > “项目”。

1. 在“新建项目”对话框中，展开“其他项目类型”节点，然后选择“Visual Studio 解决方案”。 将解决方案命名为“ClassLibraryProjects”，然后选择“确定”按钮。

   ![“新建项目”对话框，其中突出显示新的空白解决方案](./media/library-with-visual-studio/new-project-dialog.png)

## <a name="creating-the-class-library-project"></a>创建类库项目

创建类库项目：

1. 在“解决方案资源管理器”中，右键单击“ClassLibraryProjects”解决方案文件，然后从上下文菜单中选择“添加” > “新项目”。

1. 在“添加新项目”对话框中，展开“Visual C#”节点，并依次选择“.NET Standard”节点和“类库(.NET Standard)”项目模板。 在“名称”文本框中，输入项目名称“StringLibrary”。 选择“确定”，创建类库项目。

   ![“添加新的库项目”对话框](./media/library-with-visual-studio/add-new-library-project.png)

   然后，代码窗口在 Visual Studio 开发环境中打开。

   ![显示默认类库模板代码的 Visual Studio 应用程序窗口](./media/library-with-visual-studio/string-library-project.png)

1. 请检查以确保库定目标到 .NET Standard 的正确版本。 右键单击“解决方案资源管理器”窗口中的库项目，再选择“属性”。 “目标框架”文本框显示定目标到 .NET Standard 2.0。

   ![类库的项目属性](./media/library-with-visual-studio/library-project-properties.png)

1. 将代码窗口中的代码替换为以下代码，并保存文件：

   [!CODE-csharp[ClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/classlib.cs)]

   类库 `UtilityLibraries.StringLibrary` 包含 `StartsWithUpper` 方法，此方法会返回 <xref:System.Boolean> 值，以指明当前字符串实例是否以大写字符开头。 Unicode 标准会区分大小写字符。 如果为大写字符，<xref:System.Char.IsUpper(System.Char)?displayProperty=nameWithType> 方法返回 `true`。

1. 在菜单栏中，选择“生成” > “生成解决方案”。 此项目的编译应该没有错误。

   ![显示生成成功的输出窗格](./media/library-with-visual-studio/output-pane-successful-build.png)

## <a name="next-step"></a>下一步

已成功生成库。 由于尚未调用库的任何方法，因此还不知道它能否按预期运行。 开发库的下一步是使用[单元测试项目](testing-library-with-visual-studio.md)测试库。