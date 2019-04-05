---
title: 图形呈现注册表设置
ms.date: 03/30/2017
helpviewer_keywords:
- rendering graphics [WPF], registry settings
- rendering graphics [WPF]
- rendering graphics [WPF], troubleshooting
- troubleshooting graphics rendering [WPF]
- graphics [WPF], rendering
ms.assetid: f4b41b42-327d-407c-b398-3ed5f505df8b
ms.openlocfilehash: 4b02a5ef1fb28e83ecdfc257dd81d9a890b77121
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57375345"
---
# <a name="graphics-rendering-registry-settings"></a>图形呈现注册表设置
本主题概述了影响 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 图形呈现注册表设置。  
  

  
<a name="overview"></a>   
## <a name="when-to-use-graphics-rendering-registry-settings"></a>何时使用图形呈现注册表设置  
 这些注册表设置为故障排除、调试和产品支持目的而提供。 由于对注册表的更改会影响所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序，应用程序永远不应该自动或在安装期间更改这些注册表项。  
  
<a name="xpdmandwddm"></a>   
## <a name="what-are-xpdm-and-wddm"></a>什么是 XPDM 和 WDDM？  
 某些图形呈现注册表设置具有不同的默认值，具体取决于视频卡使用的是 XPDM 还是 WDDM 驱动程序。 XPDM 是 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 显示驱动程序模式，WDDM 是 Windows 显示驱动程序模型。 WDDM 适用于运行 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] 和 [!INCLUDE[win7](../../../../includes/win7-md.md)] 的计算机。 WDDM 适用于运行 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)]、[!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 和 [!INCLUDE[TLA#tla_winnetsvrfam](../../../../includes/tlasharptla-winnetsvrfam-md.md)] 的计算机。 有关 WDDM 的详细信息，请参阅 [Windows Vista 显示驱动程序模式设计指南](https://go.microsoft.com/fwlink/?LinkId=178394)。  
  
<a name="registry_settings"></a>   
## <a name="registry-settings"></a>注册表设置  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了四个注册表设置来控制 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 呈现：  
  
|设置|描述|  
|-------------|-----------------|  
|**禁用硬件加速选项**|指定是否应启用硬件加速。|  
|**最大多重采样值**|指定用于消除 [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] 内容锯齿的多重采样级别。|  
|**必需的视频驱动程序日期设置**|指定系统是否对 2004 年 11 月之前发布的驱动程序禁用硬件加速。|  
|**使用参考光栅器选项**|指定 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是否应使用参考光栅器。|  
  
 知道如何引用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 注册表设置的任何外部配置实用工具都可以访问这些设置。 还可以直接使用 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 注册表编辑器来访问这些值，从而创建或修改这些设置。  
  
<a name="disablehardwareacceleration"></a>   
## <a name="disable-hardware-acceleration-option"></a>禁用硬件加速选项  
  
|注册表项|值类型|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\DisableHWAcceleration`|DWORD|  
  
 使用“禁用硬件加速选项”，可以出于调试和测试目的而关闭硬件加速。 查看应用程序中的呈现项目时，尝试关闭硬件加速。 如果项目消失，则视频驱动程序可能有问题。  
  
 “禁用硬件加速选项”是一个等于 0 或 1 的 DWORD 值。 如果值为 1，表示禁用硬件加速。 如果值为 0，表示启用硬件加速，前提是系统满足硬件加速要求；有关详细信息，请参阅[图形呈现层](../advanced/graphics-rendering-tiers.md)。  
  
<a name="maxmultisample"></a>   
## <a name="maximum-multisample-value"></a>最大多重采样值  
  
|注册表项|值类型|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\MaxMultisampleType`|DWORD|  
  
 使用“最大多重采样值”，可以调整 [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] 内容的最大抗锯齿量。 使用此级别，在 [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] 中禁用 [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] 抗锯齿或在 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 中启用它。  
  
 “最大多重采样值”是一个 DWORD 值，范围为从 0 到 16。 如果值为 0，则指定应禁用 3-D 内容的多重采样抗锯齿；如果值为 16，将尝试设置最多 16 倍多重采样抗锯齿（如果受视频卡支持）。 请注意，在使用 XPDM 驱动程序的计算机上设置此注册表项值将导致应用程序使用大量额外视频内存，降低 [!INCLUDE[TLA2#tla_3d](../../../../includes/tla2sharptla-3d-md.md)] 呈现的性能，并且有可能导致发生呈现错误和稳定性问题。  
  
 当未设置此注册表项时， [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将默认为 0（对于 XPDM 驱动程序）和 4（对于 WDDM 驱动程序）。  
  
<a name="requiredvideodriverdatesetting"></a>   
## <a name="required-video-driver-date-setting"></a>必需的视频驱动程序日期设置  
  
|注册表项|值类型|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\RequiredVideoDriverDate`|String|  
  
 在 2004 年 11 月，[!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] 发布了新版本的驱动程序测试指南；在此日期之后写入的驱动程序提供更好的稳定性。 默认情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将为这些驱动程序使用硬件加速管道，并将回退到此日期之前发布的 XPDM 驱动程序的软件呈现。  
  
 使用“必需的视频驱动程序日期设置”，可以为 XPDM 驱动程序指定最早备用日期。 如果确信视频驱动程序足够稳定，可支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，应仅指定早于 2004 年 11 月的日期。  
  
 必需的视频驱动程序采用以下格式的字符串：  
  
| |  
|-|  
|*YYYY* `/` *MM* `/` *DD*|  
  
 其中 *YYYY* 是四位数年份，*MM* 是两位数月份，而 *DD* 是两位数日期。 当未设置此值时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用 2004 年 11 月作为必需的视频驱动程序日期。  
  
<a name="usereferencerasterizeroption"></a>   
## <a name="use-reference-rasterizer-option"></a>使用参考光栅器选项  
  
|注册表项|值类型|  
|------------------|----------------|  
|`HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\UseReferenceRasterizer`|DWORD|  
  
 使用“使用参考光栅器选项”，可以在模拟硬件呈现模式中强制执行 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 以进行调试：[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 转到硬件模式，但使用 [!INCLUDE[TLA#tla_d3d](../../../../includes/tlasharptla-d3d-md.md)] 参考软件光栅器 d3dref9.dll，而不是实际的硬件设备。  
  
 参考光栅器非常缓慢，但可以绕过视频驱动程序以避免由驱动程序问题导致的任何呈现问题。 出于此原因，可使用参考光栅器确定呈现问题是否由视频驱动程序导致。 d3dref9.dll 文件必须位于应用程序可访问它的位置，如系统路径或应用程序的本地目录中的任何位置。  
  
 “使用参考光栅器选项”采用 DWORD 值。 值为 0 指示不使用参考光栅器。 任何其他非零值都强制 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用参考光栅器。  
  
## <a name="see-also"></a>请参阅
- [图形呈现层](../advanced/graphics-rendering-tiers.md)
- [WPF 图形呈现概述](wpf-graphics-rendering-overview.md)
