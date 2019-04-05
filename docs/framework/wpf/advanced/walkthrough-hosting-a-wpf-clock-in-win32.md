---
title: 演练：承载 WPF 时钟在 Win32 中
ms.date: 03/30/2017
helpviewer_keywords:
- interoperability [WPF], tutorials
- Win32 code [WPF], WPF interoperation
- interoperability [WPF], Win32
ms.assetid: 555e55a7-0851-4ec8-b1c6-0acba7e9b648
ms.openlocfilehash: a13e21281a4bdb365c3a0541d88cd94b6476492e
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57494943"
---
# <a name="walkthrough-hosting-a-wpf-clock-in-win32"></a>演练：承载 WPF 时钟在 Win32 中

若要将放[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]应用程序，使用<xref:System.Windows.Interop.HwndSource>，其中提供了包含的 HWND 你[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容。 首先创建<xref:System.Windows.Interop.HwndSource>，为其赋予类似于 CreateWindow 的参数。 然后，通知<xref:System.Windows.Interop.HwndSource>有关[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]您要在其中包含内容。 最后，获取共 HWND <xref:System.Windows.Interop.HwndSource>。 本演练演示如何创建混合[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]重新实现操作系统的应用程序**日期和时间属性**对话框。

## <a name="prerequisites"></a>系统必备

请参阅[WPF 和 Win32 互操作](wpf-and-win32-interoperation.md)。

## <a name="how-to-use-this-tutorial"></a>如何使用本教程

本教程重点介绍生成互操作应用程序的重要步骤。 本教程采用一个示例中， [Win32 时钟互操作示例](https://go.microsoft.com/fwlink/?LinkID=160051)，但该示例是反映的最终产品。 本教程中介绍的步骤，因为如果您正在开始与某个现有[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]你自己的项目，可能是一个预先存在的项目，添加一个承载[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]到你的应用程序。 您可以比较将最终产品与[Win32 时钟互操作示例](https://go.microsoft.com/fwlink/?LinkID=160051)。

## <a name="a-walkthrough-of-windows-presentation-framework-inside-win32-hwndsource"></a>Win32 中的 Windows Presentation Framework 的演练 (HwndSource)

下图显示了本教程的预期最终产品：

![“日期和时间属性”对话框](./media/interoparch06.PNG "InteropArch06")

可以通过创建 c + + 重新创建此对话框[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]项目中[!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]，并使用对话框编辑器创建以下：

![“日期和时间属性”对话框](./media/interoparch07.PNG "InteropArch07")

(不需要使用[!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]若要使用<xref:System.Windows.Interop.HwndSource>，并且不需要使用 c + + 编写[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]程序，但这是相当典型的方法来执行此操作，并且非常适合用于分布教程说明)。

您需要完成五个特定的子步骤才能将放置[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]时钟在对话框：

1. 启用您[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]项目，以调用托管的代码 (**/clr**) 通过更改项目设置中的[!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]。

2. 创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page>在单独的 DLL 中。

3. 将它放[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page>内<xref:System.Windows.Interop.HwndSource>。

4. 为此，获取 HWND<xref:System.Windows.Controls.Page>使用<xref:System.Windows.Interop.HwndSource.Handle%2A>属性。

5. 使用[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]若要决定在何处放置 HWND 内较大[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]应用程序

## <a name="clr"></a>/clr

第一步是将此非托管[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]项目转换成了一可调用托管代码。 使用 /clr 编译器选项，它将链接到你想要使用，并调整与一起使用的 Main 方法所需的 Dll [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。

若要启用 c + + 项目内的托管代码使用：右键单击 win32clock 项目，然后选择**属性**。 上**常规**属性页 （默认值），更改到的公共语言运行时支持`/clr`。

接下来，添加对所需的 Dll 的引用[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:PresentationCore.dll、 PresentationFramework.dll、 System.dll、 WindowsBase.dll、 UIAutomationProvider.dll 和 UIAutomationTypes.dll。 （以下说明假定操作系统安装在 C: 驱动器上。）

1. 右键单击 win32clock 项目，然后选择**引用...**，并在该对话框：

2. 右键单击 win32clock 项目，然后选择**引用...**.

3. 单击**添加新引用**、 单击浏览选项卡中，输入 C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationCore.dll，并单击确定。

4. 对 PresentationFramework.dll 重复：C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationFramework.dll.

5. 对 WindowsBase.dll 重复：C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\WindowsBase.dll。

6. 对 UIAutomationTypes.dll 重复：C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\UIAutomationTypes.dll.

7. 对 UIAutomationProvider.dll 重复：C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\UIAutomationProvider.dll.

8. 单击**添加新引用**，选择 System.dll，然后单击**确定**。

9. 单击**确定**退出用于添加引用的 win32clock 属性页。

 最后，添加`STAThreadAttribute`到`_tWinMain`方法用于[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:

```cpp
[System::STAThreadAttribute]
int APIENTRY _tWinMain(HINSTANCE hInstance,
                     HINSTANCE hPrevInstance,
                     LPTSTR    lpCmdLine,
                     int       nCmdShow)
```

此属性告知[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]，当它初始化[!INCLUDE[TLA#tla_com](../../../../includes/tlasharptla-com-md.md)]，它应使用单线程的单元模式 (STA) 所必需[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] (和[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)])。

## <a name="create-a-windows-presentation-framework-page"></a>创建 Windows Presentation Framework 页

接下来，创建一个 DLL，它定义[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page>。 它通常是最简单的方法创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page>作为独立的应用程序，并编写和调试[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]部分通过这种方式。 完成后，该项目可以转换为 DLL，请右键单击项目，单击**属性**，转至该应用程序，并将输出类型更改为 Windows 类库。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] Dll 项目然后与组合[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]项目 （一个解决方案包含两个项目），右键单击解决方案，选择**添加 \ 现有项目**。

若要使用该[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]dll[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]项目中，您需要添加的引用：

1. 右键单击 win32clock 项目，然后选择**引用...**.

2. 单击**添加新引用**。

3. 单击“项目”选项卡。选择 WPFClock，单击“确定”。

4. 单击**确定**退出用于添加引用的 win32clock 属性页。

## <a name="hwndsource"></a>HwndSource

接下来，使用<xref:System.Windows.Interop.HwndSource>以使[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Page>看起来像 HWND。 将此代码块添加到 C++ 文件中：

```cpp
namespace ManagedCode
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Media;

    HWND GetHwnd(HWND parent, int x, int y, int width, int height) {
        HwndSource^ source = gcnew HwndSource(
            0, // class style
            WS_VISIBLE | WS_CHILD, // style
            0, // exstyle
            x, y, width, height,
            "hi", // NAME
            IntPtr(parent)        // parent window
            );

        UIElement^ page = gcnew WPFClock::Clock();
        source->RootVisual = page;
        return (HWND) source->Handle.ToPointer();
    }
}
}
```

 这是一长段代码，可以作一些解释。 第一部分是各种子句，无需完全限定所有调用：

```cpp
namespace ManagedCode
{
    using namespace System;
    using namespace System::Windows;
    using namespace System::Windows::Interop;
    using namespace System::Windows::Media;
```

 然后，定义一个函数来创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容，put<xref:System.Windows.Interop.HwndSource>围绕它，并返回 HWND:

```cpp
HWND GetHwnd(HWND parent, int x, int y, int width, int height) {
```

首先创建<xref:System.Windows.Interop.HwndSource>，其参数位于类似于 CreateWindow:

```cpp
HwndSource^ source = gcnew HwndSource(
    0, // class style
    WS_VISIBLE | WS_CHILD, // style
    0, // exstyle
    x, y, width, height,
    "hi", // NAME
    IntPtr(parent) // parent window
);
```

然后创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容类通过调用其构造函数：

```cpp
UIElement^ page = gcnew WPFClock::Clock();
```

然后连接到页<xref:System.Windows.Interop.HwndSource>:

```cpp
source->RootVisual = page;
```

 最后一行中返回的 HWND 和<xref:System.Windows.Interop.HwndSource>:

```cpp
return (HWND) source->Handle.ToPointer();
```

## <a name="positioning-the-hwnd"></a>放置 Hwnd

现在，已有包含 HWND[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]时钟，你需要将该 HWND[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]对话框。 如果你知道在何处放置 HWND，将只需传递该大小和位置到`GetHwnd`前面定义的函数。 但是，由于已使用资源文件来定义对话框，因此你不完全确定任何 HWND 的放置位置。 可以使用[!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]对话框编辑器将放[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]静态控制想时钟 （"此处插入时钟"），并使用它来定位[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]时钟。

只要在处理 WM_INITDIALOG，就使用`GetDlgItem`检索占位符 STATIC 的 HWND:

```cpp
HWND placeholder = GetDlgItem(hDlg, IDC_CLOCK);
```

然后，计算的大小和位置的该占位符 STATIC，以便可以将[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]时钟在该位置：

RECT 矩形；

```cpp
GetWindowRect(placeholder, &rectangle);
int width = rectangle.right - rectangle.left;
int height = rectangle.bottom - rectangle.top;
POINT point;
point.x = rectangle.left;
point.y = rectangle.top;
result = MapWindowPoints(NULL, hDlg, &point, 1);
```

然后，你隐藏占位符 STATIC：

```cpp
ShowWindow(placeholder, SW_HIDE);
```

并创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]时钟在该位置的 HWND:

```cpp
HWND clock = ManagedCode::GetHwnd(hDlg, point.x, point.y, width, height);
```

为了使教程变得有趣，并生成真正[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]时钟，你将需要创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]此时时钟控件。 你可以在标记中执行大部分操作，代码隐藏中只有几个事件处理程序。 由于本教程是关于互操作而不是关于控件设计，完成代码[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]时钟提供作为代码块，而无需另外说明如何构建或每个部分的含义。 随意尝试此代码来更改控件的外观或功能。

此处为标记：

[!code-xaml[Win32Clock#AllClockXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml#allclockxaml)]

以下是附带的代码隐藏：

[!code-csharp[Win32Clock#AllClockCS](~/samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml.cs#allclockcs)]

最终结果如下所示：

![“日期和时间属性”对话框](./media/interoparch08.PNG "InteropArch08")

若要进行比较将最终结果与生成此屏幕截图中的代码，请参阅[Win32 时钟互操作示例](https://go.microsoft.com/fwlink/?LinkID=160051)。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Interop.HwndSource>
- [WPF 和 Win32 互操作](wpf-and-win32-interoperation.md)
- [Win32 时钟互操作示例](https://go.microsoft.com/fwlink/?LinkID=160051)
