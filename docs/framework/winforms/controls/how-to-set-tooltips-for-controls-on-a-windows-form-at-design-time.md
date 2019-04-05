---
title: 如何：在设计时为 Windows 窗体上控件设置工具提示
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tooltips [Windows Forms], for controls
- examples [Windows Forms], tooltips
ms.assetid: c4b60637-4c0a-44c2-a103-f66dff887936
ms.openlocfilehash: 541e50a8ee9c5338acc7c5e347549fd03a0f6323
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710714"
---
# <a name="how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time"></a>如何：在设计时为 Windows 窗体上控件设置工具提示
可以设置<xref:System.Windows.Forms.ToolTip>字符串在代码中或在 Windows 窗体设计器中。 有关详细信息<xref:System.Windows.Forms.ToolTip>组件，请参阅[ToolTip 组件概述](tooltip-component-overview-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](/visualstudio/ide/personalizing-the-visual-studio-ide)。  
  
### <a name="to-set-a-tooltip-programmatically"></a>若要以编程方式设置工具提示  
  
1.  添加控件，将显示工具提示。  
  
2.  使用<xref:System.Windows.Forms.ToolTip.SetToolTip%2A>方法的<xref:System.Windows.Forms.ToolTip>组件。  
  
    ```vb  
    ' In this example, Button1 is the control to display the ToolTip.  
    ToolTip1.SetToolTip(Button1, "Save changes")  
    ```  
  
    ```csharp  
    // In this example, button1 is the control to display the ToolTip.  
    toolTip1.SetToolTip(button1, "Save changes");  
    ```  
  
    ```cpp  
    // In this example, button1 is the control to display the ToolTip.  
    toolTip1->SetToolTip(button1, "Save changes");  
    ```  
  
### <a name="to-set-a-tooltip-in-the-designer"></a>若要在设计器中设置工具提示  
  
1.  将 <xref:System.Windows.Forms.ToolTip> 组件添加到窗体。  
  
2.  选择将显示工具提示，或将其添加到窗体的控件。  
  
3.  在中**属性**窗口中，将**ToolTip1 上的工具提示**为相应的文本字符串的值。  

### <a name="to-remove-a-tooltip-programmatically"></a>若要以编程方式删除工具提示  
  
1.  使用<xref:System.Windows.Forms.ToolTip.SetToolTip%2A>方法的<xref:System.Windows.Forms.ToolTip>组件。  
  
    ```vb  
    ' In this example, Button1 is the control displaying the ToolTip.  
    ToolTip1.SetToolTip(Button1, Nothing)  
    ```  
  
    ```csharp  
    // In this example, button1 is the control displaying the ToolTip.  
    toolTip1.SetToolTip(button1, null);  
    ```  
  
    ```cpp  
    // In this example, button1 is the control displaying the ToolTip.  
    toolTip1->SetToolTip(button1, NULL);  
    ```  
  
### <a name="to-remove-a-tooltip-in-the-designer"></a>若要在设计器中删除一个工具提示  
  
1.  选择显示工具提示的控件。  
  
2.  在中**属性**窗口中，删除中的文本**ToolTip1 上的工具提示**。  

## <a name="see-also"></a>请参阅
- [ToolTip 组件概述](tooltip-component-overview-windows-forms.md)
- [如何：更改 Windows 窗体 ToolTip 组件的延迟](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)
- [ToolTip 组件](tooltip-component-windows-forms.md)
