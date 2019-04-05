---
title: 如何：混合应用程序中启用视觉样式
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- visual styles [Windows Forms]
ms.assetid: 95de9b9c-d804-405c-b2d1-49a88c1e0fe1
ms.openlocfilehash: 9588a2e2d839af43ffe4397303c4a45cad5af2e5
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57371913"
---
# <a name="how-to-enable-visual-styles-in-a-hybrid-application"></a>如何：混合应用程序中启用视觉样式
本主题演示如何启用[!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)]上的视觉样式[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件中托管[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-基于应用程序。  
  
 如果你的应用程序调用<xref:System.Windows.Forms.Application.EnableVisualStyles%2A>方法中，大部分你[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件将自动使用视觉样式时上运行你的应用程序[!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)]。 有关详细信息，请参阅[以视觉样式呈现控件](../../winforms/controls/rendering-controls-with-visual-styles.md)。  
  
 本主题中所涉及任务的完整代码列表，请参阅[混合应用程序示例中启用视觉样式](https://go.microsoft.com/fwlink/?LinkID=159986)。  
  
## <a name="enabling-windows-forms-visual-styles"></a>启用 Windows 窗体视觉样式  
  
#### <a name="to-enable-windows-forms-visual-styles"></a>启用 Windows 窗体视觉样式  
  
1.  创建[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]应用程序项目中名为`HostingWfWithVisualStyles`。  
  
2.  在解决方案资源管理器中，添加对下列程序集的引用。  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
3.  在工具箱中，双击<xref:System.Windows.Controls.Grid>图标将<xref:System.Windows.Controls.Grid>设计图面上的元素。  
  
4.  在属性窗口中设置的值<xref:System.Windows.FrameworkElement.Height%2A>并<xref:System.Windows.FrameworkElement.Width%2A>属性设置为**自动**。  
  
5.  在设计视图或 XAML 视图中，选择<xref:System.Windows.Window>。  
  
6.  在属性窗口中，单击**事件**选项卡。  
  
7.  双击<xref:System.Windows.FrameworkElement.Loaded>事件。
  
8.  在 MainWindow.xaml.vb 或 MainWindow.xaml.cs 中，插入以下代码以处理<xref:System.Windows.FrameworkElement.Loaded>事件。  
  
     [!code-csharp[HostingWfWithVisualStyles#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfWithVisualStyles/CSharp/HostingWfWithVisualStyles/Window1.xaml.cs#11)]
     [!code-vb[HostingWfWithVisualStyles#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfWithVisualStyles/VisualBasic/HostingWfWithVisualStyles/Window1.xaml.vb#11)]  
  
9. 按 F5 生成并运行该应用程序。  
  
     [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]用视觉样式绘制控件。  
  
## <a name="disabling-windows-forms-visual-styles"></a>禁用 Windows 窗体视觉样式  
 若要禁用视觉样式，只需删除对调用<xref:System.Windows.Forms.Application.EnableVisualStyles%2A>方法。  
  
#### <a name="to-disable-windows-forms-visual-styles"></a>禁用 Windows 窗体视觉样式  
  
1.  在代码编辑器中打开 MainWindow.xaml.vb 或 MainWindow.xaml.cs。  
  
2.  注释掉对的调用<xref:System.Windows.Forms.Application.EnableVisualStyles%2A>方法。  
  
3.  按 F5 生成并运行该应用程序。  
  
     [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件变为默认系统样式。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>
- <xref:System.Windows.Forms.VisualStyles>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [使用视觉样式呈现控件](../../winforms/controls/rendering-controls-with-visual-styles.md)
- [演练：承载在 WPF 中的 Windows 窗体控件](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
