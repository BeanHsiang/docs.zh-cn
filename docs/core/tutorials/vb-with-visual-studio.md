---
title: 在 Visual Studio 2017 中的 .NET Core Visual Basic Hello World 应用程序
description: 了解如何使用 Visual Studio 2017 生成简单的 Visual Basic .NET Core 控制台应用程序。
author: rpetrusha
ms.author: ronpet
ms.date: 08/07/2017
dev_langs:
- vb
ms.custom: vs-dotnet, seodec18
ms.openlocfilehash: 8b9d87922b543f97d4b36a37759d661298318e1e
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2019
ms.locfileid: "57846280"
---
# <a name="build-a-visual-basic-hello-world-application-with-the-net-core-sdk-in-visual-studio-2017"></a>在 Visual Studio 2017 中使用 .NET Core SDK 生成 Visual Basic Hello World 应用程序

本主题分步介绍了如何使用 Visual Studio 2017 生成、调试和发布简单的 Visual Basic .NET Core 控制台应用程序。 Visual Studio 2017 提供了功能全面的开发环境，可用于生成 .NET Core 应用程序。 只要应用程序没有平台专属依赖项，应用程序就可以在 .NET Core 的任何目标平台上和安装了 .NET Core 的任何系统上运行。

## <a name="prerequisites"></a>系统必备

安装了“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)。 可以使用 .NET Core 2.0 开发应用程序。

有关详细信息，请参阅 [Windows 上 .NET Core 的先决条件](../../core/windows-prerequisites.md)。

## <a name="a-simple-hello-world-application"></a>简单的“Hello World”应用程序

首先创建简单的“Hello World”控制台应用程序。 请执行这些步骤：

1. 启动 Visual Studio 2017。 从菜单栏中选择“文件” > “新建” > “项目”。 在“新项目”*对话框中，依次选择“Visual Basic”和“.NET Core”节点。 然后，选择“控制台应用程序(.NET Core)”项目模板。 在“名称”文本框中，键入“HelloWorld”。 选择“确定”按钮。

   ![选择了“控制台应用”的“新建项目”对话框](./media/vb-with-visual-studio/visual-studio-new-project.png)
   
1. Visual Studio 使用模板创建项目。 Visual Basic .NET Core 控制台应用程序模板自动定义类 `Program`，其中包含一个需要将 <xref:System.String> 数组用作参数的方法 `Main`。 `Main` 是应用程序入口点，同时也是在应用程序启动时由运行时自动调用的方法。 *args* 数组中包含在应用程序启动时提供的所有命令行自变量。

   ![Visual Studio 和新建的 HelloWorld 项目](./media/vb-with-visual-studio/visual-studio-main-window.png)

   用于创建简单的“Hello World”应用程序的模板。 它通过调用 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 方法在控制台窗口中 显示文本字符串“Hello World!”。 现在，选择工具栏上含绿色箭头的“HelloWorld”按钮，可以在调试模式下运行程序。 如果这样操作，控制台窗口只在较短的时间内可见，然后就会关闭。 这是因为在执行 `Main` 方法中的单个语句后，`Main` 方法和应用程序将立即终止。

1. 若要在应用程序关闭控制台窗口前将其暂停，请在调用 <xref:System.Console.WriteLine(System.String)?displayProperty=nameWithType> 方法后立即添加下列代码：

   ```vb
   Console.Write("Press any key to continue...")
   Console.ReadKey(true)
   ```
   此代码会提示用户按任意键，然后在用户按键前暂停程序。

1. 在菜单栏中，选择“生成” > “生成解决方案”。 这会将程序编译成一种中间语言 (IL)，然后由实时 (JIT) 编译器转换成二进制代码。

1. 选择工具栏上含绿色箭头的“HelloWorld”按钮，从而运行程序。

   ![控制台窗口，其中显示 Hello World Press any key to continue](./media/with-visual-studio/hello-world-console.png)

1. 按任意键关闭控制台窗口。

## <a name="enhancing-the-hello-world-application"></a>改进“Hello World”应用程序

将应用程序改进为提示用户输入名字，并将它与日期和时间一起显示。 若要修改和测试程序，请执行以下操作：

1. 在代码窗口中，在 `Sub Main(args As String())` 代码行后面的左括号和第一个右括号之间，输入以下 Visual Basic 代码：

   [!code-vb[GettingStarted#1](../../../samples/snippets/core/tutorials/vb-with-visual-studio/helloworld.vb#1)]

   此代码替换现有的 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType>、<xref:System.Console.Write%2A?displayProperty=nameWithType> 和 <xref:System.Console.ReadKey%2A?displayProperty=nameWithType> 语句。

   ![更新了 Main 方法的 Visual Studio Program 文件](./media/vb-with-visual-studio/visual-basic-code-window.png)

   此代码在控制台中显示“What is your name?”， 然后等待用户输入字符串并按 Enter 键。 它将此字符串存储到名为 `name` 的变量中。 它还会检索 <xref:System.DateTime.Now?displayProperty=nameWithType> 属性的值（其中包含当前的本地时间），并将此值赋给 `currentDate` 变量。 最后，使用[内插字符串](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md)在控制台窗口中显示这些值。

1. 依次选择 **“生成”** > **“生成解决方案”**，编译此程序。

1. 选择工具栏上的绿色箭头、按 F5 或选择“调试” > “启动调试”菜单项，在 Visual Studio 的调试模式下运行程序。 出现提示时，输入名称并按 Enter 键。

   ![控制台窗口，含已修改程序的输出](./media/with-visual-studio/hello-world-update.png)

1. 按任意键关闭控制台窗口。

现已创建并运行应用程序。 若要开发专业应用程序，仍需要执行一些其他步骤，才可发布应用程序：

- 要调试应用程序，请参阅[使用 Visual Studio 2017 调试 .NET Core Hello World 应用程序](debugging-with-visual-studio.md)。

- 若要发布可分布版本的应用程序，请参阅[使用 Visual Studio 2017 发布 .NET Core Hello World 应用程序](publishing-with-visual-studio.md)。

## <a name="related-topics"></a>相关主题

还可以使用 Visual Basic、.NET Core 和 Visual Studio 2017 生成 .NET Standard 类库，而不是控制台应用程序。 有关分步说明，请参阅[在 Visual Studio 2017 中使用 Visual Basic 和 .NET Core SDK 生成 .NET Standard 库](vb-library-with-visual-studio.md)。
