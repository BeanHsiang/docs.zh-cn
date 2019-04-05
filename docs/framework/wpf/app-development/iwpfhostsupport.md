---
title: IWpfHostSupport
ms.date: 03/30/2017
helpviewer_keywords:
- IWpfHostSupport interface [WPF]
ms.assetid: cc5a0281-de81-4cc1-87e4-0e46b1a811e9
ms.openlocfilehash: 074167111b78edc517dda019465260d0acd54737
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57376008"
---
# <a name="iwpfhostsupport"></a>IWpfHostSupport
托管的应用程序[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]内容 PresentationHost.exe 通过实现此接口可提供的主机和 PresentationHost.exe 之间的集成点。  
  
## <a name="remarks"></a>备注  
 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 应用程序，如 Web 浏览器可以托管[!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)]内容，包括[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]宽松 XAML。 到主机[!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)]内容，[!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)]应用程序创建的实例[WebBrowser 控件](https://go.microsoft.com/fwlink/?LinkId=97911)。 要托管[!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)]创建的 PresentationHost.exe，提供了托管实例[!INCLUDE[TLA#tla_titlewinclient](../../../../includes/tlasharptla-titlewinclient-md.md)]所在的主机中的显示内容[WebBrowser 控件](https://go.microsoft.com/fwlink/?LinkId=97911)。  
  
 通过启用集成`IWpfHostSupport`允许 PresentationHost.exe 到：  
  
-   发现并注册与主机应用程序感兴趣的原始输入设备 （人机接口设备）。  
  
-   接收输入的消息从已注册的原始输入的设备和适当的消息转发到主机应用程序。  
  
-   查询进度和错误的自定义用户界面的主机应用程序。  
  
> [!NOTE]
>  此 API 预期仅支持在本地客户端计算机上使用  
  
## <a name="members"></a>成员  
  
|成员|描述|  
|------------|-----------------|  
|[GetRawInputDevices](getrawinputdevices.md)|允许 PresentationHost.exe 发现主机应用程序感兴趣的原始输入的设备（人机接口设备）。|  
|[FilterInputMessage](filterinputmessage.md)|除非返回 E_NOTIMP，否则每当收到一条消息时都会由 PresentationHost.exe 调用。|  
|[GetCustomUI](getcustomui.md)|默认情况下，PresentationHost.exe 提供其自己的部署进度和部署错误会显示部署的 WPF 内容时的用户界面。|
