---
title: WPF 和 Win32 互操作
ms.date: 03/30/2017
helpviewer_keywords:
- hosting WPF content in Win32 window [WPF]
- HWND interop [WPF]
- Win32 code [WPF], WPF interoperation
- interoperability [WPF], Win32
ms.assetid: 0ffbde0d-701d-45a3-a6fa-dd71f4d9772e
ms.openlocfilehash: e5a044166023069cdb6e1091339044cd7f964825
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57377109"
---
# <a name="wpf-and-win32-interoperation"></a>WPF 和 Win32 互操作
本主题概述如何互操作 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了用于创建应用程序的丰富环境。 但是，如果对 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 代码投入很大，重复使用部分此代码可能更有效。  
  

  
<a name="basics"></a>   
## <a name="wpf-and-win32-interoperation-basics"></a>WPF 和 Win32 互操作基础知识  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码间的互操作存在两种基本方法。  
  
-   在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 内容。 通过此方法，可在标准 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口和应用程序的框架内使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的高级图形功能。  
  
-   在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容中承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口。 通过此方法，可在其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的上下文中使用现有自定义 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 控件，并可跨边界传递数据。  
  
 本主题中对上述每种方法进行了概念性介绍。 托管的更加面向代码演示[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]中[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]，请参阅[演练：Win32 中承载 WPF 内容](walkthrough-hosting-wpf-content-in-win32.md)。 托管的更加面向代码演示[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]中[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，请参阅[演练：中承载 Win32 控件在 WPF 中的](walkthrough-hosting-a-win32-control-in-wpf.md)。  
  
<a name="projects"></a>   
## <a name="wpf-interoperation-projects"></a>WPF 互操作项目  
 虽然 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 为托管代码，但大多数现有 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 程序是以非托管 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 编写而成。  无法从真正的非托管程序调用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]。 但是，通过使用 [!INCLUDE[TLA#tla_visualcpp](../../../../includes/tlasharptla-visualcpp-md.md)] 编译器的 `/clr` 选项，可创建托管与非托管混合的程序，在此程序中可无缝混合托管和非托管 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 调用。  
  
 存在的一个项目级问题是无法将 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件编译到 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 项目中。  可通过一些项目分离技术对此进行弥补。  
  
-   创建包含所有的 C# DLL 你[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]页为已编译的程序集，然后让你[!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)]可执行文件包含[!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)]作为参考。  
  
-   创建一个 C# 可执行文件[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容，并将其引用[!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] ，其中包含[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]内容。  
  
-   使用<xref:System.Windows.Markup.XamlReader.Load%2A>加载任何[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]在运行时，而不是编译您[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  
  
-   不要使用[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，并写入所有你[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]在代码中，构建元素树从<xref:System.Windows.Application>。  
  
 请使用最适合你的方法。  
  
> [!NOTE]
>  如果之前未使用过 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)]，在互操作代码示例中你可能会看到 `gcnew` 和 `nullptr` 等一些“新”关键字。 这些关键字取代旧版双下划线语法 (`__gc`)，为 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 中的托管代码提供了更加自然的语法。  若要详细了解 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 托管功能，请参阅[适用于运行时平台的组件扩展](/cpp/windows/component-extensions-for-runtime-platforms)和[了解 C++/CLI](https://go.microsoft.com/fwlink/?LinkId=98739)。  
  
<a name="hwnds"></a>   
## <a name="how-wpf-uses-hwnds"></a>WPF 如何使用 Hwnd  
 若要充分利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]“HWND 互操作”，需要了解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 如何使用 HWND。 对于任何 HWND，无法将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 绘制与 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 绘制或 [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] / [!INCLUDE[TLA2#tla_gdiplus](../../../../includes/tla2sharptla-gdiplus-md.md)] 绘制混合。 这具有许多影响。 首先，若要混合这些绘制模型，必须创建互操作解决方案，并对选择使用的每个绘制模型使用互操作的指定段。 此外，绘制行为会为互操作解决方案可实现的操作创建一个“空域”限制。 有关“空域”概念的详细信息，请参见[技术区概述](technology-regions-overview.md)主题。  
  
 屏幕上的所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素最终受 HWND 支持。 当您创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Window>，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]创建一个顶层 HWND，并使用<xref:System.Windows.Interop.HwndSource>放置<xref:System.Windows.Window>并将其[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]HWND 内的内容。  应用程序中的其余 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容共享单个 HWND。 菜单、组合框下拉列表和其他弹出窗口例外。 这些元素会创建自己的顶层窗口，因此 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 菜单可能超出所在窗口 HWND 的边缘。 当你使用<xref:System.Windows.Interop.HwndHost>将 HWND 内的放置[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]通知[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]如何定位到的新子 HWND 相对[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Window> HWND。  
  
 与之相关的 HWND 概念是每个 HWND 内及其之间的透明度。 [技术区概述](technology-regions-overview.md)主题中对此也有相关介绍。  
  
<a name="hosting_a_wpf_page"></a>   
## <a name="hosting-wpf-content-in-a-microsoft-win32-window"></a>在 Microsoft Win32 窗口中承载 WPF 内容  
 托管的关键[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]上[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]窗口是<xref:System.Windows.Interop.HwndSource>类。 此类在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中包装 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容，以便 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容可作为子窗口并入 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]。 以下方法在单个应用程序中合并 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  
  
1.  将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容（内容根元素）作为托管类实现。 通常情况下，该类继承的一个类可以包含多个子元素和/或使用作为根元素，如<xref:System.Windows.Controls.DockPanel>或<xref:System.Windows.Controls.Page>。 后续步骤中，此类被称为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类，此类的实例被称为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象。  
  
2.  使用 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 实现 [!INCLUDE[TLA2#tla_cppcli](../../../../includes/tla2sharptla-cppcli-md.md)] 应用程序。 若要以现有非托管 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 应用程序开始，可更改项目设置将 `/clr` 编译器标志包括在内，以此来允许应用程序调用托管代码（本主题中未介绍支持 `/clr` 编译可能所需内容的完整范围）。  
  
3.  将线程处理模型设置为单线程单元 (STA)。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用此线程模型。  
  
4.  处理窗口过程中的 WM_CREATE 通知。  
  
5.  在处理程序（或处理程序调用的函数）中，执行以下操作：  
  
    1.  创建一个新<xref:System.Windows.Interop.HwndSource>对象，将父窗口 HWND 作为其`parent`参数。  
  
    2.  创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类的一个实例。  
  
    3.  将分配到的引用[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容对象<xref:System.Windows.Interop.HwndSource>对象<xref:System.Windows.Interop.HwndSource.RootVisual%2A>属性。  
  
    4.  <xref:System.Windows.Interop.HwndSource>对象<xref:System.Windows.Interop.HwndSource.Handle%2A>属性包含窗口句柄 (HWND)。 要获取可在应用程序的非托管部分中使用的 HWND，需将 `Handle.ToPointer()` 强制装换为 HWND。  
  
6.  实现一个托管类，该类包含一个用于保存对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象的引用的静态字段。 此类可以获取对引用[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容对象从你[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]的代码，但重要的是，它会阻止的详细信息在<xref:System.Windows.Interop.HwndSource>无意中进行垃圾回收。  
  
7.  通过将处理程序附加到一个或多个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象事件，接收 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象的通知。  
  
8.  通过使用存储在静态字段中的引用设置属性、调用方法等，与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象进行通信。  
  
> [!NOTE]
>  如果生成一个单独的程序集然后对其进行引用，对于步骤 1，可使用内容类的默认分部类在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中完成部分或全部 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类定义。 虽然通常包括<xref:System.Windows.Application>对象作为编译的一部分[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]程序集，您不的最终使用该<xref:System.Windows.Application>作为互操作的一部分，您只需使用一个或多个用于根类[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件引用为应用程序和引用其分部类。 该过程的其余部分基本与上述相似。  
>   
>  每个步骤执行本主题中的代码所示[演练：Win32 中承载 WPF 内容](walkthrough-hosting-wpf-content-in-win32.md)。  
  
<a name="hosting_an_hwnd"></a>   
## <a name="hosting-a-microsoft-win32-window-in-wpf"></a>在 WPF 中承载 Microsoft Win32 窗口  
 托管的关键[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]内其他窗口[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容是<xref:System.Windows.Interop.HwndHost>类。 该类在可添加到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素树的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素中包装窗口。 <xref:System.Windows.Interop.HwndHost> 此外支持[!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，让你执行进程所承载的窗口消息之类的任务。 基本过程：  
  
1.  为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序创建一个元素树（可通过代码或标记）。 在元素树中查找相应的许可点其中<xref:System.Windows.Interop.HwndHost>实现可添加为子元素。 剩余步骤中，此元素称为保留元素。  
  
2.  派生自<xref:System.Windows.Interop.HwndHost>若要创建一个对象，保存你[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]内容。  
  
3.  在此主机类，重写<xref:System.Windows.Interop.HwndHost>方法<xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>。 返回承载窗口的 HWND。 可能需要将实际控件包装为返回窗口的子窗口；在承载窗口中包装控件为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容从控件接收通知提供了一种简单的方式。 此方法有助于更正一些有关主机控件边界处消息处理的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 问题。  
  
4.  重写<xref:System.Windows.Interop.HwndHost>方法<xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A>和<xref:System.Windows.Interop.HwndHost.WndProc%2A>。 这样做的目的是处理清除和删除对承载内容的引用，尤其是在已创建对非托管对象的引用的情况下。  
  
5.  在代码隐藏文件中，创建控件承载类的一个实例，并使其成为保留元素的子元素。 通常会使用事件处理程序如<xref:System.Windows.FrameworkElement.Loaded>，或使用分部类构造函数。 但也可通过运行时行为添加互操作内容。  
  
6.  处理选择的窗口消息，例如控件通知。 方法有两种。 两种方法提供对消息流的相同访问权限，因此你的选择很大程度上取决于编程简便性。  
  
    -   实现消息处理的所有消息 （而不仅仅是关闭消息） 中的重写<xref:System.Windows.Interop.HwndHost>方法<xref:System.Windows.Interop.HwndHost.WndProc%2A>。  
  
    -   使承载[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]元素处理的消息，处理<xref:System.Windows.Interop.HwndHost.MessageHook>事件。 对发送到承载窗口的主窗口过程的每个消息都会引发该事件。  
  
    -   无法处理超出进程使用的 windows 中的消息<xref:System.Windows.Interop.HwndHost.WndProc%2A>。  
  
7.  通过使用平台调用来调用非托管 `SendMessage` 函数，与承载窗口通信。  
  
 按照这些步骤，创建一个处理鼠标输入的应用程序。 可以通过实现为承载窗口添加 tab 键支持<xref:System.Windows.Interop.IKeyboardInputSink>接口。  
  
 每个步骤执行本主题中的代码所示[演练：中承载 Win32 控件在 WPF 中的](walkthrough-hosting-a-win32-control-in-wpf.md)。  
  
### <a name="hwnds-inside-wpf"></a>WPF 内部的 Hwnd  
 您可以将<xref:System.Windows.Interop.HwndHost>视为一个特殊控件。 (从技术上讲，<xref:System.Windows.Interop.HwndHost>是<xref:System.Windows.FrameworkElement>派生的类，不<xref:System.Windows.Controls.Control>派生的类，但它可被视为用于互操作的目的的控件。)<xref:System.Windows.Interop.HwndHost>抽象化基础[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]性质所承载的内容以便的其余部分[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]考虑所承载的内容是另一个类似于控件的对象，其中应呈现和处理输入。 <xref:System.Windows.Interop.HwndHost> 行为通常类似于任何其他[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.FrameworkElement>，尽管有一些重要差异围绕输出 （绘图和图形） 和基于基础 Hwnd 的限制的输入 （鼠标和键盘） 可以支持。  
  
#### <a name="notable-differences-in-output-behavior"></a>输出行为的显著差异  
  
-   <xref:System.Windows.FrameworkElement>它是<xref:System.Windows.Interop.HwndHost>基类、 具有很多属性，表示对 UI 的更改。 这些包括属性如下所述<xref:System.Windows.FrameworkElement.FlowDirection%2A?displayProperty=nameWithType>，这将更改该元素作为父级内的元素的布局。 但是，这些属性大多数未映射到可能的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 等效项（即使这类等效项可能存在）。 过多这些属性及其含义具有过高的绘制技术针对性，这使得映射并不可行。 因此，如设置属性<xref:System.Windows.FrameworkElement.FlowDirection%2A>上<xref:System.Windows.Interop.HwndHost>不起作用。  
  
-   <xref:System.Windows.Interop.HwndHost> 不能旋转、 缩放、 倾斜，或其他受 Transform 影响。  
  
-   <xref:System.Windows.Interop.HwndHost> 不支持<xref:System.Windows.UIElement.Opacity%2A>属性 （alpha 值混合处理）。 如果中的内容<xref:System.Windows.Interop.HwndHost>执行<xref:System.Drawing>操作包含 alpha 信息，本身不是冲突，但<xref:System.Windows.Interop.HwndHost>作为一个整体仅支持不透明度 = 1.0 （100%)。  
  
-   <xref:System.Windows.Interop.HwndHost> 将显示在其他之上[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]相同的顶级窗口中的元素。 但是，<xref:System.Windows.Controls.ToolTip>或<xref:System.Windows.Controls.ContextMenu>生成的菜单是一个单独的顶级窗口，并因此就能正常工作与<xref:System.Windows.Interop.HwndHost>。  
  
-   <xref:System.Windows.Interop.HwndHost> 不遵从其父级的剪辑区域<xref:System.Windows.UIElement>。 这可能是一个问题，如果你尝试将放<xref:System.Windows.Interop.HwndHost>滚动区域内的类或<xref:System.Windows.Controls.Canvas>。  
  
#### <a name="notable-differences-in-input-behavior"></a>输入行为的显著差异  
  
-   通常，虽然输入的设备作用域内<xref:System.Windows.Interop.HwndHost>托管[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]区域中，输入的事件直接转到[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]。  
  
-   尽管鼠标位于<xref:System.Windows.Interop.HwndHost>，你的应用程序不会收到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]鼠标事件和的值[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]属性<xref:System.Windows.UIElement.IsMouseOver%2A>将`false`。  
  
-   虽然<xref:System.Windows.Interop.HwndHost>具有键盘焦点，你的应用程序将不会收到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]键盘事件和的值[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]属性<xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A>将`false`。  
  
-   当焦点位于<xref:System.Windows.Interop.HwndHost>并更改到另一个控件内<xref:System.Windows.Interop.HwndHost>，你的应用程序将不会收到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]事件<xref:System.Windows.UIElement.GotFocus>或<xref:System.Windows.UIElement.LostFocus>。  
  
-   相关触笔属性和事件相似，且并不报告信息，而在触笔位于<xref:System.Windows.Interop.HwndHost>。  
  
<a name="tabbing_mnemonics_accelerators"></a>   
## <a name="tabbing-mnemonics-and-accelerators"></a>Tab 键、助记键和加速键  
 <xref:System.Windows.Interop.IKeyboardInputSink>并<xref:System.Windows.Interop.IKeyboardInputSite>接口允许你创建的无缝键盘体验，为混合[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]和[!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]应用程序：  
  
-   [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 组件之间的 Tab 键  
  
-   焦点位于 Win32 组件内和 WPF 组件内时皆起作用的助记键和加速键。  
  
 <xref:System.Windows.Interop.HwndHost>并<xref:System.Windows.Interop.HwndSource>这两个类提供的实现<xref:System.Windows.Interop.IKeyboardInputSink>，但它们不会处理更高级的方案所需的所有输入的消息。 替换为适当方法，获取所需的键盘行为。  
  
 接口仅对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 区域间的转换过程中发生的事件提供支持。 在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 区域内，Tab 键行为完全受 Tab 键的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 实现逻辑（若有）控制。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Interop.HwndHost>
- <xref:System.Windows.Interop.HwndSource>
- <xref:System.Windows.Interop>
- [演练：中承载 Win32 控件在 WPF 中](walkthrough-hosting-a-win32-control-in-wpf.md)
- [演练：Win32 中承载 WPF 内容](walkthrough-hosting-wpf-content-in-win32.md)
