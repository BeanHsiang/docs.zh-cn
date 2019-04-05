---
title: Windows 窗体和非托管应用程序
ms.date: 03/30/2017
helpviewer_keywords:
- ActiveX controls [Windows Forms]
- COM interop [Windows Forms], Windows Forms
- COM [Windows Forms]
- Windows Forms, unmanaged
- Windows Forms, interop
ms.assetid: 81bc100c-fa49-4614-85a6-0f7ab59eac8a
ms.openlocfilehash: 65465f22b1806d385523c894cce2103afe33c2f0
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57702654"
---
# <a name="windows-forms-and-unmanaged-applications"></a>Windows 窗体和非托管应用程序
Windows 窗体应用程序和控件可以与非托管应用程序进行互操作，但有一些需要注意的问题。 以下各节将介绍 Windows 窗体应用程序和控件支持和不支持的方案和配置。  
  
## <a name="in-this-section"></a>本节内容  
 [Windows 窗体和非托管应用程序概述](windows-forms-and-unmanaged-applications-overview.md)  
 提供有关如何使用和实现运用非托管应用程序的 Windows 窗体控件的常规信息。  
  
 [如何：通过显示 Windows 窗体使用 ShowDialog 方法来支持 COM 互操作](com-interop-by-displaying-a-windows-form-shadow.md)  
 提供显示如何使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法在非托管应用程序中运行 Windows 窗体的代码示例。  
  
 [如何：通过在其自己的线程上显示每个 Windows 窗体来支持 COM 互操作](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)  
 提供显示如何在各自的线程上运行 Windows 窗体的代码示例。  
  
 另请参阅[演练：通过在其自己的线程上显示每个 Windows 窗体支持 COM 互操作](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233639(v=vs.100))。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType>  
 用于为 Windows 窗体中创建单独线程。  
  
 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType>  
 启动线程的消息循环。  
  
 <xref:System.Windows.Forms.Control.Invoke%2A>  
 将来自非托管应用程序的调用封送到窗体。  
  
## <a name="related-sections"></a>相关章节  
 [向 COM 公开 .NET Framework 组件](../../interop/exposing-dotnet-components-to-com.md)  
 提供有关如何在非托管应用程序中使用 .NET Framework 类型的常规信息。
