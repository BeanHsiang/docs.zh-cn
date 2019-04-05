---
title: Windows 窗体和非托管应用程序概述
ms.date: 03/30/2017
helpviewer_keywords:
- COM [Windows Forms]
- Windows Forms, unmanaged
- COM interop
- ActiveX controls [Windows Forms], about ActiveX controls
- Windows Forms, interop
ms.assetid: 0a26d99d-8135-4895-8760-c9a2b5f67f14
ms.openlocfilehash: cb7df844458be083adefa16421a7088bd1e74893
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57717929"
---
# <a name="windows-forms-and-unmanaged-applications-overview"></a>Windows 窗体和非托管应用程序概述
Windows 窗体应用程序和控件可以与非托管应用程序进行互操作，但有一些需要注意的问题。 以下各节将介绍 Windows 窗体应用程序和控件支持和不支持的方案和配置。  
  
## <a name="windows-forms-controls-and-activex-applications"></a>Windows 窗体控件和 ActiveX 应用程序  
 由于存在 Microsoft Internet Explorer 和 Microsoft 基础类 (MFC) 的异常，因此，在为了托管 ActiveX 控件而设计的应用程序中不支持 Windows 窗体控件。 在能够托管 ActiveX 控件的其他应用程序和开发工具（包括早于 Visual Studio .NET 2003 的 Visual Studio 版本中的 ActiveX 测试容器）中也不支持托管 Windows 窗体控件。  
  
 这些约束还适用于通过组件对象模型 COM 互操作来使用 Windows 窗体控件的情况。 只在 Internet Explorer 中支持通过 COM 可调用包装器 (CCW) 来使用 Windows 窗体控件。 有关 COM 互操作的详细信息，请参阅  
  
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)。  
  
 下表显示了对 Windows 窗体控件的可用 ActiveX 托管支持。  
  
|Windows 窗体版本|支持|  
|---------------------------|-------------|  
|.NET Framework 版本 1.0|Internet Explorer 5.01 和更高版本|  
|.NET Framework 版本 1.1 和更高版本|Internet Explorer 5.01 和更高版本<br /><br /> Microsoft 基础类 (MFC) 7.0 和更高版本|  
  
## <a name="hosting-windows-forms-components-as-activex-controls"></a>作为 ActiveX 控件托管 Windows 窗体组件  
 在.NET Framework 1.1 中，此支持已扩展到包括 MFC 7.0 和更高版本。 此支持包括与 MFC 7.0 和更高版本的 ActiveX 控件容器完全兼容的任何容器。  
  
 但是，不支持将 Windows 窗体控件注册为 ActiveX 控件。 此外，不支持调用 Windows 窗体控件的 `com.ms.win32.Ole32.CoCreateInstance` 方法。 仅支持对 Windows 窗体控件进行托管激活。 一旦创建了 Windows 窗体控件，即可按与 ActiveX 控件完全相同的方式在 MFC 应用程序上托管它。  
  
 若要在非托管应用程序中使用 Windows 窗体控件，必须使用非托管 CLR 托管 API 来托管 CLR，或使用 C++ 互操作功能。 使用 C++ 互操作功能是建议采用的解决方案。  
  
## <a name="windows-forms-in-com-client-applications"></a>COM 客户端应用程序中的 Windows 窗体  
 从 COM 客户端应用程序（例如，Visual Basic 6.0 应用程序或 MFC 应用程序）打开 Windows 窗体时，窗体可能出现意外行为。 例如，当你按 Tab 键时，焦点不会从一个控件更改到另一个控件。 或者当你在命令按钮有焦点的情况下按 Enter 键时，无法引发按钮的 <xref:System.Windows.Forms.Control.Click> 事件。 还可能遇到击键或鼠标操作的其他意外行为。  
  
 发生此行为是因为非托管应用程序没有实现消息循环支持，而 Windows 窗体需要该支持才能正确工作。 COM 客户端应用程序所提供的消息循环根本不同于 Windows 窗体消息循环。  
  
 应用程序的消息循环是内部程序循环，它从线程的消息队列检索消息，然后转换这些消息，之后将它们发送给要处理的应用程序。 Windows 窗体的消息循环与更早的应用程序（例如，Visual Basic 6.0 应用程序和 MFC 应用程序）所提供的消息循环的体系结构不同。 发布到消息循环的窗口消息的处理方式可能与 Windows 窗体期望的不同。 因此，可能发生意外的行为。 某些击键组合可能不起作用，某些鼠标活动可能不工作，或者某些事件可能不会按期望引发。  
  
## <a name="resolving-interoperability-issues"></a>解决互操作性问题  
 可以通过在 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType> 消息循环（它是使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 方法创建的）上显示窗体来解决这些问题。  
  
 若要使 Windows 窗体在 COM 客户端应用程序中正确工作，必须在 Windows 窗体消息循环上运行该窗体。 若要执行此操作，请使用以下方法之一：  
  
-   使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法显示 Windows 窗体。 有关详细信息，请参阅[如何：通过显示 Windows 窗体使用 ShowDialog 方法来支持 COM 互操作](com-interop-by-displaying-a-windows-form-shadow.md)。  
  
-   在新线程上显示每个 Windows 窗体。 有关详细信息，请参阅[如何：通过在其自己的线程上显示每个 Windows 窗体来支持 COM 互操作](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)。  
  
## <a name="see-also"></a>请参阅
- [Windows Forms and Unmanaged Applications](windows-forms-and-unmanaged-applications.md)
- [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)
- [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)
- [COM 互操作性示例](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/cxcz83xf(v=vs.90))
- [Aximp.exe（Windows 窗体 ActiveX 控件导入程序）](../../tools/aximp-exe-windows-forms-activex-control-importer.md)
- [向 COM 公开 .NET Framework 组件](../../interop/exposing-dotnet-components-to-com.md)
- [将 COM 的程序集打包](../../interop/packaging-an-assembly-for-com.md)
- [向 COM 注册程序集](../../interop/registering-assemblies-with-com.md)
- [如何：通过显示 Windows 窗体使用 ShowDialog 方法来支持 COM 互操作](com-interop-by-displaying-a-windows-form-shadow.md)
- [如何：通过在其自己的线程上显示每个 Windows 窗体来支持 COM 互操作](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)
