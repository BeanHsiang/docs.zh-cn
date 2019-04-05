---
title: 如何：通过显示 Windows 窗体使用 ShowDialog 方法来支持 COM 互操作
ms.date: 03/30/2017
helpviewer_keywords:
- COM [Windows Forms]
- Windows Forms, unmanaged
- COM interop [Windows Forms], calling methods
- ActiveX controls [Windows Forms], COM interop
- Windows Forms, interop
ms.assetid: 87aac8ad-3c04-43b3-9b0c-d0b00df9ee74
ms.openlocfilehash: 56ded3118d0961f38c77d3db4fc879eb241a7520
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715433"
---
# <a name="how-to-support-com-interop-by-displaying-a-windows-form-with-the-showdialog-method"></a>如何：通过显示 Windows 窗体使用 ShowDialog 方法来支持 COM 互操作
可通过在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 消息循环上显示 Windows 窗体来解决组件对象模型 (COM) 互操作性问题，可使用 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType> 方法来创建该消息循环。  
  
 若要使窗体在 COM 客户端应用程序中正确工作，必须在 Windows 窗体消息循环上运行该窗体。 若要执行此操作，请使用以下方法之一：  
  
-   使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法显示 Windows 窗体；  
  
-   在单独的线程上显示每个 Windows 窗体。 有关详细信息，请参阅[如何：通过在其自己的线程上显示每个 Windows 窗体来支持 COM 互操作](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)。  
  
## <a name="procedure"></a>过程  
 使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法可能是在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 消息循环上显示窗体的最简单方法，因为在所有方法中，它只需最少的代码即可实现。  
  
 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法挂起非托管应用程序的消息循环，并将窗体显示为对话框。 由于宿主应用程序的消息循环已挂起， <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法创建新的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 消息循环来处理该窗体的消息。  
  
 使用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法的缺点是窗体将作为模式对话框打开。 Windows 窗体打开时，此行为将阻止调用应用程序中的任何用户界面 (UI)。 当用户退出该窗体时， [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 消息循环关闭，先前应用程序的消息循环重新运行。  
  
 可以在 Windows 窗体中创建具有显示窗体方法的类库，然后为 COM 互操作生成类库。 可以从 Visual Basic 6.0 或 Microsoft 基础类 (MFC) 中使用此 DLL 文件，在这两种环境中，都可以调用 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法来显示窗体。  
  
#### <a name="to-support-com-interop-by-displaying-a-windows-form-with-the-showdialog-method"></a>通过使用 ShowDialog 方法显示 Windows 窗体来支持 COM 互操作  
  
-   在 <xref:System.Windows.Forms.Form.Show%2A?displayProperty=nameWithType> 组件中，将所有对 <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> 方法的调用替换为对 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 方法的调用。  
  
## <a name="see-also"></a>请参阅
- [向 COM 公开 .NET Framework 组件](../../interop/exposing-dotnet-components-to-com.md)
- [如何：通过在其自己的线程上显示每个 Windows 窗体来支持 COM 互操作](how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)
- [Windows Forms and Unmanaged Applications](windows-forms-and-unmanaged-applications.md)
