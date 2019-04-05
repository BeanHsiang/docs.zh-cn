---
title: WPF 部分信任安全
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- partial trust security [WPF]
- detecting permissions [WPF]
- security settings for Internet Explorer [WPF]
- partial trust applications [WPF], debugging
- permissions [WPF], managing
- debugging partial trust applications [WPF]
- permissions [WPF], detecting
- feature security requirements [WPF]
- managing permissions [WPF]
ms.assetid: ef2c0810-1dbf-4511-babd-1fab95b523b5
ms.openlocfilehash: c0391099d02933cb8a32a2e134dad949034138ad
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57371627"
---
# <a name="wpf-partial-trust-security"></a>WPF 部分信任安全
<a name="introduction"></a>一般情况下，应该限制 Internet 应用程序直接访问关键系统资源，防止恶意损坏。 默认情况下， [!INCLUDE[TLA#tla_html](../../../includes/tlasharptla-html-md.md)] ，客户端脚本编写语言也不能访问关键系统资源。 因为 Windows Presentation Foundation (WPF) 可从浏览器启动浏览器承载的应用程序，它们应该符合一组类似的限制。 若要强制实施这些限制[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]同时依赖于[!INCLUDE[TLA#tla_cas](../../../includes/tlasharptla-cas-md.md)]并[!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)](请参阅[WPF 安全策略-平台安全性](wpf-security-strategy-platform-security.md))。 默认情况下，浏览器承载的应用程序请求 Internet 区域[!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)]组的权限，而不考虑是否从 Internet、 本地 intranet 或本地计算机启动。 如果应用程序的运行权限小于完整权限集，则说明该应用程序正在部分信任环境下运行。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] 提供各种支持，以确保在部分信任，并连同，，可以安全地使用尽可能多的功能[!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)]，为部分信任编程提供额外支持。  
  
 本主题包含以下各节：  
  
-   [WPF 功能部分信任支持](#WPF_Feature_Partial_Trust_Support)  
  
-   [部分信任编程](#Partial_Trust_Programming)  
  
-   [管理权限](#Managing_Permissions)  
  
<a name="WPF_Feature_Partial_Trust_Support"></a>   
## <a name="wpf-feature-partial-trust-support"></a>WPF 功能部分信任支持  
 下表列出了安全的 Internet 区域权限集的限制范围内使用的高级功能的 Windows Presentation Foundation (WPF)。  
  
 表 1:在部分信任环境中的安全的 WPF 功能  
  
|功能区域|功能|  
|------------------|-------------|  
|常规|浏览器窗口<br /><br /> 源站点访问<br /><br /> IsolatedStorage（512KB 限制）<br /><br /> UIAutomation 提供程序<br /><br /> 命令<br /><br /> 输入法编辑器 (IME)<br /><br /> 触笔和墨迹<br /><br /> 使用鼠标捕获和移动事件模拟的拖/放<br /><br /> OpenFileDialog<br /><br /> XAML 反序列化（通过 XamlReader.Load）|  
|Web 集成|浏览器下载对话框<br /><br /> 顶级用户启动的导航<br /><br /> mailto:links<br /><br /> 统一资源标识符参数<br /><br /> HTTPWebRequest<br /><br /> IFRAME 中托管的 WPF 内容<br /><br /> 使用框架托管同一站点 HTML 页<br /><br /> 使用 WebBrowser 托管同一站点 HTML 页<br /><br /> Web 服务 (ASMX)<br /><br /> Web 服务（使用 Windows Communication Foundation）<br /><br /> “脚本”<br /><br /> 文档对象模型|  
|视觉对象|2D 和 3D<br /><br /> 动画<br /><br /> 媒体（源站点和跨域）<br /><br /> 图像处理/音频/视频|  
|阅读|流文档<br /><br /> XPS 文档<br /><br /> 嵌入式字体与系统字体<br /><br /> CFF 字体与 TrueType 字体|  
|编辑|拼写检查<br /><br /> RichTextBox<br /><br /> 纯文本和墨迹剪贴板支持<br /><br /> 用户启动的粘贴<br /><br /> 复制选定内容|  
|Controls|常规控件|  
  
 此表涵盖了[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]在高级别的功能。 有关更多详细信息，[!INCLUDE[TLA#tla_lhsdk](../../../includes/tlasharptla-lhsdk-md.md)]文档中的每个成员所需的权限[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]。 此外，以下功能含有部分信任执行的相关详细信息，其中包括特殊注意事项。  
  
-   [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] (请参阅[XAML 概述 (WPF)](./advanced/xaml-overview-wpf.md))。  
  
-   弹出窗口 (请参阅<xref:System.Windows.Controls.Primitives.Popup?displayProperty=nameWithType>)。  
  
-   拖放到 (请参阅[拖放概述](./advanced/drag-and-drop-overview.md))。  
  
-   剪贴板 (请参阅<xref:System.Windows.Clipboard?displayProperty=nameWithType>)。  
  
-   映像 (请参阅<xref:System.Windows.Controls.Image?displayProperty=nameWithType>)。  
  
-   序列化 (请参阅<xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=nameWithType>， <xref:System.Windows.Markup.XamlWriter.Save%2A?displayProperty=nameWithType>)。  
  
-   打开文件对话框 (请参阅<xref:Microsoft.Win32.OpenFileDialog?displayProperty=nameWithType>)。  
  
 下表概括了[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]不安全的 Internet 的限制范围内运行的功能区域权限集。  
  
 表 2:在部分信任环境中不安全的 WPF 功能  
  
|功能区域|功能|  
|------------------|-------------|  
|常规|窗口（应用程序定义的窗口和对话框）<br /><br /> SaveFileDialog<br /><br /> 文件系统<br /><br /> 注册表访问<br /><br /> 拖放<br /><br /> XAML 序列化（通过 XamlWriter.Save）<br /><br /> UIAutomation 客户端<br /><br /> 源窗口访问 (HwndHost)<br /><br /> 完全语音支持<br /><br /> Windows 窗体互操作性|  
|视觉对象|位图效果<br /><br /> 图像编码|  
|编辑|RTF 格式剪贴板<br /><br /> 完全 XAML 支持|  
  
<a name="Partial_Trust_Programming"></a>   
## <a name="partial-trust-programming"></a>部分信任编程  
 有关[!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)]应用程序，超出默认权限集的代码将具有不同的行为依赖于安全区域。 在某些情况下，用户会在尝试安装它时收到警告。 用户可以选择继续或取消安装。 下表描述每个安全区域的应用程序的行为，以及为了使应用程序接收完全信任而必须执行的操作。  
  
|安全区域|行为|获取完全信任|  
|-------------------|--------------|------------------------|  
|本地计算机|自动完全信任|无需执行任何操作。|  
|Intranet 和受信任的站点|提示完全信任|使用证书对 XBAP 进行签名，以便用户在提示中看到源。|  
|Internet|失败，并显示“未授予信任”|使用证书对 XBAP 进行签名。|  
  
> [!NOTE]
>  上表中描述的行为针对不遵循 ClickOnce 受信任部署模型的完全信任 XBAP。  
  
 通常，超出允许权限的代码可能是在独立应用程序和浏览器托管的应用程序之间共享的公用代码。 [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] 和[!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]提供用于管理此方案中的几种方法。  
  
<a name="Detecting_Permissions_using_CAS"></a>   
### <a name="detecting-permissions-using-cas"></a>使用 CAS 检测权限  
 在某些情况下，很可能共享中的代码库程序集以供这两个独立应用程序和[!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)]。 这时，代码执行的功能所需要的权限可能超出应用程序的授权权限集允许的权限。 你的应用程序可以检测有特定的权限的使用 Microsoft.NET Framework 安全性。 具体而言，它可以测试它是否有特定的权限通过调用<xref:System.Security.CodeAccessPermission.Demand%2A>所需权限的实例上的方法。 以下示例对此进行了演示，示例中的代码查询其是否能够将文件保存到本地磁盘：  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode2)]  
  
 如果应用程序没有所需的权限，对调用<xref:System.Security.CodeAccessPermission.Demand%2A>将引发安全异常。 如果没有引发异常，则表示已授予该权限。 `IsPermissionGranted` 封装此行为，并返回`true`或`false`根据需要。  
  
<a name="Graceful_Degradation_of_Functionality"></a>   
### <a name="graceful-degradation-of-functionality"></a>功能下降  
 对可从不同区域执行的代码而言，能够检测代码是否具有完成所需操作的权限是很有意义的。 能够检测区域固然不错，但如果能够为用户提供替代方法，则要好得多。 例如，完全信任应用程序通常使用户能够在所需的任何位置创建文件，而部分信任应用程序只能在独立存储中创建文件。 如果用于创建文件的代码存在于完全信任（独立）应用程序和部分信任（浏览器托管的）应用程序共享的程序集中，并且这两个应用程序都希望用户能够创建文件，则共享代码应首先检测其是在部分信任环境还是完全信任环境中运行，然后才能在适当的位置创建文件。 下面的代码对这两种情况进行了演示。  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode2)]  
  
 在很多情况下，应该能够找到部分信任替代方法。  
  
 在受控环境中，如 intranet，自定义托管的框架可以安装整个客户端群到[!INCLUDE[TLA#tla_gac](../../../includes/tlasharptla-gac-md.md)]。 这些库可以执行需要完全信任的代码，只允许使用部分信任的应用程序从引用<xref:System.Security.AllowPartiallyTrustedCallersAttribute>(有关详细信息，请参阅[安全](security-wpf.md)和[WPF 安全性策略-平台安全性](wpf-security-strategy-platform-security.md))。  
  
<a name="Browser_Host_Detection"></a>   
### <a name="browser-host-detection"></a>浏览器主机检测  
 使用[!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)]以检查是否有权限是恰当的方法时您需要根据每个权限检查。 然而，这一技巧依赖于在正常处理过程中捕获异常（通常不鼓励这样做），并且可能导致性能问题。 相反，如果你[!INCLUDE[TLA#tla_xbap](../../../includes/tlasharptla-xbap-md.md)]只在 Internet 区域沙箱内的运行，可以使用<xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A?displayProperty=nameWithType>属性，返回 true [!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)]。  
  
> [!NOTE]
>  <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A> 是否在浏览器中，没有哪个应用程序的权限集运行与运行应用程序仅将区分开来。  
  
<a name="Managing_Permissions"></a>   
## <a name="managing-permissions"></a>管理权限  
 默认情况下，[!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)]以部分信任级别 （默认 Internet 区域权限集） 运行。 但是，根据应用程序的要求，可以更改默认的权限集。 例如，如果[!INCLUDE[TLA2#tla_xbap#plural](../../../includes/tla2sharptla-xbapsharpplural-md.md)]启动时从本地 intranet，它可以充分利用增强的权限集下, 表中所示。  
  
 表 3:LocalIntranet 和 Internet 权限  
  
|权限|特性|LocalIntranet|Internet|  
|----------------|---------------|-------------------|--------------|  
|DNS|访问 DNS 服务器|是|否|  
|环境变量|读取|是|否|  
|文件对话框|打开|是|是|  
|文件对话框|不受限制|是|否|  
|独立存储|按用户隔离程序集|是|否|  
|独立存储|未知隔离|是|是|  
|独立存储|无限制用户配额|是|否|  
|媒体|安全音频、视频和图像|是|是|  
|打印|默认打印|是|否|  
|打印|安全打印|是|是|  
|映像|发出|是|否|  
|安全性|托管代码执行|是|是|  
|安全性|声明授予的权限|是|否|  
|用户界面|不受限制|是|否|  
|用户界面|安全顶级窗口|是|是|  
|用户界面|自己的剪贴板|是|是|  
|Web 浏览器|HTML 中的安全框架导航|是|是|  
  
> [!NOTE]
>  如果由用户启动，则剪切和粘贴只允许以部分信任方式执行。  
  
 如果需要增加权限，则需要更改项目设置和 ClickOnce 应用程序清单。 有关详细信息，请参阅 [WPF XAML 浏览器应用程序概述](./app-development/wpf-xaml-browser-applications-overview.md)。 以下各个文档可能也会有帮助。  
  
-   [Mage.exe（清单生成和编辑工具）](../tools/mage-exe-manifest-generation-and-editing-tool.md)。  
  
-   [MageUI.exe（图形化客户端中的清单生成和编辑工具）](../tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)。  
  
-   [保护 ClickOnce 应用程序](/visualstudio/deployment/securing-clickonce-applications)。  
  
 如果你[!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)]需要完全信任，可以使用相同的工具来提高所请求的权限。 尽管[!INCLUDE[TLA2#tla_xbap](../../../includes/tla2sharptla-xbap-md.md)]将仅接收完全信任，如果它是安装并启动从本地计算机上，在 intranet 或从受信任或允许的站点在浏览器中列出的 URL。 如果从 Intranet 或受信任站点安装应用程序，则用户会收到标准 ClickOnce 提示，通知用户提升了权限。 用户可以选择继续或取消安装。  
  
 或者，可以使用 ClickOnce 受信任部署模型从任何安全区域中进行完全信任部署。 有关详细信息，请参阅[Trusted Application Deployment Overview](/visualstudio/deployment/trusted-application-deployment-overview)并[安全](security-wpf.md)。  
  
## <a name="see-also"></a>请参阅
- [安全性](security-wpf.md)
- [WPF 安全策略 - 平台安全性](wpf-security-strategy-platform-security.md)
- [WPF 安全策略 - 安全工程](wpf-security-strategy-security-engineering.md)
