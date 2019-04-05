---
title: 在 Visual Studio 中的 WPF 应用程序中创建 InkCanvas
ms.date: 08/15/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- procedural code in lieu of XAML [WPF]
- XAML [WPF], procedural code in lieu of
- InkCanvas (WPF)
ms.assetid: 760332dd-594a-475d-865b-01659db8cab7
ms.openlocfilehash: 2fb3f975fedbae1cf898d5ec2f7c0809e0215ecd
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365563"
---
# <a name="get-started-with-ink-in-wpf"></a>在 WPF 中的墨迹入门

Windows Presentation Foundation (WPF) 具有墨迹功能，可以轻松地将数字墨迹合并到您的应用程序功能。

## <a name="prerequisites"></a>系统必备

若要使用以下示例中，首先[安装 Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。 它还有助于了解如何编写基本的 WPF 应用程序。 WPF 入门的帮助，请参阅[演练：我第一个 WPF 桌面应用程序](../getting-started/walkthrough-my-first-wpf-desktop-application.md)。

## <a name="quick-start"></a>快速入门

本部分可帮助您编写的简单的 WPF 应用程序收集墨迹。

### <a name="got-ink"></a>如何获取墨迹

若要创建一个 WPF 应用程序的支持手写内容：

1. 打开 Visual Studio。

2. 创建一个新**WPF 应用**。

   在中**新的项目**对话框中，展开**已安装** > **Visual C#** 或**Visual Basic**  >  **Windows 桌面**类别。 然后，选择**WPF 应用 (.NET Framework)** 应用模板。 输入一个名称，并选择**确定**。

   Visual Studio 创建项目，并*MainWindow.xaml*设计器中打开。

3. 类型`<InkCanvas/>`之间`<Grid>`标记。

   ![使用 InkCanvas 标记的 XAML 设计器](./media/getting-started-with-ink/inkcanvas-xaml.png)

4. 按**F5**若要在调试器中启动应用程序。

5. 使用触笔或鼠标，编写**你好世界**在窗口中。

您已编写具有仅 12 击键的"你好 world"应用程序的手写内容等效项 ！

### <a name="spice-up-your-app"></a>您的应用程序的情趣

让我们来充分利用 WPF 的一些功能。 替换的所有内容的开始和结束之间\<窗口 > 使用以下标记的标记：

```xaml
<Page>
  <InkCanvas Name="myInkCanvas" MouseRightButtonUp="RightMouseUpHandler">
    <InkCanvas.Background>
      <LinearGradientBrush>
        <GradientStop Color="Yellow" Offset="0.0" />
          <GradientStop Color="Blue" Offset="0.5" />
            <GradientStop Color="HotPink" Offset="1.0" />
              </LinearGradientBrush>
    </InkCanvas.Background>
  </InkCanvas>
</Page>
```

此 XAML 创建渐变画笔背景墨迹书写表面上。

![墨迹书写在 WPF 应用中的图面上的渐变颜色](./media/getting-started-with-ink/gradient-colors.png)

### <a name="add-some-code-behind-the-xaml"></a>添加一些代码隐藏 XAML

尽管 XAML 可以非常轻松地设计用户界面，任何实际的应用程序将需要添加代码以处理事件。 下面是一个简单示例，放大以响应来自鼠标右键单击的墨迹。

1. 设置`MouseRightButtonUp`在 XAML 中的处理程序：

   [!code-xaml[DigitalInkTopics#3](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#3)]

1. 在中**解决方案资源管理器**，展开 MainWindow.xaml 并打开代码隐藏文件 （MainWindow.xaml.cs 或 MainWindow.xaml.vb）。 添加以下事件处理程序代码：

   [!code-csharp[DigitalInkTopics#4](~/samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml.cs#4)]
   [!code-vb[DigitalInkTopics#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window2.xaml.vb#4)]

1. 运行该应用程序。 添加一些墨迹，然后用鼠标右键单击或执行与触笔按下保持等效。

   用鼠标右键单击每个时间会放大显示。

### <a name="use-procedural-code-instead-of-xaml"></a>使用程序代码而不是 XAML

可以从程序代码来访问所有 WPF 功能。 请按照下列步骤为根本不使用任何 XAML 的 WPF 创建"Hello 墨迹 World"应用程序。

1. 在 Visual Studio 中创建新的控制台应用程序项目。

   在中**新的项目**对话框中，展开**已安装** > **Visual C#** 或**Visual Basic**  >  **Windows 桌面**类别。 然后，选择**控制台应用 (.NET Framework)** 应用模板。 输入一个名称，并选择**确定**。

1. 将以下代码粘贴到 Program.cs 或 Program.vb 文件：

   [!code-csharp[InkCanvasConsoleApp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasConsoleApp/CSharp/Program.cs#1)]
   [!code-vb[InkCanvasConsoleApp#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/InkCanvasConsoleApp/VisualBasic/Module1.vb#1)]

1. 通过右键单击添加对 PresentationCore、 PresentationFramework、 和 WindowsBase 程序集的引用**引用**中**解决方案资源管理器**，然后选择**添加引用**.

   ![引用管理器显示 PresentationCore 和 PresentationFramework](./media/getting-started-with-ink/references.png)

1. 生成应用程序通过按**F5**。

## <a name="see-also"></a>请参阅

- [数字墨迹](digital-ink.md)
- [收集墨迹](collecting-ink.md)
- [手写识别](handwriting-recognition.md)
- [存储墨迹](storing-ink.md)
