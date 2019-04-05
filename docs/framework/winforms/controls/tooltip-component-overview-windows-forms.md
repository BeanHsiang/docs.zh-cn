---
title: ToolTip 组件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- ToolTip
helpviewer_keywords:
- tooltips [Windows Forms], about tooltips
- ToolTip component [Windows Forms], about ToolTip component
ms.assetid: 3fbc6f08-c882-4acd-a960-a08efe3c7e6e
ms.openlocfilehash: 33a66e8ab5c8b09c5ed3dcf9dc60810a42d4d05d
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57724032"
---
# <a name="tooltip-component-overview-windows-forms"></a>ToolTip 组件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ToolTip> 组件在用户指向控件时显示文本。 ToolTip 可与任何控件关联。 此组件的示例用法： 若要在窗体上节省空间，可以在按钮上显示一个小图标，并使用 ToolTip 来解释按钮的功能。  
  
## <a name="working-with-the-tooltip-component"></a>使用工具提示组件  
 一个<xref:System.Windows.Forms.ToolTip>组件提供`ToolTip`到 Windows 窗体或其他容器上的多个控件的属性。 例如，如果您将某个<xref:System.Windows.Forms.ToolTip>窗体上的组件，可以显示"在此处键入名称"的<xref:System.Windows.Forms.TextBox>控制和"单击此处以保存更改"<xref:System.Windows.Forms.Button>控件。  
  
 主要方法<xref:System.Windows.Forms.ToolTip>组件都<xref:System.Windows.Forms.ToolTip.SetToolTip%2A>和<xref:System.Windows.Forms.ToolTip.GetToolTip%2A>。 可以使用<xref:System.Windows.Forms.ToolTip.SetToolTip%2A>方法设置为控件显示的工具提示。 有关详细信息，请参阅[如何：在设计时为 Windows 窗体上控件设置工具提示](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)。 键属性是<xref:System.Windows.Forms.ToolTip.Active%2A>，它必须设置为`true`的工具提示显示，和<xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>，用于设置的工具提示字符串所示的时间长度，多长时间，用户必须指向的工具提示显示，控件及其这将显示后续工具提示窗口。 有关详细信息，请参阅[如何：更改 Windows 窗体 ToolTip 组件的延迟](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ToolTip>
- [如何：在设计时为 Windows 窗体上控件设置工具提示](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)
- [如何：更改 Windows 窗体 ToolTip 组件的延迟](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)
