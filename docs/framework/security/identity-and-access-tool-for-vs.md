---
title: 适用于 Visual Studio 2012 的标识和访问工具
ms.date: 03/30/2017
ms.assetid: 87b8f8f2-4074-44fd-9fd6-08278e877390
author: BrucePerlerMS
ms.openlocfilehash: a1b5456f9081d807a3c9e29e1010cbfbf91e637f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54678546"
---
# <a name="identity-and-access-tool-for-visual-studio-2012"></a>适用于 Visual Studio 2012 的标识和访问工具
本主题描述了适用于 Visual Studio 11 的新的标识和访问工具。 可以从以下 URL 下载此工具： [ https://go.microsoft.com/fwlink/?LinkID=245849 ](https://go.microsoft.com/fwlink/?LinkID=245849)或直接从 Visual Studio 11 中搜索"标识"直接在扩展管理器中。  
  
 适用于 Visual Studio 11 的新的标识和访问工具提供了开发时间大大减少的体验，并具有如下要点：  
  
-   借助此新工具，您可以使用 Web 应用程序项目类型和目标 IIS Express 进行开发。  
  
-   与一般仅保护性身份验证不同，利用此新工具，您可以指定本地主页领域发现页/控制器（或处理应用程序中的身份验证体验的任何其他终结点），并且 WIF 会将所有未经身份验证的请求配置为转到此处，而不是将其重定向到 STS。  
  
-   此工具包括一项在启动调试会话时运行于你的本地计算机上的测试安全令牌服务 (STS)。 因此，您不再需要创建自定义 STS 项目并对其进行调整即可获得测试应用程序所需的声明。 声明类型和值是可完全自定义的。  
  
-   你可以通过此工具的 UI 直接修改常见设置，而无需编辑 web.config。  
  
-   您可以在单个屏幕上使用 Active Directory 联合身份验证服务 (AD FS) 2.0（或其他 WS 联合身份验证提供程序）建立联合身份验证。  
  
-   该工具为你想要使用的所有标识提供者可利用 Windows Azure 访问控制服务 (ACS) 功能使用一个简单的复选框列表：Facebook、 Google、 Live ID、 yahoo ！、 任何 OpenID 提供程序和任何 WS 联合身份验证提供程序。 选择标识提供程序，单击“确定”，然后按 F5，这会自动配置你的应用程序和 ACS，并且你的测试应用程序将是 ACS 感知的。  
  
## <a name="see-also"></a>请参阅
- [WIF 功能](../../../docs/framework/security/wif-features.md)
