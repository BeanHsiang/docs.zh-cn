---
title: SplitContainer 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- SplitContainer
helpviewer_keywords:
- SplitContainer control [Windows Forms], about SplitContainer control
ms.assetid: 6de5a5f7-97a5-402d-be6d-7e2785483db5
ms.openlocfilehash: e99683bf6746cc5a85448bb22a996c04b7dcaa8c
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57709687"
---
# <a name="splitcontainer-control-overview-windows-forms"></a>SplitContainer 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.SplitContainer> 控件可视为一个复合控件；它是由可移动条隔开的两个面板。 当鼠标指针位于条上方时，指针将改变形状以表示条可移动。  
  
> [!IMPORTANT]
>  在中**工具箱**，<xref:System.Windows.Forms.SplitContainer>控件替代<xref:System.Windows.Forms.Splitter>以前版本的 Visual Studio 中的控件。 相较于 <xref:System.Windows.Forms.Splitter> 控件，优先选择 <xref:System.Windows.Forms.SplitContainer> 控件。 <xref:System.Windows.Forms.Splitter>类仍包含在[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]为了兼容现有应用程序，但我们强烈建议你使用<xref:System.Windows.Forms.SplitContainer>为新项目的控件。  
  
 使用<xref:System.Windows.Forms.SplitContainer>控件，您可以创建复杂的用户界面; 通常情况下，在一个面板中的选项确定另一个面板中显示哪些对象。 这种安排对于显示和浏览信息非常有效。 具有两个面板使聚合区域中的信息和栏或"splitter，"使用户方便地调整面板大小。  
  
 多个<xref:System.Windows.Forms.SplitContainer>也只能嵌套控件，与第二个<xref:System.Windows.Forms.SplitContainer>控件水平，若要创建顶部和底部面板。  
  
 请注意，<xref:System.Windows.Forms.SplitContainer>控制键盘访问默认情况下; 用户可以按箭头键移动拆分器，如果<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A>属性设置为`false`。  
  
 <xref:System.Windows.Forms.SplitContainer.Orientation%2A>属性的<xref:System.Windows.Forms.SplitContainer>控件将确定拆分器，而不是控件本身的方向。 因此，此属性设置为<xref:System.Windows.Forms.Orientation.Vertical>，拆分器从顶部向底部运行，创建左侧和右侧面板。  
  
 另外，请注意，值<xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A>属性的值而异<xref:System.Windows.Forms.SplitContainer.Orientation%2A>属性。 有关详细信息，请参阅<xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A>属性。  
  
 你也可以限制的大小和移动<xref:System.Windows.Forms.SplitContainer>控件。 <xref:System.Windows.Forms.SplitContainer.FixedPanel%2A>属性确定哪个面板将保持相同的大小后<xref:System.Windows.Forms.SplitContainer>控件的大小调整，和<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A>属性确定拆分器是可由键盘或鼠标移动。  
  
> [!NOTE]
>  即使<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A>属性设置为`true`，该拆分器可能仍以编程方式; 例如，使用移<xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A>属性。  
  
 最后，每个面板<xref:System.Windows.Forms.SplitContainer>控件具有的属性以确定其单独的大小。  
  
## <a name="commonly-used-properties-methods-and-events"></a>常用的属性、方法和事件  
  
|name|描述|  
|----------|-----------------|  
|<xref:System.Windows.Forms.SplitContainer.FixedPanel%2A> 属性|确定哪个面板将保持相同大小后<xref:System.Windows.Forms.SplitContainer>调整控件的大小。|  
|<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 属性|确定是否可以使用键盘或鼠标移动拆分器。|  
|<xref:System.Windows.Forms.SplitContainer.Orientation%2A> 属性|确定是否垂直或水平排列拆分器。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A> 属性|确定在从左边缘或上边缘到可移动拆分条的像素的距离。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 属性|确定的最小距离，以像素为单位，用户可以移动拆分器。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterWidth%2A> 属性|确定的粗细，以像素为单位的拆分器。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterMoving> 事件|当拆分器移动时发生。|  
|<xref:System.Windows.Forms.SplitContainer.SplitterMoved> 事件|当拆分器移动时发生。|  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.SplitContainer>
- [SplitContainer 控件](splitcontainer-control-windows-forms.md)
- [SplitContainer 控件示例](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/0ffz7d1b(v=vs.90))
