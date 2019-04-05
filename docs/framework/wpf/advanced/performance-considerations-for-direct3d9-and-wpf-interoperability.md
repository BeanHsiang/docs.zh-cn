---
title: Direct3D9 和 WPF 互操作性的性能注意事项
ms.date: 03/30/2017
helpviewer_keywords:
- WPF [WPF], Direct3D9 interop performance
- Direct3D9 [WPF interoperability], performance
ms.assetid: ea8baf91-12fe-4b44-ac4d-477110ab14dd
ms.openlocfilehash: fd3c99f22a1d097c82494ba6eff344820162ed87
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57356710"
---
# <a name="performance-considerations-for-direct3d9-and-wpf-interoperability"></a>Direct3D9 和 WPF 互操作性的性能注意事项
你可以通过使用承载 Direct3D9 内容<xref:System.Windows.Interop.D3DImage>类。 承载 Direct3D9 内容可能会影响应用程序的性能。 本主题介绍承载 Windows Presentation Foundation (WPF) 应用程序中的 Direct3D9 内容时优化性能的最佳做法。 这些最佳实践包括如何使用<xref:System.Windows.Interop.D3DImage>和最佳做法，当你使用的 Windows Vista，Windows XP，并且多监视器显示。  
  
> [!NOTE]
>  有关代码示例说明了这些最佳实践，请参阅[WPF 和 Direct3D9 互操作](wpf-and-direct3d9-interoperation.md)。  
  
## <a name="use-d3dimage-sparingly"></a>尽量少使用 D3DImage  
 在中托管 Direct3D9 内容<xref:System.Windows.Interop.D3DImage>实例不会使同样快如纯 Direct3D 应用程序中所示。 复制图面和刷新命令缓冲区可能成本高昂的操作。 为数<xref:System.Windows.Interop.D3DImage>实例会增加，多个刷新发生，并且性能降低的程度。 因此，应使用<xref:System.Windows.Interop.D3DImage>尽量少。  
  
## <a name="best-practices-on-windows-vista"></a>Windows Vista 的最佳做法  
 与配置为使用 Windows 显示驱动程序模型 (WDDM) 显示在 Windows Vista 上获得最佳性能，创建 Direct3D9 图面上`IDirect3DDevice9Ex`设备。 这使图面上的共享。 视频卡必须支持`D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES`和`D3DCAPS2_CANSHARERESOURCE`Windows Vista 上的驱动程序功能。 任何其他设置会导致面以复制通过软件，从而显著降低性能。  
  
> [!NOTE]
>  如果 Windows Vista 具有配置为使用 Windows XP 显示驱动程序模型 (XDDM) 显示，在图面是始终复制通过软件，无论设置如何。 使用正确的设置和视频卡，会更好的性能在 Windows Vista 上时使用 WDDM，因为在硬件中执行图面上的副本。  
  
## <a name="best-practices-on-windows-xp"></a>Windows XP 的最佳做法  
 为了获得最佳性能，在 Windows XP 中，使用 Windows XP 显示驱动程序模型 (XDDM)，创建正确的行为的可锁定表面时`IDirect3DSurface9::GetDC`调用方法。 在内部，`BitBlt`方法在硬件中的设备之间传输图面。 `GetDC`方法始终适用 XRGB 图面上。 但是，如果客户端计算机正在运行 Windows XP SP3 或 SP2，并且客户端还具有分层窗口功能的修补程序，此方法仅适用于 ARGB 图面。 视频卡必须支持`D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES`驱动程序功能。  
  
 16 位桌面显示深度可以显著降低性能。 建议使用 32 位桌面。  
  
 如果你正在开发适用于 Windows Vista 和 Windows XP，测试在 Windows XP 上的性能。 在 Windows XP 上的视频内存不足是一个问题。 此外， <xref:System.Windows.Interop.D3DImage> Windows XP 上使用更多视频内存和带宽比 Windows Vista WDDM，由于所需的额外视频内存复制。 因此，可以获得更糟糕的是 Windows vista 比 Windows XP 上是相同的视频硬件的性能。  
  
> [!NOTE]
>  XDDM 是适用于 Windows XP 和 Windows Vista;但是，WDDM 是仅在 Windows Vista 上可用。  
  
## <a name="general-best-practices"></a>常规最佳做法  
 创建设备，请使用`D3DCREATE_MULTITHREADED`创建标记。 这会降低性能，但 WPF 呈现系统从另一个线程在此设备上调用方法。 务必遵循锁定协议正确，因此，没有两个线程同时访问设备。  
  
 如果 WPF 托管线程上执行呈现，则强烈建议您创建与设备`D3DCREATE_FPU_PRESERVE`创建标记。 如果没有此设置，D3D 呈现可以减少 WPF 双精度运算的准确性，并引入呈现问题。  
  
 平铺<xref:System.Windows.Interop.D3DImage>速度快，除非磁贴非 pow2 图面，而无需硬件支持，或如果选择平铺<xref:System.Windows.Media.DrawingBrush>或<xref:System.Windows.Media.VisualBrush>，其中包含<xref:System.Windows.Interop.D3DImage>。  
  
## <a name="best-practices-for-multi-monitor-displays"></a>多监视器显示的最佳做法  
 如果使用了多个监视器的计算机，你应遵循前面所述的最佳做法。 也有多监视器配置的一些额外的性能注意事项。  
  
 创建后台缓冲区时，创建在特定的设备和适配器，但 WPF 可能会显示任何适配器上的前台缓冲区。 在适配器，以更新前台缓冲区之间复制会产生大量费用。 在配置为用于多个视频卡以及 WDDM 的 Windows Vista 上`IDirect3DDevice9Ex`设备，如果上一个不同的适配器，但仍相同的视频卡前台缓冲区，没有任何性能损失。 但是，在 Windows XP 和具有多个视频卡 XDDM，没有对显著的性能产生负面影响时前台缓冲区，系统会在不同于后台缓冲区的适配器。 有关详细信息，请参阅[WPF 和 Direct3D9 互操作](wpf-and-direct3d9-interoperation.md)。  
  
## <a name="performance-summary"></a>性能摘要  
 下表显示了前台缓冲区更新的操作系统、 像素格式和图面上可锁定性的函数的性能。 前台缓冲区和后台缓冲区都假定为同一适配器上。 适配器配置中，根据硬件更新一些通常比软件更新快得多。  
  
|图面上的像素格式|Windows Vista、 WDDM 和 9Ex|其他 Windows Vista 配置|Windows XP SP3 或修补程序带 SP2|Windows XP SP2|  
|--------------------------|---------------------------------|----------------------------------------|--------------------------------------|--------------------|  
|D3DFMT_X8R8G8B8 （不是可锁定）|**硬件更新**|软件更新|软件更新|软件更新|  
|D3DFMT_X8R8G8B8 (lockable)|**硬件更新**|软件更新|**硬件更新**|**硬件更新**|  
|D3DFMT_A8R8G8B8 （不是可锁定）|**硬件更新**|软件更新|软件更新|软件更新|  
|D3DFMT_A8R8G8B8 (lockable)|**硬件更新**|软件更新|**硬件更新**|软件更新|  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Interop.D3DImage>
- [WPF 和 Direct3D9 互操作](wpf-and-direct3d9-interoperation.md)
- [演练：创建在 WPF 中承载的 Direct3D9 内容](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [演练：在 WPF 中承载 Direct3D9 内容](walkthrough-hosting-direct3d9-content-in-wpf.md)
