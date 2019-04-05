---
title: Windows 窗体中的鼠标捕获
ms.date: 03/30/2017
helpviewer_keywords:
- mouse [Windows Forms], capture
ms.assetid: 8911d4b0-a4f8-4f93-8246-371aebd27d0c
ms.openlocfilehash: afb58df99ea30f5e7e6ab5b9156af195d273c44d
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57712703"
---
# <a name="mouse-capture-in-windows-forms"></a>Windows 窗体中的鼠标捕获
*鼠标捕获*指何时控件执行的所有鼠标输入的命令。 当控件已捕获鼠标时，它接收鼠标输入，指示在其边框内为指针。  
  
## <a name="setting-mouse-capture"></a>设置鼠标捕获  
 在 Windows 窗体中鼠标用户按鼠标按钮上一个控件，, 并在用户释放鼠标按钮时由控件中释放鼠标时由该控件捕获。  
  
 <xref:System.Windows.Forms.Control.Capture%2A>属性的<xref:System.Windows.Forms.Control>类指定控件是否已捕获鼠标。 若要确定当控件失去鼠标捕获，请处理<xref:System.Windows.Forms.Control.MouseCaptureChanged>事件。  
  
 仅在前台窗口可以捕获鼠标。 当后台窗口尝试捕获鼠标时，窗口接收鼠标事件时鼠标指针位于该窗口的可见部分发生的消息。 此外，即使前景窗口已捕获鼠标，用户仍可以单击另一个窗口，将其带到前台。 时捕获鼠标、 键盘快捷方式执行操作不起作用。  
  
## <a name="see-also"></a>请参阅
- [Windows 窗体应用程序中的鼠标输入](mouse-input-in-a-windows-forms-application.md)
