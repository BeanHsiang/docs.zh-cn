---
title: 如何：配置 Visual Studio 以调试 XAML 浏览器应用程序来调用 Web 服务
ms.date: 03/30/2017
helpviewer_keywords:
- debugging XBAPs that call a Web service [WPF]
- debugging security exceptions for XBAPs [WPF]
- security exception for XBAPs [WPF], debugging
- configuring Visual Studio to debug XAML browser applications [WPF]
- configuring Visual Studio to debug XBAPs [WPF]
ms.assetid: fd1db082-a7bb-4c4b-9331-6ad74a0682d0
ms.openlocfilehash: 94d362767b92799fa54f46e71724284a92b5bf7e
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57358816"
---
# <a name="how-to-configure-visual-studio-to-debug-a-xaml-browser-application-to-call-a-web-service"></a>如何：配置 Visual Studio 以调试 XAML 浏览器应用程序来调用 Web 服务
[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 在 Internet 区域权限集仅限于部分信任安全沙箱中运行。 此权限集将限制仅 Web 服务位于 Web 服务调用[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]应用程序的源站点。 当[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]调试从 Visual Studio 2005 中，不过，它不被视为具有相同的源站点的 Web 服务它的引用。 这会导致安全异常时引发[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]尝试调用 Web 服务。 但是，Visual Studio 2005[!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)]项目可以配置为模拟有与它进行调试时将调用 Web 服务相同的源站点。 这允许[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]来安全地调用 Web 服务，而不会导致安全异常。

## <a name="configuring-visual-studio"></a>配置 Visual Studio
 若要配置 Visual Studio 2005 来调试[!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]调用 Web 服务：

1.  在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2.  在中**项目设计器**，单击**调试**选项卡。

3.  在中**启动操作**部分中，选择**启动外部程序**并输入以下命令：

     `C:\WINDOWS\System32\PresentationHost.exe`

4.  在中**启动选项**部分中，输入到以下**命令行参数**文本框中：

     `-debug`  *filename*

     *文件名*值 **-调试**参数是.xbap 文件名; 例如：

     `-debug c:\example.xbap`

> [!NOTE]
>  这是使用 Visual Studio 2005 创建的解决方案的默认配置[!INCLUDE[TLA#tla_wpfbrowserappproj](../../../../includes/tlasharptla-wpfbrowserappproj-md.md)]项目模板。

1.  在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2.  在中**项目设计器**，单击**调试**选项卡。

3.  在中**启动选项**部分中，添加以下命令行参数**命令行参数**文本框中：

     `-debugSecurityZoneURL` URL

     *URL*值 **-debugSecurityZoneURL**参数是[!INCLUDE[TLA#tla_url](../../../../includes/tlasharptla-url-md.md)]你想要模拟不会成为您的应用程序源站点的位置。

 例如，考虑[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]Web 服务使用以下[!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)]:

 `http://services.msdn.microsoft.com/ContentServices/ContentService.asmx`

 源站点的[!INCLUDE[TLA2#tla_url](../../../../includes/tla2sharptla-url-md.md)]为此 Web 服务是：

 `http://services.msdn.microsoft.com`

 因此，完整 **-debugSecurityZoneURL**命令行参数和值是：

 `-debugSecurityZoneURL http://services.msdn.microsoft.com`

## <a name="see-also"></a>请参阅
- [WPF 主机 (PresentationHost.exe)](wpf-host-presentationhost-exe.md)
