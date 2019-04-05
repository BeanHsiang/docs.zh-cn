---
title: ToolBar 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- ToolBar
helpviewer_keywords:
- toolbars [Windows Forms], about toolbars
- ToolBar control [Windows Forms], about ToolBar controls
ms.assetid: d426b203-0216-4dbe-b834-1641e50a9c29
ms.openlocfilehash: 249c5854b83a62878ecef0350e08ba4b00523aff
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57708842"
---
# <a name="toolbar-control-overview-windows-forms"></a>ToolBar 控件概述（Windows 窗体）
> [!NOTE]
>  
  <xref:System.Windows.Forms.ToolStrip> 控件取代了 <xref:System.Windows.Forms.ToolBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ToolBar> 控件以实现向后兼容并供将来使用。  
  
 Windows 窗体 <xref:System.Windows.Forms.ToolBar> 控件在窗体上用作可显示下拉菜单的行的控件条以及可激活命令的位图按钮。 因此，单击工具栏按钮相当于选择菜单命令。 可将按钮配置为以普通按钮、下拉菜单或分隔符等形式显示和表现。 通常，工具栏包含对应于应用程序菜单结构中的项的按钮和菜单，提供对应用程序最常用的函数和命令的快速访问。  
  
## <a name="working-with-the-toolbar-control"></a>使用 ToolBar 控件  
 一个<xref:System.Windows.Forms.ToolBar>控件通常"停靠"沿其父窗口的顶部，但它还可停靠到窗口的任意一侧。 用户将鼠标指针指向工具栏按钮时，工具栏可以显示工具提示。 工具提示是一个小型弹出式窗口，用以简述按钮或菜单的用途。 若要显示工具提示，请<xref:System.Windows.Forms.ToolBar.ShowToolTips%2A>属性必须设置为`true`。  
  
> [!NOTE]
>  某些应用程序具有与工具栏非常类似的控件，这些控件可“浮动”在应用程序窗口之上并可重新定位。 Windows 窗体 ToolBar 控件不能执行这些操作。  
  
 当<xref:System.Windows.Forms.ToolBar.Appearance%2A>属性设置为<xref:System.Windows.Forms.ToolBarAppearance>，工具栏按钮显示凸起和三维。 可以设置<xref:System.Windows.Forms.ToolBar.Appearance%2A>到工具栏的属性<xref:System.Windows.Forms.ToolBarAppearance>以使工具栏及其按钮为平面外观。 鼠标指针移动到平面按钮时，该按钮的外观变为三维形状。 可使用分隔符将工具栏按钮划分成多个逻辑组。 分隔符是与一个工具栏按钮<xref:System.Windows.Forms.ToolBarButton.Style%2A>属性设置为<xref:System.Windows.Forms.ToolBarButtonStyle>。 它在工具栏上显示为空白。 工具栏以平面方式显示时，按钮分隔符在按钮之间显示为直线而不是空白。  
  
 <xref:System.Windows.Forms.ToolBar>让您可以通过添加创建工具栏<xref:System.Windows.Forms.Button>对象添加到<xref:System.Windows.Forms.ToolBar.Buttons%2A>集合。 可以使用集合编辑器来将按钮添加到<xref:System.Windows.Forms.ToolBar>控件; 每个<xref:System.Windows.Forms.Button>对象应具有文本或图像分配，尽管可同时分配二者。 图像由关联的 [ImageList](imagelist-component-windows-forms.md) 组件提供。 在运行时，您可以添加或删除从按钮<xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection>使用<xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Add%2A>和<xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Remove%2A>方法。 进行编程的按钮<xref:System.Windows.Forms.ToolBar>，将代码添加到<xref:System.Windows.Forms.ToolBar.ButtonClick>的事件<xref:System.Windows.Forms.ToolBar>，并使用<xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A>属性<xref:System.Windows.Forms.ToolBarButtonClickEventArgs>类来确定单击了哪个按钮。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ToolBar>
- [ToolBar 控件](toolbar-control-windows-forms.md)
- [如何：向 ToolBar 控件添加按钮](how-to-add-buttons-to-a-toolbar-control.md)
- [如何：定义的工具栏按钮的图标](how-to-define-an-icon-for-a-toolbar-button.md)
- [如何：触发工具栏按钮的菜单事件](how-to-trigger-menu-events-for-toolbar-buttons.md)
