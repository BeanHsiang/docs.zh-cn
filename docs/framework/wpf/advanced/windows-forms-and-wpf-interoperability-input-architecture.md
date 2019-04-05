---
title: Windows 窗体和 WPF 互操作性输入体系结构
ms.date: 03/30/2017
helpviewer_keywords:
- input architecture [WPF interoperability]
- messages [WPF]
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- modeless forms [WPF]
- ElementHost keyboard and messages [WPF]
- keyboard interoperation [WPF]
- WindowsFormsHost keyboard and messages [WPF]
- modeless dialog boxes [WPF]
ms.assetid: 0eb6f137-f088-4c5e-9e37-f96afd28f235
ms.openlocfilehash: 50097ef86fb6bc5341d7ea16ccee441b89823401
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57352414"
---
# <a name="windows-forms-and-wpf-interoperability-input-architecture"></a>Windows 窗体和 WPF 互操作性输入体系结构
之间的互操作[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]和[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]要求这两种技术都有相应的键盘输入的处理。 本主题介绍这些技术如何实现键盘和消息处理，以启用混合应用程序中的平滑互操作。  
  
 本主题包含以下小节：  
  
-   无模式窗体和对话框  
  
-   WindowsFormsHost 键盘和消息处理  
  
-   ElementHost 键盘和消息处理  
  
## <a name="modeless-forms-and-dialog-boxes"></a>无模式窗体和对话框  
 调用<xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A>方法<xref:System.Windows.Forms.Integration.WindowsFormsHost>以打开一个从无模式对话框窗体或对话框中的元素[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-基于应用程序。  
  
 调用<xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>方法<xref:System.Windows.Forms.Integration.ElementHost>控制打开无模式[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]页中[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]-基于应用程序。  
  
## <a name="windowsformshost-keyboard-and-message-processing"></a>WindowsFormsHost 键盘和消息处理  
 由托管时， [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-基于应用程序，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]键盘和消息处理包括下列项：  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost>类获取来自[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]消息循环，由实现<xref:System.Windows.Interop.ComponentDispatcher>类。  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost>类创建一个代理项[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]消息循环，以确保，普通[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]键盘处理时发生。  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost>类实现<xref:System.Windows.Interop.IKeyboardInputSink>接口来协调与焦点管理[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost>控件自行注册并启动其消息循环。  
  
 以下部分介绍这些部分的更多详细信息中的过程。  
  
### <a name="acquiring-messages-from-the-wpf-message-loop"></a>获取来自 WPF 消息循环的消息  
 <xref:System.Windows.Interop.ComponentDispatcher>类实现的消息循环管理器[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。 <xref:System.Windows.Interop.ComponentDispatcher>类提供挂钩以启用外部客户端之前筛选消息到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]对其进行处理。  
  
 互操作实现句柄<xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType>事件，它使[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件来处理消息之前[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]控件。  
  
### <a name="surrogate-windows-forms-message-loop"></a>代理项 Windows 窗体消息循环  
 默认情况下<xref:System.Windows.Forms.Application?displayProperty=nameWithType>类包含的主消息循环[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序。 在互操作，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]循环不处理消息的消息。 因此，必须重新生成此逻辑。 处理程序<xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType>事件执行以下步骤：  
  
1.  消息使用筛选器<xref:System.Windows.Forms.IMessageFilter>接口。  
  
2.  调用<xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=nameWithType>方法。  
  
3.  将转换并发送消息，如有必要。  
  
4.  如果没有其他控件处理消息，消息传递到将托管控件。  
  
### <a name="ikeyboardinputsink-implementation"></a>IKeyboardInputSink 实现  
 代理项消息循环处理键盘管理。 因此，<xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType>方法是唯一<xref:System.Windows.Interop.IKeyboardInputSink>需要中的实现的成员<xref:System.Windows.Forms.Integration.WindowsFormsHost>类。  
  
 默认情况下<xref:System.Windows.Interop.HwndHost>类返回`false`有关其<xref:System.Windows.Interop.HwndHost.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A>实现。 这可以防止从 tab 键次序[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]控制对[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>的实现<xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType>方法执行以下步骤：  
  
1.  查找第一个或最后一个[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]包含由控件<xref:System.Windows.Forms.Integration.WindowsFormsHost>控制且可以接收焦点。 控件选择取决于遍历的信息。  
  
2.  将焦点设置到控件，并返回`true`。  
  
3.  如果没有控件可以接收焦点，则返回`false`。  
  
### <a name="windowsformshost-registration"></a>WindowsFormsHost 注册  
 当窗口的句柄<xref:System.Windows.Forms.Integration.WindowsFormsHost>创建控件，<xref:System.Windows.Forms.Integration.WindowsFormsHost>控件调用注册的消息循环其存在的内部静态方法。  
  
 在注册期间<xref:System.Windows.Forms.Integration.WindowsFormsHost>控件将检查消息循环。 如果尚未启动消息循环，<xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType>创建事件处理程序。 消息循环运行时被视为<xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType>附加事件处理程序。  
  
 当销毁窗口句柄时，<xref:System.Windows.Forms.Integration.WindowsFormsHost>从注册的控件删除本身。  
  
## <a name="elementhost-keyboard-and-message-processing"></a>ElementHost 键盘和消息处理  
 由托管时，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]键盘和消息处理包括下列项：  
  
-   <xref:System.Windows.Interop.HwndSource><xref:System.Windows.Interop.IKeyboardInputSink>，和<xref:System.Windows.Interop.IKeyboardInputSite>接口实现代码。  
  
-   按 tab 键和箭头键。  
  
-   命令键和对话框键。  
  
-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 快捷键处理。  
  
 以下各节介绍了这些部分中更多详细信息。  
  
### <a name="interface-implementations"></a>接口实现  
 在[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]，键盘消息路由到具有焦点的控件的窗口句柄。 在<xref:System.Windows.Forms.Integration.ElementHost>控件，这些消息路由到承载的元素。 若要完成此操作，请<xref:System.Windows.Forms.Integration.ElementHost>控件提供了<xref:System.Windows.Interop.HwndSource>实例。 如果<xref:System.Windows.Forms.Integration.ElementHost>控件具有焦点<xref:System.Windows.Interop.HwndSource>实例路由大多数键盘输入，以便可以由处理[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Input.InputManager>类。  
  
 <xref:System.Windows.Interop.HwndSource>类实现<xref:System.Windows.Interop.IKeyboardInputSink>和<xref:System.Windows.Interop.IKeyboardInputSite>接口。  
  
 键盘互操作依赖于实现<xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A>方法句柄 TAB 键和箭头键将焦点移出承载的元素的输入。  
  
### <a name="tabbing-and-arrow-keys"></a>Tab 键和箭头键  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]选择逻辑映射到<xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A>和<xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A>方法来实现选项卡和箭头键导航。 重写<xref:System.Windows.Forms.Integration.ElementHost.Select%2A>方法即可实现此映射。  
  
### <a name="command-keys-and-dialog-box-keys"></a>命令键和对话框键  
 若要让[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]处理命令键和对话框键的第一个机会[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]预处理命令连接到<xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A>方法。 重写<xref:System.Windows.Forms.Control.ProcessCmdKey%2A?displayProperty=nameWithType>方法连接这两种技术。  
  
 使用<xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A>方法中，承载的元素可以处理任何关键消息，如 WM_KEYDOWN、 WM_KEYUP、 WM_SYSKEYDOWN 或 WM_SYSKEYUP，包括命令键，例如选项卡、 ENTER、 ESC、 和箭头键。 如果未处理键消息，它将被发送，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]上级层次结构进行处理。  
  
### <a name="accelerator-processing"></a>快捷键处理  
 若要正确处理加速器[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]快捷键处理必须连接到[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Input.AccessKeyManager>类。 此外，必须将所有的 WM_CHAR 消息正确路由到承载的元素。  
  
 因为默认值<xref:System.Windows.Interop.HwndSource>的实现<xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A>方法将返回`false`，使用以下逻辑 WM_CHAR 消息进行处理：  
  
-   <xref:System.Windows.Forms.Control.IsInputChar%2A?displayProperty=nameWithType>方法被重写以确保所有的 WM_CHAR 消息都转发至承载的元素。  
  
-   如果按下 ALT 键时，消息为 WM_SYSCHAR。 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 不预处理通过此消息<xref:System.Windows.Forms.Control.IsInputChar%2A>方法。 因此，<xref:System.Windows.Forms.Control.ProcessMnemonic%2A>方法被重写查询[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Input.AccessKeyManager>已注册的快捷键。 如果找到已注册的快捷键，则<xref:System.Windows.Input.AccessKeyManager>对其进行处理。  
  
-   如果未按下 ALT 键， [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager>类处理未处理的输入。 如果输入是快捷键，<xref:System.Windows.Input.AccessKeyManager>对其进行处理。 <xref:System.Windows.Input.InputManager.PostProcessInput>的未处理的 WM_CHAR 消息处理事件。  
  
 当用户按下 ALT 键时，整个窗体上显示快捷键的可视化提示。 若要支持此行为，所有<xref:System.Windows.Forms.Integration.ElementHost>活动窗体上的控件接收 WM_SYSKEYDOWN 消息，无论哪个控件具有焦点。  
  
 消息将仅发送给<xref:System.Windows.Forms.Integration.ElementHost>活动窗体中的控件。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A>
- <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>
- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [演练：承载在 WPF 中的 Windows 窗体复合控件](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [演练：承载 WPF 复合控件在 Windows 窗体中](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [WPF 和 Win32 互操作](wpf-and-win32-interoperation.md)
