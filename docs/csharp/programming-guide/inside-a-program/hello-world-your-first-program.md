---
title: Hello World -- 首个程序 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- cs.program
- vs.csharp.startpage.firstapplication
helpviewer_keywords:
- examples [C#], Hello World
- Hello World example [C#]
ms.assetid: 6493182a-b0b6-4539-a719-518a168cb730
ms.openlocfilehash: 7ff65867f9f81118cad30852c439f8b3491bf1aa
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56969721"
---
# <a name="hello-world----your-first-program-c-programming-guide"></a>Hello World -- 首个程序（C# 编程指南）

以下过程创建传统“Hello World!”程序的 C# 版本。 该程序显示字符串 `Hello World!`

有关介绍性概念的更多示例，请参阅 [Visual C# 和 Visual Basic 入门](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)。

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-and-run-a-console-application"></a>创建并运行控制台应用程序

1. 启动 Visual Studio。

2. 在菜单栏上，依次选择“文件” 、“新建” 、“项目” 。

     **“新建项目”** 对话框随即打开。

3. 依次展开“已安装”、“模板”、“Visual C#”，然后选择“控制台应用程序”。

4. 在“名称”框中，指定项目名称，然后选择“确定”按钮。

     新项目将出现在“解决方案资源管理器”中。

5. 如果 Program.cs 未在“代码编辑器”中打开，则在“解决方案资源管理器”中打开“Program.cs”的快捷菜单，然后选择“查看代码”。

6. 将 Program.cs 的内容替换为以下代码。

     [!code-csharp[csProgGuide#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#21)]

7. 选择 F5 键运行该项目。 将显示包含行 `Hello World!` 的命令提示符窗口

接下来，将检查此程序的重要部分。

## <a name="comments"></a>注释

第一行包含一条注释。 字符 `//` 将该行的其余内容转换为一条注释。

 [!code-csharp[csProgGuide#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#32)]

还可以通过将文本块置于 `/*` 和 `*/` 字符之间，禁止对其的注释。 这在下面的示例中显示。

 [!code-csharp[csProgGuide#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#33)]

## <a name="main-method"></a>Main 方法

C# 控制台应用程序必须包含 `Main` 方法，控件在其中开始和结束。 在 `Main` 方法中，可以创建对象并执行其他方法。

`Main` 方法是驻留在类或结构中的[静态](../../../csharp/language-reference/keywords/static.md)方法。 在上一个“Hello World!” 示例中，该方法驻留在名为 `Hello` 的类中。 可以通过以下方式之一来声明 `Main` 方法：

- 它可返回 `void`。

     [!code-csharp[csProgGuideMain#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#12)]

- 还可以返回一个整数。

     [!code-csharp[csProgGuideMain#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#13)]

- 无论使用哪种返回类型，它都可以带有参数。

     [!code-csharp[csProgGuideMain#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#19)]

     或

     [!code-csharp[csProgGuideMain#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideMain/CS/Class3.cs#18)]

`Main` 方法中定义的参数 `args` 是一个 `string` 类型的数组，该数组包含用于调用该程序的命令行自变量。 与 C++ 不同的是该数组不包括可执行 (exe) 文件的名称。

若要详细了解如何使用命令行参数，请参阅 [Main() 和命令行参数](../../../csharp/programming-guide/main-and-command-args/index.md)和[操作说明：使用命令行创建和使用程序集](../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-and-use-assemblies-using-the-command-line.md)中的示例。

在调试模式下运行程序时，对 `Main` 方法末尾处 <xref:System.Console.ReadKey%2A> 的调用可以防止在有可能读取输出内容之前控制台窗口关闭，具体方法是按 F5 键。

## <a name="input-and-output"></a>输入和输出

C# 程序通常使用由 .NET Framework 的运行时库提供的输入/输出服务。 语句 `System.Console.WriteLine("Hello World!");` 使用 <xref:System.Console.WriteLine%2A> 方法。 这是运行时库中 <xref:System.Console> 类的输出方法之一。 该方法将在标准输出流中显示其字符串参数，后接新行。 其他 <xref:System.Console> 方法可用于不同的输入和输出操作。 如果程序开头包含 `using System;` 指令，则可以直接使用 <xref:System> 类和方法，而不必进行完全限定。 例如，可以调用 `Console.WriteLine`，而非 `System.Console.WriteLine`：

 [!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]

 [!code-csharp[csProgGuide#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#23)]

有关输入/输出方法的详细信息，请参阅 <xref:System.IO>。

## <a name="command-line-compilation-and-execution"></a>命令行编译和执行

通过使用命令行 而非 Visual Studio 集成开发环境 (IDE)，可以编译“Hello World!”程序。

### <a name="to-compile-and-run-from-a-command-prompt"></a>从命令提示符中编译并运行

1. 将上一过程的代码粘贴到任何文本编辑器中，然后将该文件保存为文本文件。 为 `Hello.cs` 文件命名。 C# 源代码文件使用 `.cs` 扩展。

2. 执行以下任一步骤以打开命令提示符窗口：

    - 在 Windows 10 的“开始”菜单上，搜索 `Developer Command Prompt`，然后点击或选择“VS 2017 开发人员命令提示”。

         将出现“开发人员命令提示”窗口。

    - 在 Windows 7 中，打开“启动”菜单，展开当前版本的 Visual Studio 的文件夹，打开“Visual Studio Tools”快捷菜单，然后选择“VS 2017 开发人员命令提示”。

         将出现“开发人员命令提示”窗口。

    - 从标准命令提示符窗口启用命令行生成。

         请参阅[操作说明：设置 Visual Studio 命令行的环境变量](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)。

3. 在命令提示窗口中，导航到包含 `Hello.cs` 文件的文件夹。

4. 输入以下命令以编译 `Hello.cs`。

     `csc Hello.cs`

     如果程序不存在编译错误，系统将创建名为 `Hello.exe` 的可执行文件。

5. 在命令提示窗口中，输入以下命令以运行该程序：

     `Hello`

 有关 C# 编译器及其选项的详细信息，请参阅 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)。

## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)
- [在 C# 程序内部](../../../csharp/programming-guide/inside-a-program/index.md)
- [字符串](../../../csharp/programming-guide/strings/index.md)
- [示例和教程](../../../samples-and-tutorials/index.md)
- [C# 参考](../../../csharp/language-reference/index.md)
- [Main() 和命令行参数](../../../csharp/programming-guide/main-and-command-args/index.md)
- [Visual C# 和 Visual Basic 入门](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)