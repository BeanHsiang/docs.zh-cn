---
title: 拖放操作和剪贴板支持
ms.date: 03/30/2017
helpviewer_keywords:
- drag and drop [Windows Forms]
- drag and drop [Windows Forms], Windows Forms
- Clipboard [Windows Forms], Windows Forms
ms.assetid: 7cce79b6-5835-46fd-b690-73f12ad368b2
ms.openlocfilehash: 5e7bb75b648163dab7e410a159d55ebbb75f1b0a
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711741"
---
# <a name="drag-and-drop-operations-and-clipboard-support"></a>拖放操作和剪贴板支持
可以通过处理一系列事件（最主要是 <xref:System.Windows.Forms.Control.DragEnter>、<xref:System.Windows.Forms.Control.DragLeave> 和 <xref:System.Windows.Forms.Control.DragDrop> 事件），在基于 Windows 的应用程序中启用用户拖放操作。  
  
 也可以使用简单的方法调用，在基于 Windows 的应用程序中对剪贴板实现用户剪切/复制/粘贴支持和用户数据传输。  
  
## <a name="in-this-section"></a>本节内容  
 [演练：在 Windows 窗体中执行拖放操作](walkthrough-performing-a-drag-and-drop-operation-in-windows-forms.md)  
 说明如何启动拖放操作。  
  
 [如何：执行应用程序之间的拖放操作](how-to-perform-drag-and-drop-operations-between-applications.md)  
 演示如何跨应用程序完成拖放操作。  
  
 [如何：将数据添加到剪贴板](how-to-add-data-to-the-clipboard.md)  
 介绍如何以编程方式在剪贴板上插入信息。  
  
 [如何：从剪贴板中检索数据](how-to-retrieve-data-from-the-clipboard.md)  
 介绍如何访问剪贴板上存储的数据。  
  
## <a name="related-sections"></a>相关章节  
 [Windows 窗体中的拖放功能](../drag-and-drop-functionality-in-windows-forms.md)  
 介绍用于实现拖放行为的方法、事件和类。  
  
 <xref:System.Windows.Forms.Control.QueryContinueDrag>  
 介绍要求权限才能继续拖动操作的事件的复杂性。  
  
 <xref:System.Windows.Forms.Control.DoDragDrop%2A>  
 介绍对开始拖动操作极为重要的方法的复杂性。  
  
 <xref:System.Windows.Forms.Clipboard>  
 另请参阅[如何：将数据发送到活动的 MDI 子窗体](how-to-send-data-to-the-active-mdi-child.md)。
