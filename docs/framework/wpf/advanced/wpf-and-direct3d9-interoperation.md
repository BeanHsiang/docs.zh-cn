---
title: WPF 和 Direct3D9 互操作
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 1b14b823-69c4-4e8d-99e4-f6dade58f89a
ms.openlocfilehash: e9d000ca2da9dd9b4c8a677e85bc9cca5b1b1b1d
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57372680"
---
# <a name="wpf-and-direct3d9-interoperation"></a>WPF 和 Direct3D9 互操作
可以在 Windows Presentation Foundation (WPF) 应用程序中包含 Direct3D9 内容。 本主题介绍如何创建 Direct3D9 内容，以便它有效地与 WPF 互操作。  
  
> [!NOTE]
>  在 WPF 中使用 Direct3D9 内容，还需要考虑到性能。 有关如何优化性能的详细信息，请参阅[Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)。  
  
## <a name="display-buffers"></a>显示缓冲区  
 <xref:System.Windows.Interop.D3DImage>类管理两个显示缓冲区，称为*后台缓冲区*并且*前台缓冲区*。 后台缓冲区是 Direct3D9 图面。 对后台缓冲区的更改复制前滚到前台缓冲区调用时<xref:System.Windows.Interop.D3DImage.Unlock%2A>方法。  
  
 下图显示后台缓冲区和前台缓冲区之间的关系。  
  
 ![D3DImage 显示缓冲区](./media/d3dimage-buffers.png "D3DImage_buffers")  
  
## <a name="direct3d9-device-creation"></a>创建 Direct3D9 设备  
 若要呈现 Direct3D9 内容，必须创建 Direct3D9 设备。 有两个可用于创建设备的 Direct3D9 对象`IDirect3D9`和`IDirect3D9Ex`。 使用这些对象创建`IDirect3DDevice9`和`IDirect3DDevice9Ex`设备，分别。  
  
 通过调用以下方法之一创建一个设备。  
  
-   `IDirect3D9 * Direct3DCreate9(UINT SDKVersion);`  
  
-   `HRESULT Direct3DCreate9Ex(UINT SDKVersion, IDirect3D9Ex **ppD3D);`  
  
 在 Windows Vista 或更高版本操作系统上，使用`Direct3DCreate9Ex`与配置为使用 Windows 显示驱动程序模型 (WDDM) 显示的方法。 使用`Direct3DCreate9`任何其他平台上的方法。  
  
### <a name="availability-of-the-direct3dcreate9ex-method"></a>Direct3DCreate9Ex 方法的可用性  
 D3d9.dll 具有`Direct3DCreate9Ex`仅在 Windows Vista 或更高版本操作系统上的方法。 如果直接链接在 Windows XP 上的函数，你的应用程序加载失败。 若要确定是否`Direct3DCreate9Ex`支持方法、 加载 DLL 和查找进程的地址。 下面的代码演示如何为测试`Direct3DCreate9Ex`方法。 有关完整的代码示例，请参阅[演练：创建在 WPF 中承载的 Direct3D9 内容](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureD3DObjects](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensured3dobjects)]  
  
### <a name="hwnd-creation"></a>HWND 创建  
 创建设备需要 HWND。 一般情况下，您创建 Direct3D9 使用虚拟 HWND。 下面的代码示例演示如何创建虚拟 HWND。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureHWND](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensurehwnd)]  
  
### <a name="present-parameters"></a>存在参数  
 创建设备还需要`D3DPRESENT_PARAMETERS`结构，但只有几个参数非常重要。 这些参数会选择最大程度减少内存占用量。  
  
 设置`BackBufferHeight`和`BackBufferWidth`字段为 1。 将它们设置为 0 会导致它们被设置为该 HWND 的尺寸。  
  
 始终设置`D3DCREATE_MULTITHREADED`和`D3DCREATE_FPU_PRESERVE`标记以避免损坏了用于通过 Direct3D9 并防止 Direct3D9 更改 FPU 设置。  
  
 下面的代码演示如何初始化`D3DPRESENT_PARAMETERS`结构。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_Init](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_init)]  
  
## <a name="creating-the-back-buffer-render-target"></a>创建后台缓冲区呈现器目标  
 若要显示在 Direct3D9 内容<xref:System.Windows.Interop.D3DImage>，创建 Direct3D9 面并将其分配通过调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>方法。  
  
### <a name="verifying-adapter-support"></a>验证适配器支持  
 创建图面之前, 验证所有适配器都支持所需的图面属性。 即使您呈现到只有一个适配器，可能会在系统中任何适配器上显示 WPF 窗口。 您应始终编写处理多适配器配置的 Direct3D9 代码和您应检查所有适配器的支持，因为 WPF 可能移动之间的可用适配器的图面。  
  
 下面的代码示例演示如何检查 Direct3D9 的系统上的所有适配器都支持。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_TestSurfaceSettings](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_testsurfacesettings)]  
  
### <a name="creating-the-surface"></a>创建在图面  
 创建图面之前, 请确认设备功能，在目标操作系统上支持良好的性能。 有关详细信息，请参阅[Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)。  
  
 如果你已验证设备功能，可以创建在图面。 下面的代码示例演示如何创建呈现器目标。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_CreateSurface](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_createsurface)]  
  
### <a name="wddm"></a>WDDM  
 在 Windows Vista 和更高版本的操作系统，已配置为使用 WDDM，可以创建呈现器目标纹理，并将传递到在级别 0 面<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>方法。 不建议使用此方法在 Windows XP 上因为不能创建可锁定的呈现目标纹理，并会降低性能。  
  
## <a name="handling-device-state"></a>处理设备状态  
 <xref:System.Windows.Interop.D3DImage>类管理两个显示缓冲区，称为*后台缓冲区*并且*前台缓冲区*。 后台缓冲区是 Direct3D 图面。  对后台缓冲区的更改复制前滚到前台缓冲区调用时<xref:System.Windows.Interop.D3DImage.Unlock%2A>方法，其中显示在硬件。 有时，前台缓冲区变得不可用。 缺乏可用性可能引起屏幕锁定、 全屏独占 Direct3D 应用程序、 用户切换或其他系统活动。 在 WPF 应用程序时出现这种情况，通过处理通知<xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged>事件。  你的应用程序到前台缓冲区变得不可用的响应方式取决于是否启用了 WPF 回退到软件呈现。 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>方法具有一个重载采用一个参数，指定是否 WPF 回退到软件呈现。  
  
 当您调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%29>重载或调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29>重载，并`enableSoftwareFallback`参数设置为`false`，呈现系统时前台缓冲区变得不可用和没有释放其对后台缓冲区的引用显示。 呈现系统前台缓冲区再次可用时，会引发<xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged>事件，以通知在 WPF 应用程序。  可以创建的事件处理程序<xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged>重启再次使用有效的 Direct3D 图面呈现的事件。 若要重新启动呈现，必须调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>。  
  
 当您调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29>重载，并`enableSoftwareFallback`参数设置为`true`，呈现系统保留对后台缓冲区的引用时前台缓冲区变得不可用，因此无需调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>时前面再次可用时缓冲区。  
  
 当启用软件呈现时，可能存在的用户的设备变得不可用，但呈现系统将保留的引用的 Direct3D 图面。 若要检查的 Direct3D9 设备是否不可用，请调用`TestCooperativeLevel`方法。 若要检查的 Direct3D9Ex 设备调用`CheckDeviceState`方法，因为`TestCooperativeLevel`方法已弃用，并始终返回成功。 如果用户设备已变为不可用，则调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>释放对后台缓冲区的 WPF 的引用。  如果你需要重置你的设备，则调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>与`backBuffer`参数设置为`null`，然后调用<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A>再次使用`backBuffer`设置为有效的 Direct3D 图面。  
  
 调用`Reset`方法仅当实现多适配器支持从无效的设备中恢复。 否则为释放所有 Direct3D9 接口并完全重新创建它们。 如果适配器布局已发生更改，更改之前创建的 Direct3D9 对象不会更新。  
  
## <a name="handling-resizing"></a>处理调整大小  
 如果<xref:System.Windows.Interop.D3DImage>将显示最适宜的分辨率以外其固有尺寸，则图像会根据当前<xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A>，只不过<xref:System.Windows.Media.Effects.SamplingMode.Bilinear>替换为<xref:System.Windows.Media.BitmapScalingMode.Fant>。  
  
 如果需要更高的保真度，您必须创建一个新图面时的容器<xref:System.Windows.Interop.D3DImage>更改大小。  
  
 有三种方法可以处理调整大小。  
  
-   参与布局系统时，并创建新的图面大小发生更改。 不要创建太多应用层，因为可能会用完可用抵或视频内存碎片。  
  
-   等待，直到固定时间内创建新的图面从未发生调整大小事件。  
  
-   创建<xref:System.Windows.Threading.DispatcherTimer>，用于检查每秒钟多次容器维度。  
  
## <a name="multi-monitor-optimization"></a>多监视器优化  
 呈现系统移动时，可能导致性能显著降低<xref:System.Windows.Interop.D3DImage>到另一个监视器。  
  
 在上 WDDM，只要这些监视器上相同的视频卡上，并使用`Direct3DCreate9Ex`，就不会在性能下降。 如果监视器位于不同的视频卡上，性能会下降。 在 Windows XP 中，会始终会降低性能。  
  
 当<xref:System.Windows.Interop.D3DImage>将移到另一个监视器，您可以创建新的图面上相应的适配器，以还原良好的性能。  
  
 若要避免对性能产生影响，编写专门为多监视器情况的代码。 以下列表显示了一种方法来编写多监视器的代码。  
  
1.  找到的一点<xref:System.Windows.Interop.D3DImage>中使用的屏幕空间`Visual.ProjectToScreen`方法。  
  
2.  使用`MonitorFromPoint`GDI 方法查找的监视器的显示该点。  
  
3.  使用`IDirect3D9::GetAdapterMonitor`法查找哪个 Direct3D9 适配器监视器已打开。  
  
4.  如果适配器不是与后台缓冲区的适配器相同，新的监视器上创建新的后台缓冲区，并将其分配给<xref:System.Windows.Interop.D3DImage>后台缓冲区。  
  
> [!NOTE]
>  如果<xref:System.Windows.Interop.D3DImage>跨多台监视器，性能将会很慢，除非在 WDDM 的情况下和`IDirect3D9Ex`同一适配器上。 没有方法在这种情况下提高性能。  
  
 下面的代码示例演示如何查找当前的监视器。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_SetAdapter](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_setadapter)]  
  
 更新监视器时<xref:System.Windows.Interop.D3DImage>容器的大小或位置更改或更新使用监视器`DispatcherTimer`每秒几次更新。  
  
## <a name="wpf-software-rendering"></a>WPF 软件呈现  
 在以下情况下的软件中的 UI 线程中的 WPF 呈现以同步方式。  
  
-   打印  
  
-   <xref:System.Windows.Media.Effects.BitmapEffect>  
  
-   <xref:System.Windows.Media.Imaging.RenderTargetBitmap>  
  
 当发生以下情况之一时，呈现系统调用<xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A>方法将复制到软件的硬件缓冲区。 默认实现将调用`GetRenderTargetData`方法与您的图面。 因为此调用发生在锁定/解锁模式之外，则可能会失败。 在这种情况下，`CopyBackBuffer`方法将返回`null`和不显示任何图像。  
  
 您可以重写<xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A>方法，调用基实现中，如果它返回`null`，可以返回占位符<xref:System.Windows.Media.Imaging.BitmapSource>。  
  
 此外可以实现自己的软件呈现，而不是调用基实现。  
  
> [!NOTE]
>  如果在软件中，完全呈现 WPF<xref:System.Windows.Interop.D3DImage>没有显示，因为 WPF 没有前台缓冲区。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 和 WPF 互操作性的性能注意事项](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [演练：创建在 WPF 中承载的 Direct3D9 内容](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [演练：在 WPF 中承载 Direct3D9 内容](walkthrough-hosting-direct3d9-content-in-wpf.md)
