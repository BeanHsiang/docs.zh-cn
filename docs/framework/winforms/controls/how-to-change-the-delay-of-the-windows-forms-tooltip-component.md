---
title: 如何：更改 Windows 窗体 ToolTip 组件的延迟
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- ToolTip component [Windows Forms], delay values
- tooltips [Windows Forms], delay values
- examples [Windows Forms], tooltips
ms.assetid: 08979ba7-dd84-477b-ab17-8d06e759be99
ms.openlocfilehash: 5f3be7467aad8b14aa67dc57b8c23e585a62fa25
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57704463"
---
# <a name="how-to-change-the-delay-of-the-windows-forms-tooltip-component"></a>如何：更改 Windows 窗体 ToolTip 组件的延迟
有多个可以设置为 Windows 窗体的延迟值<xref:System.Windows.Forms.ToolTip>组件。 所有这些属性的度量单位为毫秒。 <xref:System.Windows.Forms.ToolTip.InitialDelay%2A>属性确定多长时间，用户必须指向的关联控件的要显示的工具提示字符串。 <xref:System.Windows.Forms.ToolTip.ReshowDelay%2A>属性设置的后续工具提示字符串，以显示当鼠标从一个工具提示相关联的控件移到另一个所需的毫秒数。 <xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A>属性确定在显示工具提示字符串的时间长度。 单个或通过设置的值可以设置这些值<xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>属性; 属性根据分配给的值设置的其他延迟<xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>属性。 例如，当<xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>设置为的值为 N，<xref:System.Windows.Forms.ToolTip.InitialDelay%2A>设置为 N，<xref:System.Windows.Forms.ToolTip.ReshowDelay%2A>设置的值为<xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>除以 5 （或 N/5），并<xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A>设置为五次的值的值为<xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>属性 （或 5N）。  
  
### <a name="to-set-the-delay"></a>若要设置延迟  
  
1.  在此示例中所示设置以下属性。  
  
    ```vb  
    ToolTip1.InitialDelay = 500  
    ToolTip1.ReshowDelay = 100  
    ToolTip1.AutoPopDelay = 5000  
    ```  
  
    ```csharp  
    ToolTip1.InitialDelay = 500;  
    ToolTip1.ReshowDelay = 100;  
    ToolTip1.AutoPopDelay = 5000;  
    ```  
  
    ```cpp  
    toolTip1->InitialDelay = 500;  
    toolTip1->ReshowDelay = 100;  
    toolTip1->AutoPopDelay = 5000;  
    ```  
  
## <a name="see-also"></a>请参阅
- [ToolTip 组件概述](tooltip-component-overview-windows-forms.md)
- [如何：在设计时为 Windows 窗体上控件设置工具提示](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)
- [ToolTip 组件](tooltip-component-windows-forms.md)
