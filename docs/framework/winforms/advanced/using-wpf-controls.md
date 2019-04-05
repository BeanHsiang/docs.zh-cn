---
title: 使用 WPF 控件
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms Designer [Windows Forms], interoperability with WPF
- interoperability [WPF]
ms.assetid: 03c85dce-26ad-44cd-bc1d-8e0cb56de096
ms.openlocfilehash: 24b88e456628c5a0bdc3cded60b0e52a92057851
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57713795"
---
# <a name="using-wpf-controls"></a>使用 WPF 控件
基于 Windows 窗体的应用程序中，可以使用 Windows Presentation Foundation (WPF) 控件。 尽管这些是两个不同的视图技术，则它们平稳地相互操作。  
  
 Windows 窗体设计器提供用于承载 Windows Presentation Foundation 控件的可视化设计环境。 由名为的特殊 Windows 窗体控件承载 WPF 控件<xref:System.Windows.Forms.Integration.ElementHost>。 此控件，WPF 控件来参与窗体的布局并接收键盘和鼠标消息。 在设计时，可以安排<xref:System.Windows.Forms.Integration.ElementHost>控制就像对待任何 Windows 窗体控件。  
  
 此外可以基于 WPF 的应用程序中使用 Windows 窗体控件。 有关详细信息，请参阅[Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：复制并粘贴 ElementHost 控件在设计时](how-to-copy-and-paste-an-elementhost-control-at-design-time.md)  
 演示如何将复制在 Windows 窗体上的 Windows Presentation Foundation 控件。  
  
 [演练：在设计时排列 Windows 窗体上的 WPF 内容](walkthrough-arranging-wpf-content-on-windows-forms-at-design-time.md)  
 演示如何使用 Windows 窗体布局功能，例如锚定和对齐线，排列 Windows Presentation Foundation 控件。
  
 [演练：在设计时在 Windows 窗体上创建新的 WPF 内容](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)  
 演示如何创建基于 Windows 窗体的应用程序中使用的 Windows Presentation Foundation 控件。
  
 [演练：在设计时分配在 Windows 窗体上的 WPF 内容](walkthrough-assigning-wpf-content-on-windows-forms-at-design-time.md)  
 演示如何选择想要显示窗体上的 Windows Presentation Foundation 控件类型。  
  
 [演练：WPF 内容的样式](walkthrough-styling-wpf-content.md)  
 显示 Windows 窗体设计器之间的工作流和[!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]用于将样式应用到 Windows Presentation Foundation 控件。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 介绍可以承载 Windows Presentation Foundation 控件使用基于 Windows 窗体的应用程序中的类。  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 介绍可用于在基于 Windows Presentation Foundation 的应用程序中承载 Windows 窗体控件的类。  
  
## <a name="related-sections"></a>相关章节  
 [迁移和互操作性](../../wpf/advanced/migration-and-interoperability.md)  
 介绍 Windows Presentation Foundation 和 Windows 窗体技术之间的互操作。  
  
 [在 Visual Studio 中设计 XAML](/visualstudio/designers/designing-xaml-in-visual-studio)  
 介绍如何设计在 Visual Studio 中的 Windows Presentation Foundation 控件。
