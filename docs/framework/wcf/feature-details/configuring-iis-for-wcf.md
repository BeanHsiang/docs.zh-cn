---
title: 为 Windows Communication Foundation 配置 Internet Information Services 7.0
ms.date: 03/30/2017
ms.assetid: 1050d395-092e-44d3-b4ba-66be3b039ffb
ms.openlocfilehash: 53ba48d47d30bd94ae5544920041cd430526223b
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54710285"
---
# <a name="configuring-internet-information-services-70-for-windows-communication-foundation"></a>为 Windows Communication Foundation 配置 Internet Information Services 7.0

Internet Information Services (IIS) 7.0 具有模块化设计，允许有选择地安装需要的组件。 此设计基于在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 中引入的新清单驱动的组件化技术。 有 40 多个独立功能组件可以独立安装的 IIS 7.0。 这使 IT 专业人士能够轻松地按需要自定义安装。 本主题讨论如何使用 Windows Communication Foundation (WCF) 配置 IIS 7.0 和确定所需的组件。

## <a name="minimal-installation-installing-was"></a>最小安装：安装 WAS
 整个 IIS 7.0 包的最小安装是安装 Windows 进程激活服务 (WAS)。 是一个独立功能，它是从可用于所有 IIS 7.0 的唯一功能[!INCLUDE[wv](../../../../includes/wv-md.md)]操作系统 （Home Basic、 Home Premium、 Business 和旗舰版和企业版）。

 从控制面板中，单击**程序**，然后单击**打开或关闭打开的 Windows 功能**下列出的**程序和功能**，WAS 组件所示如下面的插图中所示的列表。

 ![功能打开或关闭对话框](../../../../docs/framework/wcf/feature-details/media/wcfc-turnfeaturesonoroffs.gif "wcfc_TurnFeaturesOnOrOffs")

 此功能具有下列子组件：

-   .NET Environment

-   配置 API

-   进程模型

 如果选择 WAS，根节点只**过程模型**默认情况下选中子节点。 请注意，使用此安装时，你将只安装 WAS，因为没有用于 Web 服务器的支持功能。

 若要使 WCF 或 ASP.NET 应用程序的任何工作，检查 **.NET 环境**复选框。 这意味着所有 WAS 组件需要使 WCF 和 ASP.NET 来有效工作。 您安装其中任何组件后，会自动选中这些组件。

## <a name="iis-70-default-installation"></a>IIS 7.0:默认安装
 通过检查**Internet Information Services**功能，某些子节点会自动选中，如下图中所示。

 ![IIS 7.0 功能的默认设置](../../../../docs/framework/wcf/feature-details/media/wcfc-turningfeaturesonoroff2.gif "wcfc_TurningFeaturesOnOrOff2")

 这是 IIS 7.0 的默认安装。 使用此安装时，可以使用 IIS 7.0 提供静态内容 （如 HTML 页和其他内容）。 但是，不能运行 ASP.NET 或 CGI 应用程序或托管 WCF 服务。

## <a name="iis-70-installation-with-aspnet-support"></a>IIS 7.0:带 ASP.NET 支持的安装
 必须安装 ASP.NET 以使 IIS 7.0 上运行的 ASP.NET。 在检查后**ASP.NET**，屏幕应如图所示。

 ![Asp.NET 所需的设置](../../../../docs/framework/wcf/feature-details/media/wcfc-trunfeaturesonoroff3s.gif "wcfc_TrunFeaturesOnOrOFf3s")

 这是 WCF 和 ASP.NET 应用程序能够在 IIS 7.0 中的最小环境。

## <a name="iis-70-installation-with-iis-60-compatibility-components"></a>IIS 7.0:与 IIS 6.0 兼容组件的安装
 当在 Visual Studio 2005 或某些其他自动化的脚本或工具 （如 Adsutil.vbs) 配置虚拟应用程序使用 IIS 6.0 元数据库 API 的系统上安装 IIS 7.0，请确保选中 IIS 6.0**脚本工具**. 这将自动检查 IIS 6.0 中的其他子节点**管理兼容性**。 此操作完成后下, 图显示了屏幕：

 ![IIS 6.0 管理兼容性设置](../../../../docs/framework/wcf/feature-details/media/scfc-turnfeaturesonoroff5s.gif "scfc_TurnFeaturesOnOrOff5s")

 使用此安装时，您可以在 Web 上使用 IIS 7.0、 ASP.NET 和 WCF 功能和可用的示例所需的所有内容。

## <a name="request-limits"></a>请求限制
 在带有 IIS 7 的 [!INCLUDE[wv](../../../../includes/wv-md.md)] 上，`maxUri` 和 `maxQueryStringSize` 设置的默认值均已更改。 默认情况下，IIS 7.0 中的请求筛选功能允许 URL 的长度为 4096 个字符，查询字符串的长度为 2048 个字符。 更改这些默认值，可将以下 XML 添加到 App.config 文件中。

```xml
 <system.webServer>
    <security>
        <requestFiltering>
            <requestLimits maxUrl="8192" maxQueryString="8192" />
        </requestFiltering>
    </security>
 </system.webServer>
 ```

## <a name="see-also"></a>请参阅

- [WAS 激活体系结构](../../../../docs/framework/wcf/feature-details/was-activation-architecture.md)
- [配置 WAS 以用于 WCF](../../../../docs/framework/wcf/feature-details/configuring-the-wpa--service-for-use-with-wcf.md)
- [如何：安装和配置 WCF 激活组件](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)
- [Windows Server App Fabric 承载功能](https://go.microsoft.com/fwlink/?LinkId=201276)
